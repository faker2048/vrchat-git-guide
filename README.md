# VRChat模型Git管理指南

## 目录
1. [Git简介](#git简介)
2. [在Windows上安装Git](#在windows上安装git)
3. [安装Git LFS](#安装git-lfs)
4. [为VRChat模型项目设置Git](#为vrchat模型项目设置git)
5. [常用Git操作](#常用git操作)
6. [使用Git管理Unity VRChat项目的最佳实践](#使用git管理unity-vrchat项目的最佳实践)
7. [常见问题解答](#常见问题解答)

## Git简介

Git是一个分布式版本控制系统，它可以帮助你跟踪项目中的更改，特别适合团队协作和个人项目管理。对于VRChat模型创作者来说，Git可以帮助你：

- 跟踪模型的不同版本
- 安全地尝试新功能而不破坏现有工作
- 在出现问题时回滚到之前的版本
- 与他人协作开发模型

## 在Windows上安装Git

### 步骤1：下载Git安装程序

1. 访问Git官方网站：[https://git-scm.com/download/win](https://git-scm.com/download/win)
2. 网站会自动检测你的系统并提供相应的下载链接，点击下载64位Windows版本

### 步骤2：安装Git

1. 运行下载的安装程序
2. 许可协议页面：点击"Next"
3. 选择安装位置：保持默认设置，点击"Next"
4. 选择组件：保持默认选项，确保以下选项被勾选：
   - Windows Explorer integration
   - Git Bash Here
   - Git GUI Here
   - Git LFS (Large File Support)
   - Associate .git* files with default editor
5. 点击"Next"继续
6. 开始菜单文件夹：保持默认，点击"Next"
7. 选择默认编辑器：建议选择"Notepad++"或"Visual Studio Code"（如果你已安装），否则使用默认的Vim
8. 调整PATH环境：选择"Git from the command line and also from 3rd-party software"（推荐）
9. 选择HTTPS传输后端：保持默认的"OpenSSL"，点击"Next"
10. 配置行尾符号处理：选择"Checkout Windows-style, commit Unix-style line endings"（推荐）
11. 配置终端模拟器：选择"Use MinTTY"
12. 配置额外选项：保持默认设置
13. 配置实验性选项：保持默认设置
14. 点击"Install"开始安装
15. 安装完成后，点击"Finish"

### 步骤3：验证安装

1. 打开"命令提示符"或"PowerShell"
2. 输入以下命令并按Enter：
   ```
   git --version
   ```
3. 如果显示Git版本号（如`git version 2.40.0.windows.1`），则表示安装成功

## 安装Git LFS

Git LFS（Large File Storage）是Git的扩展，专门用于处理大文件，如3D模型、纹理和音频文件。现代Git安装通常已包含Git LFS，但我们可以验证并确保它正确设置。

### 验证Git LFS是否已安装

1. 打开命令提示符或PowerShell
2. 输入以下命令：
   ```
   git lfs --version
   ```
3. 如果显示版本号（如`git-lfs/3.2.0`），则表示Git LFS已安装

### 如果需要手动安装Git LFS

1. 访问Git LFS官方网站：[https://git-lfs.github.com/](https://git-lfs.github.com/)
2. 下载Windows安装程序
3. 运行安装程序，按照提示完成安装
4. 安装完成后，打开命令提示符或PowerShell
5. 输入以下命令初始化Git LFS：
   ```
   git lfs install
   ```

## 为VRChat模型项目设置Git

### 步骤1：初始化Git仓库

1. 打开你的Unity VRChat项目文件夹
2. 右键点击空白处，选择"Git Bash Here"
3. 在Git Bash窗口中，输入以下命令初始化仓库：
   ```
   git init
   ```

### 步骤2：配置Git LFS跟踪大文件

VRChat模型项目包含许多大文件，我们需要让Git LFS来处理它们。在Git Bash中输入以下命令：

```bash
# 跟踪常见的Unity和VRChat大文件类型
git lfs track "*.fbx"
git lfs track "*.blend"
git lfs track "*.png"
git lfs track "*.jpg"
git lfs track "*.jpeg"
git lfs track "*.tga"
git lfs track "*.psd"
git lfs track "*.mp3"
git lfs track "*.wav"
git lfs track "*.mp4"
git lfs track "*.unitypackage"
git lfs track "*.asset"
```

### 步骤3：创建.gitignore文件

Unity项目包含许多不需要版本控制的临时文件和文件夹。在Git Bash中输入以下命令创建适合Unity项目的.gitignore文件：

```bash
curl -o .gitignore https://raw.githubusercontent.com/github/gitignore/main/Unity.gitignore
```

或者手动创建一个名为`.gitignore`的文件，并添加以下内容：

```
# Unity生成的文件和文件夹
[Ll]ibrary/
[Tt]emp/
[Oo]bj/
[Bb]uild/
[Bb]uilds/
[Ll]ogs/
[Uu]ser[Ss]ettings/

# MemoryCaptures可能会包含录制的内存转储
[Mm]emoryCaptures/

# 资源导入处理器的临时文件
.import/

# 自动生成的VS/MD/Consulo解决方案和项目文件
ExportedObj/
.consulo/
*.csproj
*.unityproj
*.sln
*.suo
*.tmp
*.user
*.userprefs
*.pidb
*.booproj
*.svd
*.pdb
*.mdb
*.opendb
*.VC.db

# Unity3D生成的元文件
*.pidb.meta
*.pdb.meta
*.mdb.meta

# Unity3D生成的崩溃报告
sysinfo.txt

# 构建
*.apk
*.aab
*.unitypackage
*.app

# 崩溃报告
crashlytics-build.properties

# 操作系统生成的文件
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
```

### 步骤4：提交初始文件

现在我们可以添加并提交项目文件：

```bash
# 添加所有文件到暂存区
git add .

# 提交初始文件
git commit -m "初始提交：添加VRChat模型项目"
```

## 常用Git操作

### 基本工作流程

以下是使用Git管理VRChat模型时的基本工作流程：

#### 1. 检查状态

在进行任何操作前，先检查仓库状态：

```bash
git status
```

这会显示哪些文件已修改、已暂存或未跟踪。

#### 2. 添加更改到暂存区

当你修改了模型、材质或其他文件后，将它们添加到暂存区：

```bash
# 添加特定文件
git add 文件路径

# 添加所有更改
git add .
```

#### 3. 提交更改

将暂存区的更改保存为一个新的提交：

```bash
git commit -m "描述你所做的更改"
```

提交消息应该简洁明了，例如：
- "更新猫耳模型的骨骼权重"
- "添加新的表情动画"
- "修复衣服穿模问题"

#### 4. 查看历史记录

查看之前的提交历史：

```bash
# 简洁历史
git log --oneline

# 详细历史
git log
```

#### 5. 创建和切换分支

分支可以让你安全地尝试新功能而不影响主要版本：

```bash
# 创建新分支
git branch 分支名称

# 切换到该分支
git checkout 分支名称

# 或者一步完成创建并切换
git checkout -b 分支名称
```

例如，当你想尝试为模型添加新的服装时：

```bash
git checkout -b 新服装测试
```

#### 6. 合并分支

当你对新功能满意时，可以将其合并回主分支：

```bash
# 先切换回主分支
git checkout main

# 合并你的功能分支
git checkout main
git merge 新服装测试
```

#### 7. 放弃更改

如果你不满意当前的更改，可以放弃它们：

```bash
# 放弃工作区中的更改
git checkout -- 文件路径

# 放弃所有更改
git checkout -- .
```

#### 8. 回到之前的版本

如果需要回到之前的版本：

```bash
# 查看提交历史
git log --oneline

# 回到特定提交
git checkout 提交ID
```

## 使用Git管理Unity VRChat项目的最佳实践

### 1. 频繁提交小更改

- 每完成一个小功能就提交一次
- 使用清晰的提交消息描述更改
- 避免一次提交大量不相关的更改

### 2. 使用分支进行功能开发

- 主分支（main）保持稳定，可用于发布
- 为每个新功能或实验创建单独的分支
- 功能完成并测试后再合并回主分支

### 3. 定期备份远程仓库

虽然Git是分布式的，但建议将你的仓库推送到远程服务如GitHub、GitLab或Bitbucket：

```bash
# 添加远程仓库（首次设置）
git remote add origin 远程仓库URL

# 推送到远程仓库
git push -u origin main
```

### 4. 合理使用标签标记重要版本

当你完成模型的重要版本时，可以使用标签来标记：

```bash
git tag -a v1.0 -m "模型第一个正式版本"
```

## 常见问题解答

### Q: 我的模型文件太大，Git提交很慢怎么办？
A: 确保正确设置了Git LFS来跟踪大文件。检查`.gitattributes`文件中是否包含了所有大文件类型。

### Q: 我不小心提交了错误的更改，如何撤销？
A: 使用以下命令撤销最近的提交（但保留更改）：
```bash
git reset --soft HEAD~1
```

### Q: 如何查看特定文件的修改历史？
A: 使用以下命令：
```bash
git log --follow 文件路径
```

### Q: 我的Unity场景文件经常发生冲突，如何处理？
A: Unity场景文件是YAML格式，容易产生冲突。建议团队成员不要同时编辑同一个场景，或者使用Unity协作工具如Unity Teams。

### Q: 如何忽略已经提交的文件？
A: 首先将文件添加到`.gitignore`，然后使用以下命令从仓库中删除（但保留本地文件）：
```bash
git rm --cached 文件路径
```

---

希望这份指南能帮助你开始使用Git管理VRChat模型项目。随着你对Git的熟悉，你会发现它是一个强大的工具，可以让你的模型开发更加有条理和安全。 
