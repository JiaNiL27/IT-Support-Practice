# Practice 2：账号被锁 / 重设密码

[⬅️ 返回目录](../README.md)

### 情境

> **自称 Jason（销售部）**：放假回来忘记密码，试了好几次，电脑显示 "Your account has been locked"。下午要见客户，要求直接把密码改成 **Jason123**。

### 关键线索 ⚠️

- 用户制造**紧急感**、给压力、要求**跳过流程**
- 员工编号 **正确**，但来电号码 **不是系统登记的号码**
- 回拨不可行（公司手机放在家里）

### 处理流程

1. 安抚用户，但**坚持先验证身份**
2. 询问员工编号
3. 发现来电号码不一致 → 提出回拨到登记号码（**只说最后几位数字**）
4. 回拨不可行 → 改由**主管确认**（先让用户自己说出主管名字，不要直接告诉他）
5. 主管确认身份 ✅
6. 在 AD 解锁账号，设定临时密码，勾选 **"User must change password at next logon"**
7. 请用户当场登录测试
8. 提醒用户**更新手机等设备上的密码**，避免账号再被锁

### 推荐英文说法

```text
I understand you're in a hurry, Jason. I'll get you back in as soon as possible.
But for security reasons, I need to verify your identity first.
Could you please tell me your employee ID?
```

```text
I notice you're calling from a different number than the one in our system.
For security, I'll need to call you back on your registered number ending in 5678. Is that okay?
```

```text
No problem. In that case, I'll verify with your manager.
Could you tell me who your manager is?
```

```text
I'm sorry, but I can't set a password you choose.
I'll give you a temporary password, and you'll be asked to create your own new password when you log in.
```

```text
Thanks for waiting, Jason. Your identity is confirmed, and I've unlocked your account.
Your temporary password is xxxxx. When you log in, the system will ask you to create a new password.
Could you try logging in now while I'm still on the line?
```

```text
One important thing: when you turn on your company phone, Outlook and Teams will ask for your password.
Please update it with your new password right away.
If you don't, the phone will keep trying the old password, and your account could get locked again.
```

### 技术知识

#### Social Engineering（社交工程）

攻击者假装是员工，利用以下手法让 IT 跳过安全步骤：

- **制造紧急感**："我很赶！"
- **给压力**："你直接改就好了！"
- **假装很熟**："你查一下就知道了！"

👉 不管多急，**都要先验证身份**。员工编号常出现在员工证、邮件签名上，**只靠员工编号不够**。

常见验证方法：员工编号 + 个人资料、回拨登记号码、主管确认、自助密码重设（SSPR）/ MFA。

#### 解锁账号：Active Directory Users and Computers（ADUC）

1. 打开 ADUC，用 Find 搜索用户
2. 右键用户 → **Reset Password**
3. 输入符合规则的临时密码
4. ✅ 勾选 **User must change password at next logon**
5. ✅ 勾选 **Unlock the user's account**
6. 按 OK

只解锁不改密码：用户 **Properties → Account** 标签 → 勾选 **Unlock account**

#### PowerShell（L2 常用）

```powershell
Unlock-ADAccount -Identity jlim
Set-ADAccountPassword -Identity jlim -Reset -NewPassword (Read-Host -AsSecureString "Temp Password")
Set-ADUser -Identity jlim -ChangePasswordAtLogon $true
```

#### Microsoft 365 / Entra ID

**Microsoft 365 Admin Center → Users → Active users** → 选择用户 → **Reset password**，并勾选首次登录时必须更改密码。

#### 注意事项

- **不要用用户指定的密码**，IT 人员也不应该知道用户的真正密码
- **不要用邮件发送临时密码**（用户登录不了邮箱，而且不安全）
- 账号**重复被锁**的常见原因：手机、平板上的 app 还存着旧密码

### 工单记录范例

```text
Issue: User unable to log in to computer. Error: "Your account has been locked."
       User returned from leave and forgot password.
Troubleshooting: User called from an unregistered number (+60 11-xxx 4321, registered: ending 5678).
                 Employee ID S10234 matched. Callback not possible as company phone was at home.
                 User correctly named manager. Identity verified by manager Michelle Tan via phone.
Root Cause: Account locked after 5 failed login attempts due to forgotten password.
Resolution: Unlocked account in AD and set a temporary password with
            "User must change password at next logon" enabled.
            Advised user to update the password on company phone (Outlook/Teams) to prevent re-lockout.
Result: User confirmed successful login and changed to a new password. Ticket closed.
```

> 🔐 **为什么要记录验证过程？** 安全审计、保护自己（证明有按流程做）、万一发生数据外泄时帮助调查。

---

[⬅️ 返回目录](../README.md)
