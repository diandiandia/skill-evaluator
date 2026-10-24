# Skill Evaluator (架构级技能质量评估与诊断工具)

基于 **00（TopHCI）深度拆解 Claude 官方顶级 Skills 的核心哲学**、**目标域-子目标全域通用性模型**、**架构承载力对等天平** 以及 **长周期大项目执行韧性**，专为 CLI 终端环境打造的纯架构级 Skill 评估与重构智囊。

---

## 一、核心定位与四大第一性原理

> **评估一个 Skill 的好坏，本质是一场高级架构评审（Architecture Review）。**

### 1. 为什么是“纯架构评审”，而不是跑 Python 脚本？
- **机器脚本看不懂设计意图**：搜关键字或数行数的正则脚本，既看不出逻辑断层，也分辨不出死规则，极易被“硬塞关键词的垃圾 Skill”糊弄；
- **Agent 架构师的核心价值**：纯依靠具备推理能力的 LLM，对目标 Skill 进行**意图反推、目标域与子目标通用性审视、架构承载力校验、长周期断点存盘核验与“做乘法不做加法”的终审重构**。

### 2. 核心审判关卡 A：目标域界定与子目标全域通用性 (Sub-goals Generality)
- **痛点洞察**：业界许多 Skill 最大的通病就是**“假通用与特例过拟合”**——宣称目标宏大（如“处理一切 PDF”），实际只写了作者碰到的某一个最简单的子目标（如纯文本），遇到表格、加密、跨页、格式损坏等同域常见子目标立刻崩溃；
- **高手标准**：主目标范围内的所有必然子场景（正向、变体、极端边界）具备通用方法论；做不到的子场景**必须有清晰诚实的排除声明（What-NOT）与优雅拦截降级**。

### 3. 核心审判关卡 B：目标野心与工程复杂度对等天平 (Architectural Sufficiency)
- **痛点洞察**：**“小马拉大车 / 纸上谈兵”**——目标定在火星（如“百万行全库架构重构与迁移”），实现却躺在地上：通篇就一段 100 行的 `SKILL.md` 口号，无配套规范、无模板、无状态机，模型缺乏支点必然口头糊弄；
- **高手标准**：轻量任务保持单文件极简；重型宏大目标必须匹配成体系的工程承载力（分阶段门禁、`references/` 规约外置、`assets/` 样板模板、确定性逻辑下沉）。

### 4. 核心审判关卡 C：长周期稳定执行与防假性完成 (Long-Running Resilience)
- **痛点洞察**：**“跑半天就自以为做完了（假性收工）”**——大项目任务执行数小时或一整天，中途遭遇上下文压缩或轻微受阻，模型产生“我辛勤工作了很久应该全部搞定了”的心理幻觉，草草交差；
- **高手标准**：
  1. **全量待办总账清单 (Scope Inventory)**：启动时必须先清点全量待办，严禁凭感觉找活；
  2. **磁盘持久化断点存盘 (STATE.json)**：进度实时写磁盘，抗崩溃与抗上下文压缩；
  3. **防假完成对账门禁 (Done==Total)**：只要有未完项严禁收工；
  4. **单点故障重试熔断 (Circuit Breaker)**：避免单点死锁耗尽配额。

---

## 二、四大官方顶级标杆样例库 (Canonical Exemplars)

为了让评估具备真实、可落地的参考依据，本工具在 `references/exemplars/` 中内置了覆盖业界最常见四大形态的**官方顶级标杆实现**：

1. **[创意 / 生成类标杆 (algorithmic-art / canvas-design)](./references/exemplars/creative_design_exemplar.md)**：
   - 示范：拔高天花板（立流派而非交单）、双阶段抽象（规范先行）、概念种子入物理参数、FIXED/VARIABLE 解耦、做乘法不做加法精修守卫。
2. **[工程 / 流程类标杆 (docx 转换流 / 生产发布闭环)](./references/exemplars/workflow_engineering_exemplar.md)**：
   - 示范：决策树前置、环境前置依赖探测、步骤原子性校验、失败原子回滚与自愈、操作幂等性保障。
3. **[任务 / 菜单类标杆 (pdf / ffmpeg 工具箱)](./references/exemplars/task_toolkit_exemplar.md)**：
   - 示范：入口速查表 (Capability Index)、任务原子独立解耦、输入输出强契约、依赖缺失自动降级。
4. **[规范 / 标准类标杆 (代码审查 / API 架构规范)](./references/exemplars/guideline_standards_exemplar.md)**：
   - 示范：原则→规范→操作映射、正反示例 (Good vs Bad) 鲜明对照、具象化验收 Checklist、零常识通胀。

---

## 三、目录架构

```
skill-evaluator/
├── SKILL.md                          # 评估 Skill 核心调度中枢（≤ 120 行，轻量骨架）
├── README.md                         # 核心理念与 CLI 使用说明文档
├── references/
│   ├── evaluation_rubric.md          # 100 分制品类自适应量化评分量表 (四维对称 25x4)
│   ├── structural_patterns.md        # 架构模式 + 长周期稳定性模式 + 官方 7 大高阶技法详解
│   ├── obligation_four_questions.md  # 义务入库四问与四缺陷案例库
│   └── exemplars/                    # 4 大官方顶级标杆样例库
│       ├── creative_design_exemplar.md       # 创意设计类标杆
│       ├── workflow_engineering_exemplar.md  # 工程流程类标杆
│       ├── task_toolkit_exemplar.md          # 任务菜单型标杆
│       └── guideline_standards_exemplar.md   # 规范标准型标杆
└── templates/
    └── audit_report.md               # 标准化 100 分制审计诊断报告交付模板 (含对等天平/子目标/长周期对账表)
```

---

## 四、CLI 终端使用方式

在终端中直接将目标 Skill 路径发给 Agent：

### 1. 快速体检（默认模式）
> “帮我评估一下当前目录的 Skill 写的怎么样”  
> *(Agent 会在 15 行极简卡片内输出得分、品类、子目标覆盖、承载力与稳定性诊断、Top 3 致命缺陷与对齐标杆建议)*

### 2. 深度审计与重构建议
> “请按照 skill-evaluator 的标准，为该 Skill 输出一份深度审计报告，并帮我重构优化”  
> *(Agent 会对照 4 大标杆输出完整的【目标-复杂度对等天平】、【子目标覆盖矩阵表】、【长周期稳定性核查】与行号取证分析，并当场给出一份裁剪掉 50% 冗余的重构版 `SKILL.md.suggested`)*
