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
