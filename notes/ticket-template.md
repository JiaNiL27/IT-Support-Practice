# 工单记录（Ticket Notes）模板

[⬅️ 返回目录](../README.md)

```text
Issue:           用户遇到什么问题？（包括错误讯息、设备名称）
Troubleshooting: 按顺序写出检查了什么、发现了什么
Root Cause:      为什么会发生？（不要重复 Issue）
Resolution:      做了什么来解决？（包括使用的工具、用户同意、验证身份）
Result:          用户是否确认解决？给了什么预防建议？是否关单？
```

**写工单的规则：**

- 工单记录的是**已经发生的事**，动词大多用**过去式**（*clicked*, *restarted*, *confirmed*）
- 写上**用户已确认**，这是关单的依据
- 写上**排查过程**，同事下次遇到类似问题就知道哪些已经试过
- 涉及安全的操作（验证身份、远程连线同意）**一定要记录**

**工单状态（Ticket Status）：**

| 状态 | 什么时候用 |
|---|---|
| **Open / In Progress** | 正在处理中 |
| **Pending / On Hold** | 等待用户回复、等待跟进、等待零件 |
| **Escalated** | 已上报给 L2 或其他团队 |
| **Resolved / Closed** | 问题已解决，用户已确认 |

> 问题还没完全解决时，不要直接关单：设为 **Pending**，或关闭后另开 **follow-up ticket**。

[⬅️ 返回目录](../README.md)
