# 暖卡铸造 · 温暖治愈调色板库 + HTML 模板

life-council 的 Phase 4 用此文件铸卡。产物是**单页自适应高度的 HTML 暖卡**（不是会裁切的固定尺寸 PNG）。核心原则：**配色随文案的情绪内核变化，但永远落在"温暖治愈"家族内**——每次生成不重样，都不会跑成冷色或廉价感。

## 一、选色规则（先选调色板）

会诊合成出核心洞见后，扫描它的**情绪内核**，匹配下表中**情绪最贴近的一套**。拿不准就用「破晓」。

| 调色板 | 情绪内核 / 触发信号 |
|--------|--------------------|
| 破晓 dawn | 转变、新生、希望、重新出发、"换挡/路口/天亮" |
| 暖阳 amber | 丰盛、感恩、温暖、被照亮、知足 |
| 暮光 dusk | 释怀、告别、放下、沉静、与过去和解 |
| 陶土 clay | 疗愈、自我接纳、脆弱、慢下来、允许 |
| 暖苔 sage | 平和、扎根、沉淀、长期、回到本心 |
| 蜜桃 peach | 柔软、勇气、被爱、亲密、向前一点点 |

## 二、6 套调色板（CSS 变量值）

每套给出：`--bg1/--bg2/--bg3`（背景渐变）、`--ink/--ink-soft/--ink-dim`（文字）、`--accent/--accent-soft`（主点缀）、`--act/--act-bg`（行动框）、`--rule`、`--glow`（顶部柔光）。

```
/* 破晓 dawn */
--bg1:#FFF7EF; --bg2:#FDEEE2; --bg3:#F7E2D4;
--ink:#3B2E27; --ink-soft:#7C6A5D; --ink-dim:#A8978B;
--accent:#C9743D; --accent-soft:#E5A876;
--act:#7C8A66; --act-bg:#EDEFE2; --rule:#EAD9C9; --glow:#FFE9C8;

/* 暖阳 amber */
--bg1:#FFF9EC; --bg2:#FDF1D8; --bg3:#F7E6BE;
--ink:#3E3220; --ink-soft:#7E6E4F; --ink-dim:#A99A78;
--accent:#C99A2E; --accent-soft:#E6C46B;
--act:#8A7A4A; --act-bg:#F2EAD2; --rule:#EBDFBE; --glow:#FFEFC0;

/* 暮光 dusk */
--bg1:#FBF2EE; --bg2:#F4E4E0; --bg3:#EAD2CF;
--ink:#3A2C2C; --ink-soft:#7A6260; --ink-dim:#A89492;
--accent:#B66A6A; --accent-soft:#D9A0A0;
--act:#84736E; --act-bg:#EDE6E2; --rule:#E6D2CD; --glow:#F6D9CE;

/* 陶土 clay */
--bg1:#FBF3EE; --bg2:#F6E6DC; --bg3:#EFD6C6;
--ink:#3D2E26; --ink-soft:#7E665A; --ink-dim:#AA968A;
--accent:#BE6E4E; --accent-soft:#DDA383;
--act:#8A7D5E; --act-bg:#F0E8D8; --rule:#EAD7C7; --glow:#FBDFC8;

/* 暖苔 sage */
--bg1:#F8F6EC; --bg2:#EEF0DE; --bg3:#E2E6CC;
--ink:#33352A; --ink-soft:#6A6E58; --ink-dim:#9AА087;
--accent:#7E8B5A; --accent-soft:#A9B47E;
--act:#9A7B4E; --act-bg:#F2EBD6; --rule:#DDE0C8; --glow:#EAEEC8;

/* 蜜桃 peach */
--bg1:#FFF6F1; --bg2:#FDE8DF; --bg3:#F9D8CB;
--ink:#3E2D28; --ink-soft:#80645B; --ink-dim:#AE948B;
--accent:#E0865C; --accent-soft:#F0B393;
--act:#86927A; --act-bg:#EEEDE3; --rule:#F0D9CD; --glow:#FFDFCB;
```

> 微变体（让同一调色板也不完全雷同）：可在所选调色板基础上，把 `--accent` 的色相微调 ±8°、或在两套相邻调色板间取中间值。不必每次都精确照抄。

## 三、HTML 模板

把下面模板的 `__VAR__` 占位替换后写入 `~/Downloads/{标题}.html`，再用 ljg-card 的 capture.js 截全图（fullpage）得 PNG。

- 字体：`霞鹜文楷 LXGW WenKai`（温暖、略手写），CDN：`https://cdn.jsdelivr.net/npm/lxgw-wenkai-webfont@1.7.0/style.css`
- 结构：眉标（委员会署名）→ 标题 → 柔光分隔 → 正文（highlight 金句 / 普通段 / h2 小节 / prompt 行动框 / closing 渐变收束句）→ 落款（导师名单）
- 必须自适应高度（不固定 px 高度，避免裁切）；含 `prefers-reduced-motion`；载入逐行浮现。

模板骨架见同目录 `warm-card-template.html`（直接读取、替换变量）。变量清单：
- `__TITLE__` 卡片标题（4-6字，凝练洞见，如"换挡的路口"）
- `__EYEBROW__` 眉标（默认"人生顾问委员会 · 为你会诊"）
- `__BODY__` 正文 HTML（用 `<p class="highlight">`金句 / `<p>`普通 / `<h2>`小节 / `<p class="prompt">`行动 / `<p class="closing"><span class="glow">…</span></p>`收束）
- `__MENTORS__` 落款导师名单（如"稻盛和夫 · 弗兰克尔 · 芒格 · 乔布斯"）
- 6 个调色板变量块（整段替换 `:root` 内 `/* PALETTE */` 区）

## 四、截图命令

```bash
node ~/.claude/skills/ljg-card/assets/capture.js "~/Downloads/{标题}.html" "~/Downloads/{标题}.png" 800 0 fullpage
```
（宽 800、高 0 + fullpage = 按内容自适应全高，不裁切。）

## 五、铸卡内容准则

- 卡片**只放最戳人的洞见 + 那一步行动 + 收束金句**，不放会诊全过程。
- 金句 ≤ 25 字，独立成行；行动框放"明天能做的那一句"。
- 收束句用渐变色（`.glow`），是整张卡的情感落点。
- 替第三方会诊的卡：只含当事人主动分享过的困惑，不含任何私下评价/打探信息。
