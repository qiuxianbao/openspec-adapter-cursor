## 1.变更提案(Why)

为什么做 + 做完后的效果（可验证的结果描述）

- **业务背景与价值**：为什么需要做这个变更？
- **预期收益**：上线后能带来什么业务或技术指标提升？

## 2.变更范围 (Scope)

- **In Scope (本次包含)**：明确本次实施的功能点。
- **Out of Scope (本次不含)**：明确本次不做的事情，避免需求蔓延。

### 非功能性需求 (NFR)
- **性能要求**：[如 QPS 预估、p99 延迟要求等]
- **可靠性要求**：[如 可用性 SLA、数据一致性级别（强一致 vs 最终一致）等]
- **安全与合规**：[如 敏感数据脱敏、审计日志等]

### 新功能变更
<!-- Capabilities being introduced. Replace <name> with kebab-case identifier (e.g., user-auth, data-export, api-rate-limiting). Each creates specs/<name>/spec.md -->

- `<name>`:

### 已有功能变更
<!-- Existing capabilities whose REQUIREMENTS are changing (not just implementation).
     Only list here if spec-level behavior changes. Each needs a delta spec file.
     Use existing spec names from openspec/specs/. Leave empty if no requirement changes. -->

- `<existing-name>`:

## 3.系统影响点

- **依赖模块**：哪些上下游模块会受到影响？
- **兼容性**：是否存在旧数据兼容、API 兼容问题？

