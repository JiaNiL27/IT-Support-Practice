# Practice 4：电脑无法上网（169.254 / APIPA）

[⬅️ 返回目录](../README.md)

### 情境

> **Daniel（Accounts）**: "My internet isn't working at all. I can't open any websites, and I can't open the shared drive either, the one where we keep all the invoices. Everyone around me seems fine. I'm using the desktop computer at my desk, not a laptop."

### 关键线索

- **桌上型电脑（desktop）** → 通常用**网线（Ethernet）**，不是 Wi-Fi
- **旁边同事都正常** → DHCP 服务器和整体网络应该没问题
- 昨天下午正常，今天早上开始出问题
- **清洁工昨晚搬过桌子** 🧹（问"最近有什么改变"才问出来的）
- 墙上有**两个网口**，网线插在**右边**那个
- 网口灯号（橙色、绿色）**亮着** → 物理连接正常
- `ipconfig` 显示 **169.254.83.17**，**Default Gateway 是空的** → DHCP 失败（APIPA）

### 处理流程（对应七步法）

| 步骤 | 做了什么 |
|---|---|
| 1. Identify | 询问问题什么时候开始、**最近有什么改变** → 清洁工搬过桌子 |
| 2. Theory | 先检查最简单的：网线两端有没有插好 |
| 3. Test | 网线和灯号正常 → 用 `ipconfig` 检查，发现 **169.254** |
| 4. Plan | 推测搬桌子时网线插错网口，决定换到另一个网口 |
| 5. Implement | 请用户把网线从右边网口换到左边 |
| 6. Verify + Prevent | 测试**网站和共享文件夹**都正常；上报右边网口给网络团队，并给同事临时方案 |
| 7. Document | 写工单，包括 Escalation |

### 推荐英文说法

```text
Hi Daniel, this is Eleven from the IT department. I'll help you right away.
When did this problem start? And has anything changed at your desk recently?
```

```text
Okay, so your computer uses a network cable. Has anything changed at your desk recently?
For example, was anything moved or unplugged?
Also, could you check if the blue cable is plugged in firmly at both ends,
at the back of your computer and at the wall?
```

```text
Great, it sounds like the cable is fine. Next, I'd like to check your network settings.
Please click the search box at the bottom of your screen, type cmd, and press Enter.
A black window will open. Let me know when you see it.
```

```text
Please type ipconfig, that's i-p-c-o-n-f-i-g, all one word, and press Enter.
You'll see some network information. Look for the line that says IPv4 Address,
and read me the numbers next to it.
```

```text
Your computer isn't getting an IP address from the network.
I think when the desks were moved, the cable was plugged into the wrong socket.
Please unplug the cable from the right socket on the wall, and plug it firmly into the left one.
Then wait about 30 seconds, type ipconfig again, and press Enter.
Could you read me the IPv4 Address again?
```

```text
Great! That means your computer now has a valid IP address from the network.
Let's make sure everything works. Could you open a website, like Google?
Then please open the shared drive with the invoices. Can you access both?
```

```text
Thanks for letting me know, that's a good point.
The right socket may not be connected to the network, or it might be faulty.
I'll report it to our network team so they can check it.
In the meantime, please tell your colleague to use the left socket.
```

### 技术知识

#### ipconfig

在 Command Prompt 输入 `ipconfig`，可以查看电脑的网络设置：

| 项目 | 意思 |
|---|---|
| **IPv4 Address** | 电脑在网络里的地址 |
| **Subnet Mask** | 用来判断哪些地址属于同一个网络 |
| **Default Gateway** | 通往外面网络（例如互联网）的"大门"，通常是路由器 |

常用指令：

```cmd
ipconfig            :: 查看基本网络设置
ipconfig /all       :: 查看详细资料（包括 MAC 地址、DHCP 服务器、DNS 服务器）
ipconfig /release   :: 放掉目前的 IP
ipconfig /renew     :: 重新向 DHCP 服务器申请 IP
```

> `/release` 和 `/renew` 可能需要**管理员权限**。

#### DHCP 与 APIPA

正常情况下：

1. 电脑连上网络后，向网络询问 IP 地址
2. **DHCP 服务器**分配 IP 地址、Subnet Mask、Default Gateway、DNS 给电脑
3. 电脑就可以上网、访问共享文件夹

如果**没有 DHCP 服务器回应**，电脑会自己给自己一个 **169.254.x.x** 的地址，这叫 **APIPA（Automatic Private IP Addressing）**。用这个地址**不能上网**，也**没有 Default Gateway**。

📝 **A+ 口诀：看到 169.254 → DHCP 失败。**

#### 三种常见情况

| `ipconfig` 显示 | 意思 | 常见原因 |
|---|---|---|
| **Media disconnected** | 网线**没有连接**（物理层） | 网线没插、断掉、网口坏了 |
| **169.254.x.x** | 有连接，但**拿不到 IP** | DHCP 服务器故障、网口没启用、网线有问题 |
| **正常 IP** + 有 Gateway | 网络设置正常 | 问题可能在别处，例如 DNS |

#### 拿不到 IP 的常见原因

- **DHCP 服务器故障**（多人同时出问题时，要考虑这个）
- **网线坏了**（灯亮着，但信号有问题）
- **墙上的网口没有接通**：办公室墙上常有多个网口，但不是每个都有接到**网络交换机（switch）**

#### L1 可以做什么

- 检查网线两端、灯号
- 换网口或换一条确定是好的网线
- `ipconfig /release` + `ipconfig /renew`
- 确认是网口或交换机问题 → **上报网络团队（L2）**

#### 排查思路

**先检查硬件（网线、灯号），再检查软件（IP 设置）。** 并且一定要问用户：**最近有什么改变？**

### 工单记录范例

```text
Issue: User unable to access websites and the shared drive (invoices) on desktop PC
       (wired connection) since this morning. Colleagues nearby unaffected.
Troubleshooting: User reported desks were moved by cleaners last night.
                 Cable firmly plugged in at both ends; link lights on.
                 ipconfig showed IPv4 169.254.83.17 (APIPA) with no Default Gateway,
                 indicating the PC could not obtain an IP from DHCP.
                 Wall plate has two sockets; cable was in the right socket.
Root Cause: After desks were moved, the cable was plugged into the right wall socket,
            which is not providing a network connection (possibly not patched to the switch, or faulty).
Resolution: Moved cable to the left wall socket. ipconfig showed valid IP 10.20.5.47, Gateway 10.20.5.1.
Result: User confirmed websites and shared drive accessible. Ticket closed.
Escalation: Raised a ticket to Network Team to check the right wall socket at Daniel's desk
            (Accounts dept, wall plate ID: [to be confirmed]). Socket gives no DHCP address (APIPA)
            although link lights are on. Workaround: user and colleague advised to use the left socket until fixed.
```

> 🔧 **上报时要写清楚**：哪个网口（部门、桌号、墙上网口面板编号）、发生了什么事、已经给了什么临时方案。只写 "the right socket"，网络团队到现场也找不到是哪一个。

---

[⬅️ 返回目录](../README.md)
