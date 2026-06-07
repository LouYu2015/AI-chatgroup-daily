---
title: "群友实测｜被全群骂了一个月的 DeepSeek V4，为什么舍不得卸载"
date: 2026-06-06 16:01:00 +0800
permalink: /review/2026/06/06/deepseek-v4/
categories:
  - Reviews
tags:
  - deepseek-v4
  - harness
  - tool-calling
  - instruction-following
  - ai-writing
  - model-economics
layout: post
toc: true
license: "CC BY-NC 4.0"
---

> ※ 本栏目素材来自鸭哥创建的 AI 从业者微信群，群友均以匿名昵称出现。完整每日日报开源在 GitHub：<https://louyu2015.github.io/AI-chatgroup-daily/>
>
> 文章由作者和 Claude Opus 4.8、DeepSeek V4 联合撰写。题图由 GPT Image 2 生成。

群里 <span class="mention">@今天群内信息量极大</span> 把自己最近用 AI 时骂街的对话全搜出来，统计了一下"刚才这通火是发给谁的"。一看才发现，DeepSeek V4 上线才一个多月，但它在"被骂榜"上遥遥领先。

但真正有意思的是，这位骂 V4 骂得最狠的人，下一秒却来了这么一句：

> 我对 DeepSeek 天天骂，但还是欲罢不能——因为它写作写得是真的好。

一个模型，能让一位 AI 重度爱好者一边问候它祖宗、一边卸载不掉。这事值得写一篇分析。

## 不是评价分裂，是分工不同

Deepseek V4 刚发布的那会儿，群里第一时间涌出来的情绪是："就这？"。<span class="mention">@务实的长颈鹿</span> 瞄了一眼[官方那句](https://mp.weixin.qq.com/s?__biz=Mzk0OTYwNzc3NQ==&mid=2247485745&idx=1&sn=ef3bc11042fc329e89bc66a8938e8b2c)"世界知识大幅领先其他开源模型，仅稍逊于 Gemini-Pro-3.1"，丢出四个字："有点失望。"旁边 <span class="mention">@冷静的飞鼠</span> 出来打了个圆场："人家开源 + 资源有限，本来就不可能一步登天。"

可没过多久，口碑就齐刷刷分成两半：

- 拿它来写东西、搜资料、啃长文档的，基本都说好。<span class="mention">@天真的大象</span> 的原话是："比 Sonnet 推理好。"<span class="mention">@谨慎的树懒</span> 拿 V4 Pro 配上自己那套工作流跑了一圈，"感觉比 Opus 4.6 强，但就是慢"。
- 想拿它写程序、指望它自己在那儿吭哧吭哧干活的，基本都裂开了。<span class="mention">@今天群内信息量极大</span> 那句话说得很死："TBH，这是个 deal breaker。"

同一拨 AI 老手，评价却一个天上一个地下。不是谁不会用，根本原因是**他们派给 V4 的任务不是一码事**。这条裂痕，恰好戳中了 V4 最核心的那个属性。

## 它很聪明，但没被"驯化"

由 <span class="mention">@风趣的猫头鹰</span> 转进群的一份对比报告写得很直白：V4 的"纯编程能力远强于 Kimi-K2.6 和 GLM-5.1，上下文超长，利于大量文档阅读"。<span class="mention">@活泼的羊驼</span> 通读技术报告后总结："在 coding 和数学上，V4 是开源世界最强，部分指标甚至全球最强；只有在长上下文检索上还是 Opus 领先一档。"**论原始智力，DeepSeek 就是开源届的天花板。**

可所有毛病，最后都落到同一个问题上：指令跟随（instruction following）能力，也就是"听不听话"。过去一个月群里翻来覆去骂的就是这个。

<span class="mention">@今天群内信息量极大</span> 的御三家（Gemini, Claude 和 GPT）配额全烧光了，只好把主力模型切到 DeepSeek。那几天他记下来的体验，活生生就是一部血泪史：

> 用起来真是太累了……叫它调用 Gemini，它就去调用 GPT。AGENTS.md 里说了做任何事之前先去读 xx 文件，打死都不读。当年跟 Gemini 搏斗的记忆全都回来了……

工具调用那边也不靠谱。还是这位老哥在骂：

> 看 DeepSeek Pro 工作真的想骂娘……一个简单的 edit tool，因为引号转义就一直失败，永远失败，最后直接摆烂说"搞定了"。

更吓人的是他后面补的那句"DeepSeek 特别喜欢删我库"，吓得 <span class="mention">@聪明的灰熊</span> 立即表示："卧槽，那不敢让 ds 这么操作了。"<span class="mention">@敏锐的兔子</span> 一句话把这种体感说透了：

> 它能力上没上来不知道，脾气是真上来了。

那么问题来了：一个原始智力是开源天花板的模型，为什么连"编辑文件"这种小事都做不利索？

## 原来不是"不会调"，是"格式吐歪了"

<span class="mention">@风趣的海豚</span> 转发的一篇复盘文章给出了答案。这是群里[讨论得最多的文章](https://mp.weixin.qq.com/s?__biz=Mzk0NjY1ODk0MQ==&mid=2247488084&idx=1&sn=9d1fb4b927d43ffd366d5a2a9d4c80ef)。

5 月 3 号，Command Code 的作者 Ahmad Awais 在 X 上写了篇长文，复盘他这两天把 DeepSeek V4 Pro 的工具调用能力接入自己项目的过程。他盯着几十亿个 token 的调用日志，甩出一个惊人的结论：

> 开源模型工具调用差，几乎每次都是 harness 的问题，跟模型本身没多大关系。

数据更惊人：他写了上百行修复代码之后，"DeepSeek V4 Pro 在我们的内部评测里，6/10 次胜过了 Opus 4.7"。（得补充一句：这是人家项目内部的任务，任务集、样本数、打分规则都没公开，只能算工程上的体感观察，不能当公开 benchmark 看。作者自己也特意提了。）

但这个比分不是最值得关注的。需要注意的是他详细分析"调用失败"时体现的底层毛病。他反复撞见四类结构层（shape-level）错误，占了失败案例的差不多 90%：

- optional 字段应该直接省略，模型偏塞了个 null 进去；
- 该输出数组的地方，模型给了一个 JSON 字符串；
- schema 明明要数组，模型扔了个空对象 {} 占位置；
- schema 要数组，模型直接甩一个裸字符串。

每一类问题可以通过在 harness 中添加 30 到 100 行纠正代码来兜底。代码量不大，但补完之后，评测结果立即有所改观。

有个细节几乎完美解释了文章开头那个撕裂现象：DeepSeek 偶尔会把文件路径写成 markdown 超链接——比如把 `/Users/x/proj/notes.md` 写成 `/Users/x/proj/[notes.md](http://notes.md)`。这跟模型智商没有任何关系，纯粹是它在对话和写作场景里被训练出来的格式习惯，"漏"到了工具调用的参数里。

![手里拿着锤子，看什么都像钉子](/assets/img/review/2026-06-06-deepseek-v4-1.png)

换句话说：**它不是不会调工具，是它写作太"入戏"，把 markdown 的习惯带进了函数调用过程**。 它那个"听话差"的毛病，和它那个"写作强"的优点，本质上很可能是同一件事。群里 <span class="mention">@今天群内信息量极大</span> 早先也提出过假设："适合写作的模型，可能天生就更偏创意、更任性。"

Ahmad 给了一个特别精辟的总结：

> 用"工具混淆"（tool confusion）来理解这个问题，比"能力差距"（capability gap）更准确。

Deepseek 的模型能力本来是有的，真正卡住它的是格式契约上的混淆。你帮它消除混淆，能力就释放出来了。

遇到这种问题的远不止他一个人。Fireworks 给 DeepSeek 接工具调用时直说，官方从没放出过完整的调用格式规范，只能照社区零碎信息一点点反推；Hugging Face 上有人翻开随 DeepSeek 模型一起发布的那个聊天模板示例文件，发现里面根本没有处理工具的那段逻辑——换句话说，你在请求里传进去多少工具都没用，模型连"有工具可调"这件事都不会被告知，自然无从下手。最狠的是 SambaNova 那组跨平台实测：同一份模型权重一个字节没动，只是换了不同的推理平台来跑多轮工具调用，一个平台能做到 35% 成功率，另一个只有 4%，差了近 9 倍，大概率是不同平台的工具调用格式不一样。

所以，你以为是"模型蠢"，实际上可能是"壳还没接好"。

## 对 Deepseek，harness 要反着收紧

当然，很多人不会去写那几百行修复代码。但 Ahmad 的发现至少指了一条明路：**对 V4，你得把 harness 往紧里收。** 这跟群里之前一句共识正好反着："模型越来越强，harness 就可以越来越松"。V4 就是个例外：脑子好使，但行为野，所以得反过来，把壳箍紧、把指令掰碎了说。

下面我把群友一个个坑踩出来、能直接拿来用的经验，总结成五条：

**一、让它当写手，别让它当包工头。** V4 最舒服的领域是写作、调研、读长文档、出初稿。<span class="mention">@敏锐的海狸</span> 有个固定搭配："让 ds v4 和 Opus 4.7 互相 debate 着写"——薅它的文笔，拿另一个模型的判断力来兜底它不靠谱的地方。

**二、增加一个"复核"环节。** <span class="mention">@今天群内信息量极大</span> 的原话是："我用 V4 Flash 调研，再用 GPT 复核，抓出来一大把幻觉。"初稿能让它写，但把关这道门绝不能交给它。

**三、写 prompt 要细到"手把手"。** 这是 <span class="mention">@今天群内信息量极大</span> 把自己工作流迁到 DeepSeek 之后总结出来的：

> 基本原则就是要跟它讲得特别细，像跟一个很较真的人说话，手把手教，然后再跑几轮看它会出什么幺蛾子，再在 prompt 里把它堵上。

想一句话就让 V4 自己心领神会，那不太可行。

**四、harness 选不对，能力直接打骨折。** 同一个 V4，套上不同的壳，跑出来的成绩能差出一个模型代际。[一篇广泛传播的 CSDN 实测](https://deepseek.csdn.net/69f18cc30a2f6a37c5a6c091.html)拿一个真实的 Phaser 3 游戏 bug 修复任务做对比：V4 Flash 在某框架下直接挂掉，换到 Claude Code 里两次就修好了；而 V4 Pro 在 Claude Code 里一把过、大约 18 分钟搞定，反超了改三次才成的 Opus 4.7。作者一句话收尾——"工具链的差异，比模型代际差异更大"。

不过 harness 具体怎么配，群里也有不同看法：那份内测报告就说，把 V4 塞进太复杂的智能体系统反而会拖后腿。所以更务实的路数是：先按 [DeepSeek 官方的 Claude Code 集成指南](https://api-docs.deepseek.com/guides/agent_integrations/claude_code)跑起来，然后根据自己项目的反馈慢慢调。<span class="mention">@今天群内信息量极大</span> 给的建议是："最简单的先用官方那个试试，觉得好用再上 opencode。"

**五、别小看 Flash，它可能是隐藏的王牌。** <span class="mention">@冷静的麋鹿</span> 的个人体感是"Flash 的遵循能力好像比 Pro 还强"。<span class="mention">@今天群内信息量极大</span> 进一步补充，这一代 Pro 和 Flash 的关系"有点像 Gemini 3 Flash 和 2.5 Pro，Flash 总觉得更好用，思维深度也没降低"，甚至"有一点 Composer 的感觉，很快，质量也不错"。

有意思的是，连 DeepSeek 自己也认准了“改进 harness”这条路。据[财联社报道](https://www.chinastarmarket.cn/detail/2376780)，其资深研究员陈德里确认团队正在做"DeepSeek Code Harness"，直接对标 Claude Code，并在 2026 年 5 月开出了 Agent Harness 产品经理和研发工程师的岗位，招聘要求里白纸黑字写着要"深度用过 Claude Code、Codex、Cursor"。光有一个强模型不够，还得有一个配得上它的壳。

## 同一股劲儿，换个场景就是优点

聊到这里，可以回头答一下标题那个问题了：又难伺候、又被骂得这么狠，怎么很少有人真把它删了呢？

第一个理由，就藏在前头那句"听话差和写作强是同一件事"里。把 V4 那股"写作太入戏"的劲儿放到对的位置上，也就是真的让它去写东西，它立马从一个麻烦精变成了惊喜。

<span class="mention">@乐观的灰熊</span> 提到，在 OpenRouter 的创意写作榜上，DeepSeek 上一代就已经"超级断档领先"；<span class="mention">@务实的长颈鹿</span> 说，中文会议纪要这类整理写作，现在"比较好用了"；连重度 AI 用户 <span class="mention">@今天群内信息量极大</span> 都特意去"调教 ds v4 写作"，效果好到 <span class="mention">@幽默的犀牛</span> 在边上起哄说"可以让 AI 蒸馏一下他的历史记录"学两招。

网上的公开评测也指向同一个方向，尤其在最吃"语体"的中文公文和政治术语翻译上。有[一篇评测](https://www.163.com/dy/article/KU927N2705118HA4.html)举的例子很能说明问题：翻"新质生产力"，V4 不光给出官方译法"new quality productive forces"，还能讲清楚它的四层含义；翻"绿水青山就是金山银山"，它会按场景给不同版本——官方文件用"Lucid waters and lush mountains are invaluable assets"，宣传牌则用更上口的"Green hills and clear waters are the real gold and silver"。技术文档写作它拿了 4.7/5，当裁判的 Opus 4.7 评价说"完整且结构化，是一份高质量的项目交接文档"。

群里甚至传过一个没被证实的小道消息：<span class="mention">@风趣的企鹅</span> 表示，听说 DeepSeek 专门为公文场景请了个"作家评审团"来打磨文风——但他自己也补了一句"不知道真假"。这传闻我没法核实，公开资料里也没找到实锤；但结合 V4 在公文、术语上明显的优势，至少能看出一点：写作很可能是 DeepSeek 刻意经营出来的强项，而不是顺手捎带的副产品。

![](/assets/img/review/2026-06-06-deepseek-v4-2.png)

当然得说句公道话，它也不是完美无瑕。<span class="mention">@今天群内信息量极大</span> 自己就吐槽 V4 的"中文写作感觉还是 AI 味比较浓"。那篇评测也抓到它在网络流行语上会"自信瞎编"：被问到一个根本不存在的梗"电子呕吐"，它能一本正经地编出一千多字（[网易评测里的例子](https://www.163.com/dy/article/KU927N2705118HA4.html)）。所以它写东西的甜区，是公文、技术文档、长文初稿这类讲规范、讲信息密度的体裁；越往"抽象""玩梗"那边走，越得死死盯住它。

## 便宜到没天理

除了写作之外，能让大伙儿忍它这副臭脾气的，还有一个更现实的理由：它真便宜。<span class="mention">@今天群内信息量极大</span> 晒过一笔账："Flash 确实省钱，我今天光 DeepSeek 就用了 13 亿 token，只花了不到 100 块人民币。"赶上 Pro 打二五折那阵子，他一个月在 DeepSeek 上花了三千多，"还在发愁六月价格上去了之后怎么办"——结果促销一直没停，"（打折）弄着弄着可能就永久了"。

Deepseek 开源的特性还催生了一条更极客的路：本地运行。Flash 是个 284B 的模型，有群友写了[一篇实测](https://yage.ai/share/ds4-deepseek-v4-flash-mac-20260522.html)：在 MacBook 上大概 25 token/秒，在 DGX Spark 上反而只有 15 token/秒；<span class="mention">@勇敢的老虎</span> 补了一句，"ds4 的 Q4 在 M3 Ultra 上确实能跑"。当然，理性的声音也没缺席：

> 从 Flash 的 token 价格看，就算买了设备、电费不要钱，想回本也是一百年起步。

这正好接上我在周报里的那个总结：真正省钱的不是少用 AI，而是给每个任务派一个配得上它的模型。**DeepSeek V4 就是那个"够用且极便宜"的地板**——把它放在量大、不需要太多判断力的环节（调研、初稿、格式转换、读长文档），它的性价比无人能敌。

## 总结

回到那个最初的撕裂：为什么同一个模型，有人当个宝，有人砸电脑？它到底值不值得用，答案其实特别清楚：

**如果你愿意花时间纠正它，它全场性价比最高；如果你只想要一个开箱即用、招之即来的打工人，它会让你每天问候它的祖宗。**

## 📎 附录·技术向

### 1. 真正的新东西：混合注意力（Hybrid Attention）

发布当天群里一度把 V4 的新机制讹传成了"DSA 稀疏注意力"，<span class="mention">@活泼的羊驼</span> 读完技术报告后纠正了这个说法：V4 真正的新机制是一套**混合注意力（Hybrid Attention）**，由两个新组件构成——

- **CSA（Compressed Sparse Attention，压缩稀疏注意力）**
- **HCA（Heavily Compressed Attention，高度压缩注意力）**

它的核心思路是**在 token 维度上做压缩**，再配合稀疏注意力。<span class="mention">@务实的长颈鹿</span> 引用的官方数据表示：在 1M 上下文设置下，V4-Pro 的单 token 推理 FLOPs 只有 V3.2 的约两成，KV Cache 只有 10%；V4-Flash 更极端，压得更狠。

这就是"百万上下文普惠"和那个离谱低价背后的工程底气：从这一代起，1M 上下文成了 DeepSeek 所有官方服务的标配（[官方公告](https://mp.weixin.qq.com/s?__biz=Mzk0OTYwNzc3NQ==&mid=2247485745&idx=1&sn=ef3bc11042fc329e89bc66a8938e8b2c)）。同样的长上下文能力，它的算力和显存开销比传统方法低了一个数量级——也正因如此，一个 284B 的 Flash 才有可能塞进一台 Mac 本地运行。

### 2. 聪明是预训练给的，听话是后训练欠的

正文那个"工具混淆"的故事，解释了"格式"层面的失败，但还可能有一层更底层的原因：V4 本质上是一个**重点提升世界知识的新预训练模型**。它的聪明（开源最强编程、最强世界知识、强写作）是预训练给的；而听不听话、会不会乖乖用 SubAgent、会不会读你指定的文件——这些是**后训练（尤其是智能体方向的后训练）才能补上的**。<span class="mention">@开朗的企鹅</span> 的推测是：留给后训练的资源和时间还不够。

那份由 <span class="mention">@风趣的猫头鹰</span> 转进群的内测报告，详细地描述了疑似"后训练欠课"的症状：

> **优势**：纯编程能力远强于 Kimi-K2.6 和 GLM-5.1；上下文超长，利于大量文档阅读。**劣势**：极少使用 SubAgent，导致上下文迅速膨胀；不写文档、代码注释不详实；缺乏大型项目的长程规划（不会写 rustfmt.toml / clippy 配置，C++ 的 Vcpkg 配置出错）；instruction following 差；会在任务中段就宣称"全部完成"，出 bug 还倾向于归因于外部原因。

一句话概括 V4 的性格：**聪明是预训练给的满分，听话是后训练欠的那门课。** 而正文讲的格式层 bug，则是这门欠课最表层、也最容易被 harness 兜住的那部分。

### 3. 一点冷静的旁注：别被"国运叙事"带跑

V4 发布后，群里一度有"国运级模型"的兴奋（<span class="mention">@风趣的企鹅</span> 转的《[再谈 DeepSeek：中美 AI 正式分叉](https://mp.weixin.qq.com/s?__biz=MzcwNDE5NzI3Ng==&mid=2247483872&idx=1&sn=591c60fcc70d271e03a950a43a4e3671)》）。但群友也保持了清醒：<span class="mention">@今天群内信息量极大</span> 提到，在一个专门为对抗 benchmark 饱和而设计的新编程评测里，"GPT 和 Claude 是第一梯队，Gemini 差一档，DeepSeek 以 8 分垫底"。

一份收录了上百个模型的[公开评测榜](https://www.datalearner.com/ai-models/pretrained-models/deepseek-v4-pro/analysis)则给出了更立体的画像：V4-Pro 的 LiveCodeBench 拿到 93.50、在 120 个模型里排第一，Codeforces 冲到 3206 分（接近人类顶尖程序员），数学和编程都是第一梯队；但代表超难跨域知识的 HLE 只有 48.2，落后于 Kimi K2.6 和 GLM 5.1。**强项极强，短板也很诚实。**

这些看似打架的数据，恰恰回到了全文那个结论：**V4 的成绩单极度依赖你给它配的 harness。** 同一个模型，裸用和精调，可以是两个分数。

## 延伸阅读

- [DeepSeek-V4 技术报告 PDF（HuggingFace）](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro/blob/main/DeepSeek_V4.pdf)
- [DeepSeek API 定价](https://api-docs.deepseek.com/zh-cn/quick_start/pricing)
- [我们是怎么让 DeepSeek 跑赢 Opus 4.7 的（小红书）](https://www.xiaohongshu.com/discovery/item/69f960330000000022024333)
- [为什么 V4 Pro 加了一个"几乎没用"的 Tool，回答反而变长了（知乎）](https://zhuanlan.zhihu.com/p/2036449001084565006)
- [聊聊 DeepSeek V4：技术报告里藏着的那些"小字"才是重头戏（知乎）](https://zhuanlan.zhihu.com/p/2031168317549966085)
- [DeepSeek-V4 技术报告解读：从架构到 Infra 的全栈重构（知乎）](https://zhuanlan.zhihu.com/p/2030982954617414764)
- [DeepSeek V4 论文精读：迈入百万上下文的普惠智能（CSDN）](https://blog.csdn.net/youcans/article/details/160478185)
- [deepseek-v4-pro + Harness 实战效果（LINUX DO）](https://linux.do/t/topic/2048516)
