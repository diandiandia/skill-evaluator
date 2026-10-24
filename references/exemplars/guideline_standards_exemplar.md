# 官方顶级标杆 4：规范与标准型 (Reference & Guidelines)
> **对标来源**：Claude 官方代码审查规范、企业安全基线与品牌设计标准 Skill
> **核心启示**：原则→规范→操作映射、正反示例 (Good/Bad) 鲜明对照、具象化验收 Checklist、零常识通胀。

---

## 标杆结构骨架与关键实现

```markdown
---
name: api-design-guidelines
description: >-
  固化企业级 RESTful API 设计与评审标准的规范型 Skill。
  当用户要求设计新 API、评审 API 接口定义或重构 HTTP 响应格式时使用。
  不用于底层的数据库 Schema 建模，也不用于前端页面路由配置。
---

# RESTful API 设计与审查规范

本规范旨在固化团队 API 的一致性、向后兼容性与安全防御标准。所有规则均具备明确的判据，杜绝空洞口号。

---

## 核心设计原则 (Core Principles)

1. **面向资源建模**：URI 表达名词资源，HTTP Method 表达动作。
2. **确定性状态契约**：响应结构统一，错误状态码与业务码正交解耦。
3. **向后兼容性第一**：新增字段兼容旧客户端，废弃字段保留过渡期。

---

## 核心规则与正反对比 (Rules & Contrasts)

### 规则 1：URI 命名与复数规范
- **红线**：URI 中严禁出现动词（如 `/getUser`、`/createOrder`）；一律使用小写短横线（kebab-case）复数名词。
- ❌ **Bad (错误示例)**:
  `POST /api/v1/updateUserProfile`
  `GET /api/v1/user_orders/get_by_id?id=123`
- ✅ **Good (正确示例)**:
  `PUT /api/v1/users/{userId}/profile`
  `GET /api/v1/users/{userId}/orders/{orderId}`

### 规则 2：统一响应封套与错误表达
- **红线**：禁止在 HTTP 200 中返回业务级致命错误（避免网关与客户端缓存策略失效）。
- ❌ **Bad (错误示例)**:
  ```json
  // HTTP 200 OK
  { "code": 500, "msg": "Database timeout", "data": null }
  ```
- ✅ **Good (正确示例)**:
  ```json
  // HTTP 504 Gateway Timeout
  {
    "error": {
      "code": "DB_CONNECTION_TIMEOUT",
      "message": "The upstream database connection timed out.",
      "request_id": "req-98f24a1b"
    }
  }
  ```

### 规则 3：分页与游标设计
- **红线**：集合数据超过 20 条必须支持分页，默认限制 `max_limit = 100`，杜绝全表深分页拖垮服务。
- ✅ **标准参数**：`?limit=20&cursor=eyJpZCI6MTAwfQ==`

---

## 逐项对账检查清单 (Review Checklist)

评审任何 API 设计草案时，必须逐条过筛以下清单：

| # | 检查项 | 达标判定标准 | 否决等级 |
|:---:|:---|:---|:---:|
| 1 | **名词命名** | URI 零动词，全部使用复数 kebab-case | 严重 |
| 2 | **状态码正交** | 4xx/5xx 与 HTTP 语义严格一致，无 200 报假警 | 严重 |
| 3 | **幂等方法遵守** | PUT / DELETE 方法必须具备幂等性 | 严重 |
| 4 | **字段命名一致** | 全系统统一 snake_case，禁止混用 camelCase | 普通 |
| 5 | **边界分页安全** | 包含强校验的 limit 限制，杜绝无限大请求 | 严重 |
```
