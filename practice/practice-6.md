# Practice 6：钓鱼邮件（Phishing）

[⬅️ 返回目录](../README.md)

> 🔐 这一题和前面不一样：目标不是"帮用户修好"，而是**先控制风险**。

### 情境

> **Ahmad（Procurement）**: "I think I might have done something stupid. About ten minutes ago, I got an email saying my Microsoft 365 password was going to expire today, and I needed to click a link to keep it. It had the Microsoft logo and everything, so I clicked it. But now that I look at it again, the sender's email is kind of weird… something like `support@micros0ft-security[.]com`. Is that bad? Am I going to get in trouble?"

### 关键线索

- 用户**很紧张**，担心会被骂 → 先安抚，并**称赞他快速通报**
- 寄件者地址可疑：**micros0ft**（数字 0 代替字母 o）
- 邮件**制造紧急感**："密码今天到期"
- 用户在假网页**输入了邮箱和密码** 🔑
- 用户**没有下载文件** → 不是恶意软件的情况
- 通话中收到 **MFA 通知**，地点 **Lagos, Nigeria** → **证实攻击者已经有密码**
- 用户**其他网站也用同一个密码**（私人 Gmail、网上银行）

### 处理流程（对应七步法）

| 步骤 | 做了什么 |
|---|---|
| 1. Identify | 安抚用户，问**有没有输入密码**、**有没有下载文件** |
| 2. Theory | 判断风险：**密码被偷了**（不是中病毒） |
| 3. Test | MFA 通知出现，**证实**攻击者有密码 |
| 4. Plan | 验证身份 → 重设密码 → 撤销会话 → 上报 |
| 5. Implement | 叫用户按 **Deny**、重设密码、**撤销所有会话**、**上报安全团队** |
| 6. Verify + Prevent | 用户用新密码安全登录；改私人密码、开两步验证、学会辨认钓鱼邮件 |
| 7. Document | 写工单，加上 **Timeline**，状态 **Escalated** |

### 推荐英文说法

```text
Hi Ahmad, this is Eleven from the IT department.
Don't worry, you're not in trouble. You did the right thing by calling us right away.
Let's check a few things quickly. After you clicked the link, did you type in your email or password?
And did you download or open any file?
```

```text
No, please don't go to the login page yet.
I'll reset your password and sign you out of all your Microsoft 365 sessions,
so whoever has your old password can't use it.
Before I reset it, I just need to quickly verify your identity. Could you tell me your employee ID?
```

```text
Press Deny, right now!
Someone is trying to log in to your account with your password, but because you pressed Deny, they can't get in.
If you get any more requests like this, please deny all of them.
I'm resetting your password right now, so your old password will stop working.
```

```text
We've stopped them for now, but we're not finished yet. Here's what's next.
First, I'm signing you out of all Microsoft 365 sessions, just in case they logged in somewhere before.
Second, I'll report this to our security team right away.
They'll check your account and make sure nothing else happened.
Now, a few things for you:
1. In Outlook, select that email, click Report at the top, then Report phishing.
   Please don't delete it, forward it, or click the link again.
2. To log in, open the Outlook app directly, or type office.com in your browser yourself.
   Your temporary password is xxxxx, and you'll be asked to create a new one.
3. Do you use the same password anywhere else? If so, please change it there too.
```

```text
Yes, that's a problem, so please change your Gmail and banking passwords today,
as soon as we finish this call. Attackers often try a stolen password on other websites to see if it works.
Please use a different password for each account, and turn on two-step verification if you can.
If you see anything strange in your bank account, contact your bank right away.
The security team will contact you soon and may ask you a few questions about the email.
For next time, here are some warning signs: check the sender's email address carefully,
and be careful with emails that rush you, like "your password expires today". If you're not sure, just call us.
You did a great job calling us so quickly. That really helped protect your account.
Is there anything else I can help you with today? Take care, Ahmad!
```

### 技术知识

#### 两种情况，两种处理

| 情况 | 危险在哪里 | 最优先要做的事 |
|---|---|---|
| **在假网页输入了密码** 🔑 | 密码在攻击者手上，他可以**从任何地方**登录 | **马上改密码 + 撤销所有会话（Revoke sessions）+ 上报** |
| **下载或打开了恶意文件** 🦠 | 恶意软件在**用户电脑里**，可能扩散或传出资料 | **断开网络（拔网线、关 Wi-Fi），但不要关机 + 上报** |
| **两个都做了** | 两种危险都有 | **两个都要处理** |

> ⚠️ **为什么不要关机？** 关机会让内存里的资料消失，安全团队就少了调查线索。
> ⚠️ **为什么只改密码不够？** 已经登录的攻击者**不一定会被登出**，所以要 **Revoke sessions / Sign out everywhere**。

#### MFA（多重验证）

- MFA 通知只有在**密码输入正确之后**才会出现 → **出现不是自己触发的 MFA = 攻击者已经有密码**
- **任何不是自己触发的 MFA，一律按 Deny**
- IT **不会**主动发 MFA 通知再叫用户按同意
- **MFA fatigue attack（MFA 疲劳攻击）**：攻击者一直发 MFA 通知，等用户不耐烦或误以为是 IT 发的就按下去

#### 常见攻击术语

| 术语 | 意思 |
|---|---|
| **Phishing** | 假冒可信来源的邮件或讯息，骗取密码或让用户下载恶意软件 |
| **Spear phishing** | 针对**特定人或部门**的钓鱼（例如采购部、财务部） |
| **Vishing / Smishing** | 用**电话** / **短信**的钓鱼 |
| **Credential harvesting** | 用假登录页面收集账号密码 |
| **Credential stuffing（撞库）** | 拿偷来的密码去**其他网站**试 |
| **Spoofed domain** | 模仿真实网域，例如 `micros0ft`、`rnicrosoft`（r + n 看起来像 m） |
| **BEC（Business Email Compromise）** | 攻击者控制员工邮箱后，假冒他向供应商或同事要钱 💸 |

#### 辨认钓鱼邮件的警讯

- **寄件者地址**拼法怪怪的，或和显示名称不一样
- **制造紧急感**："今天到期"、"马上处理，否则停用"
- 要求**点链接登录**或**输入密码**
- 鼠标移到链接上（**不要点**），看真正的网址
- 意外的附件，特别是 `.zip`、`.html`、`.exe`、启用宏的 Office 文件

#### 钓鱼邮件的处理原则

| ✅ 要做 | ❌ 不要做 |
|---|---|
| 用 Outlook 的 **Report → Report phishing** 举报 | 删除（安全团队需要调查） |
| 有疑问就打给 IT | 转寄给同事"提醒"他们 |
| 直接打开 Outlook 程序或自己输入网址登录 | 再点邮件里的链接 |
| 每个账户用不同的密码，开启两步验证 | 所有网站用同一个密码 |

#### Security incident 的 L1 原则

- **一定要上报安全团队（Security team / SOC）**，L1 不能自己处理完就关单
- 情况紧急也要**先验证身份**
- **不要责备用户**，称赞他快速通报，用户下次才会**一样快**通报
- 紧急时，**最重要的指示放在最前面，而且要短**
- **诚实回答**："现在挡住了，但还没结束"，不要随便说"安全了"
- 区分**IT 要做的事**和**用户要做的事**
- 私人账户（Gmail、银行）IT 没有权限处理 → **提醒用户自己处理、该找谁**

#### Defang（去除可点击性）

在工单里写恶意网址或邮箱时，要**去活化**，避免别人不小心点到：

| 原本 | Defang 后 |
|---|---|
| `support@micros0ft-security.com` | `support@micros0ft-security[.]com` |
| `https://micros0ft-login.com` | `hxxps://micros0ft-login[.]com` |

### 工单记录范例

```text
Issue: User received a phishing email claiming his Microsoft 365 password would expire today.
       User clicked the link and entered his username and password on a fake Microsoft login page.
       User called IT ~10 minutes later.
Timeline:
  ~09:55 - User received phishing email, clicked link, entered credentials on fake login page
  10:05  - User called IT Help Desk
  10:07  - Identity verified (employee ID P20871, call from registered desk ext. 4417)
  10:08  - 2 MFA prompts from Lagos, Nigeria; user denied both
  10:09  - Password reset (temporary password, must change at next logon)
  10:11  - All Microsoft 365 sessions revoked
  10:12  - Incident reported to Security team
  10:15  - User reported phishing email in Outlook; logged in via Outlook app and set new password
Troubleshooting: Sender address: support@micros0ft-security[.]com (spoofed domain using "0" instead of "o").
                 User entered credentials on the fake page. User confirmed no files downloaded.
                 Sign-in logs showed 2 failed sign-ins from Lagos, Nigeria (MFA denied by user).
Root Cause: User entered credentials on a phishing (credential harvesting) page.
            Password compromised; MFA prevented unauthorized access.
Resolution: Verified user identity. Reset password and revoked all M365 sessions.
            User denied all MFA prompts. Escalated to Security team.
            User reported the phishing email via Outlook (email not deleted, kept for investigation).
Result: User logged in via the Outlook app and set a new password. No successful attacker sign-in seen in logs.
        User uses the same password for personal Gmail and online banking; advised to change both today,
        use unique passwords, and enable two-step verification. User educated on phishing warning signs.
        Ticket status: Escalated to Security team.
```

> ⏰ **为什么要写 Timeline？** 安全团队要对照登录记录，检查在**输入密码（09:55）到撤销会话（10:11）**之间，攻击者有没有登录成功。没有 Timeline，他们就不知道要查哪一段时间。

---

[⬅️ 返回目录](../README.md)
