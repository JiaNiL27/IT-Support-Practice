# Practice 5：笔记本电脑很慢

[⬅️ 返回目录](../README.md)

### 情境

> **Mei Ling（Marketing）**: "My laptop is soooo slow! Everything takes forever. I click something and I have to wait, like, ten seconds before anything happens. It's been getting worse for a few days. I have a big presentation for a client this afternoon and I'm worried my laptop is going to freeze in the middle of it."

### 关键线索

- "很慢"是**很模糊**的描述 → 第 1 步要问清楚：**全部慢还是部分慢？什么时候开始？**
- **所有东西都慢**（连开始菜单、File Explorer 都慢）→ 不是单一程序的问题
- 开着 Outlook、Teams、PowerPoint、Excel，还有 Chrome **35 个分页** 🗂️
- **从不关机，只合上盖子** 💻 → 电脑很久没有重启
- 重启后**好多了，但还是有点慢** → 还有其他原因
- C 盘显示红色：**2.1 GB free of 237 GB**（不到 1%）💾
- 用户**下午要演示** → 先做最快、最安全的处理

### 处理流程（对应七步法）

| 步骤 | 做了什么 |
|---|---|
| 1. Identify | 问什么时候开始、全部慢还是部分慢、开了多少程序 |
| 2. Theory | 找出三个原因：**没有重启**、**35 个分页**、**硬盘快满** |
| 3. Test | 先保存 Chrome 分页，再重启 → 好多了，但还是有点慢 |
| 4. Plan | 用户赶时间，先做最快、最安全的清理（暂存文件） |
| 5. Implement | 指导用户清理暂存文件，**提醒不要勾选 Downloads** |
| 6. Verify + Prevent | 确认速度正常；建议每周重启、关闭不用的分页、开启 Storage Sense；约好 OneDrive 后续处理 |
| 7. Document | 写工单，状态设为 **Pending（follow-up）** |

### 推荐英文说法

```text
Hi Mei Ling, this is Eleven from the IT department.
Don't worry, I'll help you get it ready before your presentation.
Let me ask you a few quick questions. When did the problem start?
Is the whole laptop slow, or only certain applications?
And how many applications do you have open right now?
```

```text
Thanks for letting me know, that's really helpful. I think I see two possible causes.
First, closing the lid only puts your laptop to sleep, so it hasn't actually restarted in a long time.
Second, 35 Chrome tabs use a lot of memory. Together, they can slow everything down.
```

```text
Don't worry, you won't lose your tabs. Let's save them first.
1. In Chrome, click the three dots at the top right, then click Settings.
2. On the left side, click On startup.
3. Choose Continue where you left off.
Now Chrome will reopen all your tabs after a restart.
Next, please save your work in PowerPoint and Excel, and close all your applications.
Then click the Start button, click the Power icon, and choose Restart.
Please don't close the lid or choose Shut down this time.
```

```text
Yes, that's a problem. Your laptop's storage is almost full.
Windows needs some free space to run smoothly, so when the disk is this full,
everything slows down. Let's free up some space.
```

```text
Don't worry, we won't delete any of your client files or presentations.
We'll only remove temporary files that Windows doesn't need. Please follow these steps:
1. Click the Start button at the bottom of your screen, then click Settings.
2. When the Settings window opens, click System on the left side.
3. Click Storage. You'll see what's using your disk space.
4. Click Temporary files. You'll see a list of files that Windows can safely remove.
5. Important: please make sure Downloads is unchecked, so you don't delete any files you downloaded.
6. Also, is there anything in your Recycle Bin that you might still need?
7. Click Remove files, and wait a moment. Let me know how much free space you have after that.
```

```text
Great! To keep your laptop running smoothly, here are a few tips:
1. Please restart your laptop at least once a week, instead of just closing the lid.
2. Try to close tabs you're not using. You can bookmark them if you need them later.
3. I'll also turn on a feature called Storage Sense, which cleans temporary files automatically.
Your disk is still quite full, so after your presentation, I'd like to help you move some files to OneDrive.
With a feature called Files On-Demand, your files are saved in the cloud,
and they only download when you open them. They won't be deleted, and they'll also be backed up.
Would tomorrow morning work for you?
Is there anything else I can help you with today? Good luck with your presentation!
```

### 技术知识

#### Sleep vs Shut down vs Restart

| 操作 | 会发生什么 |
|---|---|
| **合上盖子 / Sleep** | 只是睡眠，程序和内存都保留，**系统没有重置** |
| **Shut down** | 关机。但如果开启了 **Fast Startup（快速启动）**，系统核心会被保存下来，**不会完全重置** |
| **Restart** ✅ | **完全重置**系统，排查问题时要请用户选这个 |

#### 为什么硬盘满了会变慢？

- **Virtual memory（page file）**：RAM 不够时，Windows 会借用硬盘空间暂放资料。分页开太多 + 硬盘满 → 电脑卡住
- **暂存文件（temp files）**：程序运行需要空间
- **Windows 更新**：需要空间下载和安装

📝 一般建议：**C 盘至少保留 10–15% 的空间**。

#### 安全清理空间的方法（从最安全的开始）

| 方法 | 路径 / 说明 |
|---|---|
| **Storage 设置** ⭐ | **Settings → System → Storage → Temporary files**，可以看到什么占了空间 |
| **Disk Cleanup** | `Win + R` → `cleanmgr`；**Clean up system files** 可清除旧更新（需管理员权限） |
| **Storage Sense** | 在 Storage 设置里开启，**自动**清理暂存文件和回收站（预防措施） |
| **OneDrive Files On-Demand** | 文件存在云端，右键 → **Free up space**，文件不会被删掉，同时有备份 |
| **找出大文件** | File Explorer 按大小排序，**由用户决定**要不要删 |
| **卸载不用的程序** | **Settings → Apps → Installed apps**（通常需管理员权限） |

> ⚠️ **Temporary files 列表里有 Downloads 选项**，勾选会删掉整个下载文件夹！一定要提醒用户取消勾选。

#### 清理原则

| ✅ 可以做 | ❌ 不要做 |
|---|---|
| 清除暂存文件、回收站 | 删除 `C:\Windows` 或 `System32` 里的东西 |
| 把文件移到 OneDrive / 共享文件夹 | 自己帮用户删除他的文件 |
| 让用户自己决定删哪些文件 | 勾选 Downloads 却没告诉用户 |
| 用户赶时间时，先做最快、最安全的方法 | 在用户赶时间时做大规模清理 |

#### 保存 Chrome 分页

- **Settings → On startup → Continue where you left off**：重启后自动恢复分页
- **Ctrl + Shift + D**：把所有分页存成书签（双重保险）

#### 服务技巧

- **原因 + 下一步**：每次说完原因，都要告诉用户接下来做什么
- **先回应用户的担心**（怕失去分页、怕删掉文件），再给步骤
- 问题没完全解决、但用户赶时间时 → **约后续时间（follow-up）**

### Task Manager 排查指南（English）

#### How to open Task Manager

- Press **Ctrl + Shift + Esc** (fastest)
- Or right-click the taskbar → **Task Manager**
- Or press **Ctrl + Alt + Delete** → **Task Manager**
- If you only see a small window, click **More details**

#### Where to look

| Tab | What it shows | When to use it |
|---|---|---|
| **Processes** | Every running app and background process, with CPU, Memory, Disk and Network usage | Find **which program** is using the most resources. Click a column header to sort |
| **Performance** | Live graphs for CPU, Memory, Disk, Network, GPU | See the **overall** load. CPU page shows **Up time** (how long since the last restart) |
| **Startup apps** | Programs that start automatically with Windows, with **Startup impact** | Slow boot. Right-click → **Disable** (does not uninstall the app) |
| **Details** | Process names (`.exe`), PID, user | Identify an unknown process by its exact file name |
| **Services** | Windows services and their status | Check if a service is running or stopped (e.g. Print Spooler) |

> 💡 A column turns **dark orange / red** when usage is high, so you can spot the problem quickly.

---

#### 🧠 CPU (Processor)

**What it means:** How busy the computer's "brain" is.

| Symptom | Common cause | How to fix |
|---|---|---|
| CPU stays at **90–100%**, one app at the top | The app is frozen, stuck in a loop, or doing heavy work (e.g. video export, big Excel file) | Ask the user to save work, then **End task** on that app and reopen it. If it keeps happening, **update or reinstall** the app |
| **Antimalware Service Executable** is high | Windows Defender is running a scan | **Normal.** Wait for the scan to finish. Scans can be scheduled outside working hours |
| **Windows Update** / **TiWorker.exe** / **Windows Modules Installer** is high | Updates are installing in the background | **Normal.** Let it finish, then restart |
| High CPU from a **process you don't recognize**, odd name, or unusual location | ⚠️ Possible **malware** or crypto-miner | **Don't just end it.** Disconnect from network if policy says so, run a full scan, and **escalate to the security team** |
| CPU is high **all the time** even with few apps open, and the PC is old | Hardware too slow for current workload | Document it and escalate for a **hardware upgrade / replacement** |
| Laptop is **hot**, fans loud, CPU slows down | **Thermal throttling** (overheating) from dust or blocked vents | Use on a hard, flat surface; clean vents; escalate to hardware team if it continues |

**What to tell the user:**

```text
Please click CPU at the top of the list. Which program is at the top, and what percentage does it show?
It looks like that program is stuck. Please save your work in it first, and I'll help you close and reopen it.
```

---

#### 💾 Memory (RAM)

**What it means:** Short-term working space for open apps. When it's full, Windows moves data to the disk (**virtual memory / page file**), which is much slower.

| Symptom | Common cause | How to fix |
|---|---|---|
| Memory at **85–100%** | Too many apps or browser tabs open | Close unused apps; close or bookmark tabs; use **Chrome Task Manager (Shift + Esc in Chrome)** to find the heaviest tab |
| Memory keeps **growing over days** | PC not restarted for a long time; an app has a **memory leak** | **Restart**. Check **Up time** in Performance → CPU. If one app keeps growing, update it |
| Memory always high, even after restart with few apps open | Not enough RAM for the user's work (e.g. 8 GB with heavy apps) | Document usage and escalate for a **RAM upgrade** |
| Memory high **and** Disk at 100% | RAM is full, so Windows is using the **page file** heavily | Free memory first (close apps, restart), and make sure the disk has enough free space |

**What to tell the user:**

```text
Your computer's memory is almost full. That's like a desk covered with too many papers, so everything slows down.
Let's close the programs you're not using. If you need your tabs later, you can bookmark them first.
```

---

#### 💿 Disk

**What it means:** How busy the storage drive is (reading and writing data). Note: this is **activity**, not free space. Check free space in **File Explorer** or **Settings → System → Storage**.

| Symptom | Common cause | How to fix |
|---|---|---|
| Disk at **100%** for a long time | Windows Update, antivirus scan, OneDrive syncing, or indexing | Check which process is at the top. If it's a normal system task, **wait** for it to finish |
| Disk at 100% **and** the drive is almost full | No space for page file and temp files | **Free up space**: Settings → System → Storage → Temporary files (uncheck Downloads!), `cleanmgr`, move files to OneDrive |
| Disk often at 100% on an **older PC** | The PC uses an **HDD** (hard disk drive), which is much slower than an SSD | Check the drive type in **Performance → Disk** (it shows **HDD** or **SSD**). Escalate for an **SSD upgrade** |
| Disk at 100% with **clicking noises**, freezing, or errors | ⚠️ The drive may be **failing** | **Back up the user's data immediately** and escalate to the hardware team |
| Many apps load at startup, disk is busy after login | Too many **startup apps** | Go to **Startup apps** and disable the ones with **High** impact that the user doesn't need |

**What to tell the user:**

```text
Your computer is busy reading and writing a lot of data right now, which is why it feels slow.
It looks like Windows is installing updates in the background. Let's give it a few minutes to finish.
```

---

#### 🌐 Network

**What it means:** How much data the computer is sending and receiving. High network usage usually makes **internet and online apps** slow, not the whole PC.

| Symptom | Common cause | How to fix |
|---|---|---|
| Network usage high from **OneDrive / Teams / Windows Update** | Large file sync, video calls, or update downloads | **Normal.** Pause OneDrive syncing temporarily if the user needs bandwidth (OneDrive icon → **Pause syncing**) |
| Websites slow, but Task Manager shows **low** network usage | The problem is outside the PC: Wi-Fi signal, network, ISP, or the website itself | Check if colleagues have the same issue; try a wired connection; run `ping` or `ipconfig`; escalate to the network team if many users are affected |
| High network usage from a **process you don't recognize** | ⚠️ Possible **malware** sending data out | **Escalate to the security team** |
| Streaming or large downloads in the background | User activity (e.g. video streaming, big downloads) | Ask the user to pause it if it's not work-related |
| No network activity at all and apps can't connect | No connection or no IP address | Check cable / Wi-Fi, then `ipconfig` (169.254 = DHCP problem). See [Practice 4](practice-4.md) |

**What to tell the user:**

```text
OneDrive is uploading a lot of files right now, which is using most of your internet speed.
I'll show you how to pause syncing for a while, so your video call runs smoothly.
```

---

#### ⚠️ Safety rules when using End task

- **Ask the user to save their work first**. Unsaved data in that app will be lost
- **Don't end system processes** you don't understand, such as `System`, `svchost.exe`, `csrss.exe`, `wininit.exe`. This can crash Windows
- Ending **Windows Explorer** makes the taskbar disappear for a moment. Use **Restart** on it instead of End task
- Some processes need **admin rights** to end

#### Other tools when Task Manager isn't enough

| Tool | How to open | Use it for |
|---|---|---|
| **Resource Monitor** | `resmon` | More detail than Task Manager, e.g. which **files** a process is reading or writing |
| **Event Viewer** | `eventvwr.msc` | System and app **error logs** (crashes, hardware errors) |
| **Reliability Monitor** | Search "Reliability" | A **timeline** of errors; great for finding **when** problems started |
| **Performance Monitor** | `perfmon` | Long-term performance logging (usually **L2**) |
| **Windows Update** | Settings → Windows Update | Check for updates running in the background |
| **Windows Security** | Settings → Privacy & security → Windows Security | Run a **virus and malware scan** |

#### L1 troubleshooting flow for a slow computer

1. **Ask questions**: When did it start? Is everything slow or one app? Anything changed recently?
2. **Restart** if the PC hasn't been restarted for a long time (check **Up time**)
3. **Open Task Manager**: is it CPU, Memory, Disk, or Network?
4. **Fix based on the result**: close apps, free up space, disable startup apps, wait for updates
5. **Still slow?** Check other tools, or **escalate to L2** (hardware upgrade, possible malware, failing drive)

### 工单记录范例

```text
Issue: User's laptop running very slowly for the past few days and getting worse.
       Start menu and File Explorer slow to open; ~10 sec delay on clicks.
       User has a client presentation this afternoon.
Troubleshooting: User never restarts laptop (only closes the lid). 35 Chrome tabs open,
                 plus Outlook, Teams, PowerPoint and Excel. After restart, performance improved but still slow.
                 File Explorer showed C: drive 2.1 GB free of 237 GB (<1%).
Root Cause: Laptop had not been restarted for a long time, and many Chrome tabs were using a lot of memory.
            C: drive almost full, leaving no space for virtual memory and temp files.
Resolution: Set Chrome to "Continue where you left off" to keep user's tabs. User saved work and restarted laptop.
            Guided user to Settings > System > Storage > Temporary files; Downloads unchecked.
            Removed temp files and Recycle Bin, freeing ~18 GB (now 20.4 GB free).
Result: User confirmed laptop is fast now. Advised user to restart weekly and close unused tabs
        (bookmark if needed). Disk space still below 10%; follow-up scheduled for tomorrow 10 a.m.
        to move files to OneDrive (Files On-Demand) and enable Storage Sense.
        Ticket status: Pending (follow-up).
```

> 📌 **工单要不要关闭？** 问题没完全解决时，可以把状态设为 **Pending / On Hold** 等待跟进，或者关闭后另开一张 **follow-up ticket**，依公司规定。重点是**一定要有记录**。

---

[⬅️ 返回目录](../README.md)
