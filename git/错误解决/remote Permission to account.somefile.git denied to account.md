> # error:   
> ## in windows git push to github "remote: Permission to account/somefile.git denied to account"

## 错误原因是：将仓库提交到与本地登入的github凭证上不同的账户上

> # 解决方法：
## 在windows中的 ——>Control Panel(控制面板)——>User Account and family Safety(用户账号和家庭安全)——>Manage Windows Credential(凭证管理)——>将跟Git有关的账号删除——>重新 push 仓库——>在弹出的凭证登录中登入要 push 的账户