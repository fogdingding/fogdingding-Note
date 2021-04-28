# python

在使用`VScode` 的時候，我們通常會讓他自動可以偵測錯誤等。以下是我常使用的設定。

在專案資料夾下建立 `.vscode` 的資料夾，在建立以下的setting.json檔案

#### setting.json

```javascript
{
    "editor.fontSize": 16,
    "terminal.integrated.fontSize": 14,
    "git.enableSmartCommit": true,
    "editor.renderControlCharacters": true,
    "editor.renderWhitespace": "none",
    "editor.minimap.enabled": true,
    "python.formatting.provider": "yapf",
    "python.testing.pytestEnabled": true,
    "python.testing.pytestArgs": [
        "--exitfirst"
        ,"--verbose"
        ,"--disable-warnings"
        ,"--no-cov"
        ,"-s"
    ],
    "python.linting.flake8Enabled": true,
    "python.linting.enabled": true,
    "python.linting.pycodestyleEnabled": true,
    "python.linting.pylintEnabled": false,
    "python.linting.pylintArgs": [
        "--disable=E1101,C0103,C0111,C0301,W0235,R0903,R0913"
    ],
    "python.linting.pycodestyleArgs": [
        "--ignore=W291,W293,E501" 
    ],
    "python.linting.flake8Args": [
        "--max--line-length=248"
    ],
    "standard.autoFixOnSave": true,
    "window.zoomLevel": 0,
    "workbench.editor.enablePreview": true,
    "extensions.ignoreRecommendations": false,
    "terminal.integrated.shell.osx": "/bin/zsh",
    "search.exclude": {
        "**/node_modules": true,
        "**/bower_components": true,
        "**/htmlcov": true
    },
    "files.insertFinalNewline": true,
    "files.exclude": {
        "**/*.pyc": true
    },
}

```

建立完成後，需要安裝相關套件

`VScode EXTENSIONS Python` 安裝完成後

在安裝python3 相關套件，我這邊先行安裝一些我常用的。（建立以下檔案`requirements.txt`\)

#### requirements.txt

```javascript
apturl==0.5.2
attrs==19.3.0
bcrypt==3.1.7
beautifulsoup4==4.9.3
blinker==1.4
Brlapi==0.7.0
cached-property==1.5.1
certifi==2020.12.5
chardet==4.0.0
Click==7.0
colorama==0.4.3
command-not-found==0.3
cryptography==2.8
cupshelpers==1.0
dbus-python==1.2.16
defer==1.0.6
distro==1.4.0
distro-info===0.23ubuntu1
docker==4.1.0
docker-compose==1.25.0
dockerpty==0.4.1
docopt==0.6.2
duplicity==0.8.12.0
entrypoints==0.3
fasteners==0.14.1
flake8==3.9.1
future==0.18.2
httplib2==0.14.0
idna==2.10
importlib-metadata==1.5.0
iniconfig==1.1.1
jsonschema==3.2.0
keyring==18.0.1
language-selector==0.1
launchpadlib==1.10.13
lazr.restfulclient==0.14.2
lazr.uri==1.0.3
lockfile==0.12.2
louis==3.12.0
macaroonbakery==1.3.1
Mako==1.1.0
MarkupSafe==1.1.0
mccabe==0.6.1
monotonic==1.5
more-itertools==4.2.0
netifaces==0.10.4
oauthlib==3.1.0
olefile==0.46
packaging==20.9
paramiko==2.6.0
pexpect==4.6.0
Pillow==7.0.0
pluggy==0.13.1
protobuf==3.6.1
py==1.10.0
pycairo==1.16.2
pycodestyle==2.7.0
pycups==1.9.73
pyflakes==2.3.1
PyGObject==3.36.0
PyJWT==1.7.1
pymacaroons==0.13.0
PyNaCl==1.3.0
pyparsing==2.4.7
pyRFC3339==1.1
pyrsistent==0.15.5
PySocks==1.7.1
pytest==6.2.3
python-apt==2.0.0+ubuntu0.20.4.4
python-dateutil==2.7.3
python-debian===0.1.36ubuntu1
pytz==2019.3
pyxdg==0.26
PyYAML==5.3.1
reportlab==3.5.34
requests==2.25.1
requests-unixsocket==0.2.0
SecretStorage==2.3.1
simplejson==3.16.0
six==1.14.0
socks==0
soupsieve==2.2.1
ssh-import-id==5.10
systemd-python==234
texttable==1.6.2
toml==0.10.2
tqdm==4.60.0
ubuntu-advantage-tools==20.3
ubuntu-drivers-common==0.0.0
ufw==0.36
unattended-upgrades==0.1
urllib3==1.26.4
usb-creator==0.3.7
wadllib==1.3.3
websocket-client==0.53.0
xkit==0.0.0
yap==0.5.7
yapf==0.31.0
zipp==1.0.0

```

輸入以下指令 `pip3 install -r requirements.txt` 即可自動安裝相關套件～

