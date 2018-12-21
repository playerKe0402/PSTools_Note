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

# Reference
[pstools工具下載](https://docs.microsoft.com/zh-tw/sysinternals/downloads/pstools)
[net指令使用](http://jon-and-jane.blogspot.com/2017/05/blog-post.html)
[解決拒絕存取](https://blog.twtnn.com/2013/08/pstools-win7hang.html)
