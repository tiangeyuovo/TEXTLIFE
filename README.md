# TEXTLIFE

**An emergent-ecology sandbox for synthetic biology education**
**面向合成生物学教育的涌现式生态沙盒**

A single HTML file. No install, no server, no dependencies. Open it and a world starts evolving.
单个 HTML 文件。无需安装、无需服务器、零依赖。打开即开始演化。

---

## 1. What this is / 这是什么

**EN** — TEXTLIFE is a text-only ecosystem simulator. A 72×32 grid holds up to ~2000 organisms, each a single character. Nobody is controlled directly. Every organism follows the same short rule list — burn energy, sense its neighbourhood, flee / eat / chase / reproduce / wander — and the population-level behaviour you see (booms, crashes, oscillations, extinctions, the birth of new species) is *not written anywhere in the code*. It emerges from those rules plus a strictly conserved energy budget.

You are a field observer, not a god. You get a small, slowly-refilling pool of **influence** points to nudge the environment, and then you watch what your nudge did. Close the tab and come back tomorrow: the world kept running, and a **field report** tells you what happened while you were away.

**中文** — TEXTLIFE 是一个纯文字生态模拟器。72×32 的网格上最多容纳约 2000 个生物，每个生物就是一个字符。玩家不直接操控任何个体。每个生物只遵循一份很短的规则表——消耗能量、感知邻域、逃跑／进食／追逐／繁殖／游走——而你看到的种群层面现象（暴涨、崩溃、周期振荡、灭绝、新物种诞生）**在代码里并没有被显式写出来**，它们是这些规则加上严格守恒的能量预算之后自己"涌现"出来的。

你是一名田野观察者，而不是造物主。你只有少量、缓慢恢复的 **influence（干预点数）** 去轻推环境，然后观察这一推造成了什么。关掉网页明天再来，世界仍在自行运转，回来时会有一份 **field report（考察报告）** 告诉你这段时间发生了什么。

---

## 2. Why this belongs in synthetic biology education / 为什么它适合用于合成生物学教育

**EN** — Most outreach games about biology teach vocabulary. This one teaches *constraints* — the handful of hard limits that decide whether an engineered biological system actually works. Every mechanic below was implemented because the simulation collapsed without it, so each one is a lesson the player learns by failing, not by reading.

**中文** — 大多数生物学科普游戏教的是名词。这个游戏教的是**约束**——那几条决定"一个被改造的生物系统到底能不能跑起来"的硬性限制。下表中的每一条机制，都是因为"没有它模拟就会崩溃"才被写进代码的，所以玩家是靠失败学到它，而不是靠阅读。

| In the game / 游戏中的机制                                                                                                                                                                                                                                                                                                                                                          | The synthetic biology concept / 对应的合成生物学概念                                                                                                                                                                                                                                                                                                                                                            |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Energy is strictly conserved.** Light is the only input; metabolism and the 30% loss at each feeding are the only outputs. Nothing is created from nothing.**能量严格守恒。** 光照是唯一输入，代谢与每次取食 30% 的热损失是唯一输出。没有任何东西凭空产生。                                                                                                           | **Metabolic flux balance (FBA).** Carbon and ATP budgets constrain every engineered pathway. You cannot over-express a product without taking flux from somewhere else.**代谢通量平衡（FBA）。** 碳源与 ATP 预算约束着每一条被改造的通路；想让产物高表达，通量必须从别处挪。                                                                                                                        |
| **Metabolic cost decides who survives.** A cheap organism carpets the grid; an expensive one goes extinct. Tuning `metabolism` was the single hardest balance problem.**代谢成本决定谁能活下来。** 代谢便宜的生物会铺满全场，昂贵的则会灭绝。`metabolism` 是整个调参中最难平衡的一项。                                                                              | **Metabolic burden.** The central practical problem in chassis engineering: a heavily-expressed construct slows host growth, and slow-growing cells get out-competed in the flask.**代谢负担（burden）。** 底盘工程最核心的实际问题：高强度表达的元件会拖慢宿主生长，长得慢的细胞在摇瓶里会被竞争淘汰。                                                                                             |
| **Generation time must be ordered.** Producers ~30 ticks, grazers ~120, predators ~250. Invert any pair and the system eats itself flat within 500 ticks.**世代时间必须有序。** 生产者约 30 tick、食草者约 120、捕食者约 250。任意一对倒过来，系统会在 500 tick 内把自己吃垮。                                                                                          | **Growth rate vs. yield trade-off.** Why production strains are induced *after* the growth phase, and why a fast-growing escape mutant takes over a bioreactor.**生长速率与产率的权衡。** 这解释了为什么生产菌株要在生长期*之后*才诱导，也解释了逃逸突变体为什么能占领发酵罐。                                                                                                                  |
| **Every individual carries a mutable genome** (10 numeric genes). Offspring drift; drift far enough from the species template and it is registered as a **new species** with a new glyph, colour and name.**每个个体都携带可突变的基因组**（10 个数值基因）。子代会漂变，漂变到与物种模板距离足够远时，就会被注册为**新物种**，获得新字形、新颜色和新名字。 | **Evolutionary instability of engineered constructs.** Plasmids get silenced, deleted, or mutated out precisely because the engineered function is costly. Genetic stability is a design requirement, not a given.**改造元件的进化不稳定性。** 质粒之所以会被沉默、丢失或突变掉，正是因为被改造的功能代价高昂。遗传稳定性是设计指标，而不是理所当然。                                               |
| **`IRRADIATE`** raises local mutation rate ×10 for a while. **`PRESERVE`** permanently archives a species into the **Codex**.**`IRRADIATE`** 在一小片区域内把突变率提高 10 倍并持续一段时间；**`PRESERVE`** 把某个物种永久存入 **Codex（图鉴）**。                                                                                     | **Directed evolution + strain banking.** Mutagenise, screen for a useful variant, then bank it. The Codex is a personal parts registry — the same logic as iGEM's Registry of Standard Biological Parts and a lab's glycerol stock collection.**定向进化 + 菌种保藏。** 诱变、筛选出有用变体、然后保种。Codex 就是一份私人元件库——与 iGEM 的标准生物元件登记库和实验室的甘油管保藏是同一套逻辑。 |
| **World Laws** randomise the physics each run (`VISCOUS`, `SCARCITY`, `RADIANT`, `TORPOR`, `PHOTOPERIOD`…). The same species thrives in one world and dies in the next.**World Laws（世界法则）** 每局随机化"物理定律"（黏滞、贫瘠、强辐射、低温、剧烈昼夜…）。同一个物种在这个世界繁盛，在下个世界灭绝。                                                   | **Context dependence.** A construct characterised in one chassis, medium or temperature often behaves completely differently in another. This is why iGEM requires characterisation data, not just a working gel photo.**语境依赖性。** 一个在某底盘／培养基／温度下表征过的元件，换个条件常常表现完全不同。这正是 iGEM 要求提交表征数据、而不只是一张跑通的胶图的原因。                            |
| **Introducing one species** (`SEED`) can trigger a **trophic cascade** two levels away, and the Chronicle will call it out by name.**只投放一个物种**（`SEED`）就可能在两个营养级之外触发**营养级联**，而 Chronicle 会点名记录下来。                                                                                                                    | **Biocontainment & ecological risk assessment.** The core of iGEM's Safety & Security requirement: engineered organisms released into a community have effects you did not design and cannot easily predict.**生物封存与生态风险评估。** iGEM 安全性要求的核心：被释放到群落中的工程生物，会产生你没有设计、也难以预测的效应。                                                                      |
| **Decomposers have an exclusive resource** (detritus from corpses) and recycle it back into the substrate. Remove them and nutrient cycling slows to a crawl.**分解者拥有专属资源**（尸体产生的腐殖质），并把它矿化回底物。移除它们，养分循环会慢到近乎停滞。                                                                                                           | **Microbial consortia & division of labour.** Designed communities work because members occupy non-overlapping niches. A "useless" member is often doing the recycling that keeps everyone else alive.**微生物群落与分工。** 人工群落之所以能运转，是因为成员占据互不重叠的生态位；那个看起来"没用"的成员，往往在做维持全局的循环工作。                                                             |
| **The biomass chart oscillates.** An autocorrelation detector reports the period in the Chronicle.**生物量曲线会振荡。** 自相关检测器会在 Chronicle 里报出周期。                                                                                                                                                                                                        | **Systems modelling.** Lotka–Volterra predator–prey dynamics is the standard teaching model, and population modelling is exactly what an iGEM Modelling sub-team does.**系统建模。** Lotka–Volterra 捕食者－猎物动力学是标准教学模型，而种群建模正是 iGEM 建模组的日常工作。                                                                                                                     |

## 3. How to play / 游戏流程

### Step 1 — Open it / 第一步：打开

**EN** Open `index.html` in any modern browser. A world is generated immediately with a random seed. There is no menu and no tutorial — the Chronicle at the bottom starts narrating straight away.
**中文** 用任意现代浏览器打开 `index.html`。程序会立刻用随机种子生成一个世界。没有菜单、没有教程——底部的 Chronicle 会马上开始叙述。

### Step 2 — Read the top bar / 第二步：读顶部状态栏

**EN** It shows the run name (e.g. `RUN-3F1A · Verdant Basin`), current **temperature** and **light** as small gauges, total energy split into *biomass* and *substrate*, and this run's **World Laws** as yellow tags. Hover a tag to see what that law does — it changes how the whole run behaves.
**中文** 这里显示本局名称（例如 `RUN-3F1A · Verdant Basin`）、当前**温度**与**光照**（小刻度条）、总能量（分为 *biomass* 生物量与 *substrate* 底物），以及本局的 **World Laws**（黄色标签）。把鼠标悬停在标签上可以看到该法则的作用——它会改变整局的手感。

### Step 3 — Learn to read a character / 第三步：学会读懂一个字符

**EN** This is the whole visual language. Four properties, four meanings:

| Property / 属性                | Meaning / 含义                                                                                                      |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| **Glyph** (which letter) | **Species.** Every species owns one character.                                                                |
| **Colour**               | **Trophic level.** green = producer, yellow = herbivore, red = predator, purple = decomposer, cyan = special. |
| **Size**                 | **Energy.** Small = starving, large = well fed and close to reproducing.                                      |
| **Opacity**              | **Age.** Faint = juvenile, solid = adult, fading = old.                                                       |

The dim characters *between* organisms are the substrate: **green dots = nutrient**, **purple dots = detritus** (corpses waiting to be decomposed).

**Hover or tap any character** to inspect that individual: its species, energy, age, metabolism, vision, what lineage it descends from, and how long its species has existed.

**中文** 这就是全部的视觉语言，四个属性对应四种含义：

| 属性                         | 含义                                                                     |
| ---------------------------- | ------------------------------------------------------------------------ |
| **字形**（是哪个字母） | **物种。** 每个物种独占一个字符。                                  |
| **颜色**               | **营养级。** 绿=生产者，黄=食草者，红=捕食者，紫=分解者，青=特殊。 |
| **字号**               | **能量。** 小=濒临饿死，大=吃饱且接近繁殖阈值。                    |
| **透明度**             | **年龄。** 淡=幼体，实=成体，再次转淡=老年。                       |

生物之间那些很暗的字符是底物：**绿色的点＝养分（nutrient）**，**紫色的点＝腐殖质（detritus，等待分解的尸体）**。

**把鼠标悬停或点击任意字符**即可查看该个体：物种、能量、年龄、代谢、视野、源自哪条谱系，以及该物种已存在多久。

### Step 4 — Watch one full cycle / 第四步：先完整看一轮周期

**EN** Before intervening, just watch. Use `1× / 2× / 4×` at the bottom right (spacebar toggles pause). Watch the **BIOMASS** chart in the right panel — three block-character lines, one per trophic level. A healthy world shows them rising and falling *out of phase*: producers peak, grazers peak a little later, predators later still, then producers crash. That phase lag is the whole point.

A typical cycle takes roughly 1000–1500 ticks, so at 4× that is about half a minute.

**中文** 在干预之前，先什么都别做，只看。用右下角的 `1× / 2× / 4×` 控制速度（空格键暂停）。注意右侧面板的 **BIOMASS** 图——三条由块字符组成的折线，分别对应三个营养级。一个健康的世界里，它们会**错相位**地起伏：生产者先达峰，食草者稍后达峰，捕食者再稍后，然后生产者崩盘。这个相位差正是整件事的核心。

一轮完整周期大约 1000–1500 tick，在 4× 速度下约半分钟。

### Step 5 — Read the Chronicle / 第五步：读 Chronicle（编年史）

**EN** The scrolling log at the bottom is the game's real narrative. It actively detects and reports:

- **Speciation** (cyan) — `A lineage of Drift Moss diverged. New species: Ashen Moss (m)`
- **Extinction** (red) — with how long the lineage survived
- **Boom / crash** (yellow / orange) — ±50% inside a sliding window
- **New dominant species** — when one passes 40% of the census
- **Trophic cascade** (white) — predators collapse, grazers surge two windows later
- **Predator–prey oscillation detected** — with the measured period
- **Mass mortality** — >30% of the standing population lost in one window
- **Echoes of your own interventions** — what changed a few hundred ticks after you acted

Speciation lines are the ones to watch for. They are deliberately rare.

**中文** 底部滚动的日志才是这个游戏真正的叙事。它会主动检测并记录：

- **物种分化**（青色）—— `A lineage of Drift Moss diverged. New species: Ashen Moss (m)`
- **灭绝**（红色）—— 并附上该谱系存活了多久
- **暴涨／崩溃**（黄／橙）—— 滑动窗口内 ±50%
- **新的优势物种** —— 某物种占比超过 40% 时
- **营养级联**（白色）—— 捕食者崩溃后两个窗口内食草者暴涨
- **检测到捕食者－猎物振荡** —— 并给出实测周期
- **大规模死亡** —— 单个窗口内损失超过 30% 的现存种群
- **你自己干预的回响** —— 在你操作几百 tick 之后，情况究竟变成了什么样

要特别留意"物种分化"那几行，它们被刻意设计得很罕见。

### Step 6 — Spend influence / 第六步：使用干预点数

**EN** You start with 10 **influence** points and regain **+1 every 6 minutes of real time**, capped at 10. This is the idle-game hook: intervention is genuinely scarce, so each one should be a hypothesis, not a reflex.

Click a tool, then click a cell on the grid.

| Tool                | Cost | Effect                                                 | Try it when…                               |
| ------------------- | ---- | ------------------------------------------------------ | ------------------------------------------- |
| `NUTRIENT`        | 1    | +50 nutrient over a 9×9 patch                         | a region has gone barren                    |
| `SEED`            | 2    | place one Codex species at that cell                   | you want to test an introduction            |
| `WARM` / `COOL` | 2    | temperature ±0.22 for 1200 ticks                      | metabolism is running too fast/slow         |
| `CULL`            | 3    | kill everything in a 9×9 patch                        | testing recovery, or removing a monoculture |
| `IRRADIATE`       | 4    | mutation rate ×10 in an 11×11 patch for 1500 ticks   | gambling for a speciation event             |
| `PRESERVE`        | 5    | archive that organism's species into the Codex forever | you found something worth keeping           |

Every intervention is written into the Chronicle, and most schedule a **follow-up** entry a few hundred ticks later reporting the measured consequence.

**中文** 你初始拥有 10 点 **influence**，并按**现实时间每 6 分钟恢复 1 点**，上限 10 点。这是挂机玩法的粘性来源：干预是真的稀缺，所以每一次干预都应该是一个假设，而不是一次条件反射。

先点选工具，再点击网格上的目标位置。

| 工具                | 消耗 | 效果                                     | 什么时候用                     |
| ------------------- | ---- | ---------------------------------------- | ------------------------------ |
| `NUTRIENT`        | 1    | 9×9 范围内养分 +50                      | 某片区域已经贫瘠               |
| `SEED`            | 2    | 在该格投放一个 Codex 中的物种            | 想测试引入一个外来种           |
| `WARM` / `COOL` | 2    | 温度 ±0.22，持续 1200 tick              | 代谢整体过快或过慢             |
| `CULL`            | 3    | 清除 9×9 范围内所有生物                 | 测试恢复能力，或清掉单一优势种 |
| `IRRADIATE`       | 4    | 11×11 范围内突变率 ×10，持续 1500 tick | 赌一次物种分化                 |
| `PRESERVE`        | 5    | 把该个体所属物种永久存入 Codex           | 你发现了值得留存的东西         |

每一次干预都会写入 Chronicle，并且大多数会在几百 tick 之后自动追加一条**回响**记录，报告实测到的后果。

> **Teaching note / 教学提示** — `IRRADIATE` is the most instructive tool. It usually produces nothing, sometimes produces a doomed variant, and occasionally produces a lineage that outcompetes its parent. That hit rate is an honest picture of mutagenesis-based directed evolution.
> `IRRADIATE` 是最有教学价值的工具。它通常什么也不产生，偶尔产出一个注定灭亡的变体，极少数时候会产出一条压过亲本的谱系。这个成功率，恰恰是诱变型定向进化的真实写照。

### Step 7 — Leave, and come back / 第七步：离开，然后回来

**EN** Close the tab. The world state is saved to `localStorage`. When you return, elapsed real time is converted at **1 second = 1 tick** (capped at **8 hours**, i.e. 28,800 ticks), the simulation fast-forwards with a progress bar, and a **FIELD REPORT** opens:

> *While you were away: 2 speciations, 1 extinction, biomass +31%.*

with a before/after population table per trophic level and the significant Chronicle entries from that period. This is the core reward loop — coming back is like opening a lab notebook someone else kept for you.

**中文** 直接关掉网页。世界状态会存入 `localStorage`。当你回来时，经过的现实时间按 **1 秒 = 1 tick** 换算（上限 **8 小时**，即 28,800 tick），模拟会带进度条快速补算，然后弹出 **FIELD REPORT（考察报告）**：

> *While you were away: 2 speciations, 1 extinction, biomass +31%.*

并附上各营养级的前后种群对照表，以及这段时间内的重要 Chronicle 条目。这是核心的回访奖励——回来的感觉，就像打开一本别人替你记了一夜的实验记录。

### Step 8 — End the run, keep the Codex / 第八步：结束本局，保留 Codex

**EN** A run ends when everything goes extinct, when you press **ARCHIVE**, or at the tick limit. You then get a **run report**: peak biomass, peak population, total species, speciations, extinctions, and the longest-surviving lineage.

Every species you observed is written into the **CODEX**, which persists across runs. Each entry stores its glyph, name, trophic level, parameters, the run it first appeared in, how long it survived, and a procedurally generated description (*"A far-sighted grazer, runs on a slow metabolism, and divides only when well fed. Long-lived."*).

**Codex species can be `SEED`ed into future worlds.** That is the meta-progression: you are assembling a strain collection across runs, and later runs let you deliberately introduce something you banked earlier.

**中文** 当所有生物灭绝、你主动按下 **ARCHIVE**、或达到 tick 上限时，本局结束。随后会给出**本局结算**：最高生物量、最高种群数、物种总数、分化次数、灭绝次数，以及存活最久的谱系。

你观察到的每一个物种都会被写入 **CODEX（图鉴）**，且跨局持久保存。每个条目记录字形、名称、营养级、参数、首次出现的局、存活时长，以及一句程序化生成的描述（例如 *"A far-sighted grazer, runs on a slow metabolism, and divides only when well fed. Long-lived."*）。

**Codex 里的物种可以在之后的世界里用 `SEED` 投放。** 这就是跨局的元进程：你在一局又一局中攒起一份自己的菌种库，并在后续局中有意识地把之前保藏的东西重新引入。

---

## 4. Controls / 操作一览

| Action / 操作                             | Control / 方式                                                                            |
| ----------------------------------------- | ----------------------------------------------------------------------------------------- |
| Inspect an organism / 查看个体            | hover or click a character / 悬停或点击字符                                               |
| Inspect a species genome / 查看物种基因组 | click its row in the SPECIES panel / 点击右侧物种列表中的一行                             |
| Speed / 速度                              | `⏸ 1× 2× 4×` buttons, or **spacebar** to pause / 按钮，或**空格键**暂停 |
| Use a tool / 使用工具                     | click the tool, then click the grid / 先点工具，再点网格                                  |
| Cancel a tool / 取消工具                  | **Esc**                                                                             |
| Open the Codex / 打开图鉴                 | **CODEX** button, top right / 右上角 CODEX 按钮                                     |
| End the run / 结束本局                    | **ARCHIVE** button, top right / 右上角 ARCHIVE 按钮                                 |
| Mobile / 手机                             | tabs switch**World / Species / Chronicle** / 用标签切换三个面板                     |

---

## 5. Files / 文件说明

```
index.html          the entire game / 游戏本体（单文件）
tools/simtest.js    survival across many seeds / 多种子存活率测试
tools/traj.js       population trajectory over time / 种群轨迹
tools/diag.js       per-tier energy & feeding diagnostics / 各营养级能量与取食诊断
tools/energy.js     verifies energy conservation / 能量守恒验证
tools/sweep.js      parameter sweeps / 参数扫描
tools/perf.js       tick-rate benchmark / 性能基准
tools/domtest.js    headless DOM test of the UI layer / UI 层无头测试
tools/deliverable.js single-file / zero-dependency self-check / 交付物自检
```
