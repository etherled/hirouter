# 测试报告：170 次请求，原始 2318 万 → 实发 677 万

> EN summary: 170 real requests through Codex compaction (gpt-5.6-sol): ~23.18M tokens in, ~6.77M sent upstream (−70.8%). 132 requests saved 70%–90%; savings grow with context size. Method: client-side estimate, not upstream billing. Raw per-request logs are not published.

## 数据

- 窗口：单机日志 2026-09-13，170 次请求（Codex 压缩场景，模型 gpt-5.6-sol）。
- 原始约 2318 万 token，实发约 677 万，**省 70.8%**。
- 分布：132 次省 70%–90%；压缩率随上下文增大而提高，短请求省得少、长上下文省得多。

## 口径说明（必读）

1. **客户端估算**：数字按客户端侧收发量统计，不是上游账单口径。不同客户端、不同任务类型会有浮动。
2. **场景相关**：Codex 压缩是上下文膨胀最严重的场景之一，省得最多；普通短问答省得少。首页写"实测省 70%"指该实测窗口，不是放之四海的承诺。
3. **可复现方向**：同客户端、同类长上下文任务，对比直连与走网关的收发量级即可验证。欢迎拿你的实测来 Issues 对线。
4. **逐条日志不贴**：原始请求日志含用户任务隐私，只公布聚合数。

## 结论一句话

上下文越大省得越多；长上下文 agent 任务走网关，出去的 token 按实测少约七成（客户端口径）。

## opencode 184 轮（2026-09-16 晚） {#opencode-184-rounds-sep-16}

> EN summary: 184 opencode chat rounds in one session (no resets): ~23.57M estimated → ~10.16M sent upstream (−56.9%), all ok. Same client-side-estimate caveat; output tokens (~80K) excluded. Full report with charts: [opencode-184-report.pdf](opencode-184-report.pdf).

- 窗口：单机版网关日志，同一 opencode 会话连续 184 轮（北京时间 20:54:34 → 23:52:00，无 reset，成功率 100%）。
- 估算约 2357 万 token，实发约 1016 万，**省约 1341 万（56.9%）**；输出约 8 万 token 未计（假设压缩不改变输出）。
- 压缩：累计应用 707 批次、替换 47,012 条次（含跨轮重复计数）；176/184 轮生效，尾部稳定在每轮 7 批次/479 条；首轮只有预约不冻结。
- 缓存：命中率中位数 97.1%；31 轮低于 50%（含 1 轮 0.0%），miss 的轮次由压缩顶上——压缩保下限，缓存保上限。
- 口径：与 Codex 组同样是客户端估算（请求 bytes/4）vs 上游 usage 实报；单会话、单模型实测，不外推为普遍承诺。逐轮日志、抓包、截图三方交叉验证过程见完整报告 PDF。
