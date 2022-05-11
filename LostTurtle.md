# 迷失海龜 - 小白12堂課

## 01 [合約入門與瀏覽器解說](https://www.youtube.com/watch?v=J-2LdBhAKdc)

### 智能合約
- 用程式碼操控虛擬貨幣帳戶
-- Balance：合約中目前擁有的餘額
-- Storage：合約中目前儲存的資料
-- Code：合約用來與機器互動的程式碼
- 無法跨鏈互動
-- 若要在其他鏈有一樣的合約，必須重新部屬。

### 智能合約使用語言 - Solidity
- 副檔名：.sol
- 強型別的JS(?)
- 合約內容 -> 編譯器(影片中口誤處理器) -> ABI(Application Binary Interface) & Bytecode

### 區塊鏈瀏覽器 - [Etherscan](https://etherscan.io)
- 查詢乙太鏈上發生的事情：合約、交易、交易狀態、Gas Fee......
- [查詢當前Gas Fee和交易量大戶](https://etherscan.io/gastracker)
- [乙太幣單位轉換器](https://etherscan.io/unitconverter)
-- GWei：$10^{-9}$ Ether
-- Wei：$10^{-18}$ Ether
- [檢查/撤銷Dapp授權](https://etherscan.io/tokenapprovalchecker)
- ~~看別人的錢包地址、交易紀錄~~
- 其他區塊鏈瀏覽器：Ethplorer、Blockscout

### 事前準備：申請帳號
- [Metamask](https://metamask.io) (Polygon錢包至少有 1 MATIC)
- [IPFS圖床工具](https://app.pinata.cloud/)
- [Twitter](https://twitter.com/) (海龜持有者Bonus課程)
- [Github](https://github.com) (海龜持有者Bonus課程)


## 02 [開發工具介紹 - Remix](https://www.youtube.com/watch?v=E2u6o81Apj0)

### Solidity IDE - [Remix](https://remix.ethereum.org)
- 線上IDE(Integrated Development Environment)
- 可用來開發、測試、偵錯
- 可用Linux VM(Virtual Machine)部屬
- 不用辦帳號或登入(程式碼記得備份！)

### 實作練習 - 咖啡店

#### 檔案(File)
1. 新增工作空間
2. 刪除預設的合約檔案
3. 在 *contract* 資料夾下新增一個 *.sol* 檔
4. 在檔案中加入下列程式碼

```solidity=1
//SPDX-License-Identifier: MIT

pragma solidity ^0.8.9;

contract Menu {
    string public todaySpecial;
    
    constructor(string memory firstDessert) { //創造一個菜單合約
        todaySpecial = firstDessert;          //寫上第一天的限定甜點
    }
    
    function setMenu(string memory newMenu) public {
        todaySpecial = newMenu;               //更換限定甜點
    }
}
```

#### 編譯(Compile)
1. 將編譯器的 *auto compile* 和 *enable optimization* 打勾
2. 編譯成功之後會有綠色勾勾

#### 部屬(Deploy)
1. 選擇一台VM和一個測試帳戶
2. 填入開幕第一天的甜點
3. 點開部屬好的合約可以看目前甜點或更換甜點

### 實作練習 - 杯子蛋糕販賣機
- [程式碼來源](https://ethereum.org/en/developers/docs/smart-contracts/#a-digital-vending-machine)

```solidity=1
//SPDX-License-Identifier: MIT

pragma solidity 0.8.7;

contract VendingMachine {

    // Declare state variables of the contract
    address public owner;
    mapping (address => uint) public cupcakeBalances;

    // When 'VendingMachine' contract is deployed:
    // 1. set the deploying address as the owner of the contract
    // 2. set the deployed smart contract's cupcake balance to 100
    constructor() {
        owner = msg.sender;
        cupcakeBalances[address(this)] = 100;
    }

    // Allow the owner to increase the smart contract's cupcake balance
    function refill(uint amount) public {
        require(msg.sender == owner, "Only the owner can refill.");
        cupcakeBalances[address(this)] += amount;
    }

    // Allow anyone to purchase cupcakes
    function purchase(uint amount) public payable {
        require(msg.value >= amount * 1 ether, "You must pay at least 1 ETH per cupcake");
        require(cupcakeBalances[address(this)] >= amount, "Not enough cupcakes in stock to complete this purchase");
        cupcakeBalances[address(this)] -= amount;
        cupcakeBalances[msg.sender] += amount;
    }
}
```
- 加上版權聲明
- 參數更改
-- 第27行：更改一個杯子蛋糕的價錢(在輸入value時使用單位轉換)

#### 偵錯(Debug)
- 用來看程式碼的問題在哪r

#### 設定
- 可更改IDE外觀

#### 彩蛋(?)
- 刺蝟會彈吉他
- 還有聲音！





## 03 [Visual Studio Code 介紹](https://www.youtube.com/watch?v=ER-DkFTEZXc)
### [Visual Studio Code](https://code.visualstudio.com)
- 微軟開發的跨平台編輯器
- 內建終端機
- 擴充套件

### 推薦套件
- **dbaeumer.vscode-eslint：標示某些程式碼語法**
- **DigitalBrainstem.javascript-ejs-support：標示某些程式碼語法**
- esbenp.prettier-vscode：程式碼排列整齊
- formulahendry.auto-close-tag：自動把標籤結尾
- naumous.color-highlight：框框標示色號
- file-icons：改檔案圖標
- ritwick.LiveServer：自動同步更新前端網頁

### 實作
- [藝術引擎檔案](https://github.com/HashLips/hashlips_art_engine)
- 打開 Visual Studio Code -> 開啟剛剛下載的檔案 -> 搜尋想要的套件
- 使用 *node -v* 查看框架版本
- 使用 *npm -v* 查看套件管理軟體版本
- 使用 *npm install* 安裝套件
- 使用 *node index.js* 跑藝術引擎製作圖片

### 小水母NFT
- 頭部、身體、腳、背景可自行搭配
1. [挑選喜歡的配色](https://colorhunt.co)
2. [開啟 Figma 檔案](https://www.figma.com/community/file/1098187120468428102)
3. 在 Figma 點選藍色按鈕 Duplicate
4. 從 Colorhunt 複製色碼到 Figma 找出喜歡的搭配
5. [填寫表單](https://forms.gle/NpwFCKz7aTGM1VEDA)



## 04 [圖層導入與命名](https://www.youtube.com/watch?v=EBoEsKEiwjk)

### 圖層
總共四個圖層 + 兩款特殊背景
- 背景 background
- 背景裝飾 bacjgroundDeco
- 表情 face
- 水母 jellyfish

### 圖層導入與命名
- PNG檔(可有透明背景)
- 必須使用英文命名且不可有底線或特殊符號
- 一個資料夾就是一個圖層
- 透過命名決定稀有度(#10)
- 利用程式進行圖層排序
- 利用程式進行特殊版的產出
- 利用圖片編號隨機功能將特殊版混入

### 實作
1. 用素材包的資料夾取代藝術引擎裡面原本的layers資料夾
2. 用VS Code打開藝術引擎
3. 第27行：決定產出幾張圖片
4. 第28行開始：把圖層輸入並且排序
5. 建立另一個圖層組合並進行設定
6. 將 shuffLayerConfiguration設定唯true 即可將特別版混入普通版
7. format 可以設定圖片尺寸大小
8. background 可以設定預設背景
9. 使用 *node index.js* 跑藝術引擎製作圖
10. 打開build資料夾查看製作出來的圖
11. 若在終端機跑出 *DNA exists!* 表示小水母組合已經出現過

## 05 [引擎參數調整](https://www.youtube.com/watch?v=NXoT7koXVYg)

### 藝術引擎參數調整
- 稀有度設定：圖層內的總數分之#
-- #後面的數字越小就是越稀有
-- *npm run rarity* 計算各種機率
-- 87行可以更改#成其他字元
- GIF型態的NFT：依照圖層疊加呈現動畫
-- 程式中 *gif* 設定 export 為 true
-- 可以設定是否要無限重複、畫質、速度
- 像素化NFT
-- *npm run pixelate*
- 產出預覽圖
-- 程式中 *preview* 可以設定預覽圖樣式
-- *npm run preview*
-- *node utils/preview_gif.js* 可以做動態預覽圖
- 一次更新所有NFT的資料設定
-- 更新json檔案資訊 *npm run update_info*

## 06 [IPFS與盲盒](https://www.youtube.com/watch?v=6afJsGIDOoQ)

### IPFS是什麼
- 去中心化的文件儲存系統，把檔案拆成固定大小儲存在節點中。
- 每個檔案都有自己獨特的地址。
- 根區塊鏈一樣有不可竄改的特性，但可以上傳新版本。
- 越熱門的內容越多節點會有，節點會自動刪除不常存取的內容來釋放空間。
- 節點可以釘選想要永久保存的內容。
- [Pinata](https://www.pinata.cloud)
-- 專為NFT設計的IPFS服務
-- 免費的就很夠用了(有1GB的空間)

### 盲盒怎麼做
- 透過更換網址的方式達成
- 跟NFT圖片一樣的方式上傳
- 在智能合約中定義鑄造的時候統一顯示盲盒圖片位置
- 解盲時再顯示實際圖片
- 符合Opensea的檔案規範



## 課表
![](https://i.imgur.com/foMcaH8.jpg)

# 現在就加入迷失海龜！！！
[官方網站](https://lostturtle.club/) [Discord](https://discord.gg/Un66k8n8sk) [Instagram](https://www.instagram.com/lost_turt1e/) [Youtube](https://www.youtube.com/channel/UCBt7QsF7CA5q4cTMJIX0otw/)