# HiRouter · BYOK token-saving gateway, measured −70%

![token spend −70.8%](https://img.shields.io/badge/token_spend-%E2%88%9270.8%25-brightgreen) ![status](https://img.shields.io/badge/status-public_beta-blue) ![works with](https://img.shields.io/badge/works_with-Claude_Code_%7C_Codex_%7C_opencode-purple) ![free tier](https://img.shields.io/badge/free_tier-500_req%2Fday-orange)

> **Measured on 170 real Codex requests: 23.18M tokens in → 6.77M sent upstream (−70.8%)**; 132 of them saved 70%–90%, larger contexts save more. Method: client-side estimate, not provider billing — full notes in [docs/BENCHMARK.md](docs/BENCHMARK.md).

> **Also measured on 184 opencode chat rounds: ~23.57M estimated → ~10.16M sent upstream (−56.9%)**, zero failures, zero resets. Same estimate caveat — see [docs/BENCHMARK.md](docs/BENCHMARK.md#opencode-184-rounds-sep-16).

> 中文版：[README.zh-CN.md](README.zh-CN.md) · Free public beta · Try it: https://hirouter.swancat.com · Product page + FAQ: https://swancat.com/hirouter/
>
> **Docs only in this repo. Server source is not open-sourced.**

HiRouter is a cloud gateway for AI coding agents: you bring your own upstream keys (BYOK), the gateway handles routing, rewriting, compression, caching and stable delivery. Same requests in, fewer tokens out, thinner bills.

## 3 steps to run

1. **Register + verify**: https://hirouter.swancat.com, sign up with email, verify, get your first gateway key (`hrsk_…`).
2. **Plug into your client**: with CC Switch, add a custom provider, Base URL `https://api-hirouter.swancat.com/v1`, key = your gateway key. Claude Code / Codex / opencode all work — client-specific rows in [docs/USAGE.md](docs/USAGE.md).
3. **Use as usual**: rewrite and fold apply automatically at the gateway; usage is counted daily in the console.

Free public beta: 500 requests/day, 60/minute, no credit card.

## Why it saves

One line: **fold + summarize — tokens that don't need to go upstream never do**. Repetitive context inside agent sub-calls gets folded or summarized at the gateway; only the necessary parts reach the upstream model. How it works (no implementation details) in [docs/HOW-IT-WORKS.md](docs/HOW-IT-WORKS.md).

## Security & privacy

- **BYOK, tenant-isolated**: your upstream keys live in your own account config and are only used to forward *your* requests upstream. Gateway keys, passwords and console sessions are stored as hashes and can't be read back.
- **No prompt bodies on disk**: server-side packet capture is force-disabled. Per-tenant log files keep usage/diagnostic metadata only (token counts, models, timings) — never prompt or completion text.
- **Your data stays yours**: usage, logs and config APIs are scoped to your own session; one tenant cannot read another's. Rotate or revoke gateway keys anytime in the console.

## Feedback

- Q&A / ideas → [Discussions](https://github.com/etherled/hirouter/discussions)
- Bugs / feature requests → [GitHub Issues](https://github.com/etherled/hirouter/issues) (use the templates; public threads become community assets)
- Enterprise / investment / large accounts → [CONTACT.md](CONTACT.md)

## License

Docs in this repo are [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/) (attribution, non-commercial, no derivatives), see [LICENSE](LICENSE). Server source is not open-sourced.
