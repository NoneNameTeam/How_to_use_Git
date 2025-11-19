# GitHub 项目协作新手指南

本指南将帮助你掌握 GitHub 团队协作的核心技能,从基础操作到项目管理。

## 1. 分支管理与切换

### 理解分支的作用
分支允许你在不影响主代码的情况下开发新功能或修复bug。把它想象成平行宇宙:你可以在自己的"宇宙"里自由实验,完成后再合并回主线。

### 基本分支操作

**查看所有分支:**
```bash
git branch -a
```

**创建新分支:**
```bash
git branch feature/新功能名称
```

**切换到已存在的分支:**
```bash
git checkout feature/新功能名称
```

**创建并立即切换到新分支(推荐):**
```bash
git checkout -b feature/新功能名称
```

**将本地分支推送到远程:**
```bash
git push -u origin feature/新功能名称
```

### 分支命名规范建议
- `feature/登录功能` - 新功能开发
- `bugfix/修复登录错误` - bug修复
- `hotfix/紧急修复` - 紧急修复
- `docs/更新README` - 文档更新

### 保持分支更新
在你的分支上工作时,定期同步主分支的最新改动:
```bash
git checkout main
git pull origin main
git checkout feature/你的分支
git merge main
```

## 2. Issues (问题追踪)

### 什么是 Issue?
Issue 是 GitHub 的任务管理工具,用于追踪 bug、功能请求、待办事项等。

### 创建高质量的 Issue

**在 GitHub 网页上:**
1. 进入仓库页面
2. 点击 "Issues" 标签
3. 点击 "New issue" 绿色按钮
4. 填写标题和描述

**好的 Issue 应该包含:**
- **清晰的标题:** "登录按钮在移动端无法点击"
- **详细描述:** 问题是什么?如何重现?预期行为是什么?
- **截图或错误信息:** 直观展示问题
- **环境信息:** 浏览器版本、操作系统等
- **标签(Labels):** bug、enhancement、documentation 等

### 示例 Issue 模板
```markdown
## 问题描述
用户在移动端点击登录按钮没有反应

## 重现步骤
1. 打开网站首页
2. 点击右上角"登录"按钮
3. 在移动设备(iPhone 12, iOS 15)上测试

## 预期行为
应该跳转到登录页面

## 实际行为
按钮无响应,控制台显示错误信息

## 截图
[附上截图]

## 环境
- 设备: iPhone 12
- 浏览器: Safari 15.0
- 系统: iOS 15.2
```

### Issue 管理技巧
- 使用 `#编号` 在提交信息中关联 Issue: `git commit -m "修复登录问题 #15"`
- 使用关键词自动关闭 Issue: `git commit -m "fixes #15"`、`closes #15`
- 分配责任人 (Assignees)
- 使用里程碑 (Milestones) 组织发布计划

## 3. Pull Requests (PR)

### 什么是 Pull Request?
PR 是请求将你的代码变更合并到主分支的正式流程,也是代码审查的核心机制。

### 创建 Pull Request 的完整流程

**步骤 1: 在分支上完成开发**
```bash
git checkout -b feature/添加搜索功能
# 进行开发...
git add .
git commit -m "实现搜索功能的基础框架"
git push -u origin feature/添加搜索功能
```

**步骤 2: 在 GitHub 上创建 PR**
1. 推送分支后,GitHub 会显示 "Compare & pull request" 按钮,点击它
2. 或者进入仓库,点击 "Pull requests" > "New pull request"
3. 选择基础分支 (通常是 main) 和比较分支 (你的功能分支)

**步骤 3: 填写 PR 信息**
```markdown
## 变更说明
实现了全局搜索功能,支持按标题和内容搜索

## 相关 Issue
Closes #23

## 改动内容
- 添加搜索组件
- 实现搜索API接口
- 添加搜索结果页面

## 测试说明
- [ ] 单元测试通过
- [ ] 搜索功能在不同浏览器测试通过
- [ ] 性能测试达标

## 截图
[添加功能演示截图]
```

### PR 审查流程

**作为代码提交者:**
- 确保代码通过所有自动化测试
- 主动请求团队成员审查 (Request reviewers)
- 及时回应审查意见,进行必要修改
- 保持 PR 体积适中,避免一次改动过多文件

**作为审查者:**
- 检查代码质量、可读性、是否遵循规范
- 测试功能是否正常工作
- 提出建设性意见,使用 "Request changes" 或 "Approve"
- 在代码行上直接评论具体问题

### 更新 PR
如果需要根据反馈修改代码:
```bash
# 在同一分支继续修改
git add .
git commit -m "根据审查意见优化搜索算法"
git push origin feature/添加搜索功能
```
GitHub 会自动更新 PR 内容。

### 合并 PR
审查通过后,有三种合并方式:
- **Merge commit:** 保留所有提交历史 (推荐用于重要功能)
- **Squash and merge:** 将所有提交压缩为一个 (保持主分支整洁)
- **Rebase and merge:** 线性历史,无合并提交

## 4. GitHub Projects (项目管理)

### 什么是 GitHub Projects?
Projects 是看板式的项目管理工具,可以可视化追踪工作进度,类似 Trello。

### 创建项目看板

**步骤:**
1. 在仓库页面点击 "Projects" 标签
2. 点击 "New project"
3. 选择模板:
   - **Board:** 传统看板(待办、进行中、完成)
   - **Table:** 表格视图
   - **Roadmap:** 时间线视图

### 基本工作流程

**看板栏目设置建议:**
- **Backlog (待办):** 所有待处理的任务
- **To Do (即将开始):** 近期要做的任务
- **In Progress (进行中):** 正在开发的任务
- **In Review (审查中):** 等待代码审查的 PR
- **Done (完成):** 已完成的任务

**将 Issue 添加到项目:**
1. 打开 Issue
2. 右侧边栏找到 "Projects"
3. 选择项目并分配到相应栏目

**自动化设置:**
- 新建的 Issue 自动添加到 "Backlog"
- PR 创建时自动移到 "In Review"
- PR 合并后自动移到 "Done"

### 高效使用技巧
- 使用 **Labels** 标记优先级 (P0-高、P1-中、P2-低)
- 使用 **Milestones** 规划版本发布
- 定期整理看板,保持清晰
- 在每日站会上基于看板讨论进度

## 5. .gitignore 文件使用

### 什么是 .gitignore?
.gitignore 告诉 Git 哪些文件或目录不应该被追踪和上传到仓库,避免提交敏感信息或无用文件。

### 创建 .gitignore

在项目根目录创建文件:
```bash
touch .gitignore
```

### 常见忽略规则

**Node.js 项目示例:**
```gitignore
# 依赖包
node_modules/
npm-debug.log

# 环境变量
.env
.env.local

# 构建产物
dist/
build/
*.log

# IDE 配置
.vscode/
.idea/
*.swp

# 操作系统文件
.DS_Store
Thumbs.db

# 测试覆盖率
coverage/
```

**Python 项目示例:**
```gitignore
# 虚拟环境
venv/
env/
*.pyc

# 配置文件
config.ini
secrets.json

# 缓存
__pycache__/
*.py[cod]
```

### 语法规则
- `文件名.txt` - 忽略特定文件
- `*.log` - 忽略所有 .log 文件
- `目录名/` - 忽略整个目录
- `!重要文件.log` - 例外规则,不忽略这个文件
- `**/日志/` - 忽略所有名为"日志"的目录

### 模板资源
GitHub 提供了各种语言的 .gitignore 模板:
访问 github.com/github/gitignore 查看现成模板,或在创建仓库时选择模板。

### 已提交文件的处理
如果文件已经被 Git 追踪,添加到 .gitignore 不会生效,需要先移除:
```bash
git rm --cached 文件名
git commit -m "从版本控制中移除敏感文件"
```

## 实战演练:完整协作流程

让我们串联所有知识,完成一次完整的协作:

```bash
# 1. 克隆项目并创建分支
git clone https://github.com/团队/项目.git
cd 项目
git checkout -b feature/添加用户头像

# 2. 开发功能
# [编写代码...]
git add .
git commit -m "实现用户头像上传功能 #42"

# 3. 推送分支
git push -u origin feature/添加用户头像

# 4. 在 GitHub 上创建 PR,关联 Issue #42
# 5. 团队成员审查代码,你根据反馈修改
git add .
git commit -m "优化图片压缩算法"
git push

# 6. 审查通过,合并 PR
# 7. 在 GitHub Projects 看板上将任务移到 "Done"
# 8. 删除本地和远程分支(可选)
git checkout main
git pull
git branch -d feature/添加用户头像
git push origin --delete feature/添加用户头像
```

## 协作最佳实践

1. **频繁提交,小步快跑:** 每完成一个小功能就提交,便于回溯
2. **写清晰的提交信息:** 说明"为什么"而不只是"做了什么"
3. **保持分支生命周期短:** 避免长期分支导致合并冲突
4. **先拉取后推送:** 推送前先 `git pull` 获取最新代码
5. **代码审查要及时:** 不要让 PR 长时间无人处理
6. **善用模板:** 为 Issue 和 PR 创建模板,保持信息一致性

## 遇到问题怎么办?

- **合并冲突:** 使用 `git mergetool` 或手动编辑冲突文件
- **误提交敏感信息:** 使用 `git filter-branch` 或 BFG Repo-Cleaner
- **需要回退:** `git revert` (保留历史) 或 `git reset` (重写历史,谨慎使用)
- **不确定操作:** 先在测试分支上尝试,或向有经验的团队成员求助

通过实践这些流程,你很快就能成为 GitHub 协作高手。记住,最好的学习方式就是在真实项目中动手实践!
