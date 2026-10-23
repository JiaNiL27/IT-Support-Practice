# Practice 8：新员工入职（Onboarding）

[⬅️ 返回目录](../README.md)

> 📋 这一题是**流程类**的工作，不是故障排查。重点在**收集资料**、**按照流程**和**安全意识**。

### 情境

> **Rachel（Sales Manager）**: "I have a new salesperson, Emma Wong, starting tomorrow morning at 9. Sorry, I know it's short notice. HR said they'd tell you, but I guess they forgot. She needs everything: a laptop, email, Teams, access to our sales files… you know, all the usual stuff. Can you get it ready by tomorrow? Oh, and to make it easy, can you just give her the same access as Mark? He's also in sales."

### 关键线索

- **"Everything" / "the usual stuff"** 很模糊 → 要问**具体需求**
- **HR 还没有提交正式请求** → 建账号、开权限前要有 **HR 的授权**
- **"Same access as Mark"** → Mark 还有以前 Finance 项目的权限 → **Privilege creep** 风险
- 经理要求**用邮件寄密码** → 不安全，改为**当面交给本人**
- **明天 9 点**就要用 → 不要承诺控制不了的事，说清楚**条件**

### 处理流程

| 阶段 | 做了什么 |
|---|---|
| 1. Gather requirements | 问清楚职位、办公室、经理、需要的系统、共享文件夹、Teams 频道 |
| 2. Approval | 请经理通知 HR 提交正式请求（HR-2291） |
| 3. Prepare | HR 请求到之前，先准备笔记本和标准软件；请求到之后，建账号、开权限 |
| 4. Access by role | 不复制 Mark 的权限，按 **Sales Executive 角色**（RBAC）设定 |
| 5. Day 1 | 当面确认身份、给临时密码、设定 MFA、测试所有东西 |
| 6. Document | 记录所有完成的项目，附上 HR 请求编号和资产编号 |

### 推荐英文说法

```text
Hi Rachel, this is Eleven from the IT department.
No problem, I'll do my best to get everything ready for Emma by tomorrow. Could I ask you a few quick questions first?
First, could you tell me exactly what Emma needs? For example, her job title, which office she'll work in,
and which systems, shared folders, and Teams channels she'll use.
Second, we haven't received an onboarding request from HR yet. We need it before we can create her account.
Could you ask HR to submit it today?
Last, about giving her the same access as Mark: does Emma have exactly the same role as Mark?
Sometimes people have extra access from older projects, so it's safer to set up access based on Emma's own role.
```

```text
Thanks for the details, that's really helpful.
Sure, we'll start setting up her laptop and installing the standard software today.
Once we receive the onboarding request from HR, we'll create her account and set up her access.
As long as HR sends it this afternoon, everything should be ready by 9 tomorrow.
About the Finance folders, we won't give Emma that access, because she doesn't need it for her job.
Our security policy is to give each person only the access they need. It's called the principle of least privilege.
So instead of copying Mark's access, I'll set up her access based on the Sales Executive role.
Also, you might want to check if Mark still needs the Finance access.
```

```text
I'm sorry, but for security reasons, we can't send passwords by email.
Instead, I'll come to Emma's desk at 9 tomorrow and give her a temporary password in person.
When she logs in with it for the first time, Windows will ask her to create her own new password.
I'll also help her set up Microsoft Authenticator for MFA at the same time,
so her account is protected from day one.
```

### 技术知识

#### 为什么要等 HR 的请求？

- HR 请求是**正式授权**，证明这个人**真的是新员工**
- 如果谁打电话说"有新员工"就开账号，攻击者也能用这一招（**Social Engineering**，见 [Practice 2](practice-2.md)）
- HR 的资料（职位、部门）是设定**正确权限**的依据
- HR 请求到之前，可以先做**不涉及权限**的准备（笔记本、标准软件）

#### Privilege creep 与 RBAC

| 概念 | 意思 |
|---|---|
| **Privilege creep（权限蔓延）** | 员工换项目或部门时，新权限加上去了，旧权限却没拿掉，越累积越多 |
| **Principle of least privilege（最小权限原则）** | 每个人只拿到工作需要的最少权限 |
| **RBAC（Role-Based Access Control）** | 每个职位设定一个**群组**，新员工加入群组就自动拿到该职位需要的权限 |
| **模板账号（Template account）** | 专门的停用账号（例如 `_Template_SalesExec`），只有该职位的标准群组。复制它是安全的，因为它没有真人在用，不会累积多余权限 |

> ⚠️ **不要复制真实员工的权限**，会连他多余的权限一起继承。

#### 怎么安全地交付密码？

| ❌ 不要 | ✅ 可以 |
|---|---|
| 用邮件寄密码（会留在邮箱，邮箱被入侵就外泄） | **IT 当面交给本人**，先确认身份 |
| 经过第三个人（经理、同事） | 寄短信到 HR 提供的**私人手机** |
| 使用不会过期的密码 | **Temporary Access Pass（TAP）**：有时间限制的一次性登录码 |

临时密码一定要勾选 **"User must change password at next logon"**，并在第一天设定 **MFA**。

#### Onboarding vs Offboarding

| | Onboarding（入职） | Offboarding（离职） |
|---|---|---|
| 账号 | 建立账号、分配授权 | **停用账号**、移除授权 |
| 权限 | 按角色加入群组 | **移除所有群组和权限** |
| 设备 | 准备并登记笔记本 | **收回**笔记本和配件，更新资产记录 |
| 资料 | — | 依公司政策处理邮箱和文件（例如转给经理） |

> ⚠️ 离职员工的账号没停用 = 他还能登录公司系统，是很大的安全风险。

### Onboarding Checklist（English）

#### A. Account 👤

- [ ] **Confirm the HR request** (e.g. HR-2291): full name, job title, department, manager, office, and start date are correct
- [ ] **Create the user account** in **Active Directory / Entra ID**, following the company naming convention (e.g. `emma.wong@company.com`), and fill in job title, department, manager, and office
- [ ] **Set a temporary password** and enable **"User must change password at next logon"**
- [ ] **Assign a Microsoft 365 license** → Outlook mailbox, Teams, and OneDrive are created automatically
- [ ] **Add the user to groups**:
  - **Sales-Executives** security group → access to the Sales shared drive and other role-based resources
  - **Sales team distribution list** → receives team emails
  - **Sales team / channels in Teams**
- [ ] **CRM system**: submit an access request following the process (may need approval from the CRM app owner)

#### B. Device 💻

- [ ] Prepare the laptop with the **company standard image** (or enroll it with **Intune / Autopilot**)
- [ ] Install **standard software**: Office, Teams, browser, VPN, antivirus, etc.
- [ ] Install **Windows updates**
- [ ] Confirm **BitLocker encryption is enabled** and the recovery key is backed up 🔐
- [ ] Record the laptop's **asset tag** and **serial number** in the **asset management system**, and assign it to the user
- [ ] Prepare accessories: **charger**, mouse, **headset** 🎧
- [ ] Check the desk: **docking station and monitors** are set up and working (with the **latest drivers**)
- [ ] Set up **printers**

#### C. Day 1 👋

- [ ] **Verify the new employee's identity** (staff ID card or HR records) before giving the temporary password
- [ ] Help the user **log in for the first time** and **create their own password**
- [ ] Set up **MFA** (Microsoft Authenticator)
- [ ] **Test everything**: Outlook can send and receive emails, Teams works, the Sales shared drive opens, CRM login works, printer works
- [ ] **Quick IT introduction**:
  - How to **contact IT** (phone, raise a ticket)
  - How to **spot phishing emails** and use **Report phishing**
  - Sign the **Acceptable Use Policy (AUP)**

#### D. Documentation 📝

- [ ] Record all completed items in the ticket, with the **HR request number** (e.g. HR-2291)
- [ ] Update the **asset management system**
- [ ] **Close the ticket** after confirming with both the new employee and the manager that everything works

### 系统操作流程（Hybrid：AD + Microsoft 365）

```
① 确认 HR 请求 → ② AD 建用户 → ③ 同步到云端 → ④ M365 分配授权 → ⑤ 其他权限 → ⑥ 准备电脑 → ⑦ 检查 → ⑧ 记录
```

#### ② 在 Active Directory 建立用户（ADUC）

**1. 选择正确的 OU**（Organizational Unit，AD 里的"文件夹"）

```
company.local
└── Company
    └── Users
        ├── Finance
        ├── HR
        └── Sales   ← 新员工放这里
```

> ⚠️ OU 要放对！公司常用 **Group Policy（GPO）**对整个 OU 套用设定（例如自动连接共享文件夹、打印机）。

**2. 建立用户**：在 OU 上**右键 → New → User**

| 栏位 | 填写 |
|---|---|
| **First name / Last name** | Emma / Wong |
| **Full name** | Emma Wong |
| **User logon name** | `emma.wong`（按照公司命名规则） |

设定临时密码：✅ **User must change password at next logon**；❌ 不要勾选 *Password never expires*

**3. 填写详细资料**：右键用户 → **Properties**

| 标签页 | 填写 |
|---|---|
| **General** | Display name、Office、Email |
| **Organization** | Job Title、Department、Company、**Manager** |
| **Member Of** | **Add** → Sales-Executives、打印机群组等 |
| **Account** | 合约员工可设定 **Account expires** |

> 💡 Organization 的资料会用在 Teams / Outlook 的组织图和通讯录。

**PowerShell（L2 常用）**

```powershell
New-ADUser -Name "Emma Wong" -GivenName "Emma" -Surname "Wong" `
  -SamAccountName "emma.wong" -UserPrincipalName "emma.wong@company.com" `
  -Title "Sales Executive" -Department "Sales" -Manager "rachel.tan" `
  -Path "OU=Sales,OU=Users,OU=Company,DC=company,DC=local" `
  -AccountPassword (Read-Host -AsSecureString "Temp Password") `
  -ChangePasswordAtLogon $true -Enabled $true

Add-ADGroupMember -Identity "Sales-Executives" -Members "emma.wong"
```

#### ③ 同步到 Entra ID

**Entra Connect** 通常每 **30 分钟**自动同步一次。赶时间可以手动触发（通常是 L2 权限）：

```powershell
Start-ADSyncSyncCycle -PolicyType Delta
```

#### ④ Microsoft 365：分配授权

**Microsoft 365 Admin Center → Users → Active users → 选择用户**

1. 先设定 **Usage location** ⚠️ **没有设定就不能分配授权**
2. **Licenses and apps** → 勾选授权（例如 Microsoft 365 Business Premium / E3）→ **Save changes**
3. 几分钟内自动开通 Outlook、Teams、OneDrive
4. 加入 **Distribution list** 和 **Teams 团队**（Teams Admin Center，或请团队拥有者加入）

#### ⑤ 其他系统权限

- **共享文件夹**：权限给了群组 → 加入群组就自动有权限
- **CRM 等业务系统**：另外开请求给 **app owner**，附上 HR 请求编号

#### ⑥ 准备笔记本

- **Autopilot + Intune**：硬件资讯登记在 Intune → 指定给用户 → 用户第一次登录时自动安装设定和软件
- **传统方式**：用系统映像安装 Windows → **加入网域（Join domain）** → 安装软件
- 确认 **BitLocker** 已开启、恢复密钥已备份；登记**资产编号**和**序号**

#### ⑦ 检查（第一天前）

IT **不能用新员工的账号登录**（密码要她自己设定），所以先检查设定：

- [ ] AD：OU 正确、资料完整、群组正确
- [ ] M365：授权显示 **Active**、邮箱已建立
- [ ] 群组：Sales-Executives、Distribution list、Teams 团队
- [ ] CRM 请求已提交
- [ ] 笔记本已准备好并指定给用户

#### Cloud-only 环境（没有内部 AD）

**Microsoft 365 Admin Center → Users → Active users → Add a user**：一个画面填好名字、用户名、临时密码（勾选 *Require this user to change their password when they first sign in*）、授权和群组。

### 工单记录范例

```text
Request: New user onboarding for Emma Wong (Sales Executive), starting tomorrow 9 a.m.,
         head office 3F. Manager: Rachel Tan. HR request: HR-2291.
Requirements: Laptop, M365 (email, Teams, OneDrive), Sales shared drive, CRM access.
Actions:
  - Manager requested "same access as Mark" (Sales Exec). Mark still has Finance folder access from a
    previous project. Access set by role (Sales-Executives group) instead of copying Mark's account,
    per least privilege. Manager advised to review Mark's Finance access.
  - Created AD account emma.wong in OU=Sales; temporary password, must change at next logon.
  - Added to Sales-Executives, Sales printers, sales-team distribution list, Sales team in Teams.
  - Assigned M365 Business Premium license (usage location set). Mailbox created.
  - CRM access request submitted to CRM app owner (ref: CRM-0571).
  - Laptop prepared (asset tag LT-3381, S/N 5CD1234XYZ): standard image, updates, BitLocker enabled,
    recovery key backed up. Assigned to user in asset management. Desk dock/monitors checked.
  - Manager asked for password by email; declined per security policy.
    Temporary password to be given to user in person on Day 1 after ID check.
Day 1 plan: Verify ID, first login and password change, MFA setup, test email/Teams/shared drive/CRM/printer,
            IT introduction (help desk contact, phishing reporting, AUP).
Status: Pending (Day 1 setup).
```

---

[⬅️ 返回目录](../README.md)
