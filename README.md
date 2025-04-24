# Git 新设备配置操作指南

本指南介绍如何在新设备上配置 Git 环境，以便开始使用 Git 进行版本控制。

## 1. 安装 Git
- **Windows**:
  - 下载 Git for Windows：[https://git-scm.com/download/win](https://git-scm.com/download/win)
  - 运行安装程序，推荐选择默认设置。
- **MacOS**:
  - 通过 Homebrew 安装：`brew install git`
  - 或下载官方安装包：[https://git-scm.com/download/mac](https://git-scm.com/download/mac)
- **Linux**:
  - Ubuntu/Debian：`sudo apt update && sudo apt install git`
  - CentOS/RHEL：`sudo yum install git` 或 `sudo dnf install git`

验证安装：运行 `git --version`，确保输出 Git 版本号。

## 2. 配置用户信息
设置全局用户名和邮箱，用于标识提交记录：
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
验证配置：`git config --list`

## 3. 配置 SSH 密钥
生成 SSH 密钥以安全访问远程仓库（如 GitHub、GitLab）：
1. 生成密钥：
   ```bash
   ssh-keygen -t ed25519 -C "your.email@example.com"
   ```
   - 如果系统不支持 ed25519，可使用：`ssh-keygen -t rsa -b 4096 -C "your.email@example.com"`
   - 按回车接受默认文件位置，设置密码（可选）。
2. 启动 SSH 代理：
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```
3. 复制公钥到剪贴板：
   - Windows：`clip < ~/.ssh/id_ed25519.pub`
   - MacOS/Linux：`cat ~/.ssh/id_ed25519.pub`
4. 添加公钥到远程仓库平台：
   - GitHub：进入 Settings > SSH and GPG keys > New SSH key，粘贴公钥。
   - GitLab：进入 User Settings > SSH Keys，粘贴公钥。
5. 测试 SSH 连接：
   ```bash
   ssh -T git@github.com
   ```
   或 `ssh -T git@gitlab.com`，成功会显示欢迎信息。

## 4. 配置默认编辑器（可选）
设置 Git 使用的默认文本编辑器，例如 VS Code：
```bash
git config --global core.editor "code --wait"
```
其他编辑器示例：
- Vim：`git config --global core.editor vim`
- Nano：`git config --global core.editor nano`

## 5. 配置默认分支名称（可选）
设置新仓库默认分支名称为 `main`：
```bash
git config --global init.defaultBranch main
```

## 6. 克隆仓库并开始工作
克隆远程仓库：
```bash
git clone git@github.com:username/repository.git
```
进入仓库目录：`cd repository`

## 7. 其他实用配置（可选）
- 启用颜色高亮：
  ```bash
  git config --global color.ui auto
  ```
- 设置默认拉取行为：
  ```bash
  git config --global pull.rebase false
  ```
- 配置自动处理换行符：
  ```bash
  git config --global core.autocrlf true  # Windows
  git config --global core.autocrlf input  # MacOS/Linux
  ```

## 8. 常见问题
- **SSH 连接失败**：检查 `~/.ssh/id_ed25519.pub` 是否正确添加到远程平台，确认网络连接。
- **权限错误**：确保 SSH 密钥已添加到代理（`ssh-add`）。
- **提交没有用户名**：检查 `user.name` 和 `user.email` 是否配置正确。

完成以上步骤后，您的设备已准备好使用 Git 进行版本控制！