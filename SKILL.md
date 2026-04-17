---
name: cloudcc-dev-skill
description: 用于 CloudCC CRM 二次开发设计与实施。优先通过 `cloudcc doc <module> introduction|devguide` 获取官方模块文档，再给出方案与代码。用户提到 CloudCC、cloudcc-cli、OpenAPI、模块文档、对象/字段、权限、触发器、类、组件、页面、脚本、JSP 迁移、静态资源、菜单、应用、单点登录、身份提供方、校验规则、查重过滤器（Dupe Catcher）、重复/去重、定时作业、定时类、timer、scheduleJob、共享规则时应优先使用。
---

# CloudCC CRM 二开技能

## 必须保留

- 使用前必须检查npm全局包，是否安装了cloudcc-cli ，如果没有，那么先全局安装 npm
  i -g cloudcc-cli@latest

## 快速规则

- 先确认 CLI 可用：优先检查 `cloudcc --version`。
- 需要查看发布日志时，使用：`cloudcc changelog`（当前版本）、`cloudcc changelog <version>`（指定版本）、`cloudcc changelog --all`（全部版本）。
- 若未安装，执行：`npm i -g cloudcc-cli@latest`。
- 当进行 CloudCC
  方案设计时，必须读取所有模块的`introduction`文档后，再设计，命令统一格式：`cloudcc doc <module> introduction`
- 当进行 CloudCC
  方案开发时，需要读取，对应模块的`devguide`信息后，再开发，命令统一格式：`cloudcc doc <module> devguide`
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
- 验证规则：`cloudcc doc validationRule introduction`、`cloudcc doc validationRule devguide`
- 查重过滤器（dupeCatcher）：`cloudcc doc dupeCatcher introduction`、`cloudcc doc dupeCatcher devguide`
- 共享规则（sharingRule）：`cloudcc doc sharingRule introduction`、`cloudcc doc sharingRule devguide`

### 组织与权限

- 用户：`cloudcc doc user introduction`、`cloudcc doc user devguide`
- 角色：`cloudcc doc role introduction`、`cloudcc doc role devguide`
- 简档：`cloudcc doc profile introduction`、`cloudcc doc profile devguide`
- 权限：`cloudcc doc permission introduction`、`cloudcc doc permission devguide`

### 后端扩展

- 类：`cloudcc doc classes introduction`、`cloudcc doc classes devguide`
- 触发器：`cloudcc doc triggers introduction`、`cloudcc doc triggers devguide`
- 定时类：`cloudcc doc timer introduction`、`cloudcc doc timer devguide`
- 定时作业：`cloudcc doc scheduleJob introduction`、`cloudcc doc scheduleJob devguide`

### 前端扩展

- 自定义Vue组件：`cloudcc doc plugin introduction`、`cloudcc doc plugin devguide`
- 自定义HTML组件：`cloudcc doc html introduction`、`cloudcc doc html devguide`
- Site开发规范：`cloudcc doc site introduction`、`cloudcc doc site devguide`
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
- 对象视图：`cloudcc doc view introduction`、`cloudcc doc view devguide`
- 自定义设置：`cloudcc doc customSetting introduction`、`cloudcc doc customSetting devguide`
- 身份提供方：`cloudcc doc identityProvider introduction`、`cloudcc doc identityProvider devguide`
- 单点登录：`cloudcc doc singleSignOn introduction`、`cloudcc doc singleSignOn devguide`
- OpenAPI：`cloudcc doc openapi introduction`、`cloudcc doc openapi devguide`

**调用doc，获取introduction和devguide时，用完就要从上下文中清除，不要占用上下文，只用一次，下次使用再次查询**

## 使用流程（执行顺序）

1. 方案阶段：先调用
   `cloudcc doc <module> introduction`，确认能力边界与适用场景。
2. 实施阶段：再调用 `cloudcc doc <module> devguide`，按文档落地 CLI 命令与配置。
3. 环境阶段：涉及项目初始化或鉴权问题时，优先查看 `project devguide` 与
   `config devguide`。
4. 若是旧系统 JSP 改造，先看 `cloudcc doc jsp devguide` 中的“JSP
   迁移规则”章节，再执行 `cloudcc analyze jsp` / `cloudcc split jsp`。
5. 若用户要做对象数据增删改查，优先查看 `cloudcc doc openapi introduction` 与
   `cloudcc doc openapi devguide`，默认优先使用带权限接口。

## 响应要求

- 给方案或代码前，先明确引用了哪些 `cloudcc doc` 模块文档。
- 若用户没有指定模块，先反问业务对象（如对象、权限、触发器、页面）或先给一个最小可行模块列表。
- 输出命令时保持可直接复制执行，不混用过时命令格式。
- 涉及 OpenAPI CRUD 时，优先给出
  `cloudcc query|pageQuery|create|update|delete|upsert openapi`
  命令；默认说明其直接读取 `getPackageJson(projectPath)` 解析出的 `apiSvc` 与
  `accessToken`，不走登录接口。
- 若用户在 IDE / MCP 场景中做 JSP 迁移，可使用 MCP 工具
  `get_jsp_migration_rules`、`analyze_jsp_migration`、`split_jsp_to_cloudcc`，但其规则来源仍以
  `cloudcc doc jsp devguide` 为准。
- **发布日志/Release Notes 规则（强制）**：凡是更新发布记录、版本日志、README 中
  `Release`/`Release Notes`
  区块，内容必须使用英文（标题、日期标签、条目描述均不得使用中文）。

## 最佳实践

### CCDK 与自定义类

**CCDK** 是运行在自定义页面、自定义 HTML、自定义 Site 等前端场景中的
**JavaScript 库**，作用有两类：

1. **前端 ↔ 自定义类**：通过 `$CCDK.CCCommon.post`
   调用已发布的自定义类方法（方法签名、参数类型需与 Java 侧一致）。
2. **前端 ↔ CRM 壳能力**：通过 `$CCDK.CCPage` 等与 CRM
   前端交互（如打开列表页、视图等）。

#### 示例一：自定义类（Java）

```java
package classes.MyClass;

import com.cloudcc.core.*;
// @SOURCE_CONTENT_START
public class MyClass {
    private UserInfo userInfo;
    private CCService cs;

    public MyClass(UserInfo userInfo) {
        this(userInfo, new CCService(userInfo));
    }

    public MyClass(UserInfo userInfo, CCService cs) {
        this.userInfo = userInfo;
        this.cs = cs;
    }

    public void execute(String name, String address) {
        // 业务逻辑
    }
}
// @SOURCE_CONTENT_END
```

#### 示例二：前端调用（与上面 `execute(String, String)` 对应）

上述脚本可写在自定义 Vue 组件、自定义 HTML、Site 等支持 CCDK 的页面中。

```javascript
const className = "MyClass";
const methodName = "execute";
const params = [
  { argType: "java.lang.String", argValue: "hello" },
  { argType: "java.lang.String", argValue: "world" },
];
const config = { timeout: 60000 }; // 毫秒，例如 60 秒

$CCDK.CCCommon.post(className, methodName, params, config)
  .then((res) => {
    const data = res.data;
    console.log(data);
  })
  .catch((error) => {
    console.log(error);
  });
```

#### 示例三：与CRM系统交互，打开列表视图页

```javascript
const pageId = $CCDK.CCPage.openListPage({
  menuId: "aaa-223",
  prefix: "001",
  viewId: "ace1111",
  layoutType: "list",
});
```
