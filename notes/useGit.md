# 🧰 GitHub Desktop + Git 命令使用指南（精简版）

## ✅ 1. 精简使用流程（每日开发建议）

1. 打开 GitHub Desktop，点击 `Fetch origin` 检查远程是否更新
2. 如果有远程更新：
   - 点击 `Repository > Open in Terminal`
   - 执行命令：`git pull --rebase origin main`
3. 回到 GitHub Desktop，正常开发、提交 (`Commit to main`)
4. 完成功能后点击 `Push origin` 上传你的更改

---

## ❗ 2. 常见错误分析及解决方法

| 问题描述                          | 解决办法                                                     |
| --------------------------------- | ------------------------------------------------------------ |
| `error: failed to push some refs` | 执行 `git pull --rebase origin main`，再重新 push            |
| `CONFLICT` 冲突错误               | 手动修改冲突文件，保存后执行：`git add . && git rebase --continue` |
| GitHub Desktop 无法点击 Pull      | 打开终端，手动 `git pull --rebase origin main`               |
| 提示 `non-fast-forward` 拒绝推送  | 远程有更新未同步，需先 pull                                  |

---

## 🧠 3. 常用命令推荐表

| 功能说明         | Git 命令                        |
| ---------------- | ------------------------------- |
| 查看当前状态     | `git status`                    |
| 同步远程更新     | `git pull --rebase origin main` |
| 添加改动         | `git add .`                     |
| 提交更改         | `git commit -m "说明"`          |
| 推送到远程       | `git push origin main`          |
| 创建新分支       | `git checkout -b feature/xxx`   |
| 切换到主分支     | `git checkout main`             |
| 查看提交记录     | `git log --oneline`             |
| 查看远程仓库地址 | `git remote -v`                 |

---

## ⚠️ 4. 避免事项（项目安全保障）

- ❌ 不要直接 `git push --force`，除非你完全清楚风险
- ❌ 不要在未同步远程更新的情况下直接推送
- ✅ 每次开发前先 `Fetch` 或 `Pull` 保证一致性
- ✅ Unity 项目应配置 `.gitignore`，避免上传临时/自动生成文件

