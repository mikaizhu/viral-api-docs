# ViralAPI GitBook Documentation

## 项目概述

这是 ViralAPI 的 GitBook 文档项目，使用 OpenAPI 3.0 规范作为 API Reference 的唯一数据源。

## 技术栈

- **文档平台**：GitBook（非 Mintlify）
- **API 规范**：OpenAPI 3.0.3（YAML 格式）
- **页面格式**：Markdown（`.md`），不使用 MDX
- **API 渲染**：GitBook `{% openapi %}` 块引用本地 YAML 文件

## 项目结构

```
├── README.md                         # 落地页
├── SUMMARY.md                        # GitBook 目录结构（必须维护）
├── getting-started.md                # 快速开始
├── authentication.md                 # 认证说明
├── async-workflow.md                 # 异步任务工作流
├── openapi-nanobanana.yaml           # NanoBanana (gemini-2.5-flash-image) 的 OpenAPI 规范
├── openapi-nanobanana-pro.yaml       # NanoBanana Pro (gemini-3-pro-image-preview) 的 OpenAPI 规范
├── openapi-gemini.yaml               # Gemini Native API 的 OpenAPI 规范
└── api-reference/                    # API 文档页面
    ├── query-task.md
    ├── gemini-generate-content.md
    ├── gemini-stream-generate-content.md
    ├── nanobanana-text-to-image.md
    ├── nanobanana-image-edit.md
    ├── nanobanana-pro-text-to-image.md
    └── nanobanana-pro-image-edit.md
```

## 关键规则

### API 真实结构

- **实际端点只有 2 个**：
  - `POST /v1/task/create` — 创建任务（文生图 + 图像编辑共用）
  - `GET /v1/task/query` — 查询任务状态
- `model` 参数区分模型（`gemini-2.5-flash-image` vs `gemini-3-pro-image-preview`）
- `input.image_urls` 的有无区分文生图与图像编辑
- OpenAPI 中的 `/v1/task/create-image-edit` 是**文档展示用的虚拟路径**，服务端不接受此路径

### OpenAPI 文件约定

- 每个模型一个独立 YAML 文件，避免路径冲突
- `openapi-nanobanana.yaml` 包含：`POST /v1/task/create`、`POST /v1/task/create-image-edit`
- `openapi-nanobanana-pro.yaml` 包含：`POST /v1/task/create`、`POST /v1/task/create-image-edit`、`GET /v1/task/query`
- `openapi-gemini.yaml` 包含：`POST /v1beta/models/{model}:generateContent`、`POST /v1beta/models/{model}:streamGenerateContent`（Gemini 原生 API，服务器为 xingjiabiapi.org）
- 错误响应使用 `$ref: '#/components/responses/...'` 引用，保持 DRY
- 请求体必须有 `example`（单数）以生成 curl 示例

### GitBook OpenAPI 渲染限制（重要）

GitBook 的 OpenAPI 渲染器对 `description` 字段有严格限制：

**不支持的 Markdown 语法**（会被当纯文本显示）：
- `###` 标题
- ` ``` ` 代码块
- `[text](url)` Markdown 链接
- `>` 引用块
- `- item` 列表格式

**支持的格式**：
- 纯文本描述（推荐）
- 纯文本 URL 会被自动识别为可点击超链接

**description 字段写法示例**：

```yaml
# 正确 — 纯文本，简洁
description: 创建异步图像生成任务，返回 task_id 用于后续查询。

# 正确 — 纯 URL 会自动变超链接
description: 使用 Bearer Token 进行认证。获取 API Key 请访问 https://viralapi.ai/api-key

# 错误 — Markdown 链接不渲染
description: 获取 API Key：[ViralAPI 控制台](https://viralapi.ai/api-key)

# 错误 — 标题和列表不渲染
description: |
  ### 任务状态
  - pending — 排队
  - completed — 完成
```

**其他限制**：
- `x-codeSamples` 扩展字段不被 GitBook 支持（不会改变代码示例）
- 代码示例语言选择器顺序固定为 HTTP → cURL → JavaScript → Python，无法通过配置改变
- 代码示例内容由 `requestBody.content.application/json.example` 自动生成

### GitBook 页面约定

API Reference 页面格式固定：

```markdown
# 页面标题

简短描述（1-2 句）

> **Note**: 虚拟路径说明（如适用）

{% openapi src="../openapi-xxx.yaml" path="/v1/..." method="post" %}
{% endopenapi %}
```

- 不要在 `{% openapi %}` 块外手动写参数表格（OpenAPI 会自动渲染）
- 不要在 API 页面添加额外代码示例（由 OpenAPI 的 `example` 字段自动生成）
- 可以在 openapi 块上方添加使用注意事项（如虚拟路径说明）

### 分类规则

- **Task Management**（放在最前面） — 任务查询等通用操作
- **Chat Models** — 文本对话、多模态理解模型（Gemini Native API 等）
- **Image Models** — 所有图像生成/编辑模型（NanoBanana、NanoBanana Pro、未来新增的图像模型）
- 未来如有音频/视频模型，按类型新增分类（Audio Models、Video Models 等）

### SUMMARY.md

- 每次新增或删除页面时必须同步更新 `SUMMARY.md`
- 路径相对于项目根目录
- GitBook 依赖此文件生成导航
- 导航标题不要使用横杠 `—`，直接用空格分隔（如 `NanoBanana Text to Image`）

## 添加新模型/端点的步骤

1. 创建新的 `openapi-<model-name>.yaml`
2. 创建对应的 `api-reference/<model-name>-<operation>.md`（包含 openapi 块）
3. 在 `SUMMARY.md` 中按模型类型分类添加导航条目（Image Models / Text Models 等）
4. 如果是新的任务类型，更新 `getting-started.md` 和 `async-workflow.md` 的示例

## 编写标准

- 英文用于 API 字段名、状态码、技术术语
- 中文用于描述性文字（description 字段保持中文）
- 代码示例使用真实可运行的 curl / Python / Node.js
- 不使用 placeholder 如 `YOUR_VALUE`，用具体示例值
- API Key 用 `YOUR_API_KEY` 占位（这是唯一例外）

## 不要做的事

- 不要创建 `docs.json`（那是 Mintlify 的）
- 不要使用 MDX 组件（`<Card>`、`<AccordionGroup>` 等）
- 不要在 Markdown 中手动粘贴 OpenAPI JSON/YAML 代码块来"展示"接口
- 不要合并多个模型到同一个 OpenAPI 文件（会产生路径冲突）
- 不要在 `{% openapi %}` 块内添加额外内容
- 不要在 OpenAPI description 字段中使用 Markdown 标题、代码块、链接、引用块、列表（不会渲染）
- 不要使用 `x-codeSamples` 扩展（GitBook 不支持）
- 不要在 SUMMARY.md 的导航标题中使用 `—` 横杠

## Git 工作流

- 分支：直接在 `main` 上工作（GitBook 同步 main）
- 提交信息：简洁描述改动内容
- 推送后 GitBook 自动同步更新
