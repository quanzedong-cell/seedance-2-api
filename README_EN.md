# Seedance 2.0 Enterprise API

[中文](README.md) | [API docs](https://zexitongxue.com/docs/video-api.html?utm_source=github&utm_medium=repository&utm_campaign=seedance2_api) | [Live offer](https://quanzedong-cell.github.io/seedance-2-api/en/) | [Contact sales](https://t.me/zexitongxue1)

![Seedance 2.0 video generation showcase](docs/assets/seedance-showcase.jpg)

Seedance 2.0 video generation API access for businesses, studios, and product teams.

> Mainland China pricing is **80% of the applicable Volcengine public list price**. Overseas pricing is **85% of the applicable regional public list price**. Business invoicing and settlement documentation are supported.

## Quick start

List the currently available video models:

```bash
curl 'https://zexitongxue.com/ai-api/models?type=video'
```

Submit a Seedance 2.0 video task:

```bash
curl -X POST 'https://zexitongxue.com/v1/videos' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"model":"doubao-seedance-2-0-720p","prompt":"A blue sports car driving along a coastal road at sunrise","aspect_ratio":"16:9","duration":5}'
```

See the [video generation API documentation](https://zexitongxue.com/docs/video-api.html?utm_source=github&utm_medium=repository&utm_campaign=seedance2_api) for reference inputs, parameters, and task polling.

## Commercial plans

| Region | Pricing basis | Documentation | Best for |
| --- | --- | --- | --- |
| Mainland China | Applicable Volcengine public list price x 0.80 | VAT special invoice | Companies, commerce, studios, developer teams |
| Overseas | Applicable regional public list price x 0.85 | Business settlement documents | Global apps, cross-border teams, international products |

Discounts use the public list price for the selected region, model, and specification on the quotation date. Final pricing, tax treatment, quota, and billing cycle are governed by the confirmed quotation and contract.

## Capabilities

- Text-to-video and image-to-video
- First/last-frame workflows, reference consistency, and multi-shot narratives
- Short drama, advertising, commerce, education, and production workflows
- Common resolution and aspect-ratio options, subject to the live model catalog
- A unified API layer that reduces client changes when channels or models evolve
- Enterprise quotas, usage reporting, technical support, and billing workflows

## Onboarding

1. Share your use case, expected volume, region, and output requirements.
2. Confirm available models, test quota, and technical interface.
3. Confirm quotation, contract, and billing information.
4. Receive production credentials, complete integration testing, and launch.

## Contact

- Website: [zexitongxue.com](https://zexitongxue.com/?utm_source=github&utm_medium=repository&utm_campaign=seedance2_api)
- Discord: [Zexi Seedance 2.0 Community](https://discord.gg/d9d8KNa95R)
- Telegram: [@zexitongxue1](https://t.me/zexitongxue1)

For a faster quote, include your region, estimated monthly volume, text-to-video or image-to-video workflow, and target resolution.

## Trademark notice

This service is provided by Zexi. Seedance, Volcengine, and related trademarks belong to their respective owners. This repository is not an official Volcengine account or repository. References to discounts describe pricing relative to the applicable public list price.

[Commercial terms](TERMS.md)

Copyright 2026 Zexi. All rights reserved.
