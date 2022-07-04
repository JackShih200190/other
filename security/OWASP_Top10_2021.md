OWASP 2017 vs OWASP 2021

![image](https://user-images.githubusercontent.com/55253641/177089994-f1425eb4-ad70-4127-a8ef-82a24cb0c586.png)


## OWASP_TOP10_2021
### 1.Broken Access Control (權限控制失效)
```
存取控制強化政策，使用戶不能採取在預期權限之外的行動。控制失效通常會導致未經授權的資訊洩露、修改或損壞所有資料，或執行超出用戶權限的業務功能
```
### 如何防禦

- 除公開的資源外，默認為拒絕存取。
- 一次性地建置存取控制機制，之後在整個應用程式中重複使用它們，包括最大限度地減少使用CORS。
- 模型的存取控制措施應該強化記錄所有權，而不是讓用戶可以創建、讀取、更新或刪除任何記錄。
- 獨特的應用程式業務限制要求應由領域模型予以強化。
- 停用Web伺服器目錄列表，並確保檔案中繼資料（例如，.git)和備份檔案不在web根目錄中。
- 記錄存取控制失效，並在適當的時間警示管理員（例如，重覆性失效）。
- 對API和控制器存取進行流量限制，以最小化自動攻擊工具所帶來的損害。
- JWT令牌於登出後，在伺服器端應使其失效。

### 攻擊環境範例
```
情境 #1： 應用程式在存取帳戶資訊的SQL呼叫中使用未經驗證的資料：

pstmt.setString(1, request.getParameter("acct"));

ResultSet results = pstmt.executeQuery( );

攻擊者只需修改瀏覽器的“acct”參數即可發送他們想要的任何帳號。如果沒有正確驗證，攻擊者可以存取任何用戶的帳戶。

https://example.com/app/accountInfo?acct=notmyacct

情境#2： 攻擊者僅強迫瀏覽某些目標網址。存取管理頁面需要管理員權限。

https://example.com/app/getappInfo

https://example.com/app/admin_getappInfo

如果未經身份驗證的用戶可以存取任一頁面，那就是一個缺陷。 如果一個非管理員可以存取管理頁面，這也是一個缺陷。
```
### 2.Cryptographic Failures(加密機制失效)


### 3.Injection(注入式攻擊)
### 4.Insecure Design(不安全設計)
### 5.Security Misconfiguration(安全設定缺陷)
### 6.Vulnerable and Outdated Components(危險或過舊的元件)
### 7.Identification and Authentication Failures(認證及驗證機制失效)
### 8.Software and Data Integrity Failures(軟體及資料完整性失效)
### 9.Security Logging and Monitoring Failures(資安記錄及監控失效)
### 10.Server-Side Request Forgery(伺服端請求偽造)
