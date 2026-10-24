# 官方顶级标杆 2：工程与流程类 (Engineering & Workflow)
> **对标来源**：Claude 官方 `docx` 转换流、企业级生产发布与复杂重构 Skill
> **核心启示**：决策树前置、环境前置依赖探测、步骤原子核验、失败回退自愈、操作幂等性。

---

## 标杆结构骨架与关键实现

```markdown
---
name: database-migration-flow
description: >-
  执行生产级数据库 Schema 变更与数据迁移的 SOP 流水线。
  当用户要求执行数据库变更、执行 SQL 迁移脚本或进行数据库版本升级时使用。
  不用于一般的 SQL 查询或性能慢查询单点调优；生产环境必须具备前置备份才可唤醒。
---

# Database Migration Workflow — 生产级数据库迁移闭环

本 Skill 固化了高可靠性数据库变更的标准作业程序（SOP）。核心原则是**“防卫式执行、步骤原子化、失败必回退、幂等无残留”**。

---

## 阶段决策树 (Workflow Decision Tree)

在执行任何变更前，首先评估变更类型：
```
目标变更类型判定:
├─ 只读检验 / Dry-run?
│   └─ 执行 Phase 1 → 语法与 Schema 差异对比 → 输出演练报告并终止
├─ 非破坏性新增 (ADD COLUMN / CREATE TABLE)?
│   └─ 执行 Phase 1 → Phase 2 (备份) → Phase 3 (应用变更) → Phase 4 (验收)
└─ 破坏性变更 (DROP / ALTER TYPE / RENAME)?
    └─ 强制阻断！提示用户必须显式追加 `--allow-destructive` 确认，否则终止执行。
```

---

## 四阶段标准化执行流程

### Phase 1: 环境与前置依赖探测 (Pre-flight Inspection)
在连接目标数据库前，执行确定性前置检查：
1. **依赖工具探测**：检查 `psql` / `mysql` 客户端命令是否可用，版本是否兼容；
2. **只读连通性校验**：执行 `SELECT 1` 验证网络连接与操作权限；
3. **活动连接与锁检查**：检查当前是否有排他性大事务正在持有表级锁。
> ⚠️ **前置失败判定**：若上述任何一项失败，**立刻阻断退出**，并打印具体缺失项，严禁继续推进！

### Phase 2: 快照与变更脚本准备 (Atomic Snapshot)
1. **执行元数据备份**：在当前工作区生成变更前 DDL 快照 `backup/schema_pre_<timestamp>.sql`；
2. **准备回滚脚本**：必须先在本地编写好对应的反向回滚 SQL（Rollback Script），绝不允许“先变更，后写回滚”。

### Phase 3: 确定性事务执行 (Transactional Execution)
1. 始终将变更包裹在显式事务块中（`BEGIN ... COMMIT`）；
2. 严禁让大模型在终端里直接交互式手敲 SQL，必须通过加载本地 SQL 脚本文件执行：
   ```bash
   psql -f migrations/001_add_index.sql --set ON_ERROR_STOP=on
   ```
3. **幂等性保障**：脚本内必须使用 `IF EXISTS` / `IF NOT EXISTS`，保证重复执行无破坏性副作用。

### Phase 4: 验收与失败自愈分支 (Verification & Self-Healing)
- **验收 Checklist**：
  - [ ] Schema 变更字段类型与默认值校验通过
  - [ ] 对应索引状态为 `VALID`
  - [ ] 示例写入与读取测试通过
- **失败自愈分支 (Rollback Procedure)**：
  - 若 Phase 3 报错或 Phase 4 验收未达标：
    1. 自动触发回滚脚本 `backup/rollback_<timestamp>.sql`；
    2. 检查数据库连接状态是否恢复；
    3. 收集并输出完整的 `stderr` 错误日志，给用户明确的修复建议。
```
