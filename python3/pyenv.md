# pyenv

##  安裝

### 安裝Xcode Command Line Tool

```bash
xcode-select --install
```

### 安裝Homebrew

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew doctor
```

### 安裝Pyenv

```bash
curl https://pyenv.run | bash
```

跑完後，出現類似以下的東西，會在終端器上看到，在複製一下（主要有這三行）。

```bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

複製完後，再去`~/.zshrc`檔案內加入這三行。PS:MAC 我有裝zsh

```bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

### 測試成功否

```bash
 # 查看現有可安裝版本
pyenv install -l

# 安裝別的版本
pyenv install 3.7.4

# 查看目前有的版本 （＊代表目前使用的版本）
pyenv versions

# 使用需要的版本
pyenv global 3.7.4

# 再次查看版本
pyenv versions

# 查看目前版本是誰在使用
which python
# 類似這樣的輸出 /Users/<user-name>/.pyenv/shims/python
```



## 資料來源

* [github](https://github.com/pyenv/pyenv)
* [教學安裝網站](https://stringpiggy.hpd.io/mac-osx-python3-multiple-pyenv-install/)

