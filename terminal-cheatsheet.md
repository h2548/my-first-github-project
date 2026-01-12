# 🚀 终端快捷命令速查表

> 已配置的快捷命令和实用技巧

---

## ⚡ Git快捷命令

| 快捷命令 | 完整命令 | 说明 |
|---------|---------|------|
| `gs` | `git status` | 查看状态 |
| `ga .` | `git add .` | 添加所有文件 |
| `gc "消息"` | `git commit -m "消息"` | 提交 |
| `gp` | `git push` | 推送 |
| `gl` | `git log --oneline --graph` | 美化日志 |

### 使用示例：
```bash
# 完整流程
gs              # 查看状态
ga .            # 添加文件
gc "更新文档"   # 提交
gp              # 推送到GitHub
```

---

## 📁 目录导航

| 快捷命令 | 完整命令 | 说明 |
|---------|---------|------|
| `ll` | `ls -lhG` | 详细列表（带颜色） |
| `la` | `ls -lahG` | 显示所有文件（包括隐藏） |
| `..` | `cd ..` | 返回上级目录 |
| `...` | `cd ../..` | 返回上上级目录 |
| `~` | `cd ~` | 回到主目录 |

---

## 🌤️ 实用工具

| 快捷命令 | 说明 |
|---------|------|
| `weather` | 查看兰州天气 |
| `c` | 清屏 |
| `h` | 查看历史命令 |

---

## 💡 终端技巧

### 1. 查看天气
```bash
weather
# 或者查看其他城市
curl wttr.in/北京?lang=zh
curl wttr.in/上海?lang=zh
```

### 2. 搜索历史命令
```bash
# 按 Ctrl+R，然后输入关键词
# 例如：搜索 "git"
```

### 3. 快速编辑命令
```bash
# 按 Ctrl+A：跳到行首
# 按 Ctrl+E：跳到行尾
# 按 Ctrl+U：删除光标前的内容
# 按 Ctrl+K：删除光标后的内容
# 按 Ctrl+W：删除前一个单词
```

### 4. 查看文件内容
```bash
cat 文件名           # 查看整个文件
head 文件名          # 查看前10行
tail 文件名          # 查看后10行
tail -f 文件名       # 实时查看文件更新
```

### 5. 查找文件
```bash
find . -name "*.md"  # 查找所有.md文件
find . -type f       # 查找所有文件
find . -type d       # 查找所有目录
```

### 6. 搜索文件内容
```bash
grep "关键词" 文件名
grep -r "关键词" .   # 递归搜索当前目录
```

---

## 🎨 终端美化

### 彩色输出
```bash
# ls已经配置了彩色输出
ls -G

# grep彩色输出
grep --color=auto "关键词" 文件名
```

### 自定义提示符
在 `~/.zshrc` 中添加：
```bash
# 简洁提示符
PS1='%F{cyan}%~%f $ '

# 带Git分支的提示符
autoload -Uz vcs_info
precmd() { vcs_info }
zstyle ':vcs_info:git:*' formats '%F{yellow}(%b)%f '
setopt PROMPT_SUBST
PS1='%F{cyan}%~%f ${vcs_info_msg_0_}$ '
```

---

## 📚 常用命令速查

### 文件操作
```bash
cp 源文件 目标文件    # 复制
mv 源文件 目标文件    # 移动/重命名
rm 文件名            # 删除文件
rm -rf 目录名        # 删除目录（危险！）
mkdir 目录名         # 创建目录
touch 文件名         # 创建空文件
```

### 查看系统信息
```bash
pwd                 # 当前目录
whoami              # 当前用户
date                # 当前时间
df -h               # 磁盘使用情况
du -sh *            # 当前目录各文件大小
top                 # 进程监控（按q退出）
```

### 网络相关
```bash
ping google.com     # 测试网络
curl 网址           # 下载/查看网页
wget 网址           # 下载文件
ifconfig            # 查看网络配置
```

---

## 🔧 进阶技巧

### 1. 管道和重定向
```bash
# 管道：将一个命令的输出传给另一个命令
ls -l | grep ".md"

# 重定向：保存输出到文件
ls -l > 文件列表.txt
echo "内容" >> 文件.txt  # 追加

# 错误重定向
命令 2> 错误.log
命令 &> 所有输出.log
```

### 2. 后台运行
```bash
命令 &              # 后台运行
jobs                # 查看后台任务
fg                  # 将后台任务调到前台
Ctrl+Z              # 暂停当前任务
bg                  # 继续后台运行
```

### 3. 命令组合
```bash
# 顺序执行（无论成功失败）
命令1 ; 命令2

# 只有前一个成功才执行下一个
命令1 && 命令2

# 前一个失败才执行下一个
命令1 || 命令2
```

### 4. 别名管理
```bash
# 查看所有别名
alias

# 临时创建别名
alias mycommand='ls -la'

# 删除别名
unalias mycommand
```

---

## 🎯 Git工作流速查

### 日常工作流
```bash
# 1. 查看状态
gs

# 2. 添加文件
ga .                # 添加所有
ga 文件名           # 添加单个

# 3. 提交
gc "提交说明"

# 4. 推送
gp

# 5. 查看日志
gl
```

### 分支操作
```bash
git branch                    # 查看分支
git branch 分支名             # 创建分支
git checkout 分支名           # 切换分支
git checkout -b 分支名        # 创建并切换
git merge 分支名              # 合并分支
git branch -d 分支名          # 删除分支
```

### 撤销操作
```bash
git checkout -- 文件名        # 撤销工作区修改
git reset HEAD 文件名         # 撤销暂存
git reset --hard HEAD^        # 回退到上一版本
```

### 远程操作
```bash
git remote -v                 # 查看远程仓库
git pull                      # 拉取更新
git clone 仓库地址            # 克隆仓库
```

---

## 📖 学习资源

### 在线练习
- [命令行挑战](https://cmdchallenge.com/)
- [Linux命令搜索](https://wangchujiang.com/linux-command/)
- [Git练习](https://learngitbranching.js.org/?locale=zh_CN)

### 推荐阅读
- [命令行的艺术](https://github.com/jlevy/the-art-of-command-line/blob/master/README-zh.md)
- [Linux工具快速教程](https://linuxtools-rst.readthedocs.io/zh_CN/latest/)

---

## 💡 提示

1. **Tab键自动补全** - 输入命令或文件名时按Tab
2. **上下箭头** - 浏览历史命令
3. **Ctrl+C** - 终止当前命令
4. **Ctrl+D** - 退出终端
5. **Ctrl+L** - 清屏（等同于`clear`）

---

**更新日期：** 2026-01-12
**作者：** h2548

> 💡 这些命令在新的终端窗口中生效！
>
> 🔄 如果修改了 ~/.zshrc，运行 `source ~/.zshrc` 重新加载
