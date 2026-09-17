# ANingNeo Skills

ANingNeo Skills 是一组面向真实工作场景的开源 AI Agent 能力包。它不追求堆叠提示词，而是把高频任务整理成可安装、可复用、可检查的完整工作流。

每个 Skill 都会说明适用场景、输入输出、外部依赖和执行边界。涉及写入、批量请求或付费服务时，默认先给预览和成本，再由用户决定是否继续。

## 系列目录

| Skill | 解决什么问题 | 状态 |
| --- | --- | --- |
| [`aningneo-knowledge`](skills/aningneo-knowledge/) | 搭建个人 / 团队 / 自媒体系统知识库，接入已有资料，持续检查健康状态 | v0.4.0 |
| [`aningneo-research`](skills/aningneo-research/) | 用用户自己的付费 TikHub API 调研全平台账号、作品、评论、字幕和公开数据，执行前先算请求与费用 | v0.8.0 |
| [`Jiang-local-store`](skills/jiang-local-store/) | 实体门店菜品、菜单、活动海报与图文笔记；内置模板、参考图和图片API脚本 | v0.1.1；真实门店待验收 |

## Jiang-local-store｜实体门店 Skill

[下载单个Skill包](https://github.com/8533502-dev/ANingNeo-skills/releases/latest/download/Jiang-local-store.zip) · [使用说明](skills/jiang-local-store/README.md)

把门店常见的视觉生产任务收进一个 Skill：菜品图、菜单、活动海报、门头预览和推广笔记可以沿用同一套事实校验与素材流程。包内同时提供 Image 2 同步 / 异步脚本、三种 SVG 模板、四份成品示例和风格参考；已有图片也能直接套版并填写准确文字。

图片服务由使用者自行选择、配置和付费，本包不含Key。真实门店素材仍需独立验收；不自动操作外卖后台、发布图文或上线网站。完整图文排版与网站实现还需要宿主提供相应能力。

## aningneo-research｜全平台社媒调研

[仓库目录](skills/aningneo-research/) · [直接下载最新 Skill ZIP](https://github.com/8533502-dev/ANingNeo-skills/releases/latest/download/aningneo-research.zip)

`aningneo-research` 用一套可估价、可抽样验证、可回溯证据的流程，替代零散搜索和手工复制。它先确认接口与单价，再验证少量样本，最后才扩展到批量采集和结构化交付。

它能处理：

- 抖音、小红书、视频号、TikTok、YouTube、B站、快手、微博、Instagram、X、Reddit、知乎等平台；
- 账号资料、作品列表、单条详情、评论、字幕、公开互动和关键词搜索；
- 单篇内容、账号批量、话题调研、评论洞察、逐字稿和结构化表格；
- 端点发现、请求数拆算、费用预估、1–3 条小样本验证、批量采集和脱敏交付。

### 先说清费用

Skill 代码采用 MIT 协议免费开源，但 TikHub 是第三方付费 API：

- 自动采集路线接入第三方 TikHub API，适用于账号、作品、评论、字幕和公开数据的批量调研；
- 这不代表 TikHub 官方合作、授权或商务背书；本项目不自建、不代理、不转售 TikHub，API 服务、收费、稳定性和售后由 TikHub 负责；
- 用户自行注册、充值并配置自己的 `TIKHUB_API_KEY`；
- TikHub 官方当前公开口径是多数接口从 `0.001 USD / 次`起，不同端点通常约 `0.001–0.01 USD / 次`，少数特殊端点更高；
- 新账号当前约有 `0.05 USD` 试用额度，通常可测试约 50 次基础请求；
- 每次批量调研前，Skill 会先拆请求数、查询具体端点价格、给出费用预估，只跑 1–3 条样本，确认后再批量；
- 价格、免费额度和端点会变化，以 [TikHub 价格页](https://tikhub.io/pricing)、[接入指南](https://tikhub.io/getting-started)和具体端点文档为准。

粗略量级：

| 成功请求数 | 按 0.001 USD / 次 | 按 0.01 USD / 次 |
| ---: | ---: | ---: |
| 3 次 | 0.003 USD | 0.03 USD |
| 100 次 | 0.10 USD | 1.00 USD |
| 1,000 次 | 1.00 USD | 10.00 USD |

实际费用还取决于作品列表每页条数、是否逐条抓详情、评论页数、特殊高价端点和第三方 ASR。Skill 不承诺固定价格。

### 安装

适用于支持 [Skills CLI](https://www.npmjs.com/package/skills) 的 Agent 项目：

```bash
npx -y skills@latest add 8533502-dev/ANingNeo-skills \
  --skill aningneo-research \
  -y
```

安装后可以直接说：

```text
调用 aningneo-research，抓这个小红书账号近 100 条作品和每条一页评论。
先查 TikHub 端点和价格，拆算请求数与预计费用，只跑 1–3 条样本。

调用 aningneo-research，调研这 20 个抖音账号。
Skill 免费和 API 付费要分开说明，批量前先给我费用预览。

调用 aningneo-research，处理这份已有的社媒 Excel。
保留原始文件，清洗去重后生成账号、作品、评论洞察和选题。
```

### 配置

默认把自己的 Key 保存在 Skill 内的 `scripts/.tikhub_api_key`，首次保存一次即可：

```bash
python3 .agents/skills/aningneo-research/scripts/tikhub_request.py --configure-local-key
python3 .agents/skills/aningneo-research/scripts/tikhub_request.py --check-config
```

以后每次运行都会重新读取文件，文件优先于环境变量；只要 Skill 目录保留，换会话或清空环境变量都不需要重填。也支持任意路径的 Key 文件、Skill 根目录 `config.json` 中的 `api_key`、环境变量和 macOS Keychain，不限制保存位置。用户已经提供 Key 时，Agent 直接代存，不反复要求配置环境或确认保存方式。

公开代码包不预置真实 Key。迁移自己的 Skill 时带上 Key 文件或包含它的个人完整包；整个云电脑磁盘重置、重装时覆盖或删除了该文件，仍需从自己的备份恢复。

更多配置、估价和请求说明见 [`references/configuration.md`](skills/aningneo-research/references/configuration.md) 与 [`references/paid-api-route.md`](skills/aningneo-research/references/paid-api-route.md)。

## aningneo-knowledge｜可持续运行的 AI 知识库

![aningneo-knowledge：输入、约束、执行、输出、反馈与进化的 Harness 闭环](skills/aningneo-knowledge/assets/aningneo-knowledge-harness.png)

> 资料只有被 AI 稳定找到、正确理解、按规则使用，并能在纠正后更新经验，才真正构成一套可运行的知识系统。

它提供搭建、自媒体模式、资料接入、健康检查、修复和自我纠错六个工作流。

安装：

```bash
npx -y skills@latest add 8533502-dev/ANingNeo-skills \
  --skill aningneo-knowledge \
  -y
```

## 开源标准

- 来自真实、重复发生的工作；
- 付费或外部依赖提前说清；
- 默认先预览，写入或批量扣费前确认范围；
- 原始事实、外部观点、用户判断和 Agent 提炼明确分层；
- 有清晰边界、自动化测试和可验证结果；
- 不把第三方 API、免费额度或私有连接器说成自建能力。

## 维护者

ANingNeo（GitHub: [@8533502-dev](https://github.com/8533502-dev)）

## 来源与许可

本仓库基于 [aslanyushengjiang-coder/shengjiang-skills](https://github.com/aslanyushengjiang-coder/shengjiang-skills) 按 MIT License 二次开发，保留上游 Git 历史、许可证及第三方声明。ANingNeo 版本调整了品牌标识和对外说明，原有使用流程与功能边界保持不变。

来源说明见 [NOTICE](NOTICE.md)，许可证见 [MIT](LICENSE)。
