# 🎓 Git进阶技巧完全指南

> 从入门到精通，掌握Git的核心技能

---

## 📚 目录

1. [分支管理](#分支管理)
2. [撤销与回退](#撤销与回退)
3. [查看历史](#查看历史)
4. [远程协作](#远程协作)
5. [冲突解决](#冲突解决)
6. [高级技巧](#高级技巧)
7. [最佳实践](#最佳实践)
8. [常见问题](#常见问题)

---

## 🌿 分支管理

### **为什么需要分支？**
- 🔒 保护主分支（main）不被破坏
- 🚀 并行开发多个功能
- 🧪 安全测试新想法
- 👥 团队协作不冲突

### **基础操作**

```bash
# 查看所有分支
git branch
git branch -a        # 包括远程分支

# 创建新分支
git branch feature-new

# 切换分支
git checkout feature-new

# 创建并切换（推荐）
git checkout -b feature-new

# 删除分支
git branch -d feature-new      # 安全删除（已合并）
git branch -D feature-new      # 强制删除

# 重命名分支
git branch -m old-name new-name
```

### **实战演练**

#### 场景1：开发新功能

```bash
# 1. 从main创建功能分支
git checkout main
git checkout -b feature-login

# 2. 开发功能
# ... 修改代码 ...
git add .
git commit -m "添加登录功能"

# 3. 切回main
git checkout main

# 4. 合并功能分支
git merge feature-login

# 5. 删除功能分支
git branch -d feature-login

# 6. 推送到远程
git push
```

#### 场景2：修复紧急bug

```bash
# 1. 从main创建hotfix分支
git checkout main
git checkout -b hotfix-critical-bug

# 2. 修复bug
# ... 修改代码 ...
git add .
git commit -m "修复关键bug"

# 3. 合并回main
git checkout main
git merge hotfix-critical-bug

# 4. 推送
git push

# 5. 删除hotfix分支
git branch -d hotfix-critical-bug
```

### **分支策略**

#### Git Flow（经典）
```
main (生产)
  ↓
develop (开发)
  ↓
feature/* (功能)
hotfix/* (紧急修复)
release/* (发布)
```

#### GitHub Flow（简单）
```
main (主分支)
  ↓
feature/* (功能分支)
```

---

## ⏪ 撤销与回退

### **工作区撤销**

```bash
# 撤销单个文件的修改
git checkout -- 文件名

# 撤销所有修改
git checkout -- .

# 新版本命令（推荐）
git restore 文件名
git restore .
```

### **暂存区撤销**

```bash
# 取消暂存单个文件
git reset HEAD 文件名

# 取消所有暂存
git reset HEAD .

# 新版本命令（推荐）
git restore --staged 文件名
```

### **提交撤销**

```bash
# 撤销最后一次提交（保留修改）
git reset --soft HEAD^

# 撤销最后一次提交（不保留修改）
git reset --hard HEAD^

# 撤销最近N次提交
git reset --soft HEAD~3

# 回退到指定提交
git reset --hard commit-id
```

### **修改最后一次提交**

```bash
# 修改提交信息
git commit --amend -m "新的提交信息"

# 添加遗漏的文件
git add 遗漏的文件
git commit --amend --no-edit
```

### **撤销已推送的提交**

```bash
# 方法1：revert（推荐，安全）
git revert HEAD           # 撤销最后一次
git revert commit-id      # 撤销指定提交
git push

# 方法2：reset + force push（危险！）
git reset --hard HEAD^
git push -f origin main   # 强制推送
```

---

## 📜 查看历史

### **基础查看**

```bash
# 查看提交历史
git log

# 简洁版（一行）
git log --oneline

# 图形化显示
git log --oneline --graph --decorate

# 查看最近N条
git log -5

# 查看某个文件的历史
git log 文件名
```

### **高级查看**

```bash
# 查看每次提交的详细修改
git log -p

# 查看统计信息
git log --stat

# 按作者筛选
git log --author="h2548"

# 按时间筛选
git log --since="2 weeks ago"
git log --after="2026-01-01"
git log --before="2026-01-12"

# 按提交信息搜索
git log --grep="修复"

# 查看某个文件的每一行是谁修改的
git blame 文件名
```

### **美化输出**

```bash
# 自定义格式
git log --pretty=format:"%h - %an, %ar : %s"

# 推荐的别名（添加到 ~/.zshrc）
alias glog='git log --oneline --graph --decorate --all'
alias glogp='git log --graph --pretty=format:"%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset" --abbrev-commit'
```

---

## 🌐 远程协作

### **远程仓库管理**

```bash
# 查看远程仓库
git remote -v

# 添加远程仓库
git remote add origin git@github.com:用户名/仓库名.git

# 修改远程仓库URL
git remote set-url origin 新地址

# 删除远程仓库
git remote remove origin

# 重命名远程仓库
git remote rename origin upstream
```

### **拉取与推送**

```bash
# 拉取远程更新
git pull                    # 拉取并合并
git pull --rebase          # 拉取并变基（推荐）

# 推送到远程
git push                    # 推送当前分支
git push origin main       # 推送指定分支
git push -u origin main    # 首次推送并设置上游

# 推送所有分支
git push --all

# 推送标签
git push --tags

# 强制推送（危险！）
git push -f origin main
```

### **克隆与Fork**

```bash
# 克隆仓库
git clone 仓库地址
git clone 仓库地址 自定义目录名

# 浅克隆（只克隆最近的提交）
git clone --depth 1 仓库地址

# Fork工作流
# 1. 在GitHub上Fork项目
# 2. 克隆你的Fork
git clone git@github.com:你的用户名/项目名.git

# 3. 添加上游仓库
git remote add upstream git@github.com:原作者/项目名.git

# 4. 同步上游更新
git fetch upstream
git merge upstream/main
```

---

## ⚔️ 冲突解决

### **什么是冲突？**
当两个分支修改了同一文件的同一部分时，Git无法自动合并，需要手动解决。

### **冲突标记**

```
<<<<<<< HEAD
你的修改
=======
别人的修改
>>>>>>> branch-name
```

### **解决步骤**

```bash
# 1. 尝试合并
git merge feature-branch

# 2. 查看冲突文件
git status

# 3. 手动编辑冲突文件
# 删除冲突标记，保留需要的内容

# 4. 标记为已解决
git add 冲突文件

# 5. 完成合并
git commit -m "解决合并冲突"
```

### **冲突解决工具**

```bash
# 使用VS Code解决冲突
code 冲突文件

# 使用Git自带工具
git mergetool

# 取消合并
git merge --abort
```

### **避免冲突的技巧**

1. **频繁拉取更新**
```bash
git pull --rebase
```

2. **小步提交**
```bash
# 不要一次修改太多文件
# 经常提交
```

3. **沟通协作**
```bash
# 团队成员避免同时修改同一文件
```

---

## 🚀 高级技巧

### **1. Stash（暂存）**

```bash
# 暂存当前修改
git stash

# 暂存并添加说明
git stash save "修改说明"

# 查看暂存列表
git stash list

# 恢复最近的暂存
git stash pop

# 恢复指定暂存
git stash apply stash@{0}

# 删除暂存
git stash drop stash@{0}

# 清空所有暂存
git stash clear
```

**使用场景：**
```bash
# 场景：正在开发功能，突然需要修复bug
git stash              # 暂存当前工作
git checkout main      # 切换到main
# ... 修复bug ...
git checkout feature   # 切回功能分支
git stash pop          # 恢复工作
```

### **2. Cherry-pick（挑选提交）**

```bash
# 将其他分支的某个提交应用到当前分支
git cherry-pick commit-id

# 挑选多个提交
git cherry-pick commit-id1 commit-id2

# 挑选一个范围
git cherry-pick commit-id1..commit-id2
```

### **3. Rebase（变基）**

```bash
# 将当前分支变基到main
git rebase main

# 交互式变基（整理提交历史）
git rebase -i HEAD~3

# 继续变基
git rebase --continue

# 取消变基
git rebase --abort
```

**Rebase vs Merge：**
```bash
# Merge：保留完整历史
git merge feature

# Rebase：线性历史（更清晰）
git rebase main
```

### **4. Tag（标签）**

```bash
# 创建轻量标签
git tag v1.0.0

# 创建附注标签（推荐）
git tag -a v1.0.0 -m "版本1.0.0发布"

# 查看所有标签
git tag

# 查看标签详情
git show v1.0.0

# 推送标签
git push origin v1.0.0
git push --tags

# 删除标签
git tag -d v1.0.0
git push origin :refs/tags/v1.0.0
```

### **5. Submodule（子模块）**

```bash
# 添加子模块
git submodule add 仓库地址 路径

# 克隆包含子模块的项目
git clone --recursive 仓库地址

# 更新子模块
git submodule update --init --recursive

# 拉取子模块更新
git submodule update --remote
```

---

## 📋 最佳实践

### **提交信息规范**

#### Conventional Commits（推荐）

```bash
<类型>(<范围>): <描述>

[可选的正文]

[可选的脚注]
```

**类型：**
- `feat`: 新功能
- `fix`: 修复bug
- `docs`: 文档更新
- `style`: 代码格式（不影响功能）
- `refactor`: 重构
- `test`: 测试
- `chore`: 构建/工具

**示例：**
```bash
git commit -m "feat(auth): 添加用户登录功能"
git commit -m "fix(api): 修复数据获取错误"
git commit -m "docs: 更新README安装说明"
```

### **分支命名规范**

```bash
feature/功能名      # 新功能
bugfix/bug描述      # bug修复
hotfix/紧急修复     # 紧急修复
release/版本号      # 发布分支
```

### **工作流程**

#### 个人项目
```bash
1. 在main分支开发
2. 经常提交
3. 推送到远程
```

#### 团队项目
```bash
1. 从main创建功能分支
2. 在功能分支开发
3. 提交并推送功能分支
4. 创建Pull Request
5. 代码审查
6. 合并到main
7. 删除功能分支
```

---

## ❓ 常见问题

### **Q1: 如何撤销已推送的提交？**

```bash
# 方法1：revert（推荐）
git revert HEAD
git push

# 方法2：reset（危险）
git reset --hard HEAD^
git push -f
```

### **Q2: 如何修改历史提交信息？**

```bash
# 修改最后一次
git commit --amend -m "新信息"

# 修改更早的提交
git rebase -i HEAD~3
# 将要修改的提交前的pick改为edit
# 保存退出
git commit --amend -m "新信息"
git rebase --continue
```

### **Q3: 如何合并多个提交？**

```bash
git rebase -i HEAD~3
# 将要合并的提交前的pick改为squash
# 保存退出
# 编辑合并后的提交信息
```

### **Q4: 误删了文件怎么恢复？**

```bash
# 如果还没提交
git checkout -- 文件名

# 如果已经提交
git log -- 文件名          # 找到删除前的提交
git checkout commit-id -- 文件名
```

### **Q5: 如何忽略已跟踪的文件？**

```bash
# 1. 添加到.gitignore
echo "文件名" >> .gitignore

# 2. 从Git中删除（保留本地文件）
git rm --cached 文件名

# 3. 提交
git commit -m "停止跟踪文件"
```

### **Q6: 如何查看两个分支的差异？**

```bash
# 查看差异
git diff main feature

# 查看文件列表
git diff --name-only main feature

# 查看统计
git diff --stat main feature
```

---

## 🎯 实战练习

### **练习1：分支管理**

```bash
# 1. 创建并切换到新分支
git checkout -b practice-branch

# 2. 修改README.md
echo "练习分支管理" >> README.md

# 3. 提交
git add README.md
git commit -m "练习：添加分支管理说明"

# 4. 切回main
git checkout main

# 5. 合并
git merge practice-branch

# 6. 删除分支
git branch -d practice-branch

# 7. 推送
git push
```

### **练习2：撤销操作**

```bash
# 1. 修改文件
echo "错误的修改" >> test.txt

# 2. 撤销修改
git checkout -- test.txt

# 3. 添加到暂存区
echo "测试" >> test.txt
git add test.txt

# 4. 取消暂存
git reset HEAD test.txt

# 5. 提交
git add test.txt
git commit -m "测试提交"

# 6. 撤销提交
git reset --soft HEAD^
```

### **练习3：冲突解决**

```bash
# 1. 创建两个分支
git checkout -b branch1
echo "分支1的修改" > conflict.txt
git add conflict.txt
git commit -m "分支1修改"

git checkout main
git checkout -b branch2
echo "分支2的修改" > conflict.txt
git add conflict.txt
git commit -m "分支2修改"

# 2. 合并产生冲突
git checkout main
git merge branch1
git merge branch2  # 产生冲突

# 3. 解决冲突
# 编辑conflict.txt，选择保留的内容
git add conflict.txt
git commit -m "解决冲突"

# 4. 清理
git branch -d branch1 branch2
```

---

## 📚 学习资源

### **在线学习**
- [Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN) - 可视化学习
- [Git官方文档](https://git-scm.com/book/zh/v2) - 权威指南
- [GitHub Skills](https://skills.github.com/) - 官方教程

### **速查表**
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [交互式速查表](https://ndpsoftware.com/git-cheatsheet.html)

### **推荐书籍**
- 《Pro Git》（免费在线）
- 《Git权威指南》

---

## 🎓 进阶主题

### **Git Hooks**
自动化工作流：
```bash
# 提交前检查
.git/hooks/pre-commit

# 提交信息检查
.git/hooks/commit-msg

# 推送前检查
.git/hooks/pre-push
```

### **Git LFS**
大文件存储：
```bash
git lfs install
git lfs track "*.psd"
```

### **Git Worktree**
多工作区：
```bash
git worktree add ../project-feature feature-branch
```

---

**更新日期：** 2026-01-12
**作者：** h2548

> 💡 Git是一个强大的工具，需要不断练习才能熟练掌握！
>
> 🚀 从简单的命令开始，逐步掌握高级技巧！
