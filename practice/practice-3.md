# Practice 3：打印队列卡住

[⬅️ 返回目录](../README.md)

### 情境

> **Priya（HR）**: "I'm trying to print some contracts for new employees, but nothing is coming out of the printer! I clicked print like five times already. My colleague printed something this morning and it was fine."

### 关键线索

- **同事打印正常** → 打印机硬件可能没问题，问题可能在她的电脑
- 打印机选择正确（HR-Printer-2F）
- 时钟旁边的打印机图标显示 **"5 documents waiting"**
- 第一份文件显示 **"Error - Printing"**
- 按 **Cancel All Documents** 后，文件一直停在 **"Deleting"**

### 处理流程（对应七步法）

| 步骤 | 做了什么 |
|---|---|
| 1. Identify | 用户说明打印不出来，同事正常 |
| 2. Theory | 先检查最简单的：是否选错打印机 |
| 3. Test | 发现队列卡住，请用户取消文件 → 删不掉 |
| 4. Plan | 给用户两个方案：远程连线 / 重启电脑 |
| 5. Implement | 用户同意后，用 Quick Assist 远程重启 Print Spooler |
| 6. Verify + Prevent | 确认队列清空、打印成功，教用户以后怎么做 |
| 7. Document | 写工单 |

### 推荐英文说法

```text
Hi Priya, this is Eleven from the IT department. I'll help you right away.
First, could you check if you selected the correct printer when you clicked Print?
```

```text
It looks like your print jobs are stuck in the print queue. Let's clear them.
Please double-click that printer icon near the clock.
A window will open with a list of your documents.
Click Printer at the top left, then click Cancel All Documents.
Let me know when you've done that.
```

```text
The service that manages printing on your computer is stuck, so I need to restart it.
I have two options for you. First, I can connect to your computer remotely and fix it in a few minutes,
and you won't need to close anything. Or second, you can restart your computer,
but please save all your work first. Which one do you prefer?
```

```text
Okay, I'm connected to your computer now. I'm opening Services…
and now I'm restarting the Print Spooler. Done!
Let me check the print queue… it's empty now.
Please print the contract again, just once this time.
```

```text
Sometimes a document gets an error while printing, and it blocks everything behind it.
Clicking Print many times only adds more documents to the queue.
So next time, please click Print just once, and wait a minute.
If nothing comes out, double-click the printer icon near the clock at the bottom right,
then click Cancel All Documents and try again.
If they still won't delete, just restart your computer or give us a call.
```

### 技术知识

#### Print Spooler（打印缓冲服务）

Windows 背景服务，负责**暂存和排队**打印工作（像银行的排队系统）。第一份文件出错时，Spooler 可能会卡住，后面的文件全部堵住，连删除指令也处理不了。

**方法一：Services 窗口**

1. `Win + R` → 输入 `services.msc`
2. 找到 **Print Spooler**
3. 右键 → **Restart**

**方法二：重启后文件仍删不掉**

1. 右键 Print Spooler → **Stop**
2. 删除 `C:\Windows\System32\spool\PRINTERS` 里的所有文件
3. 右键 Print Spooler → **Start**

**方法三：命令（需管理员权限）**

```cmd
net stop spooler
net start spooler
```

#### Principle of Least Privilege（最小权限原则）

一般用户（standard user）**无法重启服务**：按钮是灰色、出现 "Access is denied"，或 UAC 要求管理员密码。因为服务影响整台电脑，限制权限可以防止误操作和恶意软件利用。

#### 用户没权限时的两个方法

| 方法 | 优点 | 缺点 |
|---|---|---|
| **请用户重启电脑** | 不需要权限，也不用远程连线 | 用户要存档、关掉所有程序 |
| **IT 远程重启 Print Spooler** | 快速，用户程序不用关 | 需要远程连线和管理员权限 |

常见远程工具：Quick Assist、Remote Desktop、TeamViewer。**连线前要征求用户同意，操作时要说明在做什么。**

#### 术语区分

| 术语 | 意思 |
|---|---|
| **Paper jam** | 打印机里**卡纸**（硬件问题） |
| **Print queue stuck** | 电脑里的打印队列**卡住**（软件问题） |

### 工单记录范例

```text
Issue: User unable to print contracts to HR-Printer-2F. Print jobs not coming out.
Troubleshooting: Confirmed correct printer selected. Colleagues printing normally, so printer hardware OK.
                 Print queue showed 5 documents waiting; first job showed "Error - Printing".
                 User clicked "Cancel All Documents", but jobs stuck in "Deleting" status.
Root Cause: A print job error caused the Print Spooler service to hang, blocking all jobs in the queue.
Resolution: With user's consent, connected remotely via Quick Assist.
            Restarted Print Spooler service in services.msc. Confirmed print queue cleared.
Result: User confirmed contract printed successfully. Advised user to click Print once only,
        and how to clear the print queue or restart the PC if the issue happens again. Ticket closed.
```

---

[⬅️ 返回目录](../README.md)
