# Seedance 2.0 企业级 API

[English](README_EN.md) | [API 文档](https://zexitongxue.com/docs/video-api.html?utm_source=github&utm_medium=repository&utm_campaign=seedance2_api) | [在线方案](https://quanzedong-cell.github.io/seedance-2-api/) | [咨询接入](https://zexitongxue.com/?utm_source=github&utm_medium=repository&utm_campaign=seedance2_api)

![Seedance 2.0 视频生成展示](docs/assets/seedance-showcase.jpg)

面向企业、工作室与开发团队的 Seedance 2.0 视频生成 API 接入服务。

> 中国大陆按火山引擎官方公开价的 **7 折**，海外按对应官方公开价的 **8 折**。支持按合同开具增值税专用发票，不另收开票服务费。

## 快速开始

你需要一个本站 API 密钥。不要把密钥放进 URL、分享链接或前端公开代码里，请求时用请求头携带：

```bash
export SEEDANCE_API_KEY="你的 API 密钥"
```

### 1. 查询当前可用的视频模型

```bash
curl 'https://zexitongxue.com/ai-api/models?type=video'
```

先从实时目录确认模型名、价格和上架状态，再提交任务。不要用另一个模型的默认时长、分辨率或素材上限来推断当前模型。

### 2. 提交一个文生视频任务

V1 创建接口为 `POST /v1/videos`。`/v1/video/generations` 和 `/v1/videos/generations` 为兼容路径。

```bash
curl -X POST 'https://zexitongxue.com/v1/videos' \
  -H "Authorization: Bearer $SEEDANCE_API_KEY" \
  -H 'Content-Type: application/json' \
  -d '{"model":"doubao-seedance-2-0-720p","prompt":"清晨海边公路，一辆蓝色跑车沿海岸平稳行驶","aspect_ratio":"16:9","duration":5}'
```

V1 必须提供文字提示词 `prompt`。仅提供参考素材而不提供文字，当前返回 `400`。

保存创建响应中的任务 `id`，后续只查询原任务。

### 3. 轮询查询任务状态

```bash
curl 'https://zexitongxue.com/v1/videos/TASK_ID' \
  -H "Authorization: Bearer $SEEDANCE_API_KEY"
```

建议每 5–10 秒轮询一次。遇到 `queued` / `running` / `in_progress` 继续等待；`failed` / `cancelled` 时保留本站任务编号核查。

V1 成功状态是 `completed`。成功后读取响应中的本站媒体地址。

官方格式的创建接口为 `POST /api/v3/contents/generations/tasks`，使用 `model` 和 `content`。查询用：

```bash
curl 'https://zexitongxue.com/api/v3/contents/generations/tasks/TASK_ID' \
  -H "Authorization: Bearer $SEEDANCE_API_KEY"
```

官方格式成功状态是 `succeeded`，成功结果位于 `content.video_url`。此入口当前支持创建及按任务编号查询；未开放任务列表、删除或取消。

### 4. 下载成片

```bash
curl 'https://zexitongxue.com/v1/videos/TASK_ID/content' \
  -H "Authorization: Bearer $SEEDANCE_API_KEY" \
  -o result.mp4
```

创建、查询和媒体读取须使用同一有权访问任务的账号。私人任务的本站媒体地址须保留完整路径和查询串；拿到地址不等于取得访问权限。生成后及时保存，源文件过期或被删除后将无法下载。

### 图生视频：用参考图

普通图片、首帧、尾帧、视频、音频是不同角色。官方格式使用 `image_url`、`video_url`、`audio_url` 类型，嵌套对象包含 `url`；对应角色为 `reference_image`、`first_frame`、`last_frame`、`reference_video`、`reference_audio`。首尾帧计入图片数量，具体组合要求按所选型号。

按该型号支持的输入协议，使用服务端可读取的 HTTPS 文件地址，或本站上传返回的素材链接。上传响应中的 `assetRef` / `asset_ref` 是受当前账号权限保护的本站链接，可原样填入，不要解析或重建链接，也不要只截取查询串中的某一段。

示例（官方格式，图片地址请替换成你自己有权使用的可读取链接）：

```json
{
  "model": "doubao-seedance-2-0-720p",
  "content": [
    {"type": "text", "text": "保持场景与镜头运动，将外套改为蓝色。"},
    {"type": "image_url", "role": "reference_image", "image_url": {"url": "https://example.com/reference.jpg"}}
  ],
  "duration": 5,
  "resolution": "720p",
  "ratio": "16:9",
  "generate_audio": true
}
```

`generate_audio` 须为布尔值，`false` 不等于省略；`seed: 0` 是有效值，但 seed 是否开放须按所选入口。默认值以该型号目录为准。

### 常见问题

| 现象 | 含义 / 做法 |
| --- | --- |
| `400` | 参数不受支持，或缺少文字提示词，或用了未开放的高级参数。先核对所选型号支持的参数。 |
| `401` | 密钥无效。检查 `Authorization: Bearer` 是否正确，密钥是否过期或换了账号。 |
| `403` / `404` | 无权读取或任务不存在。确认创建、查询、下载用的是同一账号。 |
| `502` 或暂时无媒体 | 继续查询原任务，勿立即重复创建。 |
| 任务成功但下载不到 | 检查媒体地址是否完整、会话是否过期，回到有权访问的原任务页面重新打开。 |

完整参数、参考素材和任务查询方式见[视频生成 API 文档](https://zexitongxue.com/docs/video-api.html?utm_source=github&utm_medium=repository&utm_campaign=seedance2_api)。

## 商务方案

| 方案 | 价格基准 | 票据 | 适用客户 |
| --- | --- | --- | --- |
| 中国大陆 | 火山引擎官方公开价 x 0.70 | 增值税专用发票 | 企业、电商、内容机构、开发团队 |
| 海外 | 对应海外官方公开价 x 0.80 | 企业结算资料 | 海外应用、跨境团队、国际化产品 |

折扣以报价当日对应地区、模型和规格的官方公开价格为基准。最终价格、税率、额度与结算周期以双方确认的商务报价和合同为准。

## 支持能力

- 文生视频与图生视频
- 首尾帧、参考图一致性与多镜头叙事
- 人物短剧、商业广告、电商、教育和内容生产工作流
- 常用清晰度与画幅规格，具体以接入时可用模型列表为准
- 统一 API 接入，减少渠道和模型变更对客户端的影响
- 企业额度、用量统计、技术支持与发票流程

## 接入流程

1. 提交业务场景、预计用量、地区和所需规格。
2. 确认可用模型、测试额度与技术接口。
3. 完成商务报价、合同与开票资料确认。
4. 获取生产凭证，完成联调后上线。

## 联系

- 官网：[zexitongxue.com](https://zexitongxue.com/?utm_source=github&utm_medium=repository&utm_campaign=seedance2_api)
- Discord 社区：[泽西 Seedance 2.0 创作社区](https://discord.gg/d9d8KNa95R)
- Telegram：[@zexitongxue1](https://t.me/zexitongxue1)

咨询时请注明地区、预计月用量、文生视频或图生视频需求，以及目标分辨率，便于快速报价。

## 品牌声明

本服务由泽西同学提供。Seedance、火山引擎及相关商标归各自权利人所有；本项目不代表火山引擎官方账号或官方仓库。页面中的“官方价折扣”是相对于对应官方公开价格的计价说明。

[商务说明](TERMS.md)

Copyright 2026 泽西同学. All rights reserved.
