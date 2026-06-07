---
title: "群友实测｜Codex 真的赶上 Claude Code 了吗"
date: 2026-06-06 16:03:00 +0800
permalink: /review/2026/06/06/codex/
categories:
  - Reviews
tags:
  - codex
  - claude-code
  - gpt-5-5
  - agentic-coding
  - usage-limit
  - openai
layout: post
toc: true
license: "CC BY-NC 4.0"
---

> ※ 本栏目素材来自鸭哥创建的 AI 从业者微信群，群友均以匿名昵称出现。完整每日日报开源在 GitHub：<https://louyu2015.github.io/AI-chatgroup-daily/>
>
> 文章由作者和 Claude Opus 4.8 、DeepSeek V4 联合撰写。题图由 GPT Image 2 生成。

> 我曾以为，写代码是 AI 时代最高质量、最能体现模型能力的任务，相信 Anthropic 已经在代码领域形成飞轮。尤其是 mythos 发布时那种铺天盖地、原子弹爆炸般的眩晕感，让我对 Opus 充满期待。但过去几个月，从 Opus 4.6、4.7 到 4.8，实际体验不仅缺乏亮点，甚至有下滑感。相反，OpenAI 的 GPT-5.5 在 CodeX 上有一种重生感：复杂任务更稳定，结果更扎实，验证也更系统。相比 Opus 那种聪明但不够踏实的感觉，以及 Gemini 3.5 Flash 与 Benchmark 严重割裂的表现，我现在会更无脑选择 CodeX。

<span class="mention">@沉稳的仓鼠</span> 用这一段话把不少人心里那点说不清的感受挑明了。

我自己一两个月前用尽 Claude Code 的限额时用过 Codex，当时就觉得它的能力快赶上 Claude Code 了，只是后来没继续追踪新模型。这次回群里一看，搬家已经成了气氛。不是一两个人，是一群最铁杆的 Claude 重度用户正集体倒戈。我翻完聊天记录、查完评测、看了 OpenAI 的报道，发现这事比"Codex 更强了"复杂得多。

## 信心的位移：从"无脑选 Claude Code"到"无脑选 Codex"

<span class="mention">@沉稳的仓鼠</span> 那段话砸在群里的那天，没人反驳。这个群从来不缺技术细节辩论，但这一次，更多人开始补充自己的版本。<span class="mention">@直率的鹦鹉</span> 说得直白，他甚至撇开"额度重置"（Codex 每隔一阵就把你用掉的额度重新发放一次，相当于周期性免单，英文叫 reset，后面细说）这个加分项，直接下判断：

> 不重置也是codex耐用 而且openai不开倒车 还有gpt pro可以用

"不开倒车"三个字戳到了很多人。<span class="mention">@洒脱的鸳鸯</span> 接了一句，描述的是那种细水长流的不安感——不是你哪天突然发现模型变差了，而是每次新版本发布前的那种隐隐预感：

> 我体感是 claude 每次新模型出来之前，旧模型就开始性能下降，然后新模型出来感觉哇进步了一截

你可以接受一款产品有瓶颈，但你大概不能接受不了它"先偷偷变差、再假装进步"。

现在，群友已经逐渐对 Codex 产生了信任。信任到什么程度？轮子哥（GacUI 的作者「vczh」）直接把整个 monorepo 的 CI 脚本甩给 Codex，让它大修，自己忙别的去了：

> 直接把整个monorepo CI 的ps1文件交给codex，让他大修一番。但是C++编译又很慢，于是codex从昨天下午五点跑到现在十几个小时了，居然还在跑CI。感觉我的笔记本快要冒烟了。

最后整整跑了 18 个小时，他自己都说"太难为codex了"。这种"扔给它、人走开"的用法，正在变成群里的日常。

还有 <span class="mention">@幽默的犀牛</span>，更早之前就提了一嘴体感上的差别：

> 最近用codex，感觉特别听话，不像claude code喜欢跳步骤

看起来全群在用脚投票，Codex 的赢面好像已经大到不需要讨论。"听话""耐用""不重置也耐用""重生感"——这些词堆在一起，听起来就是一曲胜利的颂歌。但真的是 Codex 全面变强了吗？

![](/assets/img/review/2026-06-06-codex-cover.png)

## 评测里的真相：没人"全面超越"谁

但真去翻评测，"全面超越"这个说法立刻就站不住了。

先从最硬核的评测看起。在刷屏最多的编码测试 SWE-bench Verified（让模型修真实 GitHub issue 的标准测试）上，GPT-5.5 拿了 88.7%，Claude Opus 4.7 是 87.6%——略微领先，但远没到碾压的程度。换个更难、更贴近实战的 SWE-bench Pro（多文件、长链路的真实工程任务），Claude 直接反超，Opus 4.7 是 64.3%、GPT 只有 58.6%；而 Opus 4.8 把这个数字进一步推到了 69.2%。也就是说，越是难的真实任务，Claude 的优势越明显。

再看终端和 DevOps 场景的 Terminal-Bench 2.0，GPT-5.5 确实大幅领先（82.7% vs 69.4%），这是 Codex 的一个明确强项。但盲评代码质量——不看是谁写的、只看代码干净程度——在[一项 100+ 小时的实战对比](https://composio.dev/content/claude-code-vs-openai-codex)里，Claude 输出被评为更干净的占了 67%，Codex 只有 25%。

圈内人的看法也没有一边倒。[Reddit 上一个 500 多位开发者的偏好投票](https://dev.to/_46ea277e677b888e0cd13/claude-code-vs-codex-2026-what-500-reddit-developers-really-think-31pb)里，Codex 拿了 65.3%，加权点赞后甚至拉到 79.9% 对 Claude 的 20.1%；但有个细节，Claude Code 的讨论评论量是 Codex 的 4 倍——社区更活跃，口碑也更分化。独立开发者圈的风向标 Simon Willison 把日常主力从 Claude Code 换去了 Codex；可 AI 评论博主 [Zvi Mowshowitz](https://thezvi.substack.com/p/claude-code-codex-and-agentic-coding-f54) 又不肯下定论，他说 Codex 确实达到了"逃逸速度"，但"Claude Code 目前仍领先，还在每周修 60 多个可靠性问题"。最有意思的是[科技媒体 XDA 那位记者](https://www.xda-developers.com/ditched-claude-code-for-codex/)，切到 Codex 整整一周，最后还是回到了 Claude Code 的怀抱。

不过成本这块，Codex 是实打实地占的便宜。按 API 标价，GPT-5.5-Codex 是每百万 token $1.75/$14（输入/输出），低于 Claude Opus 4.8 的 $5/$25。但更要命的是 **token 效率**：在相同的编码任务上，Claude Code 消耗的 token 大约是 Codex 的 4 倍；换个口径，GPT-5.5 干同样的活输出 token 比 Claude Opus 4.7 少约 72%。同一件事，Codex 烧掉的量级明显更小。落到最实际的 $20 档订阅，Codex Plus 一个 5 小时窗口大概能发 30–150+ 条消息，Claude Code Pro 大约只能承受 10–45 条，跑长任务的人很容易撞墙（[Codex vs Claude Code 谁更省钱](https://www.hongkiat.com/blog/codex-vs-claude-code-2026/)）。Codex 甚至还有一个免费档位，反观 Anthropic 还尝试把 Claude Code 从 20 美元的订阅档位移出，直到看见社区的激烈反对才作罢。

所以真相不是"谁全面赢了"，是 **Codex 追上了，并在成本和某些任务上占了便宜，但 Claude 在代码质量和复杂任务上守住了阵地。**

## 关于 GPT Pro，有个容易混淆的地方

顺带说说 GPT Pro，因为群里有过一轮相关讨论。<span class="mention">@开朗的企鹅</span> 提了一个我觉得挺有代表性的观点：

> GPT-Pro一项就足以使GPT成为Must，而claude还没有哪个"必须"的feature

<span class="mention">@风趣的海豚</span> 也补了一句：

> 而且能力上gpt pro是断档第一的，但是因为太贵被各种测试都选择性忽略了 跑一遍pro的测试费用够吧（把）所有其他模型的测试跑一遍

这个判断有它的道理，GPT Pro 确实是个狠角色。不过我自己查下来，发现里头有两个地方容易混淆，顺手说清楚。

第一，**它其实跟我们这篇聊的 Codex 不是一回事。** GPT-5.5 Pro 不是一个独立模型，是标准 GPT-5.5 加上额外的并行算力（test-time compute），只在 $200 的 ChatGPT Pro 套餐里有。而 [OpenAI 官方的 Codex 模型列表](https://developers.openai.com/codex/models)里，只有标准 gpt-5.5，没有 Pro。换句话说，你拿 Codex 写代码时，跑的是标准版——那个"断档第一"的 Pro，根本上不了你的编程现场。

第二，"断档第一"放到全局看，可能也高估了它。Pro 主要在联网检索（BrowseComp 90.1%）和最难的数学题上明显领先，但硬推理反而落后——在 HLE（Humanity's Last Exam，一套号称"人类最后考卷"的超难综合题）不带工具的版本上，Pro 约 43.1%，Claude Opus 4.7 是 46.9%；GPQA（研究生级科学题）、SWE-bench Pro 也都是 Claude 或 Gemini 领先（[benchmark 对比](https://benchlm.ai/compare/gpt-5-5-vs-gpt-5-5-pro)）。它是真贵：API 每百万 token $30/$180（输入/输出），是标准版 $5/$30 的六倍。"太贵没人系统测"确实是实情，只是"没人系统测"不等于"测了就断档第一"。

还有个反直觉的细节。[科技媒体 The Decoder](https://the-decoder.com/gpt-5-5-tops-benchmarks-but-still-hallucinates-frequently-at-a-20-percent-higher-api-cost/) 测出，**Pro 版在"反忽悠"测试上反而比标准版更差**——多出来的算力，有一部分用去给烂 prompt 找理由、顺着你说，而不是顶回去。这跟 Opus 4.8 的"模型越训越谄媚"的讨论几乎是同一个剧本。

所以与其说 GPT Pro 是"非它不可的大招"，不如说它是一种"我既然付了 200 刀，关键时刻总有个顶配能掏出来"的安心感。但日常写代码这件事，它其实搭不上手。

## Codex 和 Claude Code 越长越像

既然评测没分出绝对高下，群友到底在选什么？我本以为是 Codex 有什么 Claude Code 给不了的独门绝技。但把两边的家底摆出来才发现：**Codex 当年那些惊艳的招式，在这大半年里让 Claude Code 几乎全追平了。**

云端跑任务是 Codex 2025 年 5 月推出时就打出的招牌——任务扔进云端虚拟机自己跑，人可以离开电脑。Claude Code 慢了大半年，去年十月才补上"Claude Code on the web"，同样给你一个 4 vCPU、16G 内存的云端虚拟机，还能用 --remote 或 --teleport 在本地和云端之间把正在干的活搬来搬去。

手机遥控，也是 Codex 先有的（它本来就活在 ChatGPT 里，掏出手机就能派活、看进度）。Claude Code 今年二月才出 Remote Control，手机网页上盯着 agent 干活、批准命令、审查 diff、收取推送通知。

后台异步、多 agent 并行，Claude Code 也在今年五月补齐了——claude --bg、claude agents 面板，还有 Dynamic Workflows，能在后台同时跑一堆任务。

甚至连 Codex 最让人上瘾的"改完自动跑测试验证"这招，Claude Code 也能做到——用 PostToolUse 或 Stop hook，配几条规则就能让 agent 改完代码自动跑 lint、跑类型检查、跑单元测试。

不是 Claude Code 一开始就有，而是 Codex 趟过的路，它这半年一步一步追了上来。等尘埃落定，两边的能力清单几乎完全重叠了。

真正的差别就剩两件事，而且分处两个时间点。

第一件在**动工之前——接到一个含糊的需求，默认先开干，还是默认先问清楚。** 给同样一句模棱两可的指令，Codex 往往二话不说就做起来、边做边猜你到底要什么；Claude Code 则倾向先反问你几句，把需求对齐了再动笔。

可同一个行为，有人嫌它墨迹，有人正是图它先问清楚。那位 XDA 记者就属于后者：他用了一周 Codex，最后还是回到 Claude Code，理由正是 Claude 先问需求再动手，首版代码反而更少返工。说到底这不是谁更强，而是你想要一个闷头开干的执行者，还是一个先对齐再下笔的合作者——纯看脾气。

第二件在**干活当中——默认自己拍板，还是默认每步请示你。** Codex 的沙箱默认开着，改完代码、要跑测试跑命令，它基本自己来：你只要在 AGENTS.md 里写一句"跑完测试再算完成"，它就自己跑、跑挂了自己修，不会一条命令一确认。Claude Code 默认更谨慎，跑命令前往往先问你一句"可以吗"；想让它一样放手，得自己去配 hook、调权限。差的不是能力，是"默认信任你到什么程度"。

这恰好点中了周报中 <span class="mention">@沉稳的仓鼠</span> 提的那一套"Beta 哲学"。这俩词借自炒股：beta 是你什么都不用做、买个大盘指数就能拿到的市场平均收益；alpha 是你费心研究、想跑赢大盘的那部分超额收益——可现实是，绝大多数人折腾半天，反而跑输了大盘。他把这套逻辑搬到了 AI 工具上：

> 比如搞 AI 也是的，在我看来，所谓的 Beta 就是你只用最先进的工具，比如说 Codex 或者 Claude Code，任何魔改、研究 prompt，然后搞 MCP 或者搞这些东西都属于 Alpha，也就是你试图比 Claude Code 和 CodeX 生成更多的生产力，但是实际上绝大多数人……在这个"魔改"的过程中，其实做的还不如 Codex 或者 Claude Code 的升级带来的效果更好，所以这属于既浪费了时间，又降低了收益。

他要的就是少折腾、躺在升级上。Codex 默认就偏"放手自动干"，省去大量调权限、配 hook 的功夫，正合胃口。这不是能力高低的问题，而是产品团队默认替用户做了多少决策。

**群友看似在选"更先进的工具"，其实是在选"更合自己脾气的默认行为"。** 能力已经高度趋同，真正的迁移推力是那些看似非核心的体验质地：不用操心配置、不用频繁对话、提示词扔出去就能自己完成任务。当两个工具站在同一条能力线上，谁更省心，谁就留住了用户。

## 这哪是额度重置，这是新一轮满减券

省心是一回事。但把这群人真正拽过去的，还有更实在的一条：钱。

群里慢慢冒出一个有意思的现象：比起争 Codex 和 Claude Code 谁更强，大家更常念叨的，反倒是 Codex 的额度什么时候重置——那语气，活像守着外卖 App 等满减券。<span class="mention">@80-HD</span> 的体感很直接：

> codex太耐用了 感觉干同样的活，cc用了一半，codex才削掉一层皮

<span class="mention">@今天群内信息量极大</span> 干脆给 Codex 起了个外号——"传奇耐烧王"。可耐用归耐用，人心不足：<span class="mention">@我要成为灵能高手</span> 报出"一个星期reset三次"的频率后，群里立刻炸出一种又好笑又辛酸的患得患失——有人提议搞个"Codex 会不会重置"的投票去对冲心情，有人到周中额度见底，只能眼巴巴等额度重置。<span class="mention">@认真的剑鱼</span> 一句话说穿了所有人的纠结：

> +1，reset猝不及防，有额度的时候reset难过，没额度的时候不reset也难过

当有人认真发问、200 刀的预算到底是 Codex 还是 Claude Code 更耐用时，<span class="mention">@洒脱的鸳鸯</span> 的回答几乎成了全群共识：

> 考虑到 codex 经常重置，我觉得 codex 更耐用吧

因为不断重置，所以更耐用。但你得琢磨一下：重置到底是什么性质？

鸭哥自己就点破了。当有人感叹 Codex 耐烧，他补了一句清醒的注脚：

> 不过codex确实是例外，因为还在双倍促销。claude code双倍促销的时候也是爽的。 GLM之前补贴促销的时候（没有周限额，15刀一个月）也是爽的

我们在上周周报里就算过这笔账——现在享受的 AI 价格不是真实的，是 VC 在出钱。额度重置和加倍赠送，就是新一轮的"外卖满减"和"打车红包"。群友 <span class="mention">@乐观的灰熊</span> 也直接把额度重置和 IPO 挂上了钩：

> 我猜测是想在上市之前培养大家对量的渴望冲一波销售业绩

翻一翻 [OpenAI 的财务预测](https://finance.yahoo.com/news/openais-own-forecast-predicts-14-150445813.html)，这个猜测很难反驳。2026 年预计净亏 140 亿美元，差不多是 2025 年的三倍。每收 1 美元，就得烧掉 1.69 美元。GPT-5 毛利大约 48%，远低于成熟 SaaS 产品 70% 以上的水平。分析师说可能要到 2029 年才开始盈利。Codex 的额度重置也不是随机发善心——有[完整追踪](https://knightli.com/en/2026/05/17/codex-usage-limit-reset-history/)显示，每次用户增长达成一个里程碑（比如周活突破 300 万），额度就跟着重置或加倍。科技行业分析机构 Forrester 的分析师 Ken Parmelee 把这类编程工具称为 "the new gateway drug"——新的入门毒品：先用低价编程工具把你钩住，再让你用它们其他的产品。

另一边，Anthropic 的企业端已经接近盈利，而且在主动收紧消费端的额度。这差别很能说明问题：对 OpenAI 来说，消费端的血亏是 IPO 前的战略刚需，需要增长故事撑估值；Anthropic 没有这股压力，不必硬撑这场补贴战。

所以话说回来，**Codex 的"重生感"，一部分是模型进步，更大一部分是 VC 的钱在替你续命。** 最妙的是，当初提醒大家 $200 月卡真实 API 成本高达八千美元的 <span class="mention">@沉稳的仓鼠</span>，如今也乐呵呵地蹲守额度重置。虽然满减券总有一天会退潮，但只要今天还能三块钱点一顿饭，明天的事明天再说。

## 那到底该怎么选

抛开情绪，这轮"搬家"过程中可以总结出几条能直接上手的经验。

**别再纠结"谁更强"，按脾气和任务选工具。** 能力已经趋同到这个程度，再用 benchmark 那两三个点的差距来选工具，是刻舟求剑。真正影响你每天体验的，是默认行为跟你合不合拍：要的是长程自动化、扔个 prompt 就走的"后台苦力"，Codex 更适合你；习惯边想边改、在意首版代码质量，Claude Code 依然是更好的那个。这不是谁先进谁落后，是两种工作风格。

**便宜是补贴价，别按这个成本结构来规划工作流。** VC 的钱在替你买单，但它不会一直买下去。外卖大战结束的时候，满减券一张张消失，有人提前算清账继续吃，有人等补贴退潮才发现月预算翻了一倍。Codex 现在的"耐用"是 IPO 前的战略动作，退潮一定会来。该用就用，但别把你的开发流水线，搭在一个靠烧钱维持的价格幻觉上。

**买得起就都留着，按任务分工。** 群里 <span class="mention">@淡定的喜鹊</span> 提过一个"版本号分工法"，我觉得很实用——需要稳定推进的复杂任务交给一种模型，需要快速出结果、自动验证的扔给另一个模型。这次群里的讨论也印证了，很多资深工程师会同时用多种 AI 编程工具，不是"投靠"，而是"各取所需"。

**信任是真实资产，烧掉了很难重建。** 最有代表性的是四月那次 Claude 定价风波：Anthropic 悄悄把 Claude Code 从 20 美元的 Pro 套餐挪出，改成 100 美元以上的套餐才能用，等于一次 5 倍涨价，事先没有任何公告。被网友扒出来后，Anthropic 几小时内又改了回去，解释说"只是对 2% 新用户做的小测试"。前面说 Simon Willison 把主力搬去了 Codex，导火索正是这件事——他给这次操作起了个英文说法叫 [trust bonfire](https://simonwillison.net/2026/Apr/22/claude-code-confusion/)（信任篝火）：省下的钱有限，烧掉的信任难补。这次这么多 Claude 重度用户开始搬家，不是因为 Codex 在 benchmark 上全方位碾压，而是一次次"旧模型性能滑坡""额度收紧""涨价又改口"把人一点点推走的。Anthropic 这一轮最该警惕的，不是哪条 benchmark 落后了，是把最早相信它的那批人的耐心一点点烧光了。

## 总结

回过头看群里的搬家画面，这事其实比一开始想的简单。

我一两个月前用过 Codex，当时就觉得它快赶上 Claude Code 了，只是后来没追新模型。这次翻完所有人的理由，外加扒完评测和 OpenAI 的财报，发现 Codex 确实追上来了——但追上的不是"全面超越"，是**能力拉平之后，用户在比的早就不再是模型本身了。**

三条线收束起来就是：能力趋同，所以比的不是谁更聪明，是谁更合脾气、更省心；那份"省心"是被精心设计过的默认行为，不是独门秘技；而那份让人用起来很爽的"便宜"，是一个年亏 140 亿美元的公司，为 IPO 铺路而烧出来的。

**当一群最懂行的人开始搬家，他们投的不仅仅是"谁更聪明"的票，而是"谁更省心、谁更便宜"的票。而便宜，是有人在你买单。**
