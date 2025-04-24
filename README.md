# Git_Command
Just for Git_personal study

# Git 使用 SSH Key 完整指南

## 🔑 一、配置 SSH Key（只需一次）

1. **生成 SSH key**：
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   - 默认存储在 `~/.ssh/id_ed25519`
   - 可以设置一个 passphrase（密码），也可以留空

2. **启动 ssh-agent 并添加私钥**：
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```

3. **复制公钥内容**：
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
   复制整段输出（以 `ssh-ed25519` 开头）

4. **添加到 GitHub**：
   - 进入 GitHub 个人设置 → **SSH and GPG keys**
   - 点击 **New SSH key**
     - Title：自定义说明，比如“Laptop Key”
     - Key type：选择 **Authentication Key**
     - Paste key：粘贴你复制的 `.pub` 内容

---

## 🔍 二、SSH 和 HTTPS 的区别（通俗解释）

| 项目          | HTTPS                                         | SSH                                               |
|---------------|----------------------------------------------|----------------------------------------------------|
| 认证方式      | GitHub 用户名 + 密码 或 token                 | 使用本地生成的 SSH key 与 GitHub 绑定             |
| 输入频率      | 每次 push/pull 可能都要求登录（除非记住密码） | 初次需要设置，之后自动认证                        |
| 安全性        | 安全（需搭配 token 使用）                     | 更安全（基于公钥加密 + 本地私钥 + 可选密码保护）   |
| 使用场景      | 临时操作或不熟悉 SSH 的用户                   | 日常开发推荐使用，自动认证，体验更好              |

---

## 🧭 三、检查当前仓库使用的是 SSH 还是 HTTPS

```bash
git remote -v
```

- 输出示例（HTTPS）：
  ```
  origin  https://github.com/yourname/yourrepo.git (fetch)
  origin  https://github.com/yourname/yourrepo.git (push)
  ```

- 输出示例（SSH）：
  ```
  origin  git@github.com:yourname/yourrepo.git (fetch)
  origin  git@github.com:yourname/yourrepo.git (push)
  ```

---

## 🔁 四、将仓库从 HTTPS 切换为 SSH

```bash
git remote set-url origin git@github.com:yourname/yourrepo.git
```

确认：
```bash
git remote -v
```

---

## 📤 五、常用命令（SSH 或 HTTPS 均可通用）

### 提交本地更改并推送到远程

```bash
git add .
git commit -m "Your commit message"
git push origin main        # 或 master 分支
```

### 从远程仓库获取更新

```bash
git pull origin main        # 或 master 分支
```

---

## ✅ 六、测试 SSH 是否配置成功

```bash
ssh -T git@github.com
```

成功会看到类似提示：
```
Hi yourname! You've successfully authenticated, but GitHub does not provide shell access.
```

---

> 🚀 一旦配置好 SSH key，后续 push/pull 都不需要再输入 GitHub 密码，开发效率更高，推荐使用！
