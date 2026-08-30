# FDE 技能全景（查过什么、必须会什么）

**FDE = Forward Deployed Engineer（前线 / 前沿部署工程师）**  
最早由 Palantir 做成岗位，现在 OpenAI、Anthropic、Databricks、Salesforce 以及国内 AI 落地团队都在招。一句话：**驻在客户现场，把产品能力和客户真实业务之间的缺口（Palantir 称 The Delta）用能上线的系统补上。**

本页是技能地图。1 个月怎么学，见 [FDE-1个月学习路线.md](./FDE-1个月学习路线.md)。

---

## 1. 先对齐预期（诚实边界）

公开路线几乎都写 **6–12 个月**才能称为「能独立驻场交付」：

| 来源 | 建议周期 |
|------|----------|
| [lingmo.fun FDE 路线图](http://lingmo.fun/) | 18 模块，6–12 个月，每天约 2 小时 |
| [成为 FDE 的系统学习路径（2026）](https://jishuzhan.net/article/2066337265680478210) | 5 阶段，约 6–12 个月 |
| [thecoder8890/forward-deployed-engineer-roadmap](https://github.com/thecoder8890/forward-deployed-engineer-roadmap) | 无基础时约每周 10–12 小时长期投入 |

**1 个月做不到**：达到 Palantir / OpenAI 面试通过线、独立扛企业生产级 K8s + 私有化推理 + 全量 Agent 写操作。  
**1 个月可以做到**：成为「FDE 学徒」——能进场问对问题、画清流程、判断哪该上 AI、做出可演示的最小交付（MVD），并用数字和评估集证明「有没有用」。

你的行业锚点按现有工作定为：**进港到仓 / 仓配自动化**（廊坊、北京进港到仓中心这类现场）。技术通用，案例全部用到仓。

---

## 2. 岗位在招什么（GitHub + JD 交叉）

| 公司 / 来源 | 他们强调的能力 |
|-------------|----------------|
| [Palantir FDSE](https://jobs.lever.co/palantir/dab396d4-2f14-4796-aac0-0d82883dccf0) | 强编码（Python / Java / C++ / TypeScript）、端到端像创业公司 CTO、大规模数据、定制应用、生产监控、客户从一线到高管都能聊 |
| OpenAI FDE（多篇 JD / 面试复盘） | 发现 → 范围 → 系统设计 → 构建 → 生产上线；Python/JS；**eval 驱动反馈**；成功率看生产采用，不看 Demo |
| Anthropic Applied AI | 生产级 LLM：Agent、评估框架、MCP / Skill 类工件、Python + 最好有 TypeScript |
| Databricks AI FDE | RAG、多 Agent、Text2SQL、微调认知、生产级评估、Hugging Face / LangChain / DSPy |
| Salesforce Agentforce | 企业 API / 中间件 / 事件驱动、跨系统排障、Agent 护栏、事件 RCA |
| Anduril 等 Field FDE | 硬件 + 网络 + 软件现场排障、培训用户（仓配自动化现场更接近这一路的「现场生存」） |

面试里权重最高、通过率最低的，是 **分解（decomp）案例**：给你一句含糊业务话（「到仓效率低」），你要能拆成可做的 v1，而不是立刻写代码。见 [ombharatiya FDE 面试指南](https://github.com/ombharatiya/AI-Engineer-Interview-Questions/blob/main/15-role-guides/forward-deployed-engineer.md)。

---

## 3. 四层能力模型（所有来源的公约数）

多数路线（DataCamp、GitHub roadmap、国内 CDEF）都收敛成四层。越往上越稀缺。

```text
④ 软技能 / 现场生存     沟通、抗压、说人话、守边界、建信任
③ 交付方法论              勘探→方案→最小交付→灰度→交接
② 数据 + AI 落地          SQL、RAG、Agent、评估、护栏
① 工程底座                写代码、Git、API、Docker、排障
```

### ① 工程底座（没有这个，后面全是 PPT）

| 技能 | 1 个月要到的程度 | 可后置 |
|------|------------------|--------|
| Python | 读写文件、函数、异常、requests、pandas 入门 | asyncio 精通、《流畅的 Python》全书 |
| Git | add / commit / push / branch / PR 能独立用 | 复杂 rebase、monorepo |
| SQL | SELECT / JOIN / GROUP BY / 窗口函数入门 | Spark、湖仓、查询优化专家 |
| HTTP + API | 会调 REST、懂 JSON、状态码、鉴权概念 | GraphQL / 全套 OAuth 实现 |
| FastAPI | 能写 3–5 个接口 + 简单校验 | 高并发微服务 |
| 前端原型 | Streamlit 或 Gradio 能给领导点 | React 完整产品 |
| Docker | 会写 Dockerfile，Compose 一键起 | Kubernetes / Helm / Terraform |
| Linux | ls / cd / grep / 环境变量 / 看日志 | CUDA / GPU 驱动排障专家 |

### ② 数据 + AI 落地（FDE 区别于普通开发的核心）

| 技能 | 1 个月要到的程度 | 可后置 |
|------|------------------|--------|
| LLM 使用 | 会调国内/国际 API；懂 token、温度、幻觉 | 训练 / 推导 Attention |
| Prompt | 结构化输出、少样本、让模型「找不到就说找不到」 | 提示词玄学堆砌 |
| RAG | 切分 → 向量 → 检索 → 带引用回答；会排查「答错是检索还是生成」 | 企业级混合检索调参大师 |
| Agent | 工具调用 + 失败重试 + **人工确认后再写系统** | 多 Agent 大集群、A2A 协议精通 |
| Evals | 至少 20–50 条黄金问答；失败分类；回归时能发现变差 | LLM-as-Judge 全套平台 |
| 安全 | 知道数据不出域选项；Prompt 注入；不让模型直接改生产 | 等保全案、VPC-SC 专家 |
| 微调 / vLLM | 知道「大多数时候不该微调」 | LoRA、量化、GPU 调度 |

[ombharatiya 指南](https://github.com/ombharatiya/AI-Engineer-Interview-Questions/blob/main/15-role-guides/forward-deployed-engineer.md) 明确：**别准备反传推导、GPU kernel；要准备 RAG 排障、Agent 写操作分阶段、CISO 问数据是否离网。**

### ③ 交付方法论（现场真正每天在用的）

把这些记成一套动作，不要当理论：

| 方法 | 做什么 | 来源 |
|------|--------|------|
| **CDEF** | Context 勘探 → Design 方案 → Engineer 最小系统 → Feedback 评估交接 | [云图 CDEF](https://blog.ytso.com/ai/321581.html) |
| **MVD** | Minimum Viable Delivery：最短时间，在真实（或仿真真实）环境跑通一个可感知价值的最小系统 | 同上 |
| **五要素** | 每个环节写清：输入 / 输出 / 负责人 / 耗时 / 痛点 | [sofagent FDE](https://github.com/KongFangXun/sofagent/blob/main/FDE/README.md) |
| **三问判定** | 这一环：自动执行 / 强化岗位 / 暂不动 | 同上 |
| **CASE** | Clarify → Architect 数据流 → Solve the Delta（产品缺什么胶水）→ Evaluate（怎么证明没瞎说） | [8-week FDE roadmap](https://abhijayvuyyuru.substack.com/p/the-free-8-week-roadmap-to-become) |
| **灰度** | 只读 → 草稿 → 人工门控写入 → 有限自治 | 面试指南 + sofagent |
| **知识转移** | 文档 + 培训 + 陪跑，目标是你走了系统还在 | CDEF Feedback 阶段 |

### ④ 软技能 / 现场生存

- 先跟岗看「昨天实际怎么干」，再问「AI 能做什么」（后者容易得到科幻答案）
- 对高管：**结论先行**（金字塔原理）
- 对一线：用他们的工位语言，不秀名词
- 对安全：给选项和代价，不和制度抬杠
- 敢说「这一步不该上 AI，先把数据/流程量清楚」
- 仓现场：护栏、急停、不打断生产（已有 [场地行动卡](./场地看自动化设备-行动卡.md)）

---

## 4. 到仓场景要把技术「翻译」成什么

FDE 不是学一堆工具名，是能在现场把工具接到真实链路上：

```text
来车/卸货 → 到货登记 → 扫描/识别 → 质检/异常 → 上架/交仓
         ↑ WMS / TMS          ↑ 视觉/条码         ↑ WCS / 线体 / 人工
```

本月只深挖 **1 条链、1 个卡点**（建议：扫码失败 / 到货差异 / 异常件处理），不要同时学分拣、机械臂、AGV 全套。

你会用到的行业词（够用即可）：WMS、WCS、PLC、到货单、差异、剔出线、人机交界、峰值小时产能。

---

## 5. 主要开源学习库（GitHub）

按「1 个月真正用得上」排序：

| 仓库 | 用来干什么 |
|------|------------|
| [pierpaolo28/Awesome-FDE-Roadmap](https://github.com/pierpaolo28/Awesome-FDE-Roadmap) | 技能总表 + 咨询思维 + RAG/Evals 资源索引（star 多，偏 GCP 进阶，第 2 个月再啃云架构） |
| [thecoder8890/forward-deployed-engineer-roadmap](https://github.com/thecoder8890/forward-deployed-engineer-roadmap) | 按 JD 归纳的四层技能 + 学习顺序 |
| [KongFangXun/sofagent FDE](https://github.com/KongFangXun/sofagent/tree/main/FDE) | 中文方法论：进场梳理、五要素、三问、交付物模板 |
| [ombharatiya …/forward-deployed-engineer.md](https://github.com/ombharatiya/AI-Engineer-Interview-Questions/blob/main/15-role-guides/forward-deployed-engineer.md) | 分解案例、RAG 排障、CISO、Agent 写入分阶段 |
| [tiramitree/fde-ai-systems-portfolio](https://github.com/tiramitree/fde-ai-systems-portfolio) | 可运行参考：权限 RAG、人工审批 Agent、评估门禁（第 3–4 周对照） |
| [goday-org/FDE-Handbook](https://github.com/goday-org/FDE-Handbook) | 企业落地手册：数据审计、Landing Zone、Agent、Evals（进阶） |
| [davidahmann/fde-guide](https://github.com/davidahmann/fde-guide) | 工作流章程、本体、发布门禁模板（知道有这套即可） |

必读短文：

- Palantir：[Dev vs Delta](https://blog.palantir.com/dev-versus-delta-demystifying-engineering-roles-at-palantir-ad44c2a6e87)
- Anthropic：[Evaluating AI Agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- DataCamp：[What is a Forward Deployed Engineer](https://www.datacamp.com/blog/what-is-forward-deployed-engineer)

---

## 6. 1 个月「必修 10 项」对照 lingmo 快速通道

[lingmo.fun](http://lingmo.fun/) 给初学者标了 10 个必修模块。本月覆盖其中能落地的 8 个，后置 2 个：

| 必修模块 | 本月 |
|----------|------|
| Python 全栈 | 做：脚本 + FastAPI + Streamlit |
| 前后端基础 | 做：Streamlit 演示页 |
| 云原生 DevOps | 做：Docker Compose；不做 K8s |
| 大模型使用 | 做：API + Prompt |
| RAG | 做：到仓 SOP 问答 |
| Agent | 做：异常处理草稿 + 人工确认 |
| 系统集成 | 做：假 WMS JSON 接口对接 |
| 行业纵深 | 做：到仓一条链 |
| 技术咨询沟通 | 做：每周一页纸 + 口头分解 |
| 实战项目 | 做：1 个到仓 MVD |

后置：模型微调、推理优化（vLLM/量化）、K8s、等保全案。
