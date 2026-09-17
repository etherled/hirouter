# HiRouter · BYOK 省 token 网关，实测省 70%

![token spend −70.8%](https://img.shields.io/badge/token_spend-%E2%88%9270.8%25-brightgreen) ![status](https://img.shields.io/badge/status-public_beta-blue) ![works with](https://img.shields.io/badge/works_with-Claude_Code_%7C_Codex_%7C_opencode-purple) ![free tier](https://img.shields.io/badge/free_tier-500_req%2Fday-orange)

> **170 次 Codex 真实请求实测：原始 2318 万 token → 实发 677 万（省 70.8%）**；其中 132 次省 70%–90%，上下文越大省得越多。口径：客户端估算，非上游账单——完整说明见 [docs/BENCHMARK.md](docs/BENCHMARK.md)。

> **另有 184 轮 opencode 聊天实测：估算约 2357 万 → 实发约 1016 万（省 56.9%）**，零失败、零重置。同样是客户端估算口径——见 [docs/BENCHMARK.md](docs/BENCHMARK.md#opencode-184-rounds-sep-16)。

> 英文版：[README.md](README.md) · 免费公测 · 试用：https://hirouter.swancat.com · 产品页 + FAQ：https://swancat.com/hirouter/
>
> **本仓仅含说明文档，服务端源码暂不开源。**

HiRouter 是给 AI 编程 agent 用的云端网关：你自带上游 Key（BYOK），网关做路由、改写、压缩、缓存与稳定传输。同一套接入，出去的 token 变少，账单变薄。

## 3 步上手

1. **注册验证**：https://hirouter.swancat.com，用邮箱注册，验证后拿第一把网关 Key（`hrsk_` 开头）。
2. **填进客户端**：以 CC Switch 为例，加自定义供应商，Base URL 填 `https://api-hirouter.swancat.com/v1`，Key 填网关 Key。Claude Code / Codex / opencode 都支持，分客户端配置见 [docs/USAGE.md](docs/USAGE.md)。
3. **照常用**：改写与折叠在网关侧自动生效，用量在控制台按天统计。

免费公测：500 次/天，60 次/分钟，无需绑卡。

## 它为什么能省

一句话：**fold 折叠 + 摘要，该省的 token 不发给上游**。agent 子调用里的大量重复上下文在网关侧被折叠或摘要替代，只把必要的发给上游模型。原理说明（不涉及实现细节）见 [docs/HOW-IT-WORKS.md](docs/HOW-IT-WORKS.md)。

## 安全与隐私

- **BYOK + 租户隔离**：上游 Key 只存在你自己名下的租户配置里，仅用于转发*你自己*的请求。网关 Key、登录口令、控制台 session 只存哈希，原文不可读回。
- **请求正文不落盘**：服务端抓包在 SaaS 侧被强制关闭。租户日志文件里只有用量与诊断元数据（token 数、模型、耗时），没有 prompt 与返回正文。
- **数据只归你**：用量、日志、配置接口都按你自己的 session 鉴权隔离，一个租户读不到另一个的。网关 Key 随时可在控制台轮换或吊销。

## 反馈

- 提问交流 / 功能建议 → [Discussions 讨论区](https://github.com/etherled/hirouter/discussions)
- Bug / 功能建议 → [GitHub Issues](https://github.com/etherled/hirouter/issues)（按模板填，公开讨论沉淀成社区资产）
- 企业合作 / 投资 / 大客户定制 → [CONTACT.md](CONTACT.md)

## 许可

本仓文档采用 [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)（署名-非商业-禁止演绎），见 [LICENSE](LICENSE)。服务端源码暂不开源。
