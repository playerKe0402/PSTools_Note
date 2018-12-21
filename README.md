# PSTools_Note

## psexec 
### 使用 psexec 連到目標電腦需要 Administrator 權限的帳號

新增使用者帳號/密碼
```
net user root toor /add
```
將使用者加入 Administrator 群組
```
net localgroup administrators root /add
```
查詢本機中所有使用者
```
net user 
```
查詢本機中所有群組
```
net localgroup
```
### 在目標電腦新增機碼
```
reg add HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t reg_dword /d 1
```

### 使用 psexec 連到目標電腦使用cmd
```
psexec \\127.0.0.1 -u root -p 1234 cmd.exe
```
參數
```
-c：將指定的程式複製到遠端系統以執行。如果省略這個選項，則應用程式必須在遠端系統上的系統路徑中。
-d：請勿等候應用程式終止。僅使用這個非互動式應用程式的選項。
-f：即使檔案已經存在於遠端系統內，還是將指定的程式複製到遠端系統。
-i：執行此程式，才能夠讓它與遠端系統中指定的工作階段的桌上型電腦互動。如果沒有指定的工作階段，則處理序在主控台工作階段中執行。
-l：以限制使用者的身分執行處理序（刪除系統管理員群組，且只允許使用者群組指派的權限）。在 Windows Vista 中，使用低整合性執行處理序。
-p：指定選擇性使用者名稱密碼。如果省略這個動作，則會出現輸入隱藏密碼的提示。
-u：指定選擇性使用者名稱以登入遠端電腦。
-w：設定處理序的工作目錄（相對於遠端電腦）。
```
## 補充
### CMD下載方法
vbs 下載方法
```
Download "http://127.0.0.1/", "test.txt" > down.vbs
Function Download(strUrl, strFile) >> down.vbs
Set xPost = CreateObject("MSXML2.ServerXMLHTTP") >> down.vbs
xPost.Open "GET", strUrl,0 >> down.vbs
xPost.Send() >> down.vbs
Set sGet = CreateObject("ADODB.Stream") >> down.vbs
sGet.Mode = 3 >> down.vbs
sGet.Type = 1 >> down.vbs
sGet.Open() >> down.vbs
sGet.Write(xPost.responseBody) >> down.vbs
sGet.SaveToFile strFile,2 >> down.vbs
End Function >> down.vbs
```
使用 CMD 製作下載 down.vbs 

要分 3 行做
```
echo Download "http://127.0.0.1/", "test.txt" > down.vbs & echo Function Download(strUrl, strFile) >> down.vbs & echo Set xPost = CreateObject("MSXML2.ServerXMLHTTP") >> down.vbs & echo xPost.Open "GET", strUrl,0 >> down.vbs 
echo xPost.Send() >> down.vbs & echo Set sGet = CreateObject("ADODB.Stream") >> down.vbs & echo sGet.Mode = 3 >> down.vbs & echo sGet.Type = 1 >> down.vbs & echo sGet.Open() >> down.vbs 
echo sGet.Write(xPost.responseBody) >> down.vbs & echo sGet.SaveToFile strFile,2 >> down.vbs &echo End Function >> down.vbs
```

Call down.vbs 
```
down.vbs
pause
```
# Reference
[pstools工具下載](https://docs.microsoft.com/zh-tw/sysinternals/downloads/pstools)

[net指令使用](http://jon-and-jane.blogspot.com/2017/05/blog-post.html)

[解決拒絕存取](https://blog.twtnn.com/2013/08/pstools-win7hang.html)

[psexec參數](https://blog.yowko.com/psexec/)

[CMD三種下載方法](http://sky.candy.moe/2013/06/28/cmd-download-http-wget-vbs/)

[CMD創建文件常用指令](https://blog.csdn.net/sunjinshengli/article/details/53557684)
