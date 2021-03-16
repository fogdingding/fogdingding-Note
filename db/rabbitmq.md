# rabbitMQ

### Use docker

Dockerfile

```text
#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "apply-templates.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#

FROM rabbitmq:3.8

RUN rabbitmq-plugins enable --offline rabbitmq_management

# make sure the metrics collector is re-enabled (disabled in the base image for Prometheus-style metrics by default)
RUN rm -f /etc/rabbitmq/conf.d/management_agent.disable_metrics_collector.conf

# extract "rabbitmqadmin" from inside the "rabbitmq_management-X.Y.Z.ez" plugin zipfile
# see https://github.com/docker-library/rabbitmq/issues/207
RUN set -eux; \
	erl -noinput -eval ' \
		{ ok, AdminBin } = zip:foldl(fun(FileInArchive, GetInfo, GetBin, Acc) -> \
			case Acc of \
				"" -> \
					case lists:suffix("/rabbitmqadmin", FileInArchive) of \
						true -> GetBin(); \
						false -> Acc \
					end; \
				_ -> Acc \
			end \
		end, "", init:get_plain_arguments()), \
		io:format("~s", [ AdminBin ]), \
		init:stop(). \
	' -- /plugins/rabbitmq_management-*.ez > /usr/local/bin/rabbitmqadmin; \
	[ -s /usr/local/bin/rabbitmqadmin ]; \
	chmod +x /usr/local/bin/rabbitmqadmin; \
	apt-get update; \
	apt-get install -y --no-install-recommends python3; \
	rm -rf /var/lib/apt/lists/*; \
	rabbitmqadmin --version

EXPOSE 15671 15672

```

docker-compose.yml

```bash
version: "3.7"
services:
  rabbitmq:
    hostname: 'rabbit'
    build: rabbitmq/
    ports:
      - 5672:5672
      - 15672:15672
    volumes:
      - ./rabbitmq/rabbitmq-data:/var/lib/rabbitmq
      - ./rabbitmq/rabbitmq-logs:/var/log/rabbitmq
    environment:
      RABBITMQ_DEFAULT_USER: user
      RABBITMQ_DEFAULT_PASS: password

```

### Python

### connetion on pika

```python
import pika
import time

class Rabbit():
    def __init__(self, config):
        self.config = config
        self.channel = self.connect()
    def connect(self):
        try:
            credentials = pika.PlainCredentials(
                self.config['db']['rabbit']['user'],
                self.config['db']['rabbit']['password']
            )
            connection = pika.BlockingConnection(
                pika.ConnectionParameters(
                    host=self.config['db']['rabbit']['host'],
                    port=self.config['db']['rabbit']['port'],
                    virtual_host=self.config['db']['rabbit']['virtual_host'],
                    credentials=credentials,
                    # 超時斷開連線秒數加大，預設為。
                    heartbeat=3600
                )
            )
            return connection.channel()
        except Exception as e:
            print('connect fail!', e)
            exit()
        else:
            print('connect successful!')

    def direct(self, exchange, queue, prefetch_count, callback):
        self.channel.exchange_declare(
            exchange=exchange,
            durable=True,
            exchange_type='direct'
        )
        tmp_queue = self.channel.queue_declare(
            queue,
            durable=True
        )
        self.channel.basic_qos(
            prefetch_count=prefetch_count
        )
        self.channel.queue_bind(
            exchange=exchange,
            queue=tmp_queue.method.queue,
            routing_key=queue
        )
        self.channel.basic_consume(
            on_message_callback=callback,
            queue=tmp_queue.method.queue,
            auto_ack=False,
        )
        return self.channel
```

可能會遇到這個問題`pika.exceptions.ConnectionClosedByBroker: (320, "CONNECTION_FORCED - broker forced connection closure with reason 'shutdown'")`，只要把`heartbeat` 給調大就好了。

### 範例

發布者

```python
import pika
import json

credentials = pika.PlainCredentials('user', 'password')
connection = pika.BlockingConnection(
    pika.ConnectionParameters(
        host='localhost',
        port=5672,
        virtual_host='/',
        credentials=credentials
    )
)
channel = connection.channel()
channel.exchange_declare(
    exchange='exchange_test',
    durable=True,
    exchange_type='direct'
)

for i in range(6):
    message=json.dumps({'OrderId':"test id = %s"%i})
    channel.basic_publish(
        exchange = 'exchange_test',
        routing_key = 'test',
        body = message,
        # delivery_mode = 2 為持久化
        properties=pika.BasicProperties(delivery_mode=2)
    )
    print(message)
connection.close()
```

訂閱者

```python
import pika
import time
credentials = pika.PlainCredentials('user', 'password')  # mq用户名和密码
connection = pika.BlockingConnection(
    pika.ConnectionParameters(
        host='localhost',
        port=5672,
        virtual_host='/',
        credentials=credentials
    )
)
channel = connection.channel()
channel.exchange_declare(
    exchange='exchange_test',
    durable=True,
    exchange_type='direct'
)
result = channel.queue_declare('test', durable= True )
channel.basic_qos(prefetch_count=1) 

# 定義callback函数来處理佇列中的訊息，這裡會印出來。
def callback(ch, method, properties, body):
    print(body.decode())
    ch.basic_ack(delivery_tag = method.delivery_tag)

channel.queue_bind(
    exchange='exchange_test',
    queue=result.method.queue,
    routing_key='test' )
# 告诉rabbit，用callback来接收訊息
channel.basic_consume(
    on_message_callback=callback,
    queue=result.method.queue,
    auto_ack=False,
)
#開始接受訊息，會一直等待訊息，有訊息後會觸發callback函數
channel.start_consuming()
```

### 備註

記得兩邊都先執行一遍\(第一次執行時\)，之後在讓發布者進行發布，才會開始正常的等待資料。\(因為我的設計是先創立通道後才會開始接受訊息\)

### 參考連結

* [部落客教學](https://www.cnblogs.com/dongye95/p/13206669.html)
* 
