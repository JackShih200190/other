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
```
敏感資料外洩，注重於加密金鑰失效或是資料未加密
```

### 如何防禦
- 對應用程式處理、儲存、傳輸的資料進行分類，根據隱私法、法令法規、或商業需求辨識哪些為敏感性資料。
- 依照分類執行對應的控制措施。
- 非必要不儲存敏感性資料，盡快捨棄或使用符合PCIDSS的資料記號化(tokenization)甚至截斷(truncation)。 沒有被保存的數據是不會被竊取的。
- 確保將所有靜態的敏感性資料加密。
- 確認使用最新版且標準的強演算法、協定及金鑰; 使用適當的金鑰管理。
- 使用安全的協定加密傳輸中的資料，像是有完全前向保密(PFS)、伺服器加密優先順序(cipher prioritization by the server)及安全參數的TLS。 
使用像是HTTP強制安全傳輸技術(HSTS)的指令強化加密。

- 針對包含敏感資料的回應停用快取。
- 使用具有雜湊迭代次數因素(work factor/delay factor)，如Argon2, scrypt, bcrypt或PBKDF2的強自適應性加鹽雜湊法來儲存密碼。
獨立驗證設定的有效性。

### 攻擊環境範例
```
情境 #1: 有一個應用程式使用自動化資料庫加密來加密資料庫中的信用卡卡號，但是資料被存取時是被自動解密的，進而允許透過SQL注入缺陷來存取信用卡卡號明文。

情境 #2: 有一個站台沒有對所有頁面強制使用TLS或支援脆弱的加密，攻擊者監控網路流量(如在不安全的無線網路), 將連線從HTTPS降級成HTTP，並攔截請求竊取使用者的會話(session) cookies，之後攻擊者重送竊取到的會話(session) cookies並劫持用戶(認證過的)的會話，進而存取或修改使用者的隱私資料。 除了上述以外，攻擊者也能修改傳輸的資料，如匯款收款人。

情境 #3: 密碼資料庫使用未被加鹽或簡單的雜湊來儲存每個人的密碼，一個檔案上傳的缺陷可以讓攻擊者存取密碼資料庫，所有未被加鹽的雜湊可以被預先計算好的彩虹表公開。即使雜湊有被加鹽，由簡單或快速的雜湊法算出的雜湊仍能被GPU破解。
```
### 3.Injection(注入式攻擊)
### 4.Insecure Design(不安全設計)
### 5.Security Misconfiguration(安全設定缺陷)
### 6.Vulnerable and Outdated Components(危險或過舊的元件)
### 7.Identification and Authentication Failures(認證及驗證機制失效)
### 8.Software and Data Integrity Failures(軟體及資料完整性失效)
### 9.Security Logging and Monitoring Failures(資安記錄及監控失效)
### 10.Server-Side Request Forgery(伺服端請求偽造)
