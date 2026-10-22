# Practice 7：蓝屏（BSOD）

[⬅️ 返回目录](../README.md)

### 情境

> **Lily（Customer Service）**: "My laptop keeps crashing! The whole screen suddenly turns blue with a sad face :( and some white text, and then it restarts by itself. It's happened three times this morning already! I keep losing what I'm typing to customers. Right now it's working again, but I'm scared it's going to crash any second. What's wrong with it? Is it broken?"

### 关键线索

- 用户问**"是不是坏了？"** → 先回答，让她安心
- **最近的改变**：昨天收到**新的 docking station**（接两个显示器）并安装了附带的软件；昨晚 **Windows 更新**
- 蓝屏照片 📸：
  - **Stop code**: `DRIVER_IRQL_NOT_LESS_OR_EQUAL`
  - **What failed**: `DockVid.sys`
- **没接 dock** 开会一小时 → **没有蓝屏**；回座位接上 dock → **20 分钟后蓝屏**
- Device Manager：DockVid USB Display Adapter 有 ⚠️，驱动版本 **2.1.0（2023）**
- 官网最新版本 **3.4.2**，修复了新 Windows 更新的蓝屏问题
- 同事 **Ben 和 Chloe** 也收到同一款 docking station

### 处理流程（对应七步法）

| 步骤 | 做了什么 |
|---|---|
| 1. Identify | 第一个问题就问**最近有什么改变** → 新 docking station + Windows 更新 |
| 2. Theory | 看 **Stop code** 和 **What failed: DockVid.sys** → 驱动程序问题 |
| 3. Test | 不接 dock 一小时都没事，接上 20 分钟就蓝屏 → 证实是 dock 驱动 |
| 4. Plan | 临时方案（拔 dock、HDMI 直接接）；修复计划（换新驱动） |
| 5. Implement | 远程卸载旧驱动（2.1.0），安装新驱动（3.4.2），重启两次 |
| 6. Verify + Prevent | 测试 30 分钟以上、两个屏幕都正常；主动联系 Ben 和 Chloe、通知 desktop team |
| 7. Document | 写工单；同事另开工单，建议 Problem ticket / KB |

### 推荐英文说法

```text
Hi Lily, this is Eleven from the IT department.
Don't worry, a blue screen doesn't always mean the laptop is broken.
Most of the time, it's a software or driver problem that we can fix.
Could I ask you a few quick questions? First, has anything changed on your laptop recently?
For example, did you install any new software, get a Windows update, or connect a new device?
```

```text
Yes, that really helps, thank you! Next, do you remember what the blue screen said?
Near the bottom, there's usually a line that says "Stop code".
If it happens again, please take a photo of the screen with your phone before it restarts.
And when does the blue screen happen? What are you usually doing at that moment?
```

```text
It looks like the docking station software is causing the blue screen.
When you installed it, it added a driver to your laptop.
A driver is a small program that helps Windows talk to a device.
The error message shows that this driver, DockVid, is the one that failed.
And it didn't crash when the dock wasn't connected. So let's fix the driver.
```

```text
For now, please unplug the docking station, so the blue screen won't happen again.
If you need two screens, you can connect one monitor directly to your laptop's HDMI port.
Then you'll have your laptop screen and one monitor. Also, please save your work often,
or write long replies in Word first.
Here's my plan to fix it. I'll remove the old docking station driver,
and install the latest version from the manufacturer's website.
Your laptop will need to restart twice, so it'll take about 15 minutes.
Is it okay if I connect to your laptop remotely to do this?
```

```text
Thanks, I'm connected now. First, I'm downloading the latest DockVid driver from the manufacturer's website.
This version fixes the blue screen problem with the recent Windows update.
Now I'm opening Device Manager and uninstalling the old DockVid driver.
Next, I'm restarting your laptop. Our remote connection will close during the restart,
so please open Quick Assist again and send me a new code when it's back on.
...Okay, I'm connected again. Now I'm installing the new driver, and I'll restart one more time.
Once it's back on, please plug in the docking station and check that both monitors work.
Since the blue screen happened about 20 minutes after you plugged in this morning,
please use your laptop normally for at least 30 minutes, and let me know if anything happens.
```

```text
Thanks for letting me know, that's a really good point.
If they have the same old driver and the same Windows update, they might have the same problem.
I'll contact Ben and Chloe today to update their drivers before it happens.
I'll also let our desktop team know, so everyone who gets this docking station in the future gets the new driver.
If you see a blue screen again, please take a photo and call us.
Is there anything else I can help you with today? Have a nice day, Lily!
```

### 技术知识

#### 蓝屏（BSOD）的关键资讯

- **Stop code**：错误类型，例如 `DRIVER_IRQL_NOT_LESS_OR_EQUAL`
- **What failed**：出错的文件，例如 `DockVid.sys`
- 蓝屏只显示几秒就重启 → **教用户拍照** 📸
- 不用背每个 Stop code，**拿去搜索**或查公司 KB 就好
- 看到 `DRIVER_...` 开头 + `____.sys` → 几乎可以确定是**驱动程序问题**

#### 驱动程序（Driver）

- `.sys` 结尾的文件通常是**驱动程序**
- 驱动是 Windows 和硬件之间的**翻译员**
- 驱动有很高的权限 → 出错时**整个系统**崩溃（蓝屏）；一般程序出错只会关掉那个程序
- **Windows 更新可能让旧驱动不兼容**
- ⚠️ **只从官方网站或公司软件中心下载驱动**，不要用网上的"驱动下载网站"或"驱动更新工具"
- 安装 / 卸载驱动需要**管理员权限** → 远程连线前先征求同意

#### Device Manager（`devmgmt.msc`）

| 选项 | 作用 | 什么时候用 |
|---|---|---|
| **Update driver** | 更新到新版本 | 驱动太旧，跟新的 Windows 不兼容 |
| **Roll back driver** | 回到上一个版本 | **更新驱动之后**才开始出问题（Properties → Driver） |
| **Disable device** | 暂时停用设备 | 先让电脑稳定下来 |
| **Uninstall device** | 删除设备和驱动 | 要删掉重装；勾选 *Delete the driver software* 才会真的删掉驱动 |

💡 有**黄色惊叹号** ⚠️ 的设备，通常就是驱动有问题。

#### 蓝屏的其他常见原因

| 原因 | 线索 | L1 可以怎么做 |
|---|---|---|
| **驱动程序** | `DRIVER_...`；What failed 是某个 `.sys` | Device Manager 更新、回滚或重装驱动 |
| **Windows 更新出错** | 更新后才开始蓝屏，没有特定驱动 | **Settings → Windows Update → Update history → Uninstall updates** |
| **系统文件损坏** | 各种不同的 Stop code | 管理员权限执行 `sfc /scannow` |
| **内存（RAM）故障** | 例如 `MEMORY_MANAGEMENT`；随机蓝屏，没有规律 | **Windows Memory Diagnostic**（`mdsched.exe`），有问题就上报换硬件 |
| **硬盘故障** | 蓝屏 + 硬盘异响、电脑很慢 | **立即备份资料**，上报硬件团队 |
| **过热** | 电脑很烫、风扇很吵，做重的工作时才蓝屏 | 清理通风口，放在平坦的桌面上 |

#### 一开机就蓝屏，进不了 Windows？

- **Safe Mode（安全模式）**：只载入最基本的驱动，可以在里面卸载有问题的驱动或更新
- **System Restore（系统还原）**：还原到之前正常的时间点，**不会删除用户的文件**
- **Event Viewer / Reliability Monitor**：查看蓝屏前发生了什么

#### 服务技巧

- 先回答"**是不是坏了？**"
- **临时方案（workaround）**让用户可以继续工作：拔掉 dock，用 HDMI **直接**接到笔记本
- 远程操作要**提醒用户重启会断线**，请她重新打开 Quick Assist
- **测试时间要够长**：至少比问题出现的时间更长（20 分钟出问题 → 测试 30 分钟以上）
- **Proactive support**：一个用户的问题，其他人可能也会遇到，主动联系

#### Incident vs Problem（ITIL）

| 类型 | 意思 | 例子 |
|---|---|---|
| **Incident**（事件） | **一个用户**的问题，目标是**尽快恢复** | Lily 的电脑蓝屏 |
| **Problem**（问题） | 造成**多个事件**的**根本原因**，目标是**永久解决** | DockVid 驱动 2.1.0 跟新 Windows 不兼容，影响所有用这款 dock 的人 |

同一个原因影响多个用户时：**每人各开一张工单**（注明 *Related to ticket #____*），并建议开 **Problem ticket** 和写 **KB article**。

### 工单记录范例

```text
Issue: User's laptop had 3 blue screens (BSOD) this morning, then restarted automatically.
       User lost unsaved customer chat replies. User needs two monitors via docking station for work.
Troubleshooting: User received a new DockVid docking station yesterday and installed its driver;
                 Windows update also installed last night.
                 User's photo of BSOD showed Stop code: DRIVER_IRQL_NOT_LESS_OR_EQUAL, What failed: DockVid.sys.
                 No BSOD during a 1-hour meeting without the dock; BSOD occurred ~20 min after reconnecting.
                 Device Manager showed DockVid USB Display Adapter with warning; driver version 2.1.0 (2023).
                 Manufacturer's site lists v3.4.2, which fixes this BSOD on the latest Windows update.
Root Cause: DockVid driver v2.1.0 incompatible with the latest Windows 11 update,
            causing BSOD when the docking station is connected.
Resolution: Workaround: user unplugged the dock and connected one monitor directly to the laptop via HDMI.
            With user's consent, connected via Quick Assist.
            Downloaded DockVid driver v3.4.2 from the manufacturer's official website.
            Uninstalled old driver, restarted, installed new driver, restarted.
Result: User reconnected the dock; both monitors working. No BSOD after 35+ minutes of normal use.
        Device Manager shows driver v3.4.2 with no warnings.
        Advised user to take a photo and call IT if BSOD happens again. Ticket closed.
Follow-up: Teammates Ben and Chloe received the same docking station.
           Separate tickets created to update their drivers (related to #1007).
           Desktop team notified to use driver v3.4.2 for all new DockVid deployments.
           Problem ticket / KB article recommended.
```

> 📌 **Root cause 要客观描述技术原因**，不要写成在怪用户或同事。

---

[⬅️ 返回目录](../README.md)
