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

[⬅️ 返回目录](../README.md)
