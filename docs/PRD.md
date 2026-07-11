# Personal AI OS Kernel — 个人 AI 操作系统内核层

> 项目 PRD 文档 v1.0

---

## 1. 项目概述

### 1.1 项目名称

**Personal AI OS Kernel**

中文：**个人 AI 操作系统内核层**

### 1.2 项目定位

Personal AI OS Kernel 是构建在 **Hermes Agent Runtime** 之上的个人智能操作系统核心层。

它不是替代 Hermes，而是 **扩展** Hermes。

架构关系：

```
Personal AI OS Kernel
│
Hermes Kernel
│
Tools / Skills / Agents / APIs
```

### 1.3 项目愿景

打造一个：能理解个人长期目标、管理个人知识、参与决策、协调 AI 团队、推动项目执行的 **个人 AI 总部**。

最终目标：让一个人通过 AI 获得类似一家公司的能力：

- 战略能力
- 产品能力
- 技术能力
- 研究能力
- 执行能力

---

## 2. 背景与问题分析

### 2.1 当前 Hermes 能力

| 能力 | 状态 |
|------|------|
| Agent 执行 | ✅ |
| 工具调用 | ✅ |
| 代码开发 | ✅ |
| 自动化 | ✅ |
| 子 Agent 调度 | ✅ |
| 信息搜索 | ✅ |
| 外部系统连接 | ✅ |

### 2.2 当前核心问题

Hermes 缺少以下核心能力：

#### 1. 长期状态

无法持续知道：用户当前目标、项目进度、历史决策、当前优先级。

#### 2. 结构化记忆

当前信息分散在 MEMORY.md、USER.md、Wiki、Session、Vector DB 中，缺少关系、权重、生命周期和经验沉淀。

#### 3. 主动能力

当前模式：用户提出问题 → Hermes 响应

目标模式：系统观察 → 发现问题 → 提出建议 → 推动执行

#### 4. AI 团队管理能力

当前：用户指定任务。

目标：系统自动分析任务 → 选择 Agent → 组织协作 → 审核结果

---

## 3. 产品目标

### 3.1 核心目标

建立 **Personal AI OS Kernel**，使 Hermes 从：

**AI 执行助手** 升级为：**AI 个人操作系统**。

### 3.2 第一阶段目标

实现 **Personal Context System**，让 Hermes 每次启动知道：

- 用户是谁
- 用户目标是什么
- 当前有哪些项目
- 最近发生了什么
- 下一步应该做什么

---

## 4. 产品架构

### 4.1 总体架构

```
用户
│
Personal AI OS Kernel
│
────────────────────────────────
Identity    Goal    Project    Memory
用户模型    目标系统  项目系统    记忆系统
│
Decision Engine（决策引擎）
│
Agent Router（Agent 路由）
│
Workflow Engine（工作流引擎）
│
Hermes（执行层）
│
Tools / Skills / Agents
```

---

## 5. 核心模块设计

### Module 1 — Identity Layer（用户认知层）

**目标**：建立 AI 对用户的长期理解。

**功能**：管理用户身份（姓名、背景、技能、经验）、用户偏好（技术偏好、工作方式、决策风格、沟通方式）、用户价值模型（长期价值 > 短期收益，自动化 > 手工执行，系统化 > 临时解决）。

**数据结构**：

```yaml
# user.yaml
identity:
  name: "..."
  skills: [...]
  preferences: {...}
  values: [...]
  constraints: [...]
```

### Module 2 — Goal Engine（目标管理系统）

**目标**：管理人生目标 → 长期目标 → 年度目标 → 项目 → 任务的层级结构。

**功能**：创建目标、分解目标、关联项目、检查进度、评估偏离。

**数据结构**：

```json
{
  "name": "成为AI创业者",
  "level": "long_term",
  "children": ["Personal AI OS"]
}
```

### Module 3 — Project OS（项目操作系统）

**目标**：解决 Hermes 最大问题——跨会话项目状态丢失。

**功能**：管理项目目标、当前阶段、任务、里程碑、风险、下一步行动。

**数据结构**：

```json
{
  "name": "Personal AI OS",
  "phase": "Kernel设计",
  "progress": 20,
  "risks": [],
  "next_actions": []
}
```

### Module 4 — Memory Layer（个人长期记忆系统）

**目标**：从信息存储升级为个人知识资产。

**记忆类型**：

1. **Fact Memory（事实）**：用户正在开发 AI OS
2. **Experience Memory（经验）**：过去项目失败原因
3. **Decision Memory（决策）**：为什么选择 Hermes 作为 Kernel
4. **Strategy Memory（战略）**：用户长期方向

**数据结构**：

```json
{
  "type": "experience",
  "event": "项目失败",
  "lesson": "提前架构设计"
}
```

### Module 5 — Decision Engine（决策支持系统）

**目标**：成为用户战略顾问。

**功能**：分析价值、成本、风险、收益、长期影响。

**输出格式**：

```
方案：...
价值：8/10
风险：中
建议：执行 MVP 验证
```

### Module 6 — Agent Router（AI 团队调度系统）

**目标**：管理 AI 专家团队。

**输入**：用户任务。

**分析**：任务类型（技术、产品、研究、设计、运营、战略）

**输出**：调用对应的 Agent——Developer Agent、Research Agent、Product Agent、Reviewer Agent。

### Module 7 — Workflow Engine（工作流系统）

**目标**：将任务变成流程。

**示例——开发产品的工作流**：

```
需求分析Agent
→ 架构Agent
→ 开发Agent
→ 测试Agent
→ 审核Agent
→ 部署Agent
```

### Module 8 — Heartbeat System（主动运行系统）

**目标**：让 AI 主动发现问题。

**功能**：定期检查项目状态、目标偏离、风险、机会。

**示例——每日运行**：

```
扫描项目
→ 发现：YXZS 停滞 7 天
→ 生成提醒
```

---

## 6. 用户使用流程

### 场景 1：提出想法

用户：*"我要做一个 AI 产品"*

流程：

```
Identity 读取用户背景
→ Goal 分析长期价值
→ Decision Engine 评估
→ Agent Router 组织团队
→ Hermes 执行
→ Memory 记录经验
```

### 场景 2：继续项目

用户：*"继续开发 AI OS"*

流程：

```
读取 Project 状态
→ 恢复上下文
→ 显示：当前阶段 / 完成内容 / 下一步
→ 继续执行
```

---

## 7. MVP 范围

### V1.0 必须实现

- ✅ Identity Layer
- ✅ Goal Layer
- ✅ Project Layer
- ✅ Memory Layer
- ✅ Hermes Context Injection

### V1.0 暂不实现

- ❌ 知识图谱
- ❌ 自动强化学习
- ❌ 多服务器 Agent
- ❌ 完全自主运行
- ❌ 复杂 UI

---

## 8. 技术方案

### 后端

Python + FastAPI

### 数据存储

第一阶段：SQLite + JSON/YAML + Markdown

### Memory

组合方案：Structured DB + Vector Database

### API 设计

Hermes 调用：

```
GET /context
```

返回：

```json
{
  "user": {},
  "goals": {},
  "projects": {},
  "memory": []
}
```

写入：

```
POST /memory
POST /project/update
POST /decision
```

---

## 9. 开发路线

### Phase 1 — Kernel Foundation

**时间**：2-4 周

完成：

- 数据模型
- 文件结构
- Context API
- Hermes 连接

**目标**：Hermes 拥有个人状态。

### Phase 2 — Memory Upgrade

**时间**：1-2 个月

完成：

- 自动总结
- 经验沉淀
- 记忆管理

### Phase 3 — Agent Organization

**时间**：2-4 个月

完成：

- Agent Router
- Workflow
- AI 团队模板

### Phase 4 — Autonomous Operation

**时间**：4-6 个月

完成：

- Heartbeat
- 风险检测
- 自动报告

---

## 10. 成功指标

### 技术指标

- 新会话恢复项目上下文 < 10 秒
- 项目状态完整率 > 90%
- 关键决策可追溯
- Agent 调用准确率提升

### 用户指标

达到：用户不需要重复解释"我是谁"、"我在做什么"、"为什么做"。

AI 能够主动回答："根据你的长期目标，目前最重要的是……"

---

## 11. 最终产品形态

```
你
│
Personal AI OS
│
AI CEO / COO
│
───────────────────
战略  产品  技术  研究
│
Hermes
│
AI 执行团队
```

---

## 项目核心原则

1. Hermes 不修改，只扩展。
2. 状态优先于能力。
3. 记忆优先于 Agent 数量。
4. 主动管理优先于被动回答。
5. 长期系统价值优先于短期功能。

> Personal AI OS Kernel 的第一版本目标：让 Hermes 第一次拥有"持续存在的自我状态"，从一个执行型 Agent 变成一个个人 AI 操作系统的核心。
