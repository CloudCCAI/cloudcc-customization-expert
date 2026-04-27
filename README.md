# cloudcc-customization-expert

用于 CloudCC CRM 二次开发的技能仓库，目标是让 AI/开发者在设计与实施阶段优先走官方文档与标准 CLI 流程，减少错误方案和无效命令。

## 项目用途

- 统一 CloudCC 二开的执行规范（先 `introduction`，后 `devguide`）。
- 提供模块级文档命令清单，覆盖对象、字段、权限、触发器、页面、OpenAPI 等场景。
- 约束常见高风险操作（例如：先检查 CLI、JSP 迁移前先读规则、发布日志使用英文）。

## 环境要求

- Node.js 16+（建议使用 LTS）
- npm 8+
- 全局安装 `cloudcc-cli`

安装命令：

```bash
npm i -g cloudcc-cli@latest
```

验证命令：

```bash
cloudcc --version
```

## 仓库结构

```text
.
├── SKILL.md      # 技能主文档（规则、模块命令、执行流程、最佳实践）
└── config.json   # 版本与发布日期
```

## 快速开始

1. 安装并验证 `cloudcc-cli`。
2. 进入本仓库，阅读 `SKILL.md`。
3. 按场景执行文档查询：
   - 方案阶段：`cloudcc doc <module> introduction`
   - 开发阶段：`cloudcc doc <module> devguide`
4. 按文档结果输出可执行命令与配置，不混用过时指令。

## 常用命令示例

```bash
# 查看项目与配置说明
cloudcc doc project introduction
cloudcc doc project devguide
cloudcc doc config devguide

# OpenAPI（对象 CRUD 常用）
cloudcc doc openapi introduction
cloudcc doc openapi devguide

# 发布日志
cloudcc changelog
cloudcc changelog --all
```

## 推荐工作流

- 先确认模块边界：`cloudcc doc <module> introduction`
- 再拿到落地命令：`cloudcc doc <module> devguide`
- 涉及对象数据增删改查时，优先走 OpenAPI 标准命令链路