# 原理说明：它为什么能省 token

> EN summary: AI coding requests get expensive because every agent sub-call re-sends the growing context. HiRouter sits between your client and your upstream models (you bring the keys) and shrinks what actually travels: folding long context chains, substituting summaries for verbatim history, rewriting watery prompts, reusing connections and failover across your upstreams. What is NOT disclosed here: rewrite rules, fold thresholds, routing weights, auth internals.

## 贵在哪：上下文膨胀

AI 编程请求的成本不在"某一行代码"，而在**上下文越滚越大**：

1. agent 每做一步，都要把之前的结果重新发一遍（不然模型"失忆"）；
2. 子调用（压缩、转写、并行试探）各自灌一遍上下文，水分翻倍；
3. 同样的文件、历史、说明，在一次任务里被发送几十次。

token 按量计费，膨胀的部分全是钱。

## 网关做什么：三件省钱的事

**1. fold 折叠**：超长的上下文链条在网关侧被折叠衔接——模型看到的仍是连贯的任务，但传输的体积大幅缩小。上下文越大，省得越多（实测 132 次请求省 70%–90%）。

**2. 摘要替代原文**：历史消息、压缩产物用摘要替代逐字重发，意思保留，体积只剩零头。

**3. 改写去水**：子调用里常见的客套话、重复指令、格式水词在发出前被改写掉，输出质量不变。

之外还有顺手的事：多上游聚合在一个网关 Key 后面（故障自动切换）、连接复用、安全 SSE 传输、用量按天统计。这些不直接省 token，但让"省"稳定可用。

## 为什么是 BYOK

token 是你自己的上游 Key 在烧，网关不转售 token：

- 你付的只是网关服务本身，token 账单还在你原来的上游账户里，一眼可对；
- 网关没有动力"多发 token"，利益和你一致——发得越少，你越信任它；
- 试用零边际成本，所以免费公测可以不限时，只限量（500 次/天）防刷。

## 不公开什么

实现细节不在本仓讨论：rewrite 规则、fold 触发阈值、上游选路权重、鉴权与 vault 实现。被问到只回答一句话：**效果在试用里可验证**，欢迎拿实测数来 benchmark。
