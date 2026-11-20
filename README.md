# ccd · 参考图生图提示词 Skill

[中文](#中文) · [English](#english)

---

## 中文

### 这是什么

`ccd` 默认根据**人物参考图**撰写一条完整、可直接复制的中文生图提示词，也支持图片反推和已有提示词改写。人物的五官、发色、肤色、身材比例和可见纹身以人物参考图为准。未指定画风时使用 2000 年代便携 CCD 相机的直闪质感。

- 暗背景，机顶直闪，亮度随距离快速衰减
- 真实肤质：毛孔、细小汗毛、局部水光，不磨皮
- 低动态范围、数字噪点、粗颗粒、深黑位

提示词从 `人物：` 和适用的 `身材：` 开始，有可见纹身时单列 `纹身：`，再按画面需要写表情、姿态、服装、场景和摄影。每个目标画面用一个代码块，小标题放在代码块外，方便复制。

这个 Skill **只输出文字**，不会替你调用任何生图接口或花钱。

### 安装

**最简单：交给你的 Agent。** 把下面这段话复制给 Claude Code（或 Codex），它会自己装好：

```
帮我安装这个 Skill：https://github.com/zhejian1111/ccd-skill
把它克隆到 ~/.claude/skills/ccd（如果你是 Codex，就放到 ~/.codex/skills/ccd），装好后告诉我怎么用。
```

装好后开一个新对话就能用。

**手动安装：** 需要已安装 Claude Code。把整个文件夹放到 `~/.claude/skills/ccd/`，保证 `~/.claude/skills/ccd/SKILL.md` 存在即可。

```bash
git clone https://github.com/zhejian1111/ccd-skill.git ~/.claude/skills/ccd
```

- 只想在某个项目里用：放到项目里的 `.claude/skills/ccd/`。
- 不用 git：下载 zip，解压后把文件夹改名为 `ccd` 放进 `~/.claude/skills/`。
- 装好后开一个新的 Claude Code 会话，输入 `/ccd` 能看到它就说明装上了。
- Codex 用户：放到 `~/.codex/skills/ccd/`，`agents/openai.yaml` 是给 Codex 用的界面信息。

### 使用

**参考图生图（默认）**。上传人物参考图，输入下方命令。也可以一起指定新的场景、服装、姿势或画风。

```
/ccd
```

**图片反推**。只上传要反推的图也可以直接得到完整提示词。妆容、服装、配饰、表情和姿势按源图写；源图人物的发型、发色、刘海、发长、五官、外貌、身材和纹身不会被当成目标人物特征，提示词会明确要求它们严格跟随生图时另附的人物参考图。姿态会拆解头身方向、肩线、躯干倾斜、左右四肢关节、手指动作、接触关系和支撑点。也可以现在就提供人物图，例如“图 1 用于反推画面，图 2 用作人物参考”。

**改写已有提示词**。粘贴旧提示词，并附上要使用的人物参考图。未附人物图时，沿用旧提示词中已给出的人物特征。

**局部修改**：在上一条结果的基础上说"外套换成黑色皮夹克，全给我"，它会交付修改后的**整条**提示词，而不是只给一个片段。

**几条默认行为**：

- 默认不写尺寸和画幅比例，由你在生图平台上自己设。
- 默认不附长串反向提示词。
- 四肢动作按人物自身的左右写，例如“人物的左手扶住椅背，人物的右腿屈膝”；反推时不使用“另一只手”“双手放在身前”等模糊说法。
- 保留参考图中的面部遮挡和原有取景。想改成清晰露脸的构图时，可以补一张同一人物的清晰脸部参考。
- 生图时把人物参考图和成品提示词一起提交。
- 默认省略界面和水印。可辨认的纹身字样属于人物外观，可以保留。

### 示例

输入：一张深夜便利店门口的随手抓拍 + `/ccd`

输出（节选格式，小标题在代码块外）：

**深夜便利店门口的直闪抓拍**

```
人物：成年女性，严格以随提示词上传的人物参考图为唯一外貌与身体比例依据。保留参考图中的圆润下颌、平直眉、微微下垂的外眼角、圆鼻尖和较薄的上唇。齐下巴的深棕色短发偏分，耳垂戴小银圈耳环。

身材：保留人物参考图的肩宽、胸廓和腰腹长度，维持宽松衣物下可辨认的自然轮廓。保持原有身体体积和比例，不放大胸臀，不收窄腰部。

纹身：右前臂外侧靠近腕部保留参考图中的小枝叶纹身，黑色细线，枝梢朝向肘部，纹样随着前臂转动自然改变透视，保留原有落点和大小。

皮肤：保留参考图中的暖褐肤色、细腻毛孔和自然色泽变化，鼻尖和颧骨上方有直闪形成的局部高光。

表情：嘴角轻轻上扬，像是刚被朋友叫住，视线直接看向镜头，眼神松弛。

姿态：站在便利店玻璃门外，身体微微侧向画面右侧。人物的左手插在外套口袋里，人物的右手举着一罐冰咖啡贴在下巴旁，罐身挂着细小水珠。

服装：宽松的深灰色连帽卫衣外套，厚实棉质，右袖挽到前臂中段，露出靠近手腕的纹身。内搭白色圆领 T 恤。

场景：深夜街边便利店门口，玻璃门后是模糊的货架和冷白日光灯，门外地面潮湿，反射零星灯光；画面左侧边缘露出一辆自行车的车把。

光线：整体环境极度昏暗，小型数码相机的近轴直闪直接打在人物正面，脸和咖啡罐清晰，身后玻璃上留下一个小小的闪光反射点；亮度随距离快速衰减，背景比人物暗2—3档，店内冷光只作为微弱的边缘光。

构图：齐腰中景，略高于平视的机位，人物位于画面中央偏左，玻璃门的竖直边框形成纵向线条。

相机参数：20毫米广角定焦镜头，光圈f/1.8，焦点在眼睛，背景货架保留可辨轮廓。

画面质感：2000年代日系便携CCD低光抓拍，动态范围有限，高光略溢出，轻微柔焦，明显数字噪点与粗颗粒，黑位压得很深，暖调区域白平衡略偏。皮肤、棉布、铝罐和潮湿地面各自保留不同的反射特征。
```

### 自定义

- 人物、身材和纹身的描写规则与示例见 [人物保真模板](references/defaults.md)。
- 光线、相机参数和画面质感也在 `references/defaults.md` 的「固定摄影基盘」，想换风格就改这一段。

### 文件结构

```
ccd/
├── SKILL.md                 # 入口：读图规则、交付格式、自查
├── references/
│   └── defaults.md          # 人物保真模板和 CCD 摄影默认
└── agents/openai.yaml       # Codex 界面信息（Claude Code 不读）
```

### 致谢与许可

由 [True JPEG](https://truejpeg.com) 整理，一个 AI 写实人像提示词画廊。MIT 许可，见 [LICENSE](LICENSE)。

---

## English

### What it is

`ccd` writes a copy-ready Chinese image-generation prompt to use with a character reference image. It can also reverse an image or rewrite an existing prompt using a separate character reference. Facial features, hair color, skin tone, body proportions, and visible tattoos follow the character reference. The default style is 2000s point-and-shoot CCD photography in low light.

- dark background, direct on-axis flash with fast falloff
- real skin texture: pores, fine vellus hair, local sheen, no airbrushing
- limited dynamic range, digital noise, coarse grain, crushed blacks

Portrait prompts begin with `人物` (subject) and `身材` (body), when applicable, followed by `纹身` (tattoos) if any are visible. Each target image gets a code block with a short title above it.

The Skill **only writes text**. It never calls an image API or spends money.

### Install

**Easiest: let your agent do it.** Paste this into Claude Code (or Codex):

```
Install this Skill: https://github.com/zhejian1111/ccd-skill
Clone it to ~/.claude/skills/ccd (for Codex, use ~/.codex/skills/ccd), then tell me how to use it.
```

Start a new session afterwards and it's ready.

**Manual install:** requires Claude Code. Put the folder at `~/.claude/skills/ccd/` so that `~/.claude/skills/ccd/SKILL.md` exists.

```bash
git clone https://github.com/zhejian1111/ccd-skill.git ~/.claude/skills/ccd
```

- Project-only: put it in `.claude/skills/ccd/` inside the project.
- Without git: download the zip, rename the folder to `ccd`, move it into `~/.claude/skills/`.
- Start a new Claude Code session; if `/ccd` shows up, it's installed.
- Codex: use `~/.codex/skills/ccd/`; `agents/openai.yaml` is Codex UI metadata.

### Usage

- **Write a prompt from a reference (default).** Upload a character reference and invoke the skill. You can specify a new scene, outfit, pose, or visual style.
- **Reverse an image.** A source image is enough. The prompt keeps its makeup, outfit, accessories, expression, and pose. It directs the generator to follow the hairstyle, facial features, appearance, body proportions, and visible tattoos in the character reference you attach at generation time. You can also provide the character reference upfront.
- **Rewrite a prompt.** When rewriting text without a character reference, the skill retains the supplied character traits unless asked to prepare the prompt for a separate reference.
- **Partial edits:** "swap the hoodie for a black leather jacket, give me the full prompt" returns the whole updated prompt, not a fragment.

Existing framing and face occlusion are preserved by default. Limb positions and actions use the subject's own left and right. Submit the character reference alongside the finished prompt. Set the size and aspect ratio in your generator as needed.

See the Chinese section above for a full example output.

### Customize

The [reference guide](references/defaults.md) includes a character, body, and tattoo template. The same guide contains the default lighting, camera, and texture settings.

### Credits & license

Curated by [True JPEG](https://truejpeg.com), an AI realistic-portrait prompt gallery. MIT licensed, see [LICENSE](LICENSE).
