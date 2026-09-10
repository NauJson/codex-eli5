# eli5 for Codex

Anthropic community 的 [`/eli5`](https://github.com/anthropics/claude-plugins-community/tree/main/eli5) 移植到 Codex / Agents Skills。

`$eli5 how does DNS work` 会写出一张 **大图少字** 的自包含 HTML 图解页。

原作：[Thariq Shihipar](https://github.com/anthropics/claude-plugins-community/blob/main/eli5/.claude-plugin/plugin.json)，MIT。

## 为什么不用 gist

Codex 自带的 `$skill-installer` 只认 GitHub **仓库路径**：

```text
https://github.com/<owner>/<repo>/tree/<ref>/<path-to-skill>
```

Gist 没有这个目录结构，装不进去。这个仓库就是为了让 Codex 直接装。

GitHub 上也没有现成的公开 Codex 封装——只有一些个人 dotfiles 把原文拷过去，仍带 Claude 的 `$ARGUMENTS`。

## Codex 里直装（推荐）

```text
$skill-installer install https://github.com/NauJson/codex-eli5/tree/main/eli5
```

装完重启 Codex，然后：

```text
$eli5 how does DNS work
```

## 装到全局 `~/.agents/skills`

和 Claude Code / 其它 Agents Skills 客户端共享时用这条：

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo NauJson/codex-eli5 \
  --path eli5 \
  --dest ~/.agents/skills
```

或者在 Codex 里直接说：

```text
Use $install-global-skill to install https://github.com/NauJson/codex-eli5/tree/main/eli5
```

其它客户端：

```bash
gh skill install NauJson/codex-eli5 eli5 --agent codex --scope user
npx skills add NauJson/codex-eli5 --skill eli5 -a codex -y
```

## 跟 Claude 原版的区别

| | Claude Code 原版 | 这个 Codex 端 |
|---|---|---|
| 调用 | `/eli5 <topic>` | `$eli5 <topic>` |
| 主题 | `$ARGUMENTS` | 用户消息里的主题 |
| 输出 | HTML artifact | `eli5-<slug>.html` 文件 |

原版也能装进 Codex，但 `$ARGUMENTS` 不会展开：

```text
$skill-installer install https://github.com/anthropics/claude-plugins-community/tree/main/eli5/skills/eli5
```
