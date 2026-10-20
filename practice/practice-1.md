# Practice 1：Outlook 收不到邮件

[⬅️ 返回目录](../README.md)

### 情境

> **Sarah（财务部）**：今天早上 Outlook 一直收不到新邮件，同事都正常。等一下要发重要报表给老板，很急！

### 关键线索

- 只有她有问题，同事正常
- 网页和 Teams 都正常 → **网络没问题**
- 邮件卡在 **Outbox**
- Outlook 右下角显示 **"Working Offline"**

### 处理流程

1. 安抚用户，询问问题从什么时候开始、能不能发邮件
2. 确认网络连接（网页、Teams 是否正常）
3. 请用户看 Outlook **右下角的状态栏**
4. 发现是 **Working Offline**
5. 指导用户：**Send / Receive** 标签 → 点 **Work Offline** 关掉
6. 确认状态变成 **"Connected to: Microsoft Exchange"**，邮件正常收发
7. 解释原因，教用户以后怎么自己处理

### 推荐英文说法

```text
Please look at the bottom-right corner of the Outlook window.
There's a thin bar there. Does it show any message?
```

```text
Don't worry, it's not serious. Outlook is just in offline mode, and it's an easy fix.
Please click the Send / Receive tab at the top.
You'll see a button called Work Offline. Click it once, and wait a few seconds.
The message at the bottom should change to "Connected".
```

```text
You didn't break anything. The Work Offline button is easy to click by accident,
and it happens to a lot of people.
If you see "Working Offline" again, just click that same button to turn it off.
```

### 技术知识：Working Offline vs Disconnected

**Work Offline** 是 Outlook 的一个功能（设置开关），不是故障。它让用户在没网络时也能看已下载的邮件。**这个设置重启 Outlook 后会保留**，所以重启没有用。

常见原因：

- 不小心按到（最常见）
- 出差、搭飞机时自己打开，后来忘了关
- Outlook 启动时连不上服务器，用户在提示窗口选了离线

| 状态栏显示 | 意思 | 处理方法 |
|---|---|---|
| **Working Offline** | 离线模式被**手动打开** | 关掉 Work Offline 按钮 |
| **Disconnected / Trying to connect…** | Outlook **想连但连不上** | 检查网络、VPN、账号密码、服务器状态；多人同时出问题 → 上报 L2 |

### 工单记录范例

```text
Issue: User unable to send/receive emails in Outlook since this morning. Emails stuck in Outbox.
Troubleshooting: Confirmed network OK (web & Teams working). Restarted Outlook, issue persisted.
                 Status bar showed "Working Offline".
Root Cause: Outlook "Work Offline" mode was enabled (likely clicked by accident).
Resolution: Guided user to Send/Receive tab → clicked "Work Offline" to disable it.
Result: Outlook reconnected to Exchange. User confirmed emails sent and received successfully.
        Ticket closed.
```

---

[⬅️ 返回目录](../README.md)
