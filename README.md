## 獎學金資訊整合平台
為了統整獎學金資訊，與我的夥伴 Lyndon Yeh 一起使用 Java Spring MVC 作為主要技術架構開發此專案。
![frontend](https://github.com/davewylee/ScholarshipPlatform/assets/115342968/546efd95-98c5-4d02-94f6-c09f8cea5574)![backend](https://github.com/davewylee/ScholarshipPlatform/assets/115342968/e465b4b2-bb1b-4c09-b508-d0ec4692bda2)

## 使用技術
語言 : Java

架構 : Spring MVC

前端 : Bootstrap, JSP

資料庫 : MySQL

安全性 : SSL/TLS 憑證( Https ) / OTP 信箱驗證 / Bcrypt Hash 密碼加密 / 路徑管理(分離前後台 url 訪問權限)

## [專案網址連結](http://3.107.26.132:8080/Scholarship/)

## Entity
1. Institution Table

| institutionId | institutionName   | contact  | contactNumber |
|---------------|-------------------|----------|---------------|
| 25570111      | 行天宮助寒獎學金 | 陳小姐   | 0912345678    |

2. User Table

| userId | institutionId | userName | password |
|--------|---------------|----------|----------|
| 1      | 25575888      | jojo123  | pass123  |
| 2      | 25575889      | Nono456  | pass456  |
| 3      | 25575881      | Kiki789  | pass789  |

3. Scholarship Record Table

| scholarshipId | userId | institutionId | scholarshipName | scholarshipAmount | entityId | updatedTime       | StartDate  | EndDate    | isExpired | webUrl    | contact | contactNumber |
|---------------|--------|---------------|-----------------|-------------------|----------|-------------------|------------|------------|-----------|-----------|---------|---------------|
| 101           | 1      | 25570111      | 行天宮助寒獎    | 500000            | 1        | 2023/12/13 15:00 | 2023/05/03 | 2023/05/04 | 0         | yahoo.com | 李先生  | 0988777666    |

4. Entity Table

| entityId | entityName |
|----------|------------|
| 1        | 幼稚園     |
| 2        | 國小       |
| 3        | 國中       |
| 4        | 高中       |
| 5        | 大學       |
| 6        | 研究所     |

5. Garbage Collection Table

| garbageId | institutionId | deletedData                                    |
|-----------|---------------|------------------------------------------------|
| 901       | 25575888      | {"scholoarshipId":"301", "userId":"101" ...} |
| 902       | 25575889      | {"scholoarshipId":"302", "userId":"101" ...} |
| 903       | 25575881      | {"scholoarshipId":"303", "userId":"101" ...} |


## 功能 (API) : 

### 獎助機構 institution:
1. 註冊 (新增獎助機構資訊)
2. 更改聯絡資訊
   
	2-1 更改項目聯絡人
   
	2-2 更改項目聯絡連絡電話
3. 根據id查詢機構是否已存在
4. 根據機構名稱查詢機構是否已存在
5. 查詢所有機構
6. 根據機構名稱查詢機構是否已存在

### 使用者 user:
1. 註冊帳號密碼 (新增使用者)
2. 根據userId修改密碼
3. 查詢所有使用者
4. 根據username查找使用者
5. 根據userId查找使用者
		
### 獎學金上傳紀錄 Scholarship:
1. 新增一筆獎學金
2. 根據 scholoarshipId 更改上架狀態
3. 刪除一筆獎學金
4. 查詢獎學金紀錄(包含上架與否與過期與否 僅限項目所有方)
5. 查詢所有獎學金列表 
6. 查詢所有已上架獎學金列表
7. 根據條件查詢獎學金
   
	7-1 根據entityId查詢獎學金
   
	7-2 根據entityId/scholarshipAmount查詢獎學金
   
	7-3 根據scholarshipAmount查詢獎學金
   
	7-4 根據scholarshipId查詢獎學金 
8. 根據scholarshipId刪除獎學金至資源回收桶

### 資源回收桶 GgarbageCollection:
1. 根據 scholarshipId 刪除資源回收桶的獎學金(復原)
2. 根據 institutionId 從資源回收桶查詢一筆獎學金紀錄
3. 根據 scholarshipId 從資源回收桶查詢一筆獎學金紀錄

### 身分別
1. 根據 EntityId 查找 Entity


## 資料庫
MySQL

## 功能導覽
1. 前台
   
    1-1. 篩選
   
        - 無條件
        - 篩選身分別
        - 篩選金額 : 級距、自行輸入       
        - 篩選 身分別+金額
    1-2. url 超連結可連結至獎學金頁面

2. Datatable
   
    2-1. 按照欄位遞增/遞減
   
    2-2. 可調整顯示筆數
   
    2-3. 複製
   
    2-4. 匯出
   
        - CVS
        - Excel
        - Print (可輸出 PDF)
    2-5. 搜索
   
    2-6. 上一頁/下一頁

3. 註冊
   
    3-1. 輸入無效(資料庫已存在的)mail : 顯示信箱錯誤
   
    3-2. 輸入有效 
    
    3-3. 輸入信箱驗證碼
   
    3-4. 輸入無效密碼 : 顯示錯誤
   
        - 不符合大寫小與數字規則
        - 不一致
        - 未帶入資訊

4. 忘記密碼
   
    4-1. 輸入有效 mail
   
    4-2. 輸入無效(資料庫未存在的)mail : 顯示信箱錯誤
   
    4-3. 輸入信箱驗證碼
   
    4-4. 重設密碼
   
        - 輸入無效密碼 : 顯示錯誤
            - 不符合大寫小與數字規則
            - 不一致
            - 重設成功後, 重設密碼頁將失效(再次訪問, 頁面會強制重新導向登入頁)

5. GitHub登入
   
    5-1. 登入 : menu 顯示前台 username
   
    5-2. 登出

6. 前台
   
    6-1. menu 顯示新增 : 後台首頁

7. 修改會員資料
   
    7-1. 修改聯絡人 / 連絡電話
   
        - 已登入的聯絡人透過url只能進入自己userId的網址:https://localhost:8443/Scholarship/mvc/scholarship/backend/edit/8
        - 輸入其他的 userId 將會被攔截重新導向至登入頁
    7-2. 輸入密碼確認修改
   
    7-3. 重設密碼連結至重設密碼頁

8. 後台
   
    8-1. menu 顯示新增 :
   
        - 修改資料頁
        - 資源回收桶
    8-2. 新增獎學金
   
        - 新增後獎學金進入後台
        - 日期防呆 : 截止日期大於開始日期
        - 欄位驗證
            - 未帶入資訊
        - 聯絡人與聯絡電話自動帶入 session 值
        - 複製功能 : 帶入單筆已新增獎學金資訊至新增欄位
            - 無法複製其他機構的獎學金資料(網址參數為scholarshipId)
    8-3. 上下架
   
        - 上架後變更資料庫為上架狀態, 並讓前台可以顯示
        - 下架後變更資料庫為下架狀態, 並讓資訊從前台移除     
        - 下架驗證 :
            - 截止日小於目前日期，變更資料庫為下架狀態，並在後台跳出圖示通知
            - 過期已下架獎學金無法重新上架
    8-4. 刪除 : 跳出是否刪除警告
   
        - 刪除後資訊傳入資源回收桶


9. 資源回收桶
    
    9-1. 顯示永久刪除倒數時間
   
    9-2. 設定定期清除功能 : 時間到期後自動從資料庫中永久刪除
   
    9-3. 復原 : 資料回復至後台首頁


## Jemeter 測試資料

### [完整報告](https://davewylee.github.io/ScholarshipJmeterReport/)

### 報告參數
新增獎學金次數: 3000

登入次數: 40

測試腳本

執行緒: 10個

啟動延遲: 5秒

迴圈持續時間: 20分鐘

### 測試腳本流程 

5秒內登入10個用戶

每名用戶呼叫100次請求

重複3次

### 彙整報告

總請求次數(#Samples): 3040次

平均響應時間(Average): 3918(ms)

最小響應時間(Min): 1(ms)

最大響應時間(Max): 48363(ms)

50％ 用戶的響應時間(Median): 3940.00(ms)

標準偏移量/標準差(Std.Dev): 986.29

錯誤率(Error %): 0.92%

每秒請求吞吐量(Throughtput): 2.52/sec

每秒收到流量(Received KB/sec): 3772.19 

每秒發送流量(Send KB/sec): 0.61


#Samples: 本次測試共發出了多少次請求

Average: Request 的平均響應時間

Median: 中位數 (50％ 用戶的響應時間)

Error%: 本次測試中出現錯誤的請求的數量/請求的總數

Throughput: 吞吐量，默認情況下表示每秒完成的請求數(Request per Second)，伺服器能夠接受的最大速率

KB/Sec: 每秒從伺服器接收到的數據量

ThreadGroup 線程組: 代表一定數量的並發用戶，它可以用來模擬並發用戶發送請求

Ramp-up period: 指每個請求發生的總時間間隔，單位: 秒

