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
├── .gitbook/assets/                  # OpenAPI 规范文件目录
│   ├── openapi-nanobanana.yaml       # NanoBanana (gemini-2.5-flash-image)
│   ├── openapi-nanobanana-pro.yaml   # NanoBanana Pro (gemini-3-pro-image-preview)
│   ├── openapi-gemini.yaml           # Gemini Native API
│   ├── openapi-veo.yaml              # Veo 视频生成
│   └── openapi-tongyi-wanxiang.yaml  # 通义万相视频生成
└── api-reference/                    # API 文档页面
    ├── query-task.md
    ├── gemini-native-api.md
    ├── nanobanana-text-to-image.md
    ├── nanobanana-image-edit.md
    ├── nanobanana-pro-text-to-image.md
    ├── nanobanana-pro-image-edit.md
    ├── veo-video-generation.md
    ├── wan22-text-to-video.md
    ├── wan22-image-to-video.md
    ├── wan25-text-to-video.md
    └── wan25-image-to-video.md
```

## 关键规则

### API 真实结构

- **实际端点只有 2 个**：
  - `POST /v1/task/create` — 创建任务（文生图 + 图像编辑共用）
  - `GET /v1/task/query` — 查询任务状态
- `model` 参数区分模型（`gemini-2.5-flash-image` vs `gemini-3-pro-image-preview`）
- `input.image_urls` 的有无区分文生图与图像编辑
- OpenAPI 中的 `/v1/task/create-image-edit` 是**文档展示用的虚拟路径**，服务端不接受此路径

**通义万相视频生成 API**：
- 实际端点：`POST /v1/task/create`（与图像模型共用）
- 通过 `model` 参数区分：`wan2.2-t2v`、`wan2.2-i2v`、`wan2.5-t2v`、`wan2.5-i2v`
- 通过 `task_type: "video"` 区分视频任务
- 文生视频（T2V）：无需 `input.img_url`，使用 `input.size` 参数
- 图生视频（I2V）：必需 `input.img_url`，使用 `input.resolution` 参数

### OpenAPI 文件约定

- 每个模型一个独立 YAML 文件，避免路径冲突
- `openapi-nanobanana.yaml` 包含：`POST /v1/task/create`、`POST /v1/task/create-image-edit`
- `openapi-nanobanana-pro.yaml` 包含：`POST /v1/task/create`、`POST /v1/task/create-image-edit`、`GET /v1/task/query`
- `openapi-gemini.yaml` 包含：`POST /v1beta/models/{model}:generateContent`、`POST /v1beta/models/{model}:streamGenerateContent`（Gemini 原生 API）
- `openapi-veo.yaml` 包含：`POST /v1/videos`、`GET /v1/videos/{task_id}`（Veo 视频生成）
- `openapi-tongyi-wanxiang.yaml` 包含：`POST /v1/task/create`（通义万相视频生成，通过 `model` 参数区分 wan2.2-t2v/i2v、wan2.5-t2v/i2v）
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

## 英文翻译指导原则

### 翻译策略

- **分支管理**：
  - `main` 分支：保留中文版本（本地）
  - `english` 分支：英文版本（推送到 GitBook 线上）

- **翻译范围**：
  - 所有 Markdown 文档（`.md` 文件）
  - 所有 OpenAPI YAML 文件中的 `description`、`summary`、`title` 等描述性字段
  - 保持代码示例、URL、技术术语不变

### 写作风格参考

参考 [OpenRouter API Documentation](https://openrouter.ai/docs) 的专业风格：

**核心原则**：
1. **清晰直接**（Clear & Direct）
   - 避免行话和复杂术语
   - 使用对话式语言
   - 每个概念用 1-2 句话描述

2. **问题-解决方案框架**（Problem-Solution Framework）
   - 先解释为什么需要这个功能
   - 然后说明如何使用

3. **祈使语言**（Imperative Language）
   - 使用动词开头："Generate videos", "Create task", "Returns a list"
   - 避免被动语态

4. **功能性描述**（Functional Description）
   - 避免营销语言
   - 专注于功能和技术细节
   - 保持客观和准确

5. **简洁性**（Conciseness）
   - 去除冗余词汇
   - 直接表达核心信息
   - 避免过度解释

### 翻译示例

**标题翻译**：
- ✅ "Wan2.2 Text to Video" （简洁、描述性）
- ❌ "Wan2.2 Text-to-Video Generation API" （过于冗长）

**描述翻译**：
- ✅ "Generate videos from text descriptions using the `wan2.2-t2v-plus` model."
- ❌ "This API allows you to generate high-quality videos from your text descriptions by utilizing the powerful wan2.2-t2v-plus model."

**参数描述**：
- ✅ "Video duration (seconds)"
- ❌ "The duration of the video in seconds"

**注意事项**：
- ✅ "Duration Limit: wan2.2 models generate fixed 5-second videos, cannot be modified"
- ❌ "Please note that the duration limit for wan2.2 models is fixed at 5 seconds and this cannot be modified"

### 常用术语对照表

| 中文 | 英文 |
|------|------|
| 文生视频 | Text-to-Video (T2V) |
| 图生视频 | Image-to-Video (I2V) |
| 提示词 | Prompt |
| 反向提示词 | Negative prompt |
| 智能改写 | Prompt enhancement |
| 时长 | Duration |
| 分辨率 | Resolution |
| 处理时间 | Processing time |
| 视频有效期 | Video expiration |
| 任务创建成功 | Task created successfully |
| 请求参数错误 | Invalid request parameters |
| 认证失败 | Authentication failed |
| 余额不足 | Insufficient account balance |
| 服务器内部错误 | Internal server error |

### 翻译检查清单

翻译完成后，检查以下项目：

- [ ] 所有标题使用简洁的名词短语
- [ ] 描述使用祈使语言或陈述句
- [ ] 避免使用"please", "you can", "it is possible to"等冗余表达
- [ ] 技术术语保持一致性
- [ ] 代码示例和URL保持不变
- [ ] 保持原文的段落结构和格式
