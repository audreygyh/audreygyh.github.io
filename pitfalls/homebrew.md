<!--
title: "macOS 安装 Homebrew 全流程（使用清华源）"
date: 2025-06-11
tags: [Homebrew, Mac, 清华镜像, 技术博客]
-->


# 💡 macOS 安装 Homebrew 全流程（避开官方脚本 + 使用清华镜像加速）【超详细实录】

> 📅 时间：2025年6月  
> 💻 设备：Intel 架构 MacBook Pro  
> 🚧 目标：跳过官方安装脚本，使用清华源手动配置 Homebrew（适合 GitHub 访问受限情况）

---

## 🧹 Step 1. 清理可能存在的旧安装

```bash
sudo rm -rf /usr/local/Homebrew
sudo rm -rf /Library/Developer/CommandLineTools
```

---

## 📦 Step 2. 重新安装 Command Line Tools（Xcode 工具链）

```bash
xcode-select --install
```

或手动下载：[https://developer.apple.com/download/all/](https://developer.apple.com/download/all/)

---

## 🚫 Step 3. 避开官方安装脚本

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

（常常失败，因此跳过）

---

## 🪞 Step 4. 使用清华源安装 Homebrew

```bash
git clone https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git /usr/local/Homebrew

echo 'eval "$(/usr/local/Homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/usr/local/Homebrew/bin/brew shellenv)"
brew -v
```

---

## 🌊 Step 5. 替换软件源为清华镜像

```bash
git -C "$(brew --repo)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
git -C "$(brew --repo homebrew/cask)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask.git
brew update
```

---

## 🧱 Step 6. 常见问题记录

### 🐌 问题1：卡在 "Updating Homebrew..."

- 原因：默认使用 GitHub 源，国内访问慢
- 解决：替换为清华镜像

### ❌ 问题2：ruby 下载失败

```text
Error: Failed to download ruby from ...
```

- 原因：网络中断或限速
- 解决：等网络恢复，或使用清华源继续尝试

### ❌ 问题3：core 仓库找不到

```bash
brew tap homebrew/core
git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
```

---

## ✅ Step 7. 验证安装

```bash
brew doctor
```

---

## ✍️ 结语：适合谁使用这种方式？

- GitHub 下载困难
- 想掌控流程
- 编写部署脚本需求

> ⚠️ Apple Silicon 用户请将 `/usr/local/` 替换为 `/opt/homebrew/`。

