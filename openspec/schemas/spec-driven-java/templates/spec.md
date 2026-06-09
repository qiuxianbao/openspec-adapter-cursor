## 规格定义 (Spec)

### 需求: [填写需求名称]

#### 1. 目标与范围
> 复杂度: 🟢简单 | 🟡中等 | 🔴复杂

[一句话描述这个功能做什么]

##### 1.1 Delta 增删改规范
明确列出对系统的操作：
- **新增**：(如 新增数据库表、新增接口)
- **修改**：(如 修改现有方法逻辑)
- **删除/废弃**：(如 废弃某些字段)

##### 1.2 不做清单
- [明确不在范围内的功能 1]
- [明确不在范围内的功能 2]


#### 2. 业务场景定义 (What)
- **核心流程 (Happy Path)**：正常情况下的流转过程。
- **异常分支 (Edge Cases)**：各种异常情况及处理策略。

##### [场景 1]
- **Given (假设)**：[前置条件/系统状态]
- **When (当)**：[触发事件/用户操作]
- **Then (那么)**：[预期结果/系统行为]
- **异常处理**：[错误情况及降级策略]

#### 3. 验收标准 (Acceptance Criteria): <!-- scenario name -->
[请严格使用 EARS 语法的 5 种标准模式编写验收标准]
1. **Ubiquitous (无条件/通用)**: The [system] shall [behavior]
2. **Event-driven (事件驱动)**: When [trigger], the [system] shall [response]
3. **State-driven (状态驱动)**: While [state], the [system] shall [behavior]
4. **Unwanted behavior (异常处理)**: If [condition], then the [system] shall [response]
5. **Optional feature (可选特性)**: Where [feature], the [system] shall [behavior]

- 示例：When [触发条件], the [系统] shall [行为], within [约束]

