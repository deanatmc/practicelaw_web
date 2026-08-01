# ⚖️ 法律達人競賽刷題酷（中華民國）

一套以 HTML、JavaScript 與 JSON 製作的法律選擇題練習系統，支援即時練習、模擬測驗、限時快答、成績統計及題庫管理。

目前完整題庫共收錄 26000 題，涵蓋憲法、行政法、民法、刑法、勞動法、消費者保護、智慧財產權、公司治理、金融保險、食品藥品、職業安全、移民、選舉、環境、文化資產及跨境法律等領域。

✨ 系統功能

* 每次隨機抽取 30 題
* 題目及選項隨機排列
* 即時練習模式
* 模擬考試模式
* 10 秒快答模式
* 即時顯示答案與解析
* 答對彩帶與連勝效果
* 測驗分數及正確率統計
* 歷史測驗紀錄
* 手動新增及刪除題目
* 匯入、匯出 JSON 題庫
* 自動讀取 GitHub 儲存庫中的 JSON
* 支援手機、平板及電腦
* 使用瀏覽器本機儲存學習紀錄

📚 題庫規模

檔案	題數	說明
law_bank_part_all.json	30,000	完整總題庫
law_bank_part2.json	6,721	分割題庫 Part 2
law_bank_part3.json	6,721	分割題庫 Part 3
law_bank_part4.json	6,721	分割題庫 Part 4
law_bank_part5.json	6,720	分割題庫 Part 5

law_bank_part2.json 至 law_bank_part5.json 合計 26,883 題。
如果要使用全部 30,000 題，建議直接載入 law_bank_part_all.json。

🧹 題庫整理原則

題庫已經過下列處理：

* 刪除完全重複的題目
* 排除上傳 ZIP 考卷中的原始題目
* 排除必須依賴圖片才能作答的題目
* 排除 Cxxx、特定目的代號及編碼記憶題
* 排除過度簡單或答案過於明顯的題目
* 排除罰金、罰鍰、刑期及期限數字記憶題
* 排除不合理及明顯錯誤的干擾選項
* 重新打亂題目順序
* 重新打亂每題選項
* 同步修正答案索引及解析答案字母

🗂️ 建議檔案結構

law-quiz/
├── index.html
├── law_bank_part_all.json
└── README.md

如果採用分割題庫：

law-quiz/
├── index.html
├── law_bank_part1.json
├── law_bank_part2.json
├── law_bank_part3.json
├── law_bank_part4.json
├── law_bank_part5.json
└── README.md

🚀 快速開始

方法一：使用本機伺服器

下載專案後，在專案資料夾執行：

python -m http.server 8080

接著開啟：

http://localhost:8080

不建議直接以 file:// 開啟 index.html，因為瀏覽器可能阻止 JavaScript 讀取 JSON 檔案。

方法二：部署至 GitHub Pages

1. 建立新的 GitHub Repository。
2. 上傳 index.html、題庫 JSON 與 README.md。
3. 進入 Repository 的 Settings。
4. 選擇 Pages。
5. 在 Build and deployment 選擇 Deploy from a branch。
6. 選擇 main 分支及 /root 目錄。
7. 儲存並等待 GitHub Pages 完成部署。

⚙️ 設定題庫檔案

目前 index.html 會依照 jsonCandidates 陣列尋找題庫檔案。

使用完整 30,000 題題庫

建議將程式中的檔案清單改為：

const jsonCandidates = [
    'law_bank_part_all.json'
];

使用分割題庫

const jsonCandidates = [
    'law_bank_part1.json',
    'law_bank_part2.json',
    'law_bank_part3.json',
    'law_bank_part4.json',
    'law_bank_part5.json'
];

請勿同時載入 law_bank_part_all.json 與各個 Part 檔案，否則相同題目會被重複加入。

🧾 JSON 題目格式

每一題使用以下格式：

{
  "question": "依照題目所述情境，下列法律分析何者最適當？",
  "options": [
    "選項 A",
    "選項 B",
    "選項 C",
    "選項 D"
  ],
  "answer": 2,
  "explanation": "答案：C。此處填寫法律依據及解析。"
}

欄位說明

欄位	類型	說明
question	字串	題目內容
options	陣列	四個選項
answer	整數	正確答案索引
explanation	字串	答案及法律解析

answer 採用從 0 開始的索引：

數值	答案
0	A
1	B
2	C
3	D

🎮 練習模式

即時練習

作答後立即顯示：

* 正確答案
* 法律解析
* 答題結果
* 目前連勝次數

模擬測驗

* 每次隨機抽取 30 題
* 測驗時間依題數設定
* 作答時不立即顯示答案
* 完成後統一計算分數及正確率

10 秒快答

* 每題限時 10 秒
* 超時自動判定未作答
* 適合訓練快速判斷能力

📊 學習紀錄

系統會記錄：

* 總答題量
* 平均正確率
* 最高連勝次數
* 每次測驗日期
* 測驗模式
* 得分及答對題數

學習紀錄儲存在瀏覽器的 localStorage。清除瀏覽器資料後，紀錄也會一併消失。

⚠️ 大型題庫效能提醒

完整題庫約有 30,000 題，檔案較大。部分瀏覽器的 localStorage 容量不足，可能無法快取完整題庫。

建議將快取程式改為：

try {
    localStorage.setItem(
        'law_quiz_v2026_dynamic_cache',
        JSON.stringify(quizData)
    );
} catch (error) {
    console.warn('題庫容量較大，略過 localStorage 快取。', error);
}

題庫管理頁面也不建議一次顯示全部 30,000 題。可以將：

quizData.forEach((q, idx) => {

改為：

quizData.slice(0, 100).forEach((q, idx) => {

或另外製作分頁、搜尋及虛擬列表功能。

🌐 使用的前端資源

本專案使用下列 CDN 資源：

* Tailwind CSS
* 芫荽字體 Iansui
* Font Awesome
* Canvas Confetti

因此第一次載入網頁時需要網路連線。

🛠️ 技術架構

* HTML5
* CSS3
* JavaScript
* Tailwind CSS
* JSON
* LocalStorage
* GitHub Pages

本專案不需要安裝 Node.js 套件，也不需要執行建置或編譯程序。

📌 使用提醒

* 法律可能隨時修正，題目內容應定期重新檢查。
* 本題庫適合法律教育、競賽練習及自我測驗。
* 題目與解析不應取代律師、主管機關或其他專業人士的正式法律意見。
* 若用於正式考試或教學，建議先由具法律專業者再次審核。
* 請勿同時載入總題庫及分割題庫，以免產生重複題目。

📄 專案名稱

法律達人競賽刷題酷｜30,000 題法律綜合題庫
# 如是對題目有任何疑問，請務必要加以查證
