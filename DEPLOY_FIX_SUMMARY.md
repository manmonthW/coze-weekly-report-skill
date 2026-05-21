# Skill 项目 .coze 配置修复记录

## 背景

本项目 `coze-weekly-report-skill` 是一个纯 Skill 项目（纯 Markdown 文档），用于将工程项目人员的工作流水账自动整理为结构化项目周报。

在部署过程中遇到多个配置缺失错误，以下是完整的错误与修复记录。

---

## 错误与修复汇总

### 错误 1：缺少 deploy.run
```
error: check .coze file failed, err: deploy.run is required for kind service
```

**原因**：平台将项目错误识别为 `kind=service`，要求提供 `deploy.run`。

**修复**：显式设置 `deploy.profile.kind = "skill"`

```toml
[deploy]
profile = { kind = "skill" }
```

---

### 错误 2：缺少 skill.skill_package
```
error: check .coze file failed, err: skill.skill_package is required for kind skill
```

**原因**：设置了 `kind=skill` 后，平台要求提供技能包入口文件。

**修复**：添加 `skill_package` 配置，指向技能入口文件

```toml
[skill]
skill_package = "SKILL.md"
```

---

### 错误 3：缺少 skill.name
```
error: skill.name is empty in .coze file
```

**原因**：Skill 构建流程要求技能名称。

**修复**：添加 `skill.name` 配置

```toml
[skill]
skill_package = "SKILL.md"
name = "项目周报助手"
```

---

### 错误 4：缺少 skill.description
```
error: skill.description is empty in .coze file
```

**原因**：Skill 构建流程要求技能描述。

**修复**：添加 `skill.description` 配置

```toml
[skill]
skill_package = "SKILL.md"
name = "项目周报助手"
description = "将工程项目人员的工作流水账自动整理为结构化项目周报"
```

---

## 最终 .coze 配置

```toml
[project]
sub_id = "a171ab5b"
name = "coze-weekly-report-skill"
requires = []
project_type = ""

[preview]
preview_enable = "disabled"

[deploy]
profile = { kind = "skill" }

[skill]
skill_package = "SKILL.md"
name = "项目周报助手"
description = "将工程项目人员的工作流水账自动整理为结构化项目周报"

[subprojects]
path = ["."]
```

---

## 经验总结

1. **Skill 项目必须显式设置 `deploy.profile.kind = "skill"`**，否则平台会默认按 service 类型处理并要求提供 run 命令。

2. **Skill 项目必需的 `[skill]` 配置字段**：
   - `skill_package`：技能包入口文件（必填）
   - `name`：技能名称（必填）
   - `description`：技能描述（必填）

3. **纯文档类项目没有可执行代码**，不应设置 `deploy.build` 或 `deploy.run`，只需正确配置 `kind=skill` 即可。
