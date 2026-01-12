# 🛠️ 已安装工具使用指南

> 你的终端已经升级！这些工具让命令行更强大、更美观

---

## ✅ 已安装的工具

### 1. **bat** - cat命令的超级增强版
- 📍 位置：`~/bin/bat`
- ✨ 特点：语法高亮、行号、Git集成
- 📦 版本：0.24.0

### 2. **ripgrep (rg)** - 超快的搜索工具
- 📍 位置：`~/bin/rg`
- ✨ 特点：速度极快、支持正则、自动忽略.gitignore
- 📦 版本：14.1.1

---

## 🚀 使用方法

### **bat - 查看文件**

```bash
# 基本用法
bat 文件名

# 查看README
bat README.md

# 只显示特定行
bat README.md --line-range 1:10

# 显示所有（包括不可打印字符）
bat -A 文件名

# 纯文本模式（无装饰）
bat --plain 文件名

# 查看多个文件
bat file1.md file2.md
```

**实际例子：**
```bash
cd ~/my-first-github-project
bat README.md
bat awesome-projects.md
bat hidden-gems.md
```

---

### **ripgrep (rg) - 搜索内容**

```bash
# 基本搜索
rg "关键词"

# 在当前目录搜索
rg "GitHub" .

# 忽略大小写
rg -i "github"

# 只显示文件名
rg -l "GitHub"

# 显示行号
rg -n "GitHub"

# 搜索特定类型文件
rg "GitHub" -t md

# 正则表达式搜索
rg "Git(Hub|Lab)"

# 显示上下文（前后各2行）
rg -C 2 "GitHub"
```

**实际例子：**
```bash
cd ~/my-first-github-project

# 搜索所有包含"GitHub"的地方
rg "GitHub"

# 搜索所有.md文件中的"项目"
rg "项目" -t md

# 搜索"AI"或"Web3"
rg "AI|Web3"
```

---

## 💡 实用技巧

### **bat技巧**

#### 1. 设置别名（更方便）
在 `~/.zshrc` 中添加：
```bash
alias cat='bat'  # 用bat替代cat
```

#### 2. 查看Git diff
```bash
git diff | bat
```

#### 3. 管道使用
```bash
curl https://example.com | bat -l html
```

---

### **ripgrep技巧**

#### 1. 排除特定目录
```bash
rg "关键词" --glob '!node_modules'
```

#### 2. 只搜索特定文件
```bash
rg "关键词" --glob '*.md'
```

#### 3. 统计匹配数
```bash
rg "GitHub" -c
```

#### 4. 替换grep
在 `~/.zshrc` 中添加：
```bash
alias grep='rg'
```

---

## 🎯 常见使用场景

### **场景1：查看代码文件**
```bash
# 传统方式
cat script.py

# 新方式（带语法高亮）
bat script.py
```

### **场景2：搜索项目中的TODO**
```bash
# 传统方式
grep -r "TODO" .

# 新方式（更快更美）
rg "TODO"
```

### **场景3：查看日志文件**
```bash
# 传统方式
tail -f log.txt

# 新方式
bat --paging=never -f log.txt
```

### **场景4：搜索并查看结果**
```bash
# 找到包含"error"的文件
rg -l "error"

# 查看其中一个文件
bat $(rg -l "error" | head -1)
```

---

## 🔧 配置优化

### **bat配置**

创建配置文件 `~/.config/bat/config`：
```bash
# 主题
--theme="Monokai Extended"

# 显示行号
--style="numbers,changes,header"

# 分页器
--paging=auto
```

### **ripgrep配置**

创建配置文件 `~/.ripgreprc`：
```bash
# 智能大小写
--smart-case

# 显示行号
--line-number

# 最大列宽
--max-columns=150
```

然后在 `~/.zshrc` 中添加：
```bash
export RIPGREP_CONFIG_PATH="$HOME/.ripgreprc"
```

---

## 📊 性能对比

### **搜索速度对比**
```bash
# grep（传统）
time grep -r "GitHub" .

# ripgrep（新）
time rg "GitHub"
```

ripgrep通常快**5-10倍**！

---

## 🎨 主题定制

### **bat主题**

查看可用主题：
```bash
bat --list-themes
```

临时使用主题：
```bash
bat --theme="Dracula" README.md
```

设置默认主题（在 `~/.zshrc`）：
```bash
export BAT_THEME="Dracula"
```

---

## 🆚 对比表

| 功能 | 传统工具 | 新工具 | 优势 |
|------|---------|--------|------|
| 查看文件 | `cat` | `bat` | 语法高亮、行号、Git集成 |
| 搜索内容 | `grep` | `rg` | 速度快5-10倍、更智能 |
| 查看日志 | `tail` | `bat -f` | 更美观 |
| 搜索代码 | `grep -r` | `rg` | 自动忽略.gitignore |

---

## 🚀 下一步

### **推荐安装（如果有Homebrew）：**
```bash
brew install fzf        # 模糊搜索
brew install fd         # find替代品
brew install exa        # ls替代品
brew install starship   # 终端美化
brew install lazygit    # Git可视化
```

### **不需要Homebrew的替代方案：**
我可以帮你下载这些工具的预编译版本！

---

## 💡 快速开始

**打开新的终端窗口**，然后试试：

```bash
# 1. 进入项目目录
cd ~/my-first-github-project

# 2. 用bat查看文件
bat README.md

# 3. 搜索内容
rg "GitHub"

# 4. 查看所有.md文件
bat *.md

# 5. 搜索并统计
rg "项目" -c
```

---

## 🎓 学习资源

- [bat GitHub](https://github.com/sharkdp/bat)
- [ripgrep GitHub](https://github.com/BurntSushi/ripgrep)
- [ripgrep用户指南](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md)

---

**更新日期：** 2026-01-12
**作者：** h2548

> 💡 记住：这些工具在**新的终端窗口**中才能使用！
>
> 🔄 如果不生效，运行：`source ~/.zshrc`
