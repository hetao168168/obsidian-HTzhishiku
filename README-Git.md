# Obsidian ACT 知识库 · Git 版本管理说明

> 本文件由 WorkBuddy 在启用仓库版本控制时生成，记录提交规范、分支模型与远程同步方式。
> 适用仓库：`E:\何涛的知识库\何涛的知识库`

## 1. 分支模型（单主干）

| 分支 | 用途 |
|------|------|
| `master` | 主分支，日常笔记与配置自动提交的目标（obsidian-git 默认） |

- 大范围重构（目录结构调整、批量改名、插件大改）时，可临时开 `feature/xxx` 分支，验证无误后合并回 `master`。
- 个人知识库不引入 `develop` / `release` 等复杂模型，**单主干最省心、最不易出错**。

## 2. 提交规范（Conventional Commits）

格式：`<type>(<scope>): <subject>`

| type | 含义 |
|------|------|
| `feat` | 新增笔记 / 新内容 |
| `fix` | 修正错误内容 |
| `docs` | 仅说明 / 文档变更 |
| `chore` | 配置、插件、仓库维护 |
| `refactor` | 重构（不改内容含义） |
| `style` | 格式调整 |
| `perf` | 性能优化 |

- scope 可选：`笔记` / `插件` / `模板` / `配置` / `同步`
- subject 用祈使句、简洁（≤50 字）
- 已配置 `.gitmessage` 模板，`git commit` 时自动带提示
- 示例：
  - `chore(配置): 完善 .gitignore 排除 Obsidian 缓存`
  - `feat(笔记): 新增《懂懂学定投》读书笔记`

## 3. .gitignore 要点

**忽略（本地易变 / 可重建）：**
- `.obsidian/workspace.json`、`.obsidian/workspace`（UI 布局状态）
- `.obsidian/cache`（索引缓存，体积大可重建）
- `.obsidian/.obsidian-sync-helper-backup/`（同步助手备份历史）
- `.trash/`、`*.tmp`、`.DS_Store`、`Thumbs.db`

**保留（便于换机恢复）：**
- `.obsidian/plugins/*/main.js`、`manifest.json`、`styles.css`
- `.obsidian/community-plugins.json`（插件启用列表）

## 4. 远程同步

关联远程仓库后（URL 由用户配置）：

```bash
git remote add origin <仓库URL>
git push -u origin master      # 首次推送并绑定上游
git push                       # 之后日常推送
```

- obsidian-git 插件内可在「设置 → 自动推送」中启用定时/自动推送。
- 建议远程仓库设为**私有**，避免笔记内容外泄。

## 5. 常用命令

```bash
git status                 # 查看变更
git add -A && git commit   # 按 .gitmessage 模板填写后提交
git push                   # 推送到远程
git log --oneline -10      # 查看最近提交
git pull                   # 从远程拉取（多设备同步时）
```

> 多设备协作提示：先 `git pull` 再编辑，避免产生冲突。
