# 从氛围编程到 Agentic Engineering：工程化 AI 的实战指南

*Module 2.7 — 2C：Advanced Agentic Engineering 进阶篇*

> **前置条件：** 本文是 [Module 2.6 Harness Engineering](./07-claude-code-advanced-guide.md) 的续篇。请先完成 Module 2.6，再读这份指南。
>
> ⚠️ **Decay disclaimer:** Claude Code 持续迭代，具体命令和功能可能已更新。本文的概念框架长期有效；操作细节以 [claude.ai/code](https://claude.ai/code) 当前文档为准。

---

## 这份指南是为谁写的

你已经会用 Claude Code 了。你有全局 CLAUDE.md，有项目规范，也用 Harness Engineering 构建过有验证的产品。

但你可能还是有这种感觉：**Claude 每隔五分钟来问你一次。** 你在管理它，不是在指挥它。每一个 back-and-forth 都在消耗你的注意力，而不是推进项目。

这份指南要解决的，正是这件事。

核心升级只有一句话：**从"反应式提示"升级到"目标导向编排"。** 你先定义好目标、约束和验收标准，让 Claude 自主运行，半小时后来看结果。

---

## Part 1：为什么氛围编程到顶了

### 1.1 氛围编程的本质问题

"氛围编程"（Vibe Coding）的意思是：你感觉到想要什么，告诉 AI，它给你一些东西，你再说"这不对，改一下"，如此循环。

这种方式的问题不是效率低，而是**结构性的**：

1. **没有终点定义**：如果你没有说清楚"完成"是什么样的，这个循环就永远不会结束。
2. **AI 在驱动你**：每一轮对话，你都在响应 AI 给你的输出，而不是你在主导方向。
3. **上下文持续损耗**：每次你说"不对，换一种方式"，原始目标都在偷偷漂移。
4. **可验证性为零**：你"感觉"对了，但没有办法证明它是对的。

这在小项目上可以用，在任何有复杂度的项目上都会失控。

### 1.2 Agentic Engineering 是什么

Agentic Engineering 的核心转变是：**你是导演，AI 是整个剧组。**

导演不会在拍摄途中走进摄影机后面告诉摄影师每一帧怎么拍。导演在开机之前把所有事情说清楚——故事是什么、风格是什么、哪些场景是不能妥协的红线——然后相信团队执行。

对应到 Claude Code：

- **开机前**：写清楚目标（Goal）、约束（Constraints）、验收标准（Done When）
- **拍摄中**：Claude 自主运行，只有遇到真正的歧义才来问你
- **杀青后**：你做的是评审和验收，不是逐行检查

### 1.3 两种工作方式的对比

| | 氛围编程 | Agentic Engineering |
|---|---|---|
| **交互频率** | 每 5 分钟一次 | 启动时定义，完成时评审 |
| **你的输入** | 持续指令 + 即时反馈 | 目标 + 约束 + 验收标准 |
| **Claude 的行为** | 等你告诉它下一步 | 自主执行，阻断时才暂停 |
| **完成标准** | 你"感觉"差不多了 | 预定义的验收清单通过 |
| **适合场景** | 原型探索、一次性任务 | 生产级功能、完整模块 |
| **失败模式** | 目标漂移，无限循环 | 目标定义不清，跑错方向 |

---

## Part 2：三层工作结构

Agentic Engineering 的工作结构分三层，你在 Module 2.6 已经建好了第一层，本文主要讲第二层和第三层的升级。

### 第一层：全局环境（已有）

你的 `~/.claude/CLAUDE.md` 定义了你的工作风格、设计原则、触发条件。这一层不需要改变，但可以加一行新的 agentic 触发规则：

```markdown
## Agentic Mode Rules
- When given a goal-oriented task (structured with Goal/Constraints/Done When):
  run autonomously without asking for confirmation on intermediate steps.
  Only pause if: (1) two or more valid interpretations exist and the choice changes the outcome,
  (2) a destructive operation is needed that was not mentioned upfront,
  (3) a hard technical blocker prevents progress.
```

### 第二层：任务定义（最关键的升级）

这是 Agentic Engineering 和氛围编程最大的分水岭。

**三要素结构：**

```
Goal:        你想要什么（终态描述）
Constraints: 不能碰什么、必须保留什么、技术限制
Done When:   验收标准（可以客观核查的条件）
```

**`/goal` 命令的使用方式：**

`/goal` 是 Claude Code 的内置命令（v2.1.139 引入），专门用于触发自主运行。你在命令后面跟一个**可验证的完成条件**，Claude 就会一直自主执行，直到这个条件满足为止。每轮执行结束后，有一个评估模型自动检查条件是否达成。

使用模式：先给 Claude 完整的上下文（Goal + Constraints），然后用 `/goal` 指定完成条件。

**错误写法 vs 正确写法：**

❌ 氛围编程的写法（会被打断 5 次）：
```
帮我给 Climate Dossier 的 NDC 模块加一个新功能，
就是可以按国家筛选，让结果看起来更好。
```

✅ Agentic Engineering 的写法（一次跑完）：
```
# 背景
Climate Dossier NDC 模块，React 前端，FastAPI 后端。

# 目标
在 NDC 查询界面新增国家筛选器。
用户选择国家后，检索结果只返回该国的 NDC 内容。
"全部国家"作为默认选项（不筛选）。

# 约束
- 不改动 /brief endpoint 的逻辑，只改前端 + 检索层
- 国家列表从现有 metadata 的 country 字段提取，不新增 hardcoded 列表
- UI 风格与现有 sector selector 一致（参考 frontend/src/components/ContextCard.tsx）
- 不修改 eval 测试用例

/goal 筛选器渲染正确，选中某国后 citations 全属于该国，npm run build 无报错
```

注意最后一行：`/goal` 后面跟的是完成条件——一个可以客观核查的句子。Claude 会一直运行，直到这个条件成立。

### 第三层：自主运行 + 门控检查

定义好任务后，设置两件事：

**门控规则（写在任务开头或项目 CLAUDE.md）：**
```
Interrupt only if:
1. Two valid interpretations exist and the choice materially changes the output
2. A destructive operation (delete, overwrite, schema change) was not mentioned in the task
3. A hard blocker prevents any further progress
```

**评审框架（完成后你做的事）：**

拿到结果时，不要逐行看代码。对着你写的 `Done When` 清单核查：
- 每一条验收标准是否通过？
- 有没有意外的副作用（测试 break、样式变化）？
- 对比 git diff，确认 Claude 没有动它不该动的地方

---

## Part 3：Step-by-Step 操作流程

### Step 1：任务分解（写代码之前）

把一个大目标拆成 2-4 个可以独立运行的任务块。每个任务块的标准：
- 有明确的开始状态和结束状态
- 可以在 20-40 分钟内完成
- 不依赖另一个任务块的中间状态

**例子 — Climate Dossier 添加新模块：**

❌ 错误拆法（顺序依赖，无法独立运行）：
```
任务 1：下载文档
任务 2：ingestion（依赖任务 1）
任务 3：写 eval 用例（依赖任务 2）
任务 4：调整 UI（依赖任务 3）
```

✅ 正确拆法（每块可以独立定义和验收）：
```
任务 A：准备语料 — 确定文档列表，写下 source metadata schema
任务 B：Ingestion — 根据 module-onboarding.md 跑 ingest.py，验证 chunk 数量正确
任务 C：Eval — 写 8 个 golden test cases，跑通，确认 pass 率
任务 D：UI — 在 landing page 新增模块入口，通过 npm run build
```

### Step 2：写好上下文，用 `/goal` 触发自主运行

**模板：**

```
# 背景
[当前状态，相关文件路径]

# 目标
[一句话描述终态，主语是"用户"或"系统"，动词是可观察的行为]

# 约束
- [具体文件/功能/逻辑：不能改]
- [技术限制：框架、API、格式]
- [保留的行为：现有测试必须通过]

# 参考文件
- @[相关文件路径]

/goal [完成条件的一句话描述，可以客观核查]
```

说明：`/goal` 之前的部分是给 Claude 的上下文，`/goal` 后面是触发自主运行的完成条件。Claude 会一直运行，直到完成条件被满足。

**会导致 Claude 反复来问你的措辞（避坑清单）：**

| 避免用这些词 | 原因 | 替换为 |
|---|---|---|
| "让它看起来更好" | 没有客观标准 | "与 ContextCard.tsx 样式一致" |
| "优化一下" | 范围不明确 | 具体说优化什么，目标是什么 |
| "类似于 X" | 需要 Claude 猜测 | 指向具体文件：`@X.tsx` |
| "如果可以的话" | 给了 Claude 决策权 | 明确说要还是不要 |
| "差不多就行" | 无验收标准 | 写 Done When 条目 |

### Step 3：设置门控规则

在任务头部或项目 CLAUDE.md 里声明：

```markdown
## Interrupt Policy
Pause and ask only if:
1. Ambiguity: two interpretations exist, each produces materially different output
2. Destructive: action requires deleting/overwriting something not listed in Constraints
3. Blocker: technical issue prevents further progress
Otherwise, make a decision, document it in your summary, and keep running.
```

### Step 4：运行，然后离开

字面意义上离开：去喝杯水，做点别的事。

为什么这一步重要？因为如果你坐在旁边盯着它跑，你会忍不住在它跑完之前就插手。这会打断它的运行流，也会让你陷回氛围编程的循环里。

你在 Agentic Engineering 里扮演的角色是**门控点**，不是监控员。

### Step 5：评审与收尾

拿到结果时，按这个顺序检查：

```
1. 对照 Done When 清单，逐条验证
2. 跑测试（如果有 eval harness：直接跑）
3. 看 git diff — Claude 动了哪些文件？有没有超出范围？
4. 如果有问题：修正 Goal/Constraints 定义，重新启动一次 — 不是逐行改代码
```

---

## Part 4：案例——Climate Dossier 的 Agentic Engineering 实践

### 项目背景

Climate Dossier 是一个双语 RAG 气候知识库，支持 IPCC AR6 全三卷、SBTi 科学碳目标标准、G20 NDC 国家气候承诺三个模块的自然语言问答，带完整引用和"So What"战略解读层。

后端：FastAPI + LlamaIndex + ChromaDB。前端：React。
评估层：25 个 golden test cases，25/25 passing。

这个项目的每一个主要功能，都是用 Agentic Engineering 方式构建的。下面是具体案例。

---

### 案例 A：PRD-first 定义目标（不是 code-first）

Climate Dossier 的第一步不是写代码，而是写 `PRD.md`。PRD 定义了：
- 这个产品是什么（What）
- 两类用户是谁（Who）
- 四个 Must-Have（Done When 的前身）
- 技术选型和限制（Constraints）

有了 PRD，Claude 才知道往哪里跑。没有 PRD 就开始 coding，等价于导演没有剧本就叫"开机"。

**关键决策记录方式：**

每一个重大决定，都实时写进 `CLAUDE.md`：
```markdown
# Climate Dossier — Project CLAUDE.md

## 已决定
- 不用 Vercel（大陆被封）
- 不用 Google Fonts（大陆被封，已自托管 woff2）
- LLM：DeepSeek API（有 503 备用降级到 Anthropic）
- 评估架构：先写 eval 用例，再构建模块——测试用例定义"完成"
```

这不是记笔记，这是**让 Claude 在未来每次启动都能继承这些决定**，不需要你重新解释。

---

### 案例 B：Eval Harness 即验收标准

在 Climate Dossier，每个新模块的工作流是固定的：

```
写 eval 用例（定义 Done When）→ 构建模块 → 跑 eval → 结果 pass → 完成
```

IPCC 模块：7 个 eval 用例，7/7 pass 后上线。
SBTi 模块：10 个 eval 用例，10/10 pass 后上线。
NDC 模块：8 个 eval 用例，8/8 pass 后上线。
三个模块合计 25 个 golden test cases，全部 passing。

这就是 `/go` 里 `Done When` 的真实形态——一个可以机器执行的验收清单。

```bash
# eval harness 用一行命令跑完验收
backend/venv/bin/python eval/run_eval.py --module ndc
# 输出：8/8 passing — done
```

当你把"完成"变成一个可执行的命令，Agentic Engineering 就变得非常清晰：Claude 跑到这个命令通过为止。

---

### 案例 C：Staging Workflow 即门控系统

Climate Dossier 在数据库层实现了门控：

```
ingest to dev DB → 跑 eval → pass → promote to prod
                              ↓
                           fail → 诊断，重跑
```

这个 workflow 的意义不只是技术安全，它是一个**结构化的门控**——Claude 可以在 dev 环境里自由实验，但 prod 环境有明确的进入条件（eval 全部通过）。

类比到你自己的项目：在任何有生产环境的项目里，**门控点要在任务定义里写清楚**，不要靠你在评审时临时决定。

---

### 案例 D：模块化 Onboarding 协议

Climate Dossier 有一份 `module-onboarding.md`，定义了添加任何新模块的完整步骤：定义文档列表 → 配置 metadata schema → 写 eval → 运行 ingestion → 验证 chunk 数量 → 跑 eval → 通过后更新 CLAUDE.md。

这就是一个**可重复的 `/go` 模板**。每次添加新模块，你不需要重新发明流程，只需要填入新模块的参数，然后让 Claude 按协议运行。

这是 Agentic Engineering 的最高境界之一：**流程本身就是你最有价值的工程产出**，而不只是你写出来的代码。

---

## Part 5：Claude Code vs OpenAI Codex

截至 2026 年 5 月，AI 编程工具市场有两个主要的 agentic 选手：Anthropic 的 Claude Code 和 OpenAI 的 Codex（2025 年重新发布的 cloud-based 编程 agent）。

### 核心架构差异

| | Claude Code | OpenAI Codex |
|---|---|---|
| **运行环境** | 本地 CLI（跑在你的机器上） | 云端沙箱（跑在 OpenAI 的服务器上） |
| **代码访问** | 读取你的整个本地 codebase | 连接到 GitHub repo（云端克隆） |
| **配置系统** | CLAUDE.md（持久化项目规范） | 无等价配置文件 |
| **并行能力** | 支持 sub-agent | 支持多个任务并行运行（云端沙箱） |
| **自定义命令** | 可定义 skills（`/go`、`/commit` 等） | 无自定义命令系统 |
| **本地工具** | 可直接调用本地 shell、工具链 | 运行在隔离沙箱，工具访问受限 |

### 分别适合什么场景

**Claude Code 更适合：**
- 本地开发环境（需要读写本地文件、跑本地服务器）
- 有复杂项目规范（CLAUDE.md 的价值在于持久化上下文）
- 需要自定义 workflow（skills、hooks）
- 在中国大陆以外部署的项目（API 直连）

**OpenAI Codex 更适合：**
- GitHub-first 工作流（代码全在云端）
- 需要同时跑多个独立任务（并行沙箱）
- 没有本地开发环境的纯云端场景

### 这份指南的工具选择

本指南所有示例都基于 Claude Code。**Agentic Engineering 的核心原则（Goal + Constraints + Done When + 门控评审）与工具无关**，可以迁移到 Codex 或任何其他 agentic 工具。工具会变，工程思维不会。

---

## Part 6：常见问题

**Q：这和 Harness Engineering 是什么关系？**

Harness Engineering（Module 2.6）是**基础设施层**：它让 Claude 知道怎么证明代码是正确的（CLAUDE.md、proof of correctness、context hygiene）。

Agentic Engineering 是**工作流层**：它让 Claude 知道往哪里跑、跑多久、遇到什么情况停下来。

两者叠加才是完整体系。没有 Harness Engineering，Agentic Engineering 会产生快速但错误的输出。没有 Agentic Engineering，Harness Engineering 会让你构建得正确但效率没有提升。

**Q：如果 Claude 跑了半小时但方向完全错了怎么办？**

这几乎总是因为 Goal 定义不清，或者 Constraints 里遗漏了关键限制。不要在错误的输出上继续修改，而是：

1. 找到 Goal 里哪句话导致了偏差
2. 修正 Goal/Constraints
3. 重新启动一次

一次完整的重新运行比无数次零碎修改更快。

**Q：`/goal` 是 Claude Code 的内置命令吗？**

是的，`/goal` 是 Claude Code 的内置命令（v2.1.139 引入），不需要自己创建。使用方式：`/goal` 后面跟一个可以客观验证的完成条件（例如：`/goal all tests pass and npm run build succeeds`）。Claude 会自主运行并在每轮结束后自动检查条件，直到条件满足为止。

**Q：如果项目很小，有必要这样做吗？**

对于一次性小脚本或原型，氛围编程完全没问题。Agentic Engineering 的价值在**复杂度临界点之后**：当一个任务涉及多个文件、有副作用风险、或者需要反复执行时，结构化定义的投入会在第一次运行就回收。

---

## 升级路径

| 阶段 | 能力 | 对应工具 |
|---|---|---|
| 阶段 1 | 单任务 agentic 运行 | `/goal` 命令 + 结构化上下文 + 门控规则 |
| 阶段 2 | 项目级规范沉淀 | 项目 CLAUDE.md — 让每次会话继承决策 |
| 阶段 3 | 可重复模块化流程 | Onboarding 协议 + Eval Harness |
| 阶段 4 | 自动化闭环 | CI/CD 集成（eval 跑通才允许 merge） |

---

## 附录：模板库

### `/goal` 启动模板（可直接复制）

```
# 背景
[当前状态描述]

# 目标
[一句话终态描述]

# 约束
- [不能动的文件或功能]
- [技术限制]
- [必须保留的行为]

# 参考文件
- @[相关文件路径]

/goal [完成条件的一句话，可以客观核查]
```

### 门控规则模板（放入 CLAUDE.md）

```markdown
## Interrupt Policy
Pause and ask only if:
1. Two valid interpretations exist and the choice materially changes the output
2. A destructive operation is required that was not mentioned in the task definition
3. A hard technical blocker prevents further progress
Otherwise: decide, document your reasoning, and keep running.
```

### 评审清单模板

```markdown
## Review Checklist
- [ ] Done When 条目 1：通过 / 失败
- [ ] Done When 条目 2：通过 / 失败
- [ ] Done When 条目 3：通过 / 失败
- [ ] git diff 范围合理，没有超出 Constraints
- [ ] 测试通过（或 eval harness pass）
- [ ] 没有新引入的依赖或架构变化
```
