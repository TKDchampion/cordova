# Codova環境架設
###### tags: `APP`
使用codova將網站轉換成APP，使用步驟如下附標題
## 1.安裝Node.js
- [安裝Node.js](https://nodejs.org/en/)
- 安裝後可於cmder輸入指令`node -v`來確認版本

    ![](https://i.imgur.com/9kiSccT.png)
## 2.安裝git client
- [安裝git](https://git-scm.com/)
- 安裝後可於cmder輸入指令`git --version`來確認版本

    ![](https://i.imgur.com/pw2lIyT.png)
## 3.使用NPM安裝Cordova套件
- cmder輸入指令`npm install -g cordova`進行安裝
- cmder輸入指令`cordova -v`確認版本

    ![](https://i.imgur.com/aKd8ECg.png)
## 4.安裝Java JDK
- [安裝Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
- 安裝後設定環境變數PATH，將JDK安裝路徑加於分號後
;C:\Program Files\Java\jdk1.8_65\bin

    ![](https://i.imgur.com/irfhJpt.png)
- 新增環境變數JAVA_HOME，新增變數值C:\Program Files\Java\jdk1.8_65

    ![](https://i.imgur.com/4vZ3YMH.png)
- cmder輸入`javac -version`確認JAVA版本

    ![](https://i.imgur.com/HJrFbU3.png)
## 5.安裝Apache Ant
- [安裝Apache Ant](http://ant.apache.org/bindownload.cgi)
Ant是Android的編譯程式，他為開發Andorid的必要環境下載.zip檔，並解壓縮
- 設定PATH環境變數，一樣將安裝路徑加於分號後
;C:\ant\apache-ant-1.9.6\bin

    ![](https://i.imgur.com/nonF8pc.png)
- 新增ANT_HOME環境變數，新增變數值C:\ant\apache-ant-1.9.6
- cmder輸入指令`ant -version`確認版本

    ![](https://i.imgur.com/px9XJYd.png)
## 6.Android SDK Tools
- [安裝Android SDK](https://developer.android.com/studio/index.html?hl=zh-tw)
- 設定環境變數PATH，一樣將安裝路徑加於分號後(此安裝路徑有兩個路徑需要加上;[SDK Tools位置];[SDK platform-tools位置])
;C:\Program Files (x86)\Android\android-sdk\tools
;C:\Program Files (x86)\Android\android-sdk\platform-tools
- cmder輸入指令`adb version`確認版本

    ![](https://i.imgur.com/Od4rN9u.png)
- cmder輸入指令`android`後會跳出SDK Manager，將建議安裝的套件安裝完成

    ![](https://i.imgur.com/WmDxqmS.png)
## 7.測試Codova
- 在cmder輸入指令確認是否能夠執行模擬器
```linux=
cordova create WangApp
cd WangApp
cordova platform add android
cordova build
cordova run android
```
![](https://i.imgur.com/76cVYXw.png)
- 若上述模擬器無法執行可用其他模擬器代替[BlueStacks](http://www.bluestacks.com/download.html?utm_campaign=homepage-dl-button)
## 8.Android撰寫及編譯打包(補充說明)
- 撰寫程式
Cordova是個跨平台解決方案，還記得在前面我們用「cordova platform add」指令加入了Android平台嗎？你的App最終可能要執行在Android, iOS, WP8, BlackBerry等平台，既然是跨平台，當然希望「寫一次」程式就可以執行在各個平台上，為了實現這個需求，你可以編輯的資源僅限於「www」資料夾內的檔案。
    那麼之前在platforms\android\assets\www中看到的檔案呢？若你直接異動它，再透過對應的IDE還是可以產出可執行的App，但無法兼顧其他平台，既然選擇Cordova，最好不要這樣處理。
    另外有關App的基本資訊，Cordova為了兼顧多平台，統一將設定放在專案根目錄中的config.xml檔案，若欲調整App名稱與版本等資料請編輯該檔。

- 編譯打包
在完成程式的新增與編輯之後(記得，僅存取\www內的資源)，於cmder執行以下指令即可，執行前請確認有完成「開發前置準備」裡面提到的環境變數設定。
```htmlmixed=
cordova build
```
build指令會自動把\www內的東西copy至各平台的\assets\www，並且依各平台不同特性加入與修正必要檔案，為確保整個流程正確，這部分請不要手動完成。
     但是！若你不想要使用這種命令方式來打包成apk檔案，可以借用其他IDE來完成，若你有這個打算，請不要直接執行build，而改用以下指令(不同平台請自行抽換參數)。
```htmlmixed=
cordova prepare android
```
prepare會把相關檔案copy至正確的地方，但不進行編譯與打包之動作。實際上執行前面說的build，它也是自動幫你在背後執行prepare與compile兩個指令。
## 9.結束
