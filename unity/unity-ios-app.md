---
description: 建立一個ios的App
---

# unity-ios-App

#### 安裝與註冊

於[官網](https://unity.com/) 進行下載並安裝。  
於[官網](https://id.unity.com/en/conversations/97d5e839-f0fd-4bc9-9a9c-5df2445bdf5e00df) 進行註冊

#### 簡單介紹

![unityHub&#x7BA1;&#x7406;&#x4ECB;&#x9762;](../.gitbook/assets/unityhub.png)

* 專案
  * 控管專案的地方
* 學習
  * 官網提供一些基礎功能的介紹教學
* 社群
  * 透過社群的力量來進行議題或問題的發問與解答
* 安裝
  * 透過套件來進行相關軟體的安裝。

#### 管理授權

在管理介面的右上角齒輪（設定）點選後，點擊授權管理即可進行更新或是查看（避免無法使用Unity）

![unity-&#x6388;&#x6B0A;&#x7BA1;&#x7406;](../.gitbook/assets/unity-guan-li-shou-quan-.png)

#### 軟體安裝

點選管理介面的左邊控制列裡面的安裝後，點選已安裝的版本上的三個小點點後進行相關套件的安裝（勾選）。（安裝時間會蠻久的）

![&#x8EDF;&#x9AD4;&#x5B89;&#x88DD;](../.gitbook/assets/unity-guan-li-an-zhuang-ruan-ti-.png)

![&#x76EE;&#x524D;&#x5DF2;&#x65B0;&#x589E;&#x7684;&#x8EDF;&#x9AD4;&#x5957;&#x4EF6;](../.gitbook/assets/unity-mu-qian-yi-an-zhuang-de-ruan-ti-.png)

#### 開始建立第一隻APP

從管理介面選擇新增專案後，輸入名稱（本教學已經建立完畢）。

![&#x5EFA;&#x7ACB;3D&#x5C08;&#x6848;](../.gitbook/assets/unity-create.png)

即可看到Unity的開發介面

![Unity&#x958B;&#x767C;&#x4ECB;&#x9762;](../.gitbook/assets/unity.png)

在左邊的SampleScene地方新增一個3D物件-Cube

![&#x65B0;&#x589E;3D&#x7269;&#x4EF6;-Cube](../.gitbook/assets/create-cube.png)

稍微調整一下Main Camera 跟 Cube的相互位置（Camera 能夠順利看到Cube\)。

![&#x8ABF;&#x6574;&#x8DDD;&#x96E2;](../.gitbook/assets/unity-diao-zheng-ju-li-.png)

中間的播放按鈕，點選之後能夠順利看到一個立方體即代表成功。

![&#x958B;&#x59CB;Game&#x7684;&#x756B;&#x9762;](../.gitbook/assets/startgame.png)

#### 輸出成App檔案

點選File &gt; Build setting。

![Build Settings](../.gitbook/assets/build-settings.png)

Run in Xcode 選擇mac上的Xcode來進行編譯。  
點選IOS以及Switch platform 再點選Player Settings，即可看到下列圖表（右手邊）

![playerSetting](../.gitbook/assets/playersettings.png)

這邊比較特別，不知道Unity為何要如此設計。  
需要更改名稱的有兩個地方。

![appName1](../.gitbook/assets/appname.png)

![appName2](../.gitbook/assets/appname2.png)

將Company Name 以及 ProductName 改成自己想要的之後。  
在下面的Other Settings的 Identification 內的 Bundle Identifier 需要改成相同的名稱。  
com.Company Name.ProductName

之後即可開始進行編譯，但是因為Ios比較特別，需要使用Mac電腦，Apple公司內開發的Xcode才行哦～[下載來源](https://apps.apple.com/us/app/xcode/id497799835?mt=12)

完成上述設定之後，就能回到Build Settings 按下Build了。（這邊會運行比較久）

#### 讀取APP檔案

開啟Xcode 後 針對剛剛儲存的路徑進行讀取。（要讀取剛剛Unity產生出的檔案夾位址）  
讀取完之後，能看到以下圖表。

![Xcode-&#x958B;&#x767C;&#x9801;&#x9762;](../.gitbook/assets/xcode-kai-fa-ye-mian-.png)

在左上角選擇Unity-Iphone &gt; 我的Iphone（這邊需要手機有線的連接至Mac上面）。  
即可按下播放鍵（開始編譯）。  
這時候應該會發生錯誤，主要錯誤是因為我們還需要指定開發人員是誰（基於Ios-APP的安全性議題吧，出了事情能夠快速的追蹤是誰開發的？）

![Xcode-&#x958B;&#x767C;&#x4EBA;&#x54E1;&#x932F;&#x8AA4;](../.gitbook/assets/xcode-kai-fa-ren-yuan-cuo-wu-.png)

如需要解決這個問題，我們只需要指定開發人員即可。  
修正（指定）開發人員

![&#x9EDE;&#x9078;Unity-Iphone](../.gitbook/assets/dian-xuan-unityiphone.png)

![Unity-Iphone&#x7DE8;&#x8F2F;&#x756B;&#x9762;](../.gitbook/assets/unityiphone-hua-mian-.png)

![&#x9EDE;&#x9078;Singing](../.gitbook/assets/dian-xuan-singing.png)

![&#x6307;&#x5B9A;&#x958B;&#x767C;&#x4EBA;&#x54E1;](../.gitbook/assets/gou-xuan-bing-zhi-ding-.png)

在上圖點選Singing&Capabilites後  
勾選Automatically manage Signing  
即可選擇開發人員（這邊需要登入自己的APPLE ID）哦  
完成後即可再次按下播放鍵（編譯）。這次應該就能成功了。（在途中可能會需要打開IPhone的安全性設定，供APP能夠在手機上執行）

備註：編譯過程中會出現很多warning，是正常的（？）

#### Iphone

![&#x5B8C;&#x6210;&#x7DE8;&#x8B6F;&#x4E26;&#x5B89;&#x88DD;&#x65BC;&#x624B;&#x6A5F;&#x4E0A;](../.gitbook/assets/iphone-app.jpg)

![&#x6253;&#x958B;&#x8A2D;&#x5B9A;&#x4EE5;&#x53CA;&#x9EDE;&#x9078;&#x4E00;&#x822C;](../.gitbook/assets/da-kai-she-ding-.jpg)

![&#x9EDE;&#x9078;&#x88DD;&#x7F6E;&#x7BA1;&#x7406;](../.gitbook/assets/dian-xuan-zhuang-zhi-guan-li-.jpg)

![&#x4FE1;&#x4EFB;&#x958B;&#x767C;&#x8005;](../.gitbook/assets/xin-ren-wan-cheng-.jpg)

![App&#x904A;&#x6232;&#x756B;&#x9762;&#x6210;&#x529F;&#x57F7;&#x884C;](../.gitbook/assets/you-xi-hua-mian-.jpg)

























  




