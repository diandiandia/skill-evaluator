# Skill 质量评估与深度审计报告 (Evaluation & Audit Report)

## 一、基本信息与概览

| 属性 | 评估记录 |
|:---|:---|
| **被审 Skill 名称** | `{{skill_name}}` |
| **文档路径** | `{{skill_path}}` |
| **识别品类** | 创意设计类 / 工程流程类 / 任务菜单类 / 规范准则类 |
| **主文档行数** | `{{line_count}}` 行（标准推荐 ≤ 500 行） |
| **选用架构模式** | Workflow-based / Task-based / Reference-Guidelines / Capabilities-based / 结构混乱 |
| **配套资源目录** | `references/` ({{has_refs}}), `assets/` ({{has_assets}}) |
| **综合评分 / 评级** | **{{total_score}} / 100**（评级：**{{grade}} 级**） |

---

## 二、四维量化评分卡

```
[综合总分: {{total_score}}/100  |  最终评级: {{grade}} 级]
├─ 维度一：目标域界定与长周期承载力 [{{score_dim1}}/25]  {{bar_dim1}}
├─ 维度二：元数据与渐进式信息架构   [{{score_dim2}}/25]  {{bar_dim2}}
├─ 维度三：指令工程与四缺陷诊断     [{{score_dim3}}/25]  {{bar_dim3}}
└─ 维度四：品类高阶技法与精修闭环   [{{score_dim4}}/25]  {{bar_dim4}}
```

---

## 三、目标野心 vs 架构复杂度对等天平 (Proportionality & Sufficiency)

> [!IMPORTANT]
> 审查核心：目标野心与工程承载力是否相符？严防“小马拉大车（百行文本口号企图撬动复杂系统）”与“大炮打蚊子（轻量任务过度设计）”。

| 维度 | 审查记录与判定 |
|:---|:---|
| **宣称主目标 (Declared Goal)** | `{{declared_primary_goal}}` |
| **真实需要的工程复杂度** | 轻量级单点 / 中量级专业规范 / 宏大重型工程体系 |
| **实际交付的架构支撑** | 仅单薄纯文本 / 纯文本+轻量 Checklist / 具备决策树+状态机+模板分流 |
| **承载力诊断结论** | ✅ **严密匹配** / ⚠️ **轻度倒挂** / ❌ **严重贫血 (小马拉大车纸上谈兵)** |

---

## 四、目标域与子目标通用性对账表 (Goal Scope & Sub-goals Generality)

| # | 目标域内必然存在的子目标/子场景 | 该 Skill 的应对策略与覆盖状态 | 是否存在特例过拟合? | 判定结果 |
|:---:|:---|:---|:---:|:---:|
| 1 | **基础常规正向子目标**<br>*(Happy Path)* | {{subgoal_1_strategy}} | 是 / 否 | ✅ 充分通用 / ⚠️ 局部可用 / ❌ 缺失 |
| 2 | **数据/结构/形态复杂变体**<br>*(Complex Variations)* | {{subgoal_2_strategy}} | 是 / 否 | ✅ 充分通用 / ⚠️ 局部可用 / ❌ 缺失 |
| 3 | **极端边界与输入损坏场景**<br>*(Edge / Corrupted Cases)* | {{subgoal_3_strategy}} | 是 / 否 | ✅ 充分通用 / ⚠️ 局部可用 / ❌ 缺失 |
| 4 | **环境依赖失败或权限受限**<br>*(Failure & Permission)* | {{subgoal_4_strategy}} | 是 / 否 | ✅ 具备自愈 / ⚠️ 单向假设 / ❌ 崩溃 |
| 5 | **超出能力的子场景**<br>*(Out-of-Scope Scenarios)* | {{subgoal_5_strategy}} | — | ✅ 诚实排除拦截 / ❌ 假装能做后翻车 |

---

## 五、长周期大工程执行稳定性审查 (Long-Running Resilience)

针对可能运行数小时甚至整整一天的长任务，核验其防假性完成与容错机制：

| # | 稳定性关键机制 | 是否具备 | 现场核查记录与分析 |
|:---:|:---|:---:|:---|
| 1 | **全量待办总账清单 (Scope Inventory)** | 是 / 否 / 不适用 | {{resilience_inventory}} |
| 2 | **磁盘持久化断点存盘 (STATE.json)** | 是 / 否 / 不适用 | {{resilience_checkpoint}} |
| 3 | **防假性完成对账门禁 (Done==Total)** | 是 / 否 / 不适用 | {{resilience_accounting_gate}} |
| 4 | **单点故障重试熔断机制 (Circuit Breaker)**| 是 / 否 / 不适用 | {{resilience_circuit_breaker}} |

---

## 六、一票否决项与致命缺陷筛查

- [ ] **去项目化失败**：正文是否存在硬编码本地绝对路径或特定项目私有代号？（{{veto_project_leakage}}）
- [ ] **伪通用严重过拟合**：是否将单一测试文件的局部特征硬写为全局规则导致其他用例全翻车？（{{veto_overfitting}}）
- [ ] **大目标架构严重脱节**：目标宏大但无任何状态机、模板、门禁支撑，纯属口头承诺纸上谈兵？（{{veto_starvation}}）
- [ ] **触发描述丢失**：Description 是否缺失“何时出场”或过于泛滥？（{{veto_trigger_missing}}）
- [ ] **循环/深度嵌套**：是否存在超过 1 层的套娃引用？（{{veto_nesting_error}}）

*(注：任一票否决项命中，总评级直接锁定为 F 级)*

---

## 七、品类专属技法对账表 (Category-Adaptive Radar)

*(根据识别品类对标官方顶级标杆库)*

### 通道 A：创意 / 设计 / 生成类 Skill (对标 `creative_design_exemplar`)
- 提高天花板 (立流派/立范式): {{radar_a1}}
- 双阶段结构 (规范抽象先行): {{radar_a2}}
- 概念种子深嵌 (参数非文案): {{radar_a3}}
- 模版解耦 (FIXED vs VARIABLE): {{radar_a4}}
- 做乘法不做加法 (精修守卫): {{radar_a5}}

### 通道 B：工程 / 流程 / 运维类 Skill (对标 `workflow_engineering_exemplar`)
- 决策树前置 (类型显式分流): {{radar_b1}}
- 环境前置探测 (工具连通性): {{radar_b2}}
- 操作原子性与快照备份: {{radar_b3}}
- 原子回滚与自愈 (失败自愈): {{radar_b4}}
- 严格幂等性 (多次重复无害): {{radar_b5}}

### 通道 C：任务 / 菜单类 Skill (对标 `task_toolkit_exemplar`)
- 能力速查表 (Capability Index): {{radar_c1}}
- 任务独立原子解耦: {{radar_c2}}
- 输入输出强契约校验: {{radar_c3}}
- 依赖缺失优雅降级提示: {{radar_c4}}

### 通道 D：规范 / 准则 / 能力类 Skill (对标 `guideline_standards_exemplar`)
- 规范→操作映射体系: {{radar_d1}}
- 正反示例对照 (Good/Bad): {{radar_d2}}
- 逐项对账 Checklist 具象化: {{radar_d3}}
- 提示词密度精修 (无常识堆砌): {{radar_d4}}

---

## 八、缺陷取证清单 (Defect Findings & Evidence)

> [!IMPORTANT]
> 坚持取证先行原则，每条缺陷必须直接对应原文代码或行号，杜绝主观臆断。

### 缺陷 1：【{{Defect_Class}}】{{Defect_Title}}
- **原文定位**：`{{file_path}}:第 {{line_number}} 行`
- **原文摘录**：
  ```markdown
  {{quoted_text}}
  ```
- **危害分析**：{{impact_analysis}}
- **整改建议**：{{remediation_advice}}

---

## 九、义务入库四问过筛表 (Obligation Justification Table)

针对疑似冗余、过度设计的可疑规则条目进行裁决：

| # | 待审查规则摘要 | 触发条件明确? | 消费者明确? | 删掉后果严重? | 模型原生可推导? | 最终裁决 |
|---|---------------|:------------:|:-----------:|:-----------:|:-------------:|:--------:|
| 1 | `{{rule_1}}` | 是 / 否 | 是 / 否 | 是 / 否 | 是 / 否 | 保留 / 裁除 / 降级 |
| 2 | `{{rule_2}}` | 是 / 否 | 是 / 否 | 是 / 否 | 是 / 否 | 保留 / 裁除 / 降级 |

---

## 十、终审重构优化方案（遵循“做乘法不做加法”）

针对上述缺陷、承载力脱节与长周期稳定性漏洞，给出裁剪优化后的建议重构版 `SKILL.md.suggested`：

```markdown
{{refactored_skill_markdown}}
```
