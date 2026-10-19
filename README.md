# ANingNeo Skills · 自媒体与企业知识工作流

> 把内容生产中反复出现的环节——找资料、做调研、拆爆款、管知识——交给 AI 按规则稳定完成。

ANingNeo Skills 是一组开源 AI Agent 能力包，核心服务自媒体创作：搭建内容知识库、调研全平台账号与作品、深度拆解短视频。知识库 Skill 另带企业三库模式，可直接用于公司资料整理，尤其适合文旅、研学和营地类机构。

[下载最新版本](https://github.com/8533502-dev/ANingNeo-skills/releases/latest) · [浏览全部 Skills](skills/)

## Skill 一览

| Skill | 用来做什么 | 版本 |
| --- | --- | --- |
| [`aningneo-knowledge`](skills/aningneo-knowledge/) | 搭建企业三库（产品 / 客户 / 技能），也可建通用或自媒体知识库 | v0.5.0 · 新增企业模式 |
| [`aningneo-research`](skills/aningneo-research/) | 用你自己的 TikHub API 调研各平台账号、作品、评论、字幕与公开数据，开跑前先算请求数和费用 | v0.8.0 |
| [`aningneo-viral-breakdown`](skills/aningneo-viral-breakdown/) | 拆解别人的爆款或复盘自己的视频，交付观看价值、逐段分析、评论、分镜和逐字稿 | v1.0.0 |
| [`ANingNeo Local Store`](skills/aningneo-local-store/) | 为实体门店制作菜品图、菜单、活动海报、门头预览和图文笔记 | v0.1.1 |

推荐的组合方式：`aningneo-research` 负责采集素材 → `aningneo-viral-breakdown` 负责深挖单条作品 → `aningneo-knowledge` 负责把结论、规则和经验沉淀下来。

## 仓库约定

- 这里只放可复用的部分：Skill 说明、必要脚本和通用模板。
- 每个 Skill 都要写清输入、执行边界、交付物和验收方式。
- 具体某条视频的完整演示项目另建仓库；视频素材、录屏、客户资料、真实工作区和运行产物都留在各自项目里，不整包上传到这里。

---

## aningneo-knowledge

### 企业三库：产品库 · 客户库 · 技能库

选择 `enterprise` 模式即可为公司搭三库：

- **产品库**：线路、酒店、景点、报价、公众号文章等对外产品资料；
- **客户库**：客户名单、客户档案、导出的聊天记录；
- **技能库**：团队 SOP、检查清单和常用模板。

Agent 会先了解公司业务和现有资料，原文件原地不动，通过索引接入三库；完成后列出每个库收录了什么、还缺什么。

三库下共预置 24 类文旅行业子库，覆盖产品研发、供应采购、团期交付、交易服务与方法沉淀，可按实际资料逐项启用。模板同时附带任务导航、执行前提、结果核验、中断续办和反馈更新规则。详见 [企业三库模式](skills/aningneo-knowledge/references/enterprise-mode.md) 与 [安装和完整提示词](skills/aningneo-knowledge/README.md)。

### 不只是存文件，而是让 AI 能持续干活

![aningneo-knowledge：输入、约束、执行、输出、反馈与进化的 Harness 闭环](skills/aningneo-knowledge/assets/aningneo-knowledge-harness.png)

> 文件堆在一起还不算知识库。AI 能稳定读到你是谁、手上在做什么、业务规则和原始事实，做完能被检查、被纠正、把经验升级进规则——这才是一套能运转的知识库。

内置六个工作流：搭建、自媒体模式、资料接入、健康检查、修复、自我纠错。

做自媒体选 `creator` 模式，会建立账号定位、对标调研、用户洞察、素材、选题、稿件、发布和复盘等入口，知识库保存在你自己的内容工作区。Claude Code 用户可按需启用 `assets/optional/claude-code/CLAUDE.md`。

```bash
npx -y skills@latest add 8533502-dev/ANingNeo-skills \
  --skill aningneo-knowledge \
  -y
```

```text
调用 aningneo-knowledge，用 creator 模式在我指定的目录搭自媒体知识库。
先看已有资料和目录结构，再补齐定位、对标、素材、选题、稿件、发布和复盘入口。
每条视频的完整项目单独建仓库，知识库里只留链接。
```

[详细说明](skills/aningneo-knowledge/README.md) · [下载 ZIP](https://github.com/8533502-dev/ANingNeo-skills/releases/latest/download/aningneo-knowledge.zip)

---

## aningneo-viral-breakdown

针对一条指定短视频，分析它的观看价值、开头设计、逐段推进、评论反馈和分镜，保留带时间戳的逐字稿，最后提炼成可迁移到你账号的方法。手上已有素材可直接分析；需要在线采集时搭配 `aningneo-research`。

```bash
npx -y skills@latest add 8533502-dev/ANingNeo-skills \
  --skill aningneo-viral-breakdown \
  -y
```

```text
调用 aningneo-viral-breakdown，拆解这条视频：[链接或本地文件]。
保留带时间戳的逐字稿，最后给出适合我账号的方法。
```

[详细说明](skills/aningneo-viral-breakdown/README.md) · [下载 ZIP](https://github.com/8533502-dev/ANingNeo-skills/releases/latest/download/aningneo-viral-breakdown.zip)

---

## aningneo-research

API 优先的全平台社媒调研 Skill。

**覆盖平台**：抖音、小红书、视频号、快手、微博、B站、知乎、TikTok、YouTube、Instagram、X、Reddit 等。

**能抓什么**：账号资料、作品列表、单条详情、评论、字幕、公开互动数据、关键词搜索结果。

**能做什么**：单条内容分析、账号批量采集、话题调研、评论洞察、逐字稿和结构化表格。全流程为：找端点 → 拆请求数 → 估费用 → 1–3 条小样本 → 批量采集 → 脱敏交付。

### 费用说明

Skill 代码按 MIT 协议免费开源；自动采集用的 TikHub 是第三方付费 API，两者要分开看：

- 本项目选用 TikHub 是因为它在账号、作品、评论、字幕等批量调研上覆盖面广、好用；这不代表 TikHub 官方合作或背书，本项目也不自建、代理或转售它的接口，服务、计费和售后由 TikHub 负责；
- 你需要自己注册、充值，并配置自己的 `TIKHUB_API_KEY`；
- 按官方目前公开的价格，多数接口每次 `0.001 USD` 起，常见端点在 `0.001–0.01 USD / 次`，个别特殊端点更贵；
- 新账号目前有约 `0.05 USD` 试用额度，大致够测 50 次基础请求；
- 每次批量前，Skill 都会先算请求数、查具体端点单价、给出费用预估，只跑 1–3 条样本，等你确认再批量；
- 价格、额度和端点都可能调整，以 [TikHub 价格页](https://tikhub.io/pricing)、[接入指南](https://tikhub.io/getting-started) 和端点文档为准。

费用量级参考：

| 成功请求数 | 0.001 USD / 次 | 0.01 USD / 次 |
| ---: | ---: | ---: |
| 3 | 0.003 USD | 0.03 USD |
| 100 | 0.10 USD | 1.00 USD |
| 1,000 | 1.00 USD | 10.00 USD |

最终花费还取决于每页条数、是否逐条抓详情、评论翻几页、是否用到高价端点和第三方语音转写，Skill 不承诺固定价格。

### 安装与调用

```bash
npx -y skills@latest add 8533502-dev/ANingNeo-skills \
  --skill aningneo-research \
  -y
```

```text
调用 aningneo-research，抓这个小红书账号最近 100 条作品，每条带一页评论。
先查端点和单价，算出请求数和预计费用，只跑 1–3 条样本。

调用 aningneo-research，调研这 20 个抖音账号。
把 Skill 免费和 API 付费分开讲清，批量前先给我看费用预估。

调用 aningneo-research，处理这份现成的社媒 Excel。
原文件保留，清洗去重后输出账号、作品、评论洞察和选题建议。
```

### 配置 Key

Key 默认存在 Skill 目录下的 `scripts/.tikhub_api_key`，保存一次即可长期使用：

```bash
python3 .agents/skills/aningneo-research/scripts/tikhub_request.py --configure-local-key
python3 .agents/skills/aningneo-research/scripts/tikhub_request.py --check-config
```

每次运行都会重新读这个文件，且它的优先级高于环境变量；只要 Skill 目录还在，换会话、清空环境变量都不用重填。也可以改用任意路径的 Key 文件、Skill 根目录 `config.json` 里的 `api_key`、环境变量或 macOS Keychain。你已经把 Key 给了 Agent 时，它会直接帮你保存，不会反复让你配置。

公开仓库和 Release 包里不含任何真实 Key。迁移时记得带上自己的 Key 文件；如果磁盘重置或重装覆盖了它，需要从自己的备份恢复。

更多说明见 [`configuration.md`](skills/aningneo-research/references/configuration.md) 和 [`paid-api-route.md`](skills/aningneo-research/references/paid-api-route.md)。

[详细说明](skills/aningneo-research/) · [下载 ZIP](https://github.com/8533502-dev/ANingNeo-skills/releases/latest/download/aningneo-research.zip)

---

## ANingNeo Local Store

面向实体门店的视觉内容入口：先核对商品、价格、活动等门店事实，再出图和写文案，可制作菜品图、菜单价目表、活动海报、门头与店内物料预览，以及小红书、抖音、朋友圈图文。图片服务由使用者自选、自配、自付，Skill 不含 API Key，也不会自动操作外卖后台或发布内容。

[使用说明](skills/aningneo-local-store/README.md) · [下载 ZIP](https://github.com/8533502-dev/ANingNeo-skills/releases/latest/download/aningneo-local-store.zip)

---

## 收录标准

- 源自真实、反复出现的工作场景；
- 付费项和外部依赖事先讲清楚；
- 默认先预览，写入文件或批量扣费前先确认范围；
- 原始事实、外部观点、用户判断、Agent 提炼分层记录；
- 边界清晰，有自动化测试和可验证的结果；
- 不把第三方 API、免费额度或私有连接器包装成自有能力。

## 维护者

ANingNeo（GitHub：[@8533502-dev](https://github.com/8533502-dev)）

版本和下载包统一发布在 [GitHub Releases](https://github.com/8533502-dev/ANingNeo-skills/releases)。

## License

[MIT](LICENSE)
