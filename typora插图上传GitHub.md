# GitHub注册

## 登录官网进行注册

https://github.com

在网站首页选择`sign up fro GitHub`按钮使用邮箱进行注册

![image-20260107204451366](C:\Users\acer\AppData\Roaming\Typora\typora-user-images\image-20260107204451366.png)

推荐使用微软邮箱，可以正常收发邮件，后面会有邮件验证

![image-20260107211029528](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107211029649.png)

上面填写完成后，选择 `Create account` 按钮进行账户创建

## 安装Git

[https://git-scm.com/downloads](https://git-scm.com/downloads?spm=5176.28103460.0.0.7cdb7551nShTWl)

根据版本号选择需要安装的程序

![image-20260107205842693](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107205842732.png

![image-20260107210916434](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107210916662.png)

下载之后一直点击`next`按钮，注意替换安装路径，避免安装在C盘；

![image-20260107211509662](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107211509712.png)

安装完成后 在需要将云端代码拉取到本地的文件夹中右击鼠标右键，选择`Open Git Bash here`

![image-20260107211741990](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222502017.png)

## 配置git

### 检查git版本

```bash
acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库
$ git --version
git version 2.52.0.windows.1
```

### 配置个人名称及邮箱

这个邮箱就是前面注册GitHub的时候的微软邮箱

```bash
acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库
$ git config --global user.name "fanxiaofan"

acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库
$ git config --global user.email "fanwensheng019@outlook.com"


```

### 检查密钥对

检查本地是否存在ssh的密钥对，这是远程链接上git的关键；

```bash
acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库
$ ls -al ～/.ssh
ls: cannot access '～/.ssh': No such file or directory
```

本地显示没有，需要生成一下

生成命令如下

```bash
acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库
$ ssh-keygen -t ed25519 -C "fanwensheng019@outlook.com"

```

这一步不需要操作，直接回车就行；

![image-20260107213328393](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222452466.png)

这一步直接输入yes就可以了 回车执行

![image-20260107213409519](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222445421.png)

![image-20260107213439329](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222441431.png)

上面回车后到 这一步是显示需要是否设置密码，默认不设置，直接回车

![image-20260107213453222](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222435882.png)

再次确认，直接回车

![image-20260107213546180](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222430038.png)

最后生成密钥

```bash
acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库
$ ssh-keygen -t ed25519 -C "fanwensheng019@outlook.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/acer/.ssh/id_ed25519):
/c/Users/acer/.ssh/id_ed25519 already exists.
Overwrite (y/n)? yes
Enter passphrase for "/c/Users/acer/.ssh/id_ed25519" (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/acer/.ssh/id_ed25519
Your public key has been saved in /c/Users/acer/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:CUQo73CYT9Be+hLpmspfSV+tf1hKO5ON7LkPRSyM+6U fanwensheng019@outlook.com
The key's randomart image is:
+--[ED25519 256]--+
|   . oo          |
|  o o..   o .    |
|   B +.  . o o   |
|  + O  . .o o    |
|   B +  So . o   |
|    * + . o.+.   |
|   o + . .oEO    |
|. o .     .Xoo   |
|.o..      .=*.   |
+----[SHA256]-----+

```

### **启动** `ssh-agent` **并添加私钥**

```bash
acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库
$ eval $(ssh-agent -s)
Agent pid 161

```

检查生成的密钥对

```bash
acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库
$ ls -al ~/.ssh/
total 39
drwxr-xr-x 1 acer 197609   0 Jan  6 21:57 ./
drwxr-xr-x 1 acer 197609   0 Jan  7 21:23 ../
drwxr-xr-x 1 acer 197609   0 Jan  7 21:37 agent/
-rw-r--r-- 1 acer 197609 419 Jan  7 21:30 id_ed25519
-rw-r--r-- 1 acer 197609 108 Jan  7 21:30 id_ed25519.pub
-rw-r--r-- 1 acer 197609 923 Jan  6 21:57 known_hosts
-rw-r--r-- 1 acer 197609 188 Jan  6 21:50 known_hosts.old
```

添加私钥

```bash
acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库
$ ssh-add ~/.ssh/id_ed25519
Identity added: /c/Users/acer/.ssh/id_ed25519 (fanwensheng019@outlook.com)

```

### GitHub添加公钥

查看公钥，并将复制下来

![image-20260107214417518](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222422025.png)

打开GitHub界面，依次进入右上角图像➔`settings`➔`SSH and GPG keys`➔`New SSH key`➔

![image-20260107214745775](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222415605.png)

将前面复制过来的公钥复制进行，title名字随意，点击`add ssh key`完成公钥配置

![image-20260107214959980](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222409870.png)

测试链接

```bash
acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库
$ ssh -T git@github.com
Hi fanxiaofan01! You've successfully authenticated, but GitHub does not provide shell access.

```

### 克隆代码

![image-20260107215411901](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222402288.png)

从这个界面上查找GitHub的ssh克隆地址，在git上进行克隆

```bash
git clone git@github.com:fanxiaofan01/fanxiaofan_work.git
```

克隆完成，从远端拉取代码

```bash
acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库/my_notes_imgs (main)
$ git pull
remote: Enumerating objects: 81, done.
remote: Counting objects: 100% (81/81), done.
remote: Compressing objects: 100% (79/79), done.
Unpacking objects:  37% (30/79), 2.08 MiB | 19.00 KiB/s

```

当第一提交的时候报这个警告

```bash
acer@˧С▒▒▒ĵ MINGW64 /d/GitHub_代码库/fanxiaofan_work (notes)
$ git push
fatal: The current branch notes has no upstream branch.
To push the current branch and set the remote as upstream,
 use

    git push --set-upstream origin notes

To have this happen automatically for branches without a t
racking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```

直接按照警告，推送新建分支

```bash
git push --set-upstream origin notes
```

后续就是同步代码常用命令

```bash
# 添加修改
git add .

# 提交
git commit -m "docs: update Git notes"

# 推送（现在可以直接用 git push！）
git push
```

### 安装小乌龟

拉取代码后正常该文件夹里面的图标应该是绿色的，类似这样的，如果没有变化，需要安装小乌龟；

![image-20260107220436811](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222354936.png)



https://tortoisegit.org/download/

小乌龟下载地址，选择适合的版本号

![image-20260107220737473](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222349474.png)

下载后正常安装即可

问题：安装小乌龟 后  文件图标并没有 带上

需要到注册机 处处理

- 按 `Win + R`，输入 `regedit`，回车

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
```

将9个人间前面都添加8个空格，

![image-20260107220943243](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222343916.png)

### **重启资源管理器（无需重启电脑！）**

1. 按 `Ctrl + Shift + Esc` 打开任务管理器
2. 找到 **Windows 资源管理器**
3. 右键 → **重新启动**

就能够看到对应的文件带上了图标

## GitHub本地远程链接

### 下载FastGithub安装包

下载途径一：清华大学云盘下载地址：

[清华大学云盘](https://cloud.tsinghua.edu.cn/d/df482a15afb64dfeaff8/) 下载地址

下载途径二：官方地址：https://github.com/dotnetcore/fastgithub/releases

![image-20260119232118382](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260119232118464.png)

2、解压后进入主目录下，双击fastgihub.exe即可运行

![image-20260119232310836](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260119232310898.png)

![image-20260119232404191](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260119232404243.png)

3、从github上更新程序包

目前最新版还是2.1.4，地址：https://github.com/dotnetcore/fastgithub/releases

运行效果：

PS：建议exe运行10秒钟后再尝试打开github链接嗷
————————————————
版权声明：本文为CSDN博主「蓝多多的小仓库」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_43554335/article/details/134066165

# PicGo

## 软件下载

https://github.com/Molunerfinn/PicGo/releases

![image-20260107221253330](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222333775.png)

下载后直接安装即可

## GitHub配置

### **第一步：在 GitHub 创建图床仓库**

1. 登录 GitHub，点击右上角 **+ → New repository**
2. 填写：
   - **Repository name**: `my-notes-imgs`（可自定义）
   - **Description**: 可选
   - ✅ **Public**（必须公开！否则图片无法外链）
   - ❌ 不要勾 “Add a README”
3. 点击 **Create repository**

------

### **第二步：生成 GitHub Personal Access Token (PAT)**

1. 进入 https://github.com/settings/tokens
2. 点击 **Tokens (classic) → Generate new token → Generate new token (classic)**
3. 填写：
   - **Note**: `Typora PicGo`
   - **Expiration**: 90 天或更长
   - ✅ **勾选 `repo` 权限**（关键！）
4. 滚动到底部，点击 **Generate token**
5. **复制生成的 token**（只显示一次！建议保存到记事本）

> 示例 token：`ghp_AbCdEfGhIjKlMnOpQrStUvWxYz123456789`

------

### **第三步：安装并配置 PicGo**

#### 安装 PicGo

- 下载 **PicGo-Setup-x.x.x.exe**（Windows 用户）
- 安装时**不要装在 `Program Files`**（权限问题），建议装在 `D:\PicGo`

#### 配置 GitHub 图床

打开 PicGo → 左侧 **图床设置** → 选择 **GitHub**

填写以下信息：

表格



| 字段       | 值                                                     |
| :--------- | :----------------------------------------------------- |
| 仓库名     | `你的用户名/仓库名`（如 `fanxiaofan01/my-notes-imgs`） |
| 分支名     | `main`（新仓库默认是 `main`，不是 `master`）           |
| Token      | 粘贴你刚才生成的 **Personal Access Token**             |
| 存储路径   | `img/`（可选，图片会存到仓库的 `img` 文件夹）          |
| 自定义域名 | `https://cdn.jsdelivr.net/gh/你的用户名/仓库名`        |

![image-20260107221517585](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222326913.png)

需要注意，自定义域名，是这个

`https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs`

而不是GitHub的https地址，注意区分

![image-20260107221849972](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222320417.png)

上面配置完成后，可以上传照片测试一下

![image-20260107222050757](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222312193.png)

![image-20260107222056895](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222305267.png)

显示上传成功

> ✅ **自定义域名说明**：
> GitHub 原始链接（`raw.githubusercontent.com`）在国内可能慢或打不开，
> 使用 **jsDelivr CDN 加速** 可大幅提升加载速度！

#### 启用时间戳重命名（避免冲突）

- 左侧 **PicGo 设置** → 勾选 **✅ 时间戳重命名**
- 避免同名图片覆盖

#### 设为默认图床

- 回到 **图床设置** → 点击 **设为默认图床**

#### 测试上传

- 点击顶部 **上传区** → 选择一张图片 → 点击 **打开**
- 成功后会弹出链接，说明配置 OK ✅

## typora配置

1. 打开 Typora
2. 进入 **文件 → 偏好设置 → 图像**
3. 按如下配置：

表格



| 选项                           | 设置                                                |
| :----------------------------- | :-------------------------------------------------- |
| 插入图片时...                  | **上传图片**                                        |
| ✅ 对本地位置的图片应用上述规则 | **勾选**                                            |
| 上传服务                       | **PicGo (app)**                                     |
| PicGo 路径                     | 选择你安装的 `PicGo.exe`（如 `D:\PicGo\PicGo.exe`） |

1. 点击 

   验证图片上传选项

   - 如果弹出“上传成功” → 配置完成！
   - 如果失败 → 检查 PicGo 是否运行、Token 是否正确

![image-20260107222146227](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222146294.png)

按照这个进行配置

![image-20260107222246679](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260107222246754.png)

## SM.SM配置

### **✅ 配置步骤：PicGo + sm.ms 图床**

#### **第一步：确保已安装 Node.js**

sm.ms 插件依赖 Node.js 环境：

- 下载地址：[https://nodejs.org/](https://nodejs.org/?spm=5176.28103460.0.0.7cdb7551izxWQV) （推荐 LTS 版本）

- 安装后，在终端执行：

  ![image-20260115215836436](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260115225711603.png)![image-20260115220001882](D:\GitHub_代码库\fanxiaofan_work\typora插图上传GitHub.assets\image-20260115220001882.png)

  随便打开git运行语句查看软件是否安装成功

  ```bash
  acer@˧С▒▒▒ĵ MINGW64 /d
  $ node -v
  v24.13.0
  
  acer@˧С▒▒▒ĵ MINGW64 /d
  $ npm -v
  11.6.2
  
  ```

  若能显示版本号，说明安装成功。

------

#### **第二步：安装 sm.ms 插件**

1. 打开 **PicGo**。

2. 点击左侧菜单 **「插件设置」**。

3. 在搜索框中输入：picgo-plugin-smms

   ![image-20260115220355498](https://cdn.jsdelivr.net/gh/fanxiaofan01/my_notes_imgs/img/20260115225633980.png)

   显示找不到插件，需要在手动安装一下

   ```bash
   acer@˧С▒▒▒ĵ MINGW64 /d
   $ npm install -g picgo-plugin-smms
   npm error code E404
   npm error 404 Not Found - GET https://registry.npmjs.org/picgo-plugin-smms - Not
    found
   npm error 404
   npm error 404  The requested resource 'picgo-plugin-smms@*' could not be found o
   r you do not have permission to access it.
   npm error 404
   npm error 404 Note that you can also install from a
   npm error 404 tarball, folder, http url, or git url.
   npm error A complete log of this run can be found in: C:\Users\acer\AppData\Loca
   l\npm-cache\_logs\2026-01-15T14_03_24_614Z-debug-0.log
   
   ```

   显示安装完成，重启`picgo`

4. 找到插件 

   `picgo-plugin-smms`

   （作者通常是 

   ```
   CodeFalling
   ```

    或社区维护者），点击 

   「安装」

   。

   > 💡 如果搜索不到，可手动安装：

   bash

   

   ```
   npm install -g picgo-plugin-smms
   ```

   然后在 PicGo 插件设置中点击「导入插件」，选择全局安装的路径。

5. 安装完成后，**重启 PicGo**。

------

#### **第三步：配置 sm.ms 图床**

1. 重启后，进入 **「图床设置」**。
2. 你会看到新增的 **「SM.MS」** 选项（或类似名称）。
3. 点击进入配置页面，填写以下信息：

表格



| 配置项         | 说明                                                         |
| :------------- | :----------------------------------------------------------- |
| **Token**      | 可选。如果你有 [sm.ms 的 API Token](https://sm.ms/home/user)（登录后在用户中心获取），可以填写以提升上传限额和稳定性；否则留空也可上传（但可能受限）。 |
| **自定义域名** | 一般不需要填。默认返回 `https://i.loli.net/...` 或 `https://s2.loli.net/...` 等 sm.ms 的 CDN 链接。 |

> 🔔 注意：sm.ms **无需仓库名、分支等参数**，它是一个独立的图床服务，不是基于 Git 的。

1. 点击 **「确定」**，然后 **「设为默认图床」**。

------

#### **第四步：测试上传**

- 在 PicGo 主界面点击「上传区」，选择一张图片上传。

- 成功后会自动复制链接，格式类似：

  text

  

  ```
  https://s2.loli.net/2026/01/15/xxxxxx.png
  ```

------

### **⚠️ 注意事项**

1. sm.ms 是免费图床，但有使用限制

   ：

   - 免费用户单文件 ≤ 5MB（部分时期放宽至 10MB）。
   - 上传频率过高可能被临时限流。
   - 不保证永久存储（虽然目前大多数图片长期可用）。

2. 隐私问题

   ：

   - 所有图片公开可访问，**切勿上传敏感内容**。

3. 国内访问速度

   ：

   - sm.ms 使用了 `loli.net` CDN，**在中国大陆访问速度较快**，这是它受欢迎的主要原因。

4. Token 获取方式

   ：

   - 访问 [https://sm.ms](https://sm.ms/) → 登录账号 → 进入「User Center」→ 查看 **API Token**。

------

### **🔁 替代建议（如 sm.ms 不稳定）**

如果 sm.ms 出现上传失败或限流，可考虑以下方案：

- **GitHub + jsDelivr CDN**（完全免费，适合技术用户）
- **Gitee / GitCode**（国内加速，需插件）
- **阿里云 OSS**（低费用，高稳定，适合长期使用）

------

### **📌 总结**

表格



| 步骤 | 操作                                        |
| :--- | :------------------------------------------ |
| 1    | 安装 Node.js                                |
| 2    | 在 PicGo 中安装 `picgo-plugin-smms` 插件    |
| 3    | 重启 PicGo，配置 SM.MS 图床（可选填 Token） |
| 4    | 测试上传，享受快速图床服务                  |

















