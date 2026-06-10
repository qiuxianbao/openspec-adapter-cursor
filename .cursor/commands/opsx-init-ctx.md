---
name: /opsx-init-ctx
id: opsx-init-ctx
category: Workflow
description: 初始化项目上下文 (Initialize project context)
---

用于初始化项目，并填充 OpenSpec 所需的工程上下文与业务领域上下文。

**前置**：建议在首次 `/opsx:new` 或 `/opsx:propose` 之前执行。

**产出物**

| 文件 | 来源模板 | 作用 |
| --- | --- | --- |
| `openspec/context/project-context.md` | `openspec/schemas/context/project-context.md` | 工程侧：技术栈、目录、模块、分层 |
| `openspec/context/domain.md` | `openspec/schemas/context/domain.md` | 业务侧：规则、术语、状态机、流程 |
| `openspec/config.yaml`（`context` 字段） | 由上述两文件合并生成 | OpenSpec CLI 注入 `<project_context>` 的唯一入口 |

**Steps**

1. **复制或合并上下文模板**
   将 `openspec/schemas/context/` 下的模板应用到 `openspec/context/` 目录。
   - 如果 `openspec/context` 目录不存在，请先创建它。
   - **注意：如果目标文件已经存在，不能直接删除或覆盖**。必须读取现有内容，并根据新的模板格式或项目分析结果进行增量更新或合并。

2. **分析当前项目**
   使用工具（如 `Glob`, `Shell`, `Read`）扫描当前项目：
   - 查找依赖文件（如 `pom.xml`, `build.gradle`, `package.json`, `go.mod` 等）以确定技术栈和构建工具。
   - 扫描目录结构以了解模块划分、分层架构。
   - 从领域模型、枚举、常量、表结构推断业务规则与术语。
   - 提取项目名称、简介和关键依赖（中间件等）。

3. **填充 `project-context.md`**
   按模板各节更新 `openspec/context/project-context.md`：
   - §1 项目概述、§2 技术栈（表格）、§3 目录结构（**必须 tree 格式**）
   - §4 模块依赖、§5 分层架构、§6 项目特有开发约定
   - 无法确定的部分保留 TODO；**保留用户已手动添加的有效信息**

4. **填充 `domain.md`**
   按模板各节更新 `openspec/context/domain.md`：
   - §3 项目特定业务规则、§4 术语表、§5 核心实体、§6 状态流转、§7 业务流程
   - §2 通用领域规则：仅当项目有明确偏离时再修改，否则保留模板默认值
   - 无法推断时保留 TODO，**不要编造**

5. **同步到 `openspec/config.yaml`**
   OpenSpec CLI **只**从 `config.yaml` 的 `context` 字段注入上下文（上限 50KB），不会自动读取 `openspec/context/`。
   - 读取 `openspec/config.yaml`（不存在则创建，至少含 `schema` 字段）
   - 将 `project-context.md` 与 `domain.md` 合并写入 `context:` 多行字符串，格式如下：

     ```
     # 项目上下文
     <project-context.md 正文>

     ---

     # 业务领域
     <domain.md 正文>
     ```

   - 合并后超过 50KB 时：保留 §1–§5 核心节，删减冗长 tree/表格，并在 `context` 末尾注明「完整版见 openspec/context/」
   - **保留** `config.yaml` 中已有的 `schema`、`rules` 等字段，仅更新 `context`
   - 执行 `openspec instructions proposal --change <任意已有change> --json` 或新建临时 change 验证 `context` 字段已被 CLI 识别（可选）

6. **完成与总结**
   完成文件修改后，向用户输出总结信息。

**Output**

执行完毕后，请输出以下总结：
- 提示上下文初始化完成，并列出已创建/修改的文件路径（含 `config.yaml` 的 `context` 是否已同步）
- 简要展示分析到的项目信息（如识别出的技术栈、核心模块、业务域）
- 提醒用户检查 `openspec/context/` 下的 TODO 项，并根据实际情况手动补充或修正
- 提示下一步：执行 `/opsx:propose` 或 `/opsx:new` 开始变更

**Guardrails**
- 确保在修改文件前已经完整读取模板内容。
- 如果项目结构过于复杂，仅提取核心目录和模块，避免上下文文件过长。
- 保持客观，对于不确定的技术栈或业务流程，不要随意编造，应留空或添加 TODO 标记让用户确认。
- `project-context.md` 不写业务状态机；`domain.md` 不写 Maven 依赖——严格分工。
