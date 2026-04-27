# 跨领域扩展设计笔记 (Cross-Genre Extension Design Notes)

## 前提

这份笔记记录我们对 Listening Atlas Agent Kit 做跨领域适配的两次**纸面推演**（dry-run）以及由此引出的关于 kit 通用性结构的设计判断。

**两次推演都未落地：** 京剧和爵士的扩展都没有写入 repo；目前 `specs/extensions/` 目录尚未存在，没有任何真实的 domain extension 文件。下文所有字段、章节模型、平台优先级建议都还是设计草案，需要通过实际撰写 stub extension 来验证。

接手 agent 应当：

1. 先通读全文，不要跳到执行步骤
2. 理解第三节"为什么不新增 phase 0.5"的论证
3. 按文末顺序行动，不要并行展开

---

## 一、京剧推演的关键发现

### 能直接复用

- 项目 brief 模板、章节式指南结构、"先平台无关 TSV、再平台执行 log"流程、QA 清单、release 政策
- `docs/PLAYBOOK.md` 已显式允许章节模型替换

### 真正的结构性冲突

**1. PLAYLIST_SCHEMA 是西方古典音乐编码的**

`composer` 字段在京剧里几乎是空概念——传统剧目无单一作曲家，唱腔属流派传承。`composer_ipa` 对中文专名无用。京剧的真正结构变量是：

- 剧目 (play) ≠ 选段 (excerpt) ≠ 唱段 (vocal phrase)
- 流派 (school)：梅、程、荀、尚 / 余、言、马、谭、杨
- 行当 (role type)：生、旦、净、丑及其子类
- 板式 (rhythmic mode)：西皮 / 二黄 / 原板 / 慢板 / 快板 / 流水 / 散板 / 导板
- 主演、配演、琴师 三类身份要分开
- 录音年代和载体（78 转 / 50–60 年代实况 / 棚内 / 电影版 / 当代）

按现行 schema，这些只能塞进 `performers` 和 `role` 的自由文本里，下游 prompt 拿不到结构化字段去做平台搜索和章节归类。

**2. 录音版本敏感度比古典还高**

同一段《贵妃醉酒》，梅兰芳 1925 年百代老唱片、1955 年电影版、张君秋 1962 实况，是听感差异巨大的三个东西。`fallback_recording` 一条不够用。`match_status` 枚举要新增"不同流派""不同琴师""不同录音年代""老唱片不同转录""实况 vs 棚内"。否则平台执行 agent 会把"梅派"和"张派"当可互换替代，留下严重错误。

**3. 平台优先级反转**

对京剧而言，Apple Music / Spotify / TIDAL 的 catalog 最稀薄。真正的主战场：

- 网易云音乐（当代录音 + 部分 50–80 年代实况）
- QQ 音乐
- B 站（实况视频 / 老艺术家影像 / 折子戏全本——大量历史录音的唯一可达点）
- YouTube（海外用户的 B 站替代）
- 中国京剧老唱片资料类网站（非流媒体，但是检索锚点）

`specs/PLATFORM_ADAPTERS.md` 没有 "video-as-primary" 模式——对戏曲、舞剧、能剧这类表演艺术，listen audio-only 本身就是失真。"playlist" 抽象需要扩展到 "playable item" (audio | video | archival)。

**4. 视觉素材版权可获得性骤降**

京剧名家大多是 20 世纪人物，PD 边界要逐人核：梅兰芳 (1961 逝)、程砚秋 (1958 逝) 同理；50 年代之后的剧照基本仍在保护期。脸谱图样在传统范畴内可能视为公共领域，具体绘制版本仍可能有作者权益。Wikimedia Commons 上的京剧名家影像比西方古典作曲家薄一个量级。

### 京剧版扩展的最小改动建议

**Schema 扩展**（不动 core spec 契约，只在可选字段里加几列）：

- `creator_role`：tradition / playwright / school_founder / lead_performer
- `school_派`：流派标签
- `role_type_行当`：生 / 旦 / 净 / 丑 子分类
- `vocal_pattern_板式`：西皮 / 二黄 / etc.
- `accompanist_琴师`
- `recording_year` 与 `recording_format`（78rpm / LP / 实况 / 电影 / 棚内 / 数字）
- `playable_type`：audio_track / video / archival_only

把 `composer_ipa` 在京剧版重命名为 `name_pinyin`；允许 `composer` 字段填演员、流派或"传统/集体创作"。

**PLATFORM_ADAPTERS 补丁文档**：网易云、QQ 音乐、B 站升为 primary；Apple Music / Spotify 降为 secondary；加 "video-as-primary" 这一节；archival-only 路径写清楚（log 里仍占一行，`selected_url` 指向 archival 页面，`match_status = archival_only`）。

**章节模型 (10 章)**：

1. 京剧形成（徽班进京至同光十三绝，约 1790–1880）
2. 老生流派与早期录音（谭、余、言、高、马、麒、杨…）
3. 四大名旦与旦角流派（梅、程、荀、尚 + 张君秋 / 四小名旦）
4. 净行与丑行
5. 板式与听法（横切章：从前几章里挑示范段集中讲西皮二黄、慢板原板的辨识）
6. 武戏与文戏分野
7. 老唱片史与转录传统
8. 样板戏与革命现代戏（独立章节，因为唱腔语汇在这里发生剧烈变形）
9. 改革开放后与当代京剧
10. 京剧走向影视、海外与跨界

**体量预估**：100–120 行歌单（比古典 demo 小，可识别传世录音池本身就窄）。

**视觉减法**：放弃西式肖像时间线 SVG；用脸谱图谱 + 戏单复制件 + PD 剧照 + 流派网络图。"音乐史地图"重新解释为"流派传承网络图"，节点是流派和代表演员，边是师承。

### 京剧场景下的硬约束（kit 改造解决不了）

- 大量历史录音不在任何流媒体平台上。"完整听完歌单"在京剧场景下未必成立——指南必须诚实写进"How to use"
- 流派辨识对入门者是真正的门槛，"How to listen"章节责任比古典 demo 重得多
- 名家影像版权要 case-by-case 核到每一张，不能像 Wikimedia 古典作曲家肖像那样批量搬运

### 给 maintainer 的两个未决问题

1. 是否接受 schema 扩展不进入 core spec、只作为 "domain extension" 文件落到 `specs/extensions/peking_opera_schema.md`？这样既不污染 kit 核心字段集，又能让京剧版自洽。
2. video-as-primary 模式是否要回写到 PLATFORM_ADAPTERS 主文件？倾向于要——戏曲、能剧、舞剧、相声这些表演艺术都会触发同一个问题，与其每个 domain 各自打补丁，不如让 kit 主线承认 "playable item ≠ audio track"。

---

## 二、爵士推演的关键发现

爵士比京剧顺手很多，但要动的地方完全不一样。京剧的结构性问题是"京剧没有作曲家、表演艺术不是音轨"；爵士的结构性问题是"录音本身就是作品，schema 默认的 composer/work/recording 三层结构在爵士里要倒过来"。

### 直接顺手的部分

- 平台层基本不用改：Apple Music、Spotify、TIDAL、Qobuz、YouTube Music 的爵士 catalog 都很深；TIDAL/Qobuz 的 master quality 特别适合爵士；Bandcamp 对当代独立厂牌重要。`specs/PLATFORM_ADAPTERS.md` 加一节 Qobuz、加一节 Bandcamp 即可，不需反转优先级
- 章节式指南、入门曲目表、按 `track_no` 平台执行、QA 清单——距离古典 demo 比京剧近
- `order_verification` 流程能直接复用

### 结构性硬冲突：作品就是录音

古典 schema 的隐含假设是 `composer + work` 是作品身份，`recommended_recording` 是该作品的实例。爵士反过来——1959 年 3 月 2 日哥伦比亚 30 街 studio 的 "So What"、1965 年 Plugged Nickel 现场版 "So What"、Wayne Shorter 90 年代翻奏 "So What"，是三个不同的音乐对象。"All the Things You Are" 这个 Kern standard 只是骨架，被 Bird、Coltrane、Mehldau 用完全不同方式血肉化。

schema 第一件事是把作品身份从 "composer + work" 迁到 "recording_id"，并把 "standard_composer"（写曲的人）和 "recording_leader"（这次录音的领班）作为两个独立字段。

### 爵士版需要新增的字段

- `standard_composer`：标准曲写曲者（Cole Porter, Gershwin, Rodgers/Hart, Monk, Wayne Shorter…）；原创曲就是 leader
- `recording_leader`：本次录音领班
- `ensemble_name`：固定团体（Miles Davis Quintet, Modern Jazz Quartet, Art Ensemble of Chicago, Bad Plus）
- `personnel`：结构化"姓名 (乐器); 姓名 (乐器); ..."。**最重要**——同 leader 不同时期 lineup 是不同乐手生态
- `session_date`
- `session_location`：Rudy Van Gelder Studio (Hackensack / Englewood Cliffs), Village Vanguard, Plugged Nickel, Showplace, Five Spot, Slugs', Both/And, Iridium, Smalls...
- `release_year`：与 session_date 经常隔几年甚至几十年
- `label_catalog`：Blue Note BLP 1577, Atlantic SD 1311, Impulse A-77, ECM 1064, Verve V6-8579
- `take` 与 `is_alternate_take`：Bird Savoy/Dial sessions、Coltrane "Giant Steps" 都有 master + alt takes，是不同音乐内容
- `live_or_studio` 与 `venue`
- `scene`：Kansas City swing / 52nd Street bebop / West Coast cool / hard bop / modal / free / fusion / loft / AACM / ECM aesthetic / M-Base / Young Lions / contemporary Brooklyn
- `label_arc`：Blue Note 黄金期 / Impulse 自由派 / ECM 美学 / Bandcamp 独立时代

`match_status` 加：`wrong_take`、`wrong_master`、`compilation_substitute`、`remaster_difference`。这是真实风险——平台搜 "Kind of Blue" 默认上来的常常是 Legacy Edition / mono / 60th anniversary remaster，不是 1959 立体声 master；agent 不显式比对发行年和 catalog 编号会无声替代。

`composer_ipa` 大多没用（爵士名字大多在英语圈），但保留为可选——东欧 (Tomasz Stańko, Esbjörn Svensson, Tigran Hamasyan)、北欧 (Jan Garbarek, Bobo Stenson)、法国 (Stéphane Grappelli) 偶尔需要。

### Discography 系统支持

爵士的版本身份依赖 Tom Lord Discography 和 jazzdisco.org 这种 session-level 索引。schema 应允许：

- `lord_discography_id`（可选；Tom Lord 是付费数据库，agent 不能直接拉，但能填就给平台执行 agent 一个外部 ground truth）
- `matrix_number`（78 转老唱片母带编号；早期爵士复刻常以此区分）

不加这些，Bird Savoy/Dial、早期 Ellington、King Oliver Creole Jazz Band 这些关键早期录音的版本辨识基本失语。

### 章节模型 (11 章 + 横切教学)

1. 起源：新奥尔良、blues、ragtime 到爵士 (Armstrong, King Oliver, Jelly Roll Morton, Bessie Smith)
2. Swing 时代：big band 作为美国大众文化 (Ellington, Basie, Goodman, Hawkins, Webster, Lester Young, Holiday, Fitzgerald)
3. Bebop 革命：52nd Street 工坊 (Bird, Diz, Bud, Monk, Roach)
4. Cool / West Coast / Third Stream
5. Hard bop 与 Blue Note 时代 (Clifford Brown, Silver, Blakey, Mobley, Donald Byrd, Lee Morgan)
6. Modal 与漫长的 60 年代 (Miles 二代五重奏, Coltrane, Hancock, Tyner, Shorter, Jarrett 早期)
7. Free jazz 与火焰音乐 (Ornette, Cecil Taylor, Ayler, AACM, Coltrane 晚期, Sanders)
8. Fusion 与电声化 (Miles 电声期, Mahavishnu, Headhunters, Weather Report, RTF)
9. ECM 与欧洲转向 (Jarrett, Garbarek, Towner, Stańko, Svensson)
10. 当代爵士 2000 后 (Vijay Iyer, Brad Mehldau, Robert Glasper, Kamasi Washington, Ambrose Akinmusire, Mary Halvorson, Tomasz Stańko 晚期, Esperanza Spalding, James Brandon Lewis, Brooklyn 当代)
11. **横切听法章**（古典 demo 没有对应物）：piano trio 怎么听 / head-solos-head 怎么听 / modal vs changes / free vs structured

横切教学章对爵士尤其必要——爵士的一半门槛在 form sense 上，不是历史叙事。

### 视觉素材现实

**可用：**

- 1928 年前发表照片在美国进入 PD（Armstrong 早期、Bessie Smith、King Oliver、Jelly Roll Morton 部分）
- WPA / Library of Congress 公共领域影像
- 在世音乐家的 CC-licensed 现场摄影（部分 Wikimedia 上有）
- 早期失效乐谱封面

**拿不到（且很多读者期望看到）：**

- Francis Wolff 的 Blue Note 录音棚摄影（1971 逝，权属现归 Blue Note/Universal）
- Reid Miles 设计的 Blue Note 唱片封面
- 50–70 年代大多数宣传照
- 大部分 Miles / Coltrane / Mingus / Monk 标志性肖像

**视觉减法：** 自绘 lineup 图（Miles 一代/二代/三代五重奏 personnel 演变）；自绘 scene-network 图（Blue Note 厂牌作 hub，连出 Silver, Mobley, Morgan, Hancock, Shorter）；自绘 lineage 图（Bird → Bud → Hancock → Mehldau；Pres → Stan Getz / Trane / Sonny Rollins）；早期爵士用 PD 照片；当代用 CC 现场摄影；"唱片美学史"附录谈 Reid Miles / ECM Manfred Eicher 美学但不复制版权封面。

`asset_manifest` 现行 spec 严格够用，不用扩；但视觉密度比古典 demo 低。

### 平台执行隐性陷阱（爵士独有）

- "Kind of Blue" 默认上来是 Legacy / 60th Anniversary / Mono Edition，不是 1959 立体声 master
- "A Love Supreme" 普遍被 Deluxe Edition 替换（多 Live in Seattle bonus）
- 早期 Bird Savoy 录音在不同 reissue 里曲目顺序、master/alt 选择不同
- ECM streaming 版本和 LP 母带不同
- Bandcamp 当代发行有时 streaming-exclusive，跟 Apple/Spotify 不能 1:1 复刻

`prompts/04_platform_execution.md` 必须显式要求 agent 在 `selected_album_or_source` 字段记录到 catalog 级（"Columbia CL 1355 (1959 stereo master)" 而非只 "Kind of Blue"），遇 Legacy / Anniversary / Remastered 主动比对发行年。这是 prompt 04 在爵士场景下的关键加固点。

### 体量与边界

- 150–180 行歌单合理，与古典 demo 持平
- phase 3 (recording review) 时间多于古典 demo
- "什么是爵士"边界争议（smooth jazz 算不算？Kamasi 算 jazz 还是 spiritual revival？）必须在 brief 写死，否则下游会反复返工

### 与京剧场景对照

| 维度 | 京剧 | 爵士 |
|---|---|---|
| 核心难点 | 表演艺术不是音轨 | 录音即作品 |
| 身份模型问题 | 无作曲家，流派+行当+板式 | composer/work/recording 三层倒挂 |
| 平台优先级 | 反转（中国生态 + B 站为主） | 微调（加 Qobuz, Bandcamp） |
| Personnel 颗粒度 | 演员 + 琴师 + 流派 | 结构化 lineup + take 级 |
| 视觉素材 | 案例最稀缺 | 早期 PD + 当代 CC，中段断层 |
| 章节模型 | 流派 + 行当 + 板式 + 老唱片 | 年代 + 流派 + 横切教学章 |
| 共同问题 | chapter model 不能照搬古典 demo | 同 |
| 共同解法 | schema extension + 章节模型分文件 + prompt 04 域内补丁 | 同 |

如果让 kit 优先做爵士再做京剧，是合理的——爵士能把 kit 推到一个"录音作为作品 + 结构化 personnel"的扩展形态，这个扩展对后续做任何录音中心的领域（摇滚、电子、嘻哈、当代独立）都会复用。

---

## 三、关于 "通用性" 的元判断：不要新增 phase

User 直觉是该多一个 "genre transfer analysis" 步骤来识别 gap 和必要补充。**直觉对，但"加一个步骤"不是最干净的形状。**

### 为什么不应做成 phase 0.5

1. **过早抽象的风险。** 现在只有古典 demo 一个真实跑通过的领域，加爵士、京剧两次纸面推演——三个数据点不足以确认领域间差异沿哪些轴展开。如果现在就把 transfer analysis 固化成有 prompt + spec + template + QA 项的正式 phase，等到第四第五个领域真正落地时，多半会发现固化下来的轴选错了或漏了关键维度。Kit 是文档驱动的，加一个 phase 的边际成本是一份 prompt + 一份 spec + 一份 template + 一份 QA 清单条目——撤回成本远高于添加成本。
2. **让简单 case 变累。** 摇滚、独立电子、K-pop、film score 的 identity model 跟古典/爵士距离很近（recording + artist + release year），几乎不需要 schema 扩展。强制走 transfer analysis 会让 80% 的领域跑一个产出"无显著 gap"的步骤，是纯摩擦。
3. **"步骤"暗示线性。** 真实做法更像 declarative：项目声明"我用古典扩展"或"我用爵士扩展"，schema 装上对应字段。这是 layer/extension 模型，不是 phase 模型。Phase 模型暗示 agent 每次都要重新分析；extension 模型让 agent 只在领域是新的时候才动脑。

### 真正缺的不是 step，是 extension layer

**a. 新增 `specs/extensions/` 目录**

每个领域一个文件（`jazz.md`, `peking_opera.md`, `film_score.md`）。每个 extension 声明三件事：

- 在 core schema 上要新增哪些字段（带 rationale）
- 哪些 core 字段在本领域语义不同（如 `composer` 在京剧里指流派而非个人）
- `match_status` 枚举要扩展哪些值

不动 core spec 的前提下，把"领域差异"从 phase 0.5 prompt 移到一个可版本化、可被 agent `Read` 进上下文的文件里。

**b. 新增 `specs/EXTENSION_CONTRACT.md`**

约束扩展能改什么、不能改什么：

- 哪些字段是 cross-domain invariant，扩展不能重定义（`track_no` 必须可排序、`row_id` 必须稳定）
- 扩展可以新增字段，但每个新字段必须挂在一个明示的 "differential axis" 上：identity model / personnel granularity / version sensitivity / playable medium / platform fit / asset availability / repertoire model / chapter axis
- 扩展不能删除 core 字段，只能在该领域里把它标为 `not_applicable`

这条 contract 是为了防止扩展无限膨胀——每个领域都想加 30 列，加完之后 kit 没纪律。强制每个新字段挂轴，能让 maintainer 看出来是不是某条轴该提升进 core。

**c. phase 1 (brief) 内嵌一份 "domain fit worksheet"**（不是新 phase）

回答几个结构问题：

- 作品身份是 composer+work、recording、performer 还是 scene？
- personnel 颗粒度需要到 named member 吗？
- 版本敏感度：take 级 / 录音年代级 / 演员级 / 不敏感？
- 主要 playable 形态：audio / audio+video / video-primary / archival-only？
- 主要平台簇：Western streaming / Chinese streaming / Bandcamp / 专业 archive？
- 视觉素材时代分布：pre-1928 重 / mid-20c 中 / 当代轻？
- 章节轴选哪个？年代 / 流派 / 厂牌 / 乐器 / 地区 / lineage？
- 用哪个已有 extension（如果有）？还是要新写一个？

worksheet 输出有两种可能：(a) "用 extension X，不需要新字段"，结束；(b) "需要写新 extension，这是初稿"。把 gap analysis 嵌进 brief，但不让它阻塞简单 case。

### Phase 模型 vs Extension Layer 模型

- **Phase 模型**：每个项目都跑一遍 transfer analysis prompt → agent 自由发挥 → 产出不可控
- **Extension layer + worksheet**：worksheet 是固定问卷，已有 extension 的领域 5 分钟跑完，新领域才进入扩展撰写流程

后者把"已经做过的领域"和"新领域"区分开，前者把它们都当新领域。

### 必须诚实承认的 tradeoff

- **Extension 不一定能保持同步。** Core spec 演进时，已有 extension 可能过时。Kit 现在没有 schema 版本号、没有 extension 兼容性声明、没有 deprecation policy。引入 extension layer 就是引入这套治理负担——如果 maintainer 没准备好做版本管理，不如不开这个口子。
- **Worksheet 自身会成为新训练负担。** Agent 跑得机械会把不该套的 extension 套用上去（如把"录音即作品"错误套在 K-pop 上——K-pop 作品身份其实更接近 producer + idol release，不是 jazz 式 session 身份）。Worksheet 必须有"都不像，要写新 extension"的逃生口。
- **维护方应至少持有 2–3 个 reference extension。** 只有 jazz 一个 extension 在仓库里时，新人会以为 extension 就是"加一些字段"，不会理解 extension 也可以重定义语义、扩展枚举。Reference 太少，contract 教不出来。
- **Alternative：根本不引入 extension layer。** 把 jazz/京剧 schema 差异留在用户侧。优点：维护负担最小。缺点：每个用户都要从零做 transfer analysis，集体重复劳动。这是真实可选项，取决于 kit 想不想成为有领域积累的库，还是只想做一个干净的方法论模板。

---

## 四、推荐的执行顺序

**不要并行展开。** 按以下顺序推进：

1. **先把古典 demo 拉回 spec contract。** 这是前一轮审计的建议；不做这件事谈通用性会失焦。
2. **写爵士和京剧的 stub extension** 到 `specs/extensions/`，看冲突在哪。这是验证 extension 模型够不够用的最低成本方式。
   - 如果两个 extension 能在不冲突 core spec 的前提下声明完整，extension 模型就成立
   - 如果写到一半发现 core spec 字段语义在不同领域互斥，那说明 core spec 本身要先做一次 normalization，不能急着上 extension layer
3. **看完冲突再写 EXTENSION_CONTRACT。** Contract 的 differential axes 应当从两份真实 extension 里归纳，不是先验设计。先有 case，再抽 contract——这跟"demo 应当真的 demonstrate spec"是同一个原则：抽象层只在两个具体实例之间产生。
4. **Worksheet 留到第二个真领域（爵士）跑通之后，再从经验里抽出来。**

**不要现在就把 transfer analysis 设计成一个独立 phase。** Kit 还没成熟到那个阶段。等到三四个真实领域跑过、看到重复出现的失败模式，那时 worksheet 的设计才有依据。

---

## 摘要 (TL;DR)

- **京剧推演结论：** 表演艺术不是音轨 + 平台优先级反转 + 视觉素材稀缺。需要 schema 扩展（流派 / 行当 / 板式 / 琴师 / 录音载体 / playable_type）、PLATFORM_ADAPTERS 反转 + video-as-primary、章节模型重写、视觉减法。歌单体量 100–120 行。
- **爵士推演结论：** 录音即作品（schema 三层结构倒挂）+ personnel 必须结构化 + master/take/reissue 辨识。需要 schema 扩展（standard_composer / recording_leader / personnel / session_date / session_location / take / scene / label_arc）、`match_status` 扩枚举、prompt 04 加 catalog 级比对要求、章节加横切教学章。歌单体量 150–180 行，与古典 demo 持平。
- **通用性元判断：不要新增 transfer analysis phase。** 改用 `specs/extensions/` 目录 + `EXTENSION_CONTRACT.md` + brief 内嵌 worksheet。Phase 模型让简单 case 也变累；extension layer 把已有领域和新领域分开。
- **落地顺序：** demo 拉回 spec → 写两份 stub extension → 据冲突写 contract → 第二个真领域跑通后再写 worksheet。
