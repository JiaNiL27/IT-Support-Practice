# IT Support L1 练习笔记 🛠️

通过角色扮演练习 L1 Help Desk 常见情况，并结合 **CompTIA A+** 知识点整理而成。

## 📂 目录

### 🎫 Practice

| # | 情境 | 重点知识 |
|---|---|---|
| [Practice 1](practice/practice-1.md) | Outlook 收不到邮件 | Working Offline vs Disconnected |
| [Practice 2](practice/practice-2.md) | 账号被锁 / 重设密码 | Social Engineering、身份验证、Active Directory |
| [Practice 3](practice/practice-3.md) | 打印队列卡住 | Print Spooler、最小权限原则、远程支持 |
| [Practice 4](practice/practice-4.md) | 电脑无法上网 | ipconfig、DHCP、APIPA (169.254)、Escalation |

### 📝 Notes

- [通话基本流程（开场与结束）](notes/call-flow.md)
- [工单记录（Ticket Notes）模板](notes/ticket-template.md)
- [常犯英文错误清单](notes/english-mistakes.md)
- [A+ 模拟题重点](notes/aplus-quiz.md)

---

## L1 / L2 / L3 是什么

| 级别 | 角色 | 常见工作 |
|---|---|---|
| **L0** | 自助服务 | 自助密码重设门户、FAQ、知识库 |
| **L1** | 一线支持 / Help Desk | 接电话和工单，处理常见问题（密码、软件、打印机、基础网络），按 SOP/KB 处理，解决不了就上报 |
| **L2** | 二线技术支持 | 服务器、Active Directory、GPO、网络设备、日志分析，拥有更高权限 |
| **L3** | 专家 / 工程师 / 厂商 | 根本原因分析、修 bug、架构层面的问题 |

---

## CompTIA A+ 简介

- IT Support 最常见的**入门认证**，需要通过两个考试
- 目前版本：**220-1201（Core 1）** 和 **220-1202（Core 2）**，也叫 V15，2025 年 3 月推出
- **Core 1**：硬件、打印机、移动设备、网络基础、虚拟化与云端
- **Core 2**：操作系统、安全、软件故障排查、操作流程（Operational Procedures）
- 免费学习资源：Professor Messer（YouTube）

---

## CompTIA 故障排查七步法

> 面试非常常问，实际工作也一直在用。

| 步骤 | 英文 | 意思 |
|---|---|---|
| 1 | **Identify the problem** | 询问用户、了解发生了什么变化 |
| 2 | **Establish a theory of probable cause** | 推测原因，先从最简单的开始（*question the obvious*） |
| 3 | **Test the theory** | 测试推测；如果不对，回到第 2 步 |
| 4 | **Establish a plan of action** | 制定解决方案 |
| 5 | **Implement the solution or escalate** | 执行方案，解决不了就上报 |
| 6 | **Verify full system functionality** | 确认问题完全解决，并做好**预防措施** |
| 7 | **Document findings** | 记录在工单里 |

💡 考试题目常出现 **FIRST / NEXT / MOST likely**，要按照步骤顺序来选答案。

---

---

> 📌 持续更新中：之后会加入更多 L1 情境、L2 挑战题和面试问题。
