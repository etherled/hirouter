# HiRouter · BYOK token-saving gateway, measured −70%

> 中文版：[README.md](README.md) · Free public beta · Try it: https://hirouter.swancat.com
>
> **Docs only in this repo. Server source is not open-sourced.**

HiRouter is a cloud gateway for AI coding agents: you bring your own upstream keys (BYOK), the gateway handles routing, rewriting, compression, caching and stable delivery. Same requests in, fewer tokens out, thinner bills.

## Measured numbers (read this first)

170 real requests (Codex compaction, gpt-5.6-sol): ~23.18M tokens in, ~6.77M sent upstream, **−70.8%**; 132 of them saved 70%–90%, larger contexts save more.

Method: client-side estimate, not provider billing. Full notes in [docs/BENCHMARK.md](docs/BENCHMARK.md).

## 3 steps to run

1. **Register + verify**: https://hirouter.swancat.com, sign up with email, verify, get your first gateway key (`hrsk_…`).
2. **Plug into your client**: with CC Switch, add a custom provider, Base URL `https://api-hirouter.swancat.com/v1`, key = your gateway key. Details in [docs/USAGE.md](docs/USAGE.md).
3. **Use as usual**: rewrite and fold apply automatically at the gateway; usage is counted daily in the console.

Free public beta: 500 requests/day, 60/minute, no credit card.

## Why it saves

One line: **fold + summarize — tokens that don't need to go upstream never do**. Repetitive context inside agent sub-calls gets folded or summarized at the gateway; only the necessary parts reach the upstream model. How it works (no implementation details) in [docs/HOW-IT-WORKS.md](docs/HOW-IT-WORKS.md).

## Feedback

- Bugs / feature requests → [GitHub Issues](https://github.com/etherled/hirouter/issues) (use the templates; public threads become community assets)
- Enterprise / investment / large accounts → [CONTACT.md](CONTACT.md)

## License

Docs in this repo are [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/) (attribution, non-commercial, no derivatives), see [LICENSE](LICENSE). Server source is not open-sourced.
