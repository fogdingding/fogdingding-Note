# navicat premium crack

### 開始

#### Step1.下載原始檔

從[官網](https://www.navicat.com/cht/download/navicat-premium)下載ubuntu適合的檔案\(放到桌面上\)，檔案名稱可能會叫做`navicat15-premium-ct.AppImage`

#### Step2.提取檔案內部的資料

```bash
mkdir ~/Desktop/navicat15-premium-ct
sudo mount -o loop ~/Desktop/navicat15-premium-ct.AppImage ~/Desktop/navicat15-premium-ct
cp -r ~/Desktop/navicat15-premium-ct ~/Desktop/navicat15-premium-ct-patched
sudo umount ~/Desktop/navicat15-premium-ct
rm -rf ~/Desktop/navicat15-premium-ct
```

#### Step3.編譯patcher和keygen

請確保有安裝下列三項套件 `capstone`、`keystone`、`rapidjson`

```bash
# install capstone
sudo apt-get install libcapstone-dev
```

```bash
# install keystone
sudo apt-get install cmake
git clone https://github.com/keystone-engine/keystone.git
cd keystone
mkdir build
cd build
../make-share.sh
sudo make install
sudo ldconfig
```

```bash
# install rapidjson
sudo apt-get install rapidjson-dev
```

產生 `patcher` 和 `keygen` ，以下指令完成後，應該會在 `navicat-keygen/bin/` 下看到生產的檔案。

```bash
# patcher and keygen
git clone -b linux --single-branch https://gitee.com/andisolo/navicat-keygen.git
cd navicat-keygen
make all
```

#### Step4.使用 navicat-patcher 產生官方公鑰

```bash
./bin/navicat-patcher ~/Desktop/navicat15-premium-ct-patched
```

#### Step5.將檔案重新打包成AppImage

```bash
wget 'https://github.com/AppImage/AppImageKit/releases/download/continuous/appimagetool-x86_64.AppImage'
chmod +x appimagetool-x86_64.AppImage
./appimagetool-x86_64.AppImage ~/Desktop/navicat15-premium-ct-patched ~/Desktop/navicat15-premium-ct-patched.AppImage
```

#### Step6.執行剛生成的AppImage

```bash
chmod +x ~/Desktop/navicat15-premium-ct-patched.AppImage
~/Desktop/navicat15-premium-ct-patched.AppImage
```

#### Step7.使用 `navicat-keygen` 來生成 **序列號** 和 **啟用碼**

```bash
./bin/navicat-keygen --text ./RegPrivateKey.pem
```

選好相關基本資訊即可準備生成啟用碼

```bash
[*] Select Navicat product:
(Input index)> 1
[*] Select product language:
(Input index)> 2
[*] Input major version number:
(range: 0 ~ 15, default: 12)> 15
[*] Serial number:
xxxx-xxxx-xxxx-xxxx
[*] Your name: test
[*] Your organization: test
[*] Input request code in Base64: (Double press ENTER to end)
```

到這個`Input request code in Base64` 的時候，先別亂輸入。

#### Step8.開始crack

斷開網路. 找到註冊視窗，填寫keygen給你的 `序列號`，然後點選 `啟用`。  
通常線上啟用會失敗，所以在彈出的提示中選擇 `手動啟用`。  
複製`請求碼`到keygen\(Step7.\)，連按兩次回車結束。\(將會獲得啟用碼\)

```bash
[*] Input request code in Base64: (Double press ENTER to end)
OpGPC3MmjJ/pINbajFzLRkrV2OaSxtL......
[*] Request Info:
{"K":"...", "DI":"...", "P":"linux"}
[*] Response Info:
{"K":"...","DI":"...","N":"...","O":"...","T":"..."}
[*] Activation Code:
i25HIr7T1g69Cm9g3bN2dbqM/xio7......
```

#### Step10.啟用

把`啟用碼` \(`[*] Activation Code:`\)給的字串貼回去軟體上，就可以啟用成功了。

#### Step11.刪除不必要的東西

留下`navicat15-premium-ct-patched.AppImage` 即可，剩下不必要了。

### 資料來源

* [部落客教學](https://www.796t.com/article.php?id=64870)

