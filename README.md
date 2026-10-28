# Novel AI Detox

**一句话简介：** 面向网文章节与场景改写的 Codex 技能，通过「控制者 + 读者子代理 + 改写工子代理」的迭代流程，在保留情节事实的前提下削弱 AI 感文风。

## 解决什么问题

AI 生成或 AI 辅助润色的小说常见问题是：对白过短、过「完成任务式」的工整功能句、缺少微表情与现场感、章末用作者旁白解释悬念而非落在场景里。本仓库不提供独立可执行程序，而是一套 **Agent 技能（Skill）** 说明：教 Codex（及同类支持 `$skill-name` 的会话）如何组织多轮 **读者批判 → 段落级改写 → 合并 → 再批判**，直到读者无法再指出具体的「AI 感」问题。

适用场景（来自技能描述）：用户要求去 AI 味、让 AI 生成的小说正文更有人味、修订章节正文，或在章节可安全切分时使用并行读者/改写子代理。

## 功能概览

| 能力 | 说明 |
| --- | --- |
| 情节约束 | 保留情节事实、人物行为与事件顺序；只改被读者标记的段落 |
| 控制者模式 | 首个启用技能的 Agent 担任控制者：编号、简报、委派、合并与终检；有子代理时不亲自改正文段落 |
| 并行读者 | 章节足够长且可切分时 spawn 多名读者（至少 2 名，长章 3–4 名），视角示例：对白、节奏与场景流、AI 痕迹与 exposition、连贯性与逻辑、过 polish 的功能句等（详见 [`references/parallel-review.md`](references/parallel-review.md)） |
| 并行改写 | 将被标记段落划分为互不重叠的归属集，每名 worker 只改自己拥有的段落 |
| 迭代终止 | 合并后重新跑读者轮，直到无法给出带段落 ID 的具体问题；「还有一点 AI 感」视为未完成 |
| 文风导向 | 减少「能力展示式」过 polish 句；对白可更暖、略松；自然段宜紧凑（技能中建议中文自然段尽量约 40 字以内，但不过度压缩）；主角在合适场景可更懒、更 swagger；章末钩子落在可见节拍而非解释 |

完整工作流、硬性规则与改写纪律见 [`SKILL.md`](SKILL.md)；并行读者/改写协议见 [`references/parallel-review.md`](references/parallel-review.md)。

## 安装

将本仓库克隆或下载到 Codex 的 **skills** 目录下，文件夹名建议为 `novel-ai-detox`（与技能名一致）。

Windows（PowerShell，与仓库原有说明一致）：

```powershell
git clone https://github.com/lishan85/novel-ai-detox.git $env:USERPROFILE\.codex\skills\novel-ai-detox
```

其他系统：请将仓库放到你当前 Codex 配置所识别的 skills 目录中的 `novel-ai-detox` 子目录；具体路径以你本地的 Codex 文档为准（本仓库未提供非 Windows 的一行命令示例）。

安装后 **新开一次 Codex 会话**，技能才会被加载。

## 使用方式

在会话中用 `$novel-ai-detox` 引用本技能。仓库中已有的 invocation 示例：

```text
Use $novel-ai-detox to revise this chapter.
```

[`agents/openai.yaml`](agents/openai.yaml) 中还定义了更完整的默认提示（`default_prompt`），大意是：以控制者工作流运行；首个 Agent 负责规划、委派、合并与终检；读者/worker 子代理负责批判与段落改写；保留情节事实；自然段保持较短；在合适时让主角更懒、更张扬。若你的客户端会读取该 YAML，可直接使用其中的 `default_prompt` 字段原文。

### 单次会话内 Agent 大致做什么

1. 控制者为段落打上稳定 ID（如 `P1`、`P2`）。
2. 整理简报：情节事实、目标语气、禁止改动项。
3. 视长度 spawn 读者子代理，收集 **带段落 ID** 的具体批判（禁止读者直接输出改写稿）。
4. 按互不重叠的段落归属 spawn worker，只返回被改写的段落。
5. 控制者合并全文，再跑读者轮，循环直至满足停止规则。
6. 输出终稿与 **变更日志**（仅列出有改动的段落）。

若无子代理能力，技能要求 **明确说明** 并退化为单 Agent 执行（控制者仍负责管理与终检角色）。

## 配置与元数据

| 文件 | 作用 |
| --- | --- |
| [`SKILL.md`](SKILL.md) | 技能主文档：YAML frontmatter（`name: novel-ai-detox`）+ 工作流与非协商规则 |
| [`agents/openai.yaml`](agents/openai.yaml) | 界面展示名、短描述与 `default_prompt` |
| [`references/parallel-review.md`](references/parallel-review.md) | 读者/改写角色、合并规则、常见 AI 感检查项与改写手法 |

本仓库 **没有** 独立的 `environment.json`、API 密钥或运行时配置文件；行为完全由上述 Markdown/YAML 驱动 Agent 遵循。

## 目录结构

```text
.
├── README.md                 # 本文件
├── SKILL.md                  # Codex 技能定义（工作流与规则）
├── agents/
│   └── openai.yaml           # 展示名与默认提示
└── references/
    └── parallel-review.md    # 并行读者/改写协议与检查清单
```

## 已知限制

- **依赖 Agent 平台能力**：完整流程假设可 spawn 读者/worker 子代理；不可用时只能按技能说明做单 Agent 降级。
- **非自动化批处理工具**：没有 CLI、没有 guaranteed 的固定输出格式校验；效果取决于模型与会话是否严格遵循 `SKILL.md`。
- **文体预设**：规则明显针对 **中文网文/场景改写**（如自然段长度、主角语气、章末钩子），其他语种或文体需自行调整简报，技能未单独描述。
- **人工终检**：技能要求 vague 反馈（如「还是像 AI」且未指向段落）应被拒绝；实际仍建议作者自行通读终稿。
- **许可证**：仓库 **尚未附带** `LICENSE` 文件；使用与分发前请与维护者确认授权方式。

## 相关链接

- 上游仓库：`https://github.com/lishan85/novel-ai-detox`

---

英文简要说明见历史 commit；当前 README 以中文为主，技术细节以 [`SKILL.md`](SKILL.md) 英文原文为准。

## License

This project is licensed under the [MIT License](LICENSE).
