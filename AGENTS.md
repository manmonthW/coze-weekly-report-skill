## 项目概述

`coze-weekly-report-skill` 是扣子（Coze）平台的技能项目，用于将工程项目人员的工作流水账自动整理为结构化项目周报。

## 技术栈

- 纯 Markdown/Skill 文档驱动，无代码实现
- 依赖扣子平台运行时解析 SKILL.md

## 目录结构

```
/workspace/projects/
├── .coze                          # 项目配置
├── AGENTS.md                      # Agent 规范文档（本文件）
├── README.md                      # 项目说明
├── SKILL.md                       # 技能核心说明（必选）
├── assets/
│   └── weekly_report_template.md  # 周报输出模板
├── references/
│   └── classification_guide.md   # 工作分类参考标准
└── scripts/                       # 预留（暂无）
```

## 关键入口

- `SKILL.md`：技能核心逻辑，定义 5 步处理流程
- `assets/weekly_report_template.md`：周报输出模板
- `references/classification_guide.md`：工作分类标准

## 运行与预览

- 项目为 Skill 类型，不支持 Web 预览
- 导入扣子平台后，在技能列表中可见"项目周报助手"
- 用户输入工作流水账后触发 5 步处理流程

## 用户偏好与长期约束

- 技能仅适用于工程项目管理场景的周报整理
- 输出必须专业正式，适合直接提交给上级
- 数据和事实不得编造，仅基于用户输入内容整理

## 常见问题和预防

- 技能依赖 SKILL.md 的完整定义，确保导入前该文件存在
- 分类和状态标注需严格按参考标准执行
