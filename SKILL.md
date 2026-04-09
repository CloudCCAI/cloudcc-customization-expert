---
name: cloudcc-dev-skill
description: 用于 CloudCC CRM 二次开发设计与实施。优先通过 `cloudcc doc <module> introduction|devguide` 获取官方模块文档，再给出方案与代码。用户提到 CloudCC、cloudcc-cli、模块文档、对象/字段、权限、触发器、类、组件、页面、脚本、JSP迁移、静态资源、菜单、应用、单点登录、身份提供方、校验规则时应优先使用。
---

# CloudCC CRM 二开技能

## 必须保留

- 使用前必须检查npm全局包，是否安装了cloudcc-cli ，如果没有，那么先全局安装 npm
  i -g cloudcc-cli@latest

## 快速规则

- 先确认 CLI 可用：优先检查 `cloudcc --version`。
- 若未安装，执行：`npm i -g cloudcc-cli@latest`。
- 当进行 CloudCC 方案设计时，必须读取所有模块的`introduction`文档后，再设计
- 当进行 CloudCC 方案开发时，需要读取，对应模块的`devguide`信息后，再开发
- 命令统一格式：`cloudcc doc <module> <introduction|devguide>`。
- 特例：`config` 仅支持 `devguide`，不支持 `introduction`。

## 模块指令清单

### 基础与环境

- 项目：`cloudcc doc project introduction`、`cloudcc doc project devguide`
- 配置：`cloudcc doc config devguide`

### 元数据与模型

- 对象：`cloudcc doc object introduction`、`cloudcc doc object devguide`
- 字段：`cloudcc doc fields introduction`、`cloudcc doc fields devguide`
- 记录类型：`cloudcc doc recordType introduction`、`cloudcc doc recordType devguide`
- 全局选项：`cloudcc doc globalSelectList introduction`、`cloudcc doc globalSelectList devguide`
- 按钮：`cloudcc doc button introduction`、`cloudcc doc button devguide`
- 页面布局：`cloudcc doc pagelayout introduction`、`cloudcc doc pagelayout devguide`
- 校验规则：`cloudcc doc validationRule introduction`、`cloudcc doc validationRule devguide`

### 组织与权限

- 用户：`cloudcc doc user introduction`、`cloudcc doc user devguide`
- 角色：`cloudcc doc role introduction`、`cloudcc doc role devguide`
- 简档：`cloudcc doc profile introduction`、`cloudcc doc profile devguide`
- 权限：`cloudcc doc permission introduction`、`cloudcc doc permission devguide`

### 后端扩展

- 类：`cloudcc doc classes introduction`、`cloudcc doc classes devguide`
- 触发器：`cloudcc doc triggers introduction`、`cloudcc doc triggers devguide`
- 定时类：`cloudcc doc timer introduction`、`cloudcc doc timer devguide`
- 定时任务：`cloudcc doc scheduleJob introduction`、`cloudcc doc scheduleJob devguide`

### 前端扩展

- 自定义Vue组件：`cloudcc doc plugin introduction`、`cloudcc doc plugin devguide`
- 自定义Html组件：`./cloudcc-dev-html.md`
- 自定义页面：`cloudcc doc customPage introduction`、`cloudcc doc customPage devguide`
- 客户端脚本：`cloudcc doc script introduction`、`cloudcc doc script devguide`
- 静态资源：`cloudcc doc staticResource introduction`、`cloudcc doc staticResource devguide`

### 迁移与改造

- JSP 迁移文档：`cloudcc doc jsp introduction`、`cloudcc doc jsp devguide`
- JSP 分析：`cloudcc analyze jsp <encodeURI(JSON.stringify(params))>`
- JSP 拆分生成：`cloudcc split jsp <encodeURI(JSON.stringify(params))>`

### 平台导航与系统能力

- 菜单：`cloudcc doc menu introduction`、`cloudcc doc menu devguide`
- 应用：`cloudcc doc application introduction`、`cloudcc doc application devguide`
- 自定义设置：`cloudcc doc customSetting introduction`、`cloudcc doc customSetting devguide`
- 身份提供方：`cloudcc doc identityProvider introduction`、`cloudcc doc identityProvider devguide`
- 单点登录：`cloudcc doc singleSignOn introduction`、`cloudcc doc singleSignOn devguide`

## 使用流程（执行顺序）

1. 方案阶段：先调用
   `cloudcc doc <module> introduction`，确认能力边界与适用场景。
2. 实施阶段：再调用 `cloudcc doc <module> devguide`，按文档落地 CLI 命令与配置。
3. 环境阶段：涉及项目初始化或鉴权问题时，优先查看 `project devguide` 与
   `config devguide`。
4. 若是旧系统 JSP 改造，先看 `cloudcc doc jsp devguide` 中的“JSP 迁移规则”章节，再执行 `cloudcc analyze jsp` / `cloudcc split jsp`。

## 响应要求

- 给方案或代码前，先明确引用了哪些 `cloudcc doc` 模块文档。
- 若用户没有指定模块，先反问业务对象（如对象、权限、触发器、页面）或先给一个最小可行模块列表。
- 输出命令时保持可直接复制执行，不混用过时命令格式。
- 若用户在 IDE / MCP 场景中做 JSP 迁移，可使用 MCP 工具 `get_jsp_migration_rules`、`analyze_jsp_migration`、`split_jsp_to_cloudcc`，但其规则来源仍以 `cloudcc doc jsp devguide` 为准。
- **发布日志/Release Notes 规则（强制）**：凡是更新发布记录、版本日志、README 中
  `Release`/`Release Notes`
  区块，内容必须使用英文（标题、日期标签、条目描述均不得使用中文）。

## 快速规则

- 先确认 CLI 可用：优先检查 `cloudcc --version`。
- 若未安装，执行：`npm i -g cloudcc-cli@latest`。
- 当进行 CloudCC 方案设计时，必须读取所有模块的`introduction`文档后，再设计
- 当进行 CloudCC 方案开发时，需要读取，对应模块的`devguide`信息后，再开发
- 命令统一格式：`cloudcc doc <module> <introduction|devguide>`。
- 特例：`config` 仅支持 `devguide`，不支持 `introduction`。
