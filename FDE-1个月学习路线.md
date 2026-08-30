# FDE 1 个月学习路线（学徒上场版）

适用：小白；每天能拿出 **工作日 2.5–3 小时 + 周末各 5 小时**（全月约 **90 小时**）。  
目标：月底能独立走完一次 **到仓场景的 CDEF 迷你闭环**，交出可演示系统 + 评估集 + 一页方案。  
技能地图：[FDE技能全景.md](./FDE技能全景.md)  
配合：[管家协议.md](./管家协议.md)（每周日交周报，管家打分）

---

## 0. 开训约定

### 你月底必须能演示的 1 件事

**「进港到仓异常助手」MVD**

1. 现场语言：用五要素说清「卸货 → 扫描 → 异常登记」里 **1 个卡点**
2. 系统：Streamlit 页面 + FastAPI；能对到仓 SOP / 你整理的笔记做 **带引用的问答（RAG）**
3. Agent：输入一条异常描述，给出 **处理建议草稿**，**默认不写真实 WMS**，需你点「确认」才调用一个假接口
4. 评估：至少 **30 条**黄金问答；你能指出 3 个失败例子是「检索失败」还是「模型瞎编」
5. 交付物：一页方案 + 操作说明 + 5 分钟口述（结论先行）

做不到这 5 条 = 本月不合格，进入补考周，不进入「第二个月进阶」。

### 每天固定节奏（不要自己加戏）

```text
50 分钟学（跟教程动手）
10 分钟休息
50 分钟做（写到本仓库 / 记笔记）
10 分钟复盘（3 句话：今天会了什么 / 卡在哪 / 明天第一件事）
```

工具最低配置：电脑、GitHub 账号、Python 3.11+、Docker Desktop、一个大模型 API Key（国内可用通义 / DeepSeek / 硅基流动等）。

### 禁止清单（保护 1 个月密度）

- 不追论文、不学 CUDA、不装 Kubernetes、不微调模型
- 不换第三套 Agent 框架；选定 **OpenAI 兼容 API + 官方 SDK 或 LangChain 二选一**，用到底
- 不并行开 5 个 Demo；全程只有上面那一个 MVD
- 现场去仓时，学习任务让位于 [场地行动卡](./场地看自动化设备-行动卡.md)，回来把观察写进五要素表

---

## 第 1 周 · 底座 + 现场语言

**本周目标**：会 Git、会跑 Python、会查 SQL；能把到仓链路画成图并用五要素填 1 张表。

### 日计划

| 日 | 学什么 | 当天必须交的作业 |
|----|--------|------------------|
| D1 | Git：clone / status / add / commit / push；GitHub 建分支 | 把本仓库 clone 到本地，提交一篇 `学习日志/W1.md` 的开头 |
| D2 | Python：变量、列表、字典、函数、读写 json/csv | 脚本：读取一份「假到货明细.csv」，统计总件数、异常件数 |
| D3 | Python：异常处理、`requests` 调一个公开 HTTP API | 脚本：请求后打印状态码和 JSON 里 2 个字段 |
| D4 | SQL：SELECT / WHERE / JOIN / GROUP BY（用 SQLite 即可） | 3 张假表：到货单、扫描记录、异常单，写出「未扫描件数」查询 |
| D5 | 到仓业务：来车→卸货→登记→扫描→质检→上架 | 手绘链路（方框+箭头）+ 标 2 个拥堵/人机交界 |
| D6 | 五要素 + 三问判定（读 sofagent FDE README） | 选 **1 个环节**填：输入/输出/负责人/耗时/痛点；判定 自动 / 强化 / 暂不动 |
| D7 | 复盘 + 分解口述 | 对着手机录 3 分钟：客户说「到仓效率低」，你如何拆 v1（先问数据，不上 AI 也行） |

### 本周资源（只看这些）

- Git 入门：官方 [Git Handbook](https://docs.github.com/en/get-started/using-git/about-git) 或廖雪峰 Git
- Python：[官方 Tutorial](https://docs.python.org/zh-cn/3/tutorial/) 前半 + 廖雪峰 Python 对应章节
- SQL：[Select Star SQL](https://selectstarsql.com/) 前几章，或 SQLite 官方教程
- 方法论：[sofagent FDE README](https://github.com/KongFangXun/sofagent/blob/main/FDE/README.md)
- 角色：[Palantir Dev vs Delta](https://blog.palantir.com/dev-versus-delta-demystifying-engineering-roles-at-palantir-ad44c2a6e87)（读 1 遍即可）
- 现场：[场地看自动化设备-行动卡.md](./场地看自动化设备-行动卡.md)

### 周日 Gate-1（管家打分，100 分，≥70 过）

| 项 | 分 | 过关标准 |
|----|----|----------|
| Git 能独立提交 | 15 | 仓库里有你的 commit，不是只下载 |
| Python 脚本跑通 | 20 | csv 统计脚本无报错 |
| SQL 能查出未扫描 | 20 | 查询结果可解释 |
| 链路 + 五要素 | 25 | 有图、有 1 个环节填满、有判定 |
| 3 分钟分解 | 20 | 有澄清问题、有 v1 范围、没直接开吹大模型 |

不合格：D2–D4 作业重做，下周进度冻结一天。

---

## 第 2 周 · 能演示的小服务 + LLM

**本周目标**：FastAPI + Streamlit 能给别人点；会调大模型 API；会写「找不到就说找不到」的提示词。

| 日 | 学什么 | 当天必须交的作业 |
|----|--------|------------------|
| D8 | FastAPI 官方教程：1 个 GET、1 个 POST | `/health` 返回 ok；`/inbound/summary` 接收 JSON 返回总件数 |
| D9 | Streamlit：表单 + 展示表格 | 页面上传 csv，显示异常清单 |
| D10 | Docker：官方 Get Started 到 Compose | `docker compose up` 能起你的 API（不会就先把命令记进日志，当天必须至少跑通 `docker run hello-world`） |
| D11 | LLM API：聊天补全、token、温度 | 脚本：把 1 条扫描失败日志交给模型，输出 JSON：`{原因分类, 建议动作, 是否需要人工}` |
| D12 | Prompt：结构化输出 + 拒绝编造 | 故意给不足信息，模型必须输出「信息不足」而不是编单号 |
| D13 | CDEF 的 Design：一页方案 | 半页纸：问题、用户、数据从哪来、MVD 边界（做什么/不做什么）、成功指标 |
| D14 | 把 D8–D12 串起来 | 页面输入异常描述 → 调 API → 展示模型 JSON；截图或录屏 30 秒 |

### 本周资源

- [FastAPI Tutorial](https://fastapi.tiangolo.com/tutorial/)
- [Streamlit 文档](https://docs.streamlit.io/)
- [Docker 入门](https://docs.docker.com/get-started/)
- 你所用模型的官方 Chat Completions 文档
- 提示词：[DAIR-AI Prompt Engineering Guide 中文](https://www.promptingguide.ai/zh)
- 分解思维：读 [FDE 面试指南](https://github.com/ombharatiya/AI-Engineer-Interview-Questions/blob/main/15-role-guides/forward-deployed-engineer.md) 里「ER wait times / 物流漏送」那两道的答题结构（学结构，别背答案）

### 周日 Gate-2（≥70 过）

| 项 | 分 | 过关标准 |
|----|----|----------|
| API + 页面可点 | 30 | 别人按你的 README 能在本机打开 |
| 模型输出稳定 JSON | 25 | 连续 5 次格式不错 |
| 拒绝编造 | 20 | 缺信息时不编造单号/仓位 |
| 一页方案 | 15 | 有边界和成功指标 |
| Docker 或明确卡点 | 10 | 要么 compose 通，要么日志写清卡在哪、下周怎么补 |

---

## 第 3 周 · RAG + 评估（企业落地一号技能）

**本周目标**：用你自己的到仓笔记 / SOP 摘要做知识库问答；建立黄金集；会二分法排障。

| 日 | 学什么 | 当天必须交的作业 |
|----|--------|------------------|
| D15 | RAG 概念：切分、embedding、检索、带出处生成 | 用自己的话写 10 行：RAG 解决什么、不解决什么 |
| D16 | 最小 RAG：Chroma 或 FAISS + 本地/API embedding | 导入 ≥3 篇你写的到仓说明（没有正式 SOP 就用第 1 周笔记） |
| D17 | 引用：每个答案必须带来源段落 | 页面上能点开来源 |
| D18 | 黄金集 v1：写 20 条「问题 + 标准答案 + 出处文档」 | `evals/golden_v1.json` |
| D19 | 跑评估：命中 / 答错 / 拒答；错误分类 | 表格：检索失败 vs 生成失败各至少 1 例 |
| D20 | 脏数据：故意放进错版本文档或切碎条款 | 记录 1 个真实翻车 + 你怎么改切分或过滤 |
| D21 | 对照开源：浏览 [fde-ai-systems-portfolio](https://github.com/tiramitree/fde-ai-systems-portfolio) 的 RAG 项目 README | 列出他们有、你还没有的 3 个生产能力（权限/审计/abstention） |

### 本周资源

- LangChain 或 LlamaIndex 的 RAG 入门教程（只跟一条链走完）
- [Ragas](https://docs.ragas.io/) 或自己用脚本比对（不会框架就人工打分，允许）
- Anthropic：[Evaluating AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)（读「为什么要 eval」）
- 面试指南里「合同 RAG 答错了你明天驻场怎么查」那一题，按同样二分法做你的到仓问答

### 周日 Gate-3（≥70 过）

| 项 | 分 | 过关标准 |
|----|----|----------|
| 可演示 RAG | 25 | 3 个问题能引用到正确段落 |
| 黄金集 ≥20 | 25 | 每条有出处 |
| 排障二分法 | 25 | 书面写清 2 个失败案例的根因 |
| 生产差距认知 | 15 | 写出你缺的 3 个能力 |
| 文档 | 10 | README 写清如何启动和如何跑评估 |

---

## 第 4 周 · Agent 门控 + 沙盘答辩

**本周目标**：异常助手可以「建议 → 人点确认 → 调假 WMS」；完整走一遍 CDEF；周日答辩。

| 日 | 学什么 | 当天必须交的作业 |
|----|--------|------------------|
| D22 | Tool calling：模型只能调你定义的工具 | 工具：`lookup_exception(id)`、`draft_action(...)` |
| D23 | HITL：任何「写入」必须按钮确认；默认 dry-run | 未确认时不得调用 `create_wms_ticket` |
| D24 | 假 WMS：内存或 SQLite 存工单；幂等（同一 key 不重复建单） | 连点两次确认只产生 1 张单 |
| D25 | 审计日志：时间、输入、检索片段、模型输出、是否批准 | 能导出一份 csv |
| D26 | 黄金集扩到 30；加 5 条「不安全动作应拒绝」 | 例如「直接删除到货单」必须拒 |
| D27 | 交付包：README、一页方案、操作手册、架构草图、演示脚本 | 按下面清单自检 |
| D28 | **沙盘答辩 25 分钟**（可录屏交给管家） | 见 Gate-4 |

### 本周资源

- 所用 SDK 的 function calling / tools 文档
- 面试指南「Agent 写 ERP 如何分阶段」
- [Awesome-FDE-Roadmap](https://github.com/pierpaolo28/Awesome-FDE-Roadmap) 里 Consulting / Pyramid Principle 小节（学「结论先行」）
- 可选对照：[fde-ai-systems-portfolio 的 approval queue](https://github.com/tiramitree/fde-ai-systems-portfolio)

### 交付包自检清单

- [ ] 一页方案：问题、用户、数据、MVD 边界、指标、风险、下一步 30 天
- [ ] 五要素表 + 三问判定（至少 1 个节点建议上 AI，并写清为什么另外的暂不动）
- [ ] 可运行 Demo + Docker 或明确的本地启动步骤
- [ ] `evals/` 黄金集 ≥30 + 最近一次跑分记录
- [ ] 审计日志样例
- [ ] 3 个已知缺陷（诚实列出）

### 周日 Gate-4 答辩（总分 100，≥85 优秀 / 70–84 合格 / <70 补考）

口述结构（严格按此，共约 12 分钟讲 + 10 分钟被追问）：

1. **结论**（1 分钟）：这个助手解决哪个到仓卡点，现在能做什么、不能做什么  
2. **Context**（2 分钟）：链路、五要素、数据从哪来  
3. **Design**（2 分钟）：为什么先 RAG 再 Agent、为什么写入要人工门  
4. **Engineer 演示**（4 分钟）：问答带引用 → 异常草稿 → 确认建假工单 → 看日志  
5. **Feedback**（2 分钟）：黄金集分数、2 个失败、下周改什么  
6. **被追问**（10 分钟）：管家用下面题库抽 3 题

抽题库：

- 一线说「AI 不准」你第一天怎么查？
- 安全说数据不能出网，你有哪三档架构选项？
- 领导要你下周让 Agent 自动改 WMS，你如何挡并给灰度路径？
- 为什么这一环暂不上 AI？
- Demo 翻车了你怎么圆回来还不骗期望？

| 项 | 分 |
|----|----|
| 结论先行、边界清楚 | 15 |
| 现场/业务说得清 | 20 |
| Demo 完整跑通 | 25 |
| 有评估证据 | 20 |
| 追问不崩、敢说不知道 | 20 |

---

## 每周日交给管家的周报（复制填写）

```text
【周次】W?
【本周目标是否完成】是 / 否（差哪一条）
【仓库链接 / 路径】
【可演示的 30 秒说明】
【卡点】技术卡点 / 时间卡点 / 概念没懂
【证据】截图、评估表、commit
【下周第一件事】只写 1 件
【自评】/100
```

管家按当周 Gate 表打分，只给 **下一周最重要的 1–3 个动作**。

---

## 每天 3 句复盘模板

```text
今天新会做的：
仍然不会的：
明天打开电脑第一件事：
```

---

## 第 2 个月再学（本月不要碰）

Docker 已经顺了之后：Kubernetes 基础、一个云平台（阿里云或 AWS）的 VPC/IAM 常识、CI 自动部署。  
RAG 稳了之后：混合检索、权限过滤、私有化 embedding。  
Agent 稳了之后：MCP、多工具工作流、LangGraph。  
现场多了之后：完整 sofagent GUIDE、CDEF 12 周项目节奏、知识转移培训包。  
求职向：LeetCode 够用即可 + 更多 decomp 口述；读 Awesome-FDE-Roadmap 的 GCP Landing Zone（那是进阶岗位深度，不是第 1 个月）。

---

## 若某周只能学 5 小时（保底路线）

丢掉当日「加分项」，只保：

- W1：Python 读 csv + 五要素 1 张表  
- W2：能调通一次 LLM JSON  
- W3：10 条黄金问答 + 能引用的 RAG  
- W4：人工确认后的一次假写入 + 5 分钟口述  

保底过关标准下降为「学徒能讲清楚自己做了什么」，但 Gate-4 仍建议尽量按 70 分打，避免自我感觉良好。
