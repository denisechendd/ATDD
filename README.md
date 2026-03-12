# ATDD
Selenium 自動化工具來測試一個停車費計算網頁（ParkCalc)
1. 測試劇本 (Cucumber Scenario)

圖片上方顯示了 Cucumber 的執行結果和劇本內容：

Scenario (情境): 計算代客泊車（Valet Parking）的費用。

Given/When: 當我將車停在代客泊車停車場 30 分鐘。

Then: 我必須支付 $12.00。

狀態: 目前顯示 1 pending（待處理），因為程式碼中使用了 pending 關鍵字，表示測試邏輯尚未完全實作。

2. 環境初始化與自動化設定 (Selenium Setup)

這部分負責啟動瀏覽器並準備測試環境：

引入函式庫: 使用 selenium-client 來控制瀏覽器，並引入 parkcalc 的頁面物件邏輯。

Before All: 建立一個 Selenium 驅動實例，設定連線到 localhost:4444，模擬 Firefox 瀏覽器，並打開目標網址 http://www.shino.de/parkcalc。

$parkcalc: 建立一個全局變數，初始化 ParkCalcPage 類別。

After All (at_exit): 在程式結束時關閉瀏覽器會話。

3. 頁面物件模型 (Page Object Model - ParkCalcPage Class)

這是一種設計模式，將網頁操作封裝在類別中，讓測試碼更易讀：

initialize: 初始化時存儲頁面控制代碼（page_handle），並呼叫 @page.open '/parkcalc' 開啟特定路徑。

雖然圖片中沒顯示完整，但這個類別通常會包含 select、enter_parking_duration 等方法來操作網頁上的選單和輸入框。

4. 步驟定義 (Step Definitions)

這部分是將測試劇本的文字轉化為實際動作：

正則表達式: When /^I park my car in the Valet Parking Lot for (.*)$/ 負責匹配劇本中的文字，並將時間（如 "30 minutes"）擷取到變數 duration 中。

動作:

$parkcalc.select('Valet Parking'): 在網頁下拉選單選擇「代客泊車」。

$parkcalc.enter_parking_duration(duration): 在網頁輸入框填入停車時長。

pending: 這裡目前被標記為待辦，因此測試會停在這裡，不會繼續執行後續的驗證邏輯。

### code 存放位置和用途
1. 頁面物件模型 (park_calc_page.py)
2. 環境設定 (environment.py)
3. 步驟定義 (steps/valet_steps.py)
4. .feature 檔案

### 專案目錄結構
my_parking_test/
├── features/                 <-- 核心資料夾  <\br>
│   ├── environment.py        <-- 環境設定   <\br>
│   ├── valet_parking.feature <-- 測試劇本 (需新增)   <\br>
│   └── steps/                <-- 步驟實作資料夾  <\br>   
│       └── valet_steps.py    <-- 步驟定義    <\br>
└── park_calc_page.py         <-- 頁面物件模型 (放在根目錄或 lib)
