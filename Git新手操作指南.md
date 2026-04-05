# Git 新手操作指南

> 作者：Yuan Hao | 生成日期：2026-04-05
> 放在桌面或项目文件夹里，忘记命令时随时翻看

---

## 一、准备工作（只需做一次）

### 1. 打开终端

- **方法一**：在任意文件夹空白处，右键 → "在终端中打开" 或 "Open in Terminal"
- **方法二**：按 `Win + R`，输入 `cmd` 或 `powershell`，回车
- **方法三**：VS Code 里按 `Ctrl + ~` 打开终端

### 2. 进入你的项目文件夹

```bash
cd C:/Users/windows/git-practice
```

> `cd` = change directory（切换目录）
> 你可以用 `ls` 查看当前文件夹里有什么文件

---

## 二、日常三件套（最常用，必须记住）

每次写完代码，走这三步：

```
git add .              → 选择要存档的文件（. 代表所有改动的文件）
git commit -m "说明"    → 存档，写一句备注说明改了什么
git push               → 上传到 GitHub
```

### 详细步骤

```bash
# 第1步：看看改了什么（可选，建议看一眼）
git status

# 第2步：选择要存档的文件
git add 文件名          # 存档某一个文件
git add .              # 存档所有改动的文件（最常用）

# 第3步：存档
git commit -m "修复了登录bug"

# 第4步：上传到 GitHub
git push
```

### 完整例子

```bash
# 你创建了一个新文件 hello.py
cd C:/Users/windows/git-practice
git add .
git commit -m "添加hello.py"
git push
```

---

## 三、从 GitHub 下载最新代码

如果你在别的电脑上改了代码，或者和别人合作，需要拉取最新版本：

```bash
git pull
```

> 建议每次开始写代码前，先 `git pull` 一下，确保本地是最新的。

---

## 四、从零开始一个新项目

如果你有一个新项目想放到 GitHub：

### 方法一：在 GitHub 上先建仓库，再克隆

1. 打开 https://github.com/new，创建新仓库
2. 复制仓库地址
3. 在终端执行：

```bash
git clone https://github.com/你的用户名/仓库名.git
cd 仓库名
# 然后就可以写代码了，写完走三件套
```

### 方法二：本地已有项目，推到 GitHub

1. 在 GitHub 上创建空仓库（不要勾选 README）
2. 在终端执行：

```bash
cd 你的项目文件夹
git init                          # 初始化 Git
git add .                         # 添加所有文件
git commit -m "第一次提交"          # 存档
git remote add origin https://github.com/你的用户名/仓库名.git
git push -u origin main           # 推送到 GitHub
```

---

## 五、常用命令速查

| 命令 | 作用 | 使用场景 |
|------|------|---------|
| `git status` | 查看当前状态 | 忘了改了什么文件时用 |
| `git log --oneline` | 查看提交历史 | 看之前存了哪些档 |
| `git diff` | 查看具体改了什么 | 提交前检查改动 |
| `git pull` | 从 GitHub 拉取最新 | 开始写代码前 |
| `git add .` | 暂存所有改动 | 最常用的 add 方式 |
| `git add 文件名` | 暂存指定文件 | 只想提交部分文件时 |
| `git commit -m "消息"` | 提交存档 | 每次改动后 |
| `git push` | 推送到 GitHub | 提交后 |
| `git clone 地址` | 克隆远程仓库 | 第一次下载项目时 |

---

## 六、常见问题

### Q: push 时弹出了登录窗口/要求输入密码？

GitHub 从 2021 年起不再支持密码登录，需要用 Personal Access Token：
1. 打开 https://github.com/settings/tokens
2. 点击 "Generate new token (classic)"
3. 勾选 `repo` 权限，生成 token
4. 密码处粘贴 token（只显示一次，记得保存）

### Q: commit 消息写错了怎么办？

```bash
git commit --amend -m "正确的消息"    # 修改最近一次提交的消息
```

### Q: 改错了想撤销？

```bash
# 还没 add（还没暂存）：
git restore 文件名                   # 恢复到上一次提交的状态

# 已经 add 了（已暂存，但还没 commit）：
git restore --staged 文件名           # 取消暂存
git restore 文件名                   # 再恢复文件内容

# 已经 commit 了（已提交，但还没 push）：
git revert HEAD                      # 撤销最近一次提交（会生成新提交）
```

### Q: 有些文件不想上传到 GitHub（比如密码、缓存）？

在项目根目录创建 `.gitignore` 文件：

```bash
# 创建 .gitignore
notepad .gitignore
```

在里面写要忽略的文件/文件夹，例如：
```
.env
node_modules/
__pycache__/
*.pyc
.DS_Store
```

### Q: 想看某个文件改了什么？

```bash
git diff 文件名                       # 看还没 add 的改动
git diff --staged 文件名              # 看 add 了但还没 commit 的改动
```

---

## 七、工作流总结图

```
┌──────────────────────────────────────────────┐
│              日常开发循环                      │
│                                              │
│   git pull        ← 拉取最新代码              │
│       ↓                                      │
│   写代码 / 改文件                              │
│       ↓                                      │
│   git status      ← 检查改了什么（可选）        │
│       ↓                                      │
│   git add .       ← 暂存所有改动               │
│       ↓                                      │
│   git commit -m   ← 存档                      │
│       ↓                                      │
│   git push        ← 上传到 GitHub             │
│       ↓                                      │
│   回到顶部，继续写代码                          │
└──────────────────────────────────────────────┘
```

---

## 八、推荐学习资源

- **Git 官方教程（中文）**：https://git-scm.com/book/zh/v2
- **交互式学习 Git**：https://learngitbranching.js.org/?locale=zh_CN
- **GitHub 官方文档**：https://docs.github.com/zh

---

> 提示：这份指南就在你的 `git-practice` 项目文件夹里，随时可以查看！
