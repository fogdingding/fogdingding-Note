# shell script

新增一個檔案，test.sh

```bash
vim test.sh
```

新增一個檔案，test.py作為測試錯誤輸出等

```python
print("hello word python3")
print(hi) #故意錯誤
```

輸入以下內容

```bash
#!/bin/bash

echo "hello word"

echo "hello word" > test.log
echo "hello word" >> test.log

python3 test.py >> test.log 2>&1

```



#### 可以看到上面指令第三行，就是普通的在終端機上執行 印出 hello word 第五行，就是把輸出的東西丟入到`test.log` 第六行，就是把輸出的東西丟入到`test.log` 五、六行的差異，就是一個是寫入 \(write\)，一個是加入\(append\)。 第八行，則是執行python來進行，其中印出的東西會丟入`test.log`來進行 而其中會把錯誤印入裡面，其中後面的2&gt;&1意思是 0 表示鍵盤輸入 1 表示螢幕輸出 2 表示錯誤輸出 & 表示重新導向（可能是因為 &gt; 只吃左邊的東西，所以才需要 &） PS：&gt; 等價於 1&gt;

### 還可以在裡面編寫一些簡單的邏輯運算

```bash
if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi

```

```bash
a=10
b=20
if [ $a > $b ]
then
    echo "a > b"
elif [ $a < $b ]
then
    echo "a < b"
elif [ $a = $b ]
then
    echo "a = b"
else
then
    echo "???"
fi
```

### 也可以拿參數

```bash
bash test.sh 10 20
```

```bash
a=$1
b=$2
if [ $a > $b ]
then
    echo "a > b"
elif [ $a < $b ]
then
    echo "a < b"
elif [ $a = $b ]
then
    echo "a = b"
else
then
    echo "???"
fi
```



  
  




