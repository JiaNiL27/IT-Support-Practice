# A+ 模拟题重点

[⬅️ 返回目录](../README.md)

| 题目情境 | 答案 |
|---|---|
| 用户说不能打印，第一步要做什么？ | **Identify the problem**（询问用户） |
| 执行方案后下一步？ | **Verify full system functionality + preventive measures** |
| 打印文件卡在队列删不掉 | **Restart the Print Spooler service** |
| 陌生号码打来，急着要求重设密码 | **先按公司流程验证身份** |
| 假装员工打电话骗取密码重设 | **Social engineering (impersonation)**；电话形式也叫 **vishing** |
| 一般用户不能重启 Windows 服务 | **Principle of least privilege** |
| 重设密码时应该勾选什么？ | **User must change password at next logon** |
| 解锁后几分钟账号又被锁 | **手机等设备还在用旧密码** |
| `ipconfig` 显示 169.254.x.x | **APIPA → DHCP 失败**，电脑拿不到 IP |
| `ipconfig` 显示 Media disconnected | **网线没有连接**（物理层问题） |
| 重新向 DHCP 申请 IP 的指令 | **ipconfig /release** + **ipconfig /renew** |
| 网络排查应该先检查什么？ | **物理层**：网线、灯号（先硬件，后软件） |
| 排查效能问题时应该选 Shut down 还是 Restart？ | **Restart**（Fast Startup 开启时，Shut down 不会完全重置） |
| RAM 不够时 Windows 借用硬盘的空间叫什么？ | **Virtual memory / page file** |
| 自动清理暂存文件和回收站的 Windows 功能 | **Storage Sense** |
| Disk Cleanup 的指令 | **cleanmgr** |
| 电脑很慢，先用什么工具找出最占资源的程序？ | **Task Manager** |
| 哪个 Task Manager 标签可以停用开机启动程序？ | **Startup apps** |
| 在哪里看电脑多久没有重启？ | **Task Manager → Performance → CPU → Up time** |
| 查看系统错误记录的工具 | **Event Viewer**（`eventvwr.msc`） |
| 硬盘一直 100% 且有异响 | **硬盘可能故障 → 立即备份并上报** |
| 用户在钓鱼网页输入了密码，最优先要做什么？ | **重设密码 + 撤销所有会话（Revoke sessions）** |
| 用户打开了可疑附件，最优先要做什么？ | **断开网络（不要关机）+ 上报** |
| 用户收到不是自己触发的 MFA 通知，代表什么？ | **攻击者已经知道密码** → 按 Deny |
| 攻击者一直发 MFA 通知，等用户按同意 | **MFA fatigue attack** |
| 拿偷来的密码去其他网站试 | **Credential stuffing** |
| 用电话 / 短信进行的钓鱼 | **Vishing / Smishing** |
| 针对特定人或部门的钓鱼 | **Spear phishing** |

[⬅️ 返回目录](../README.md)
