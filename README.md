
### 第二步：修改用户文件夹名（C:\Users\xxxxx）

#### 新建账户迁移法

这个方法的逻辑是：创建一个名字完美的新账户，把旧文件搬过去，然后删掉旧账户。

1.  **创建新账户**
    *   进入 **“设置”** > **“账户”** > **“其他用户”**。
    *   点击 **“添加账户”** > 选择 **“我没有这个人的登录信息”** > **“添加一个不带 Microsoft 账户的用户”**。
    *   **关键点：** 在这里输入你想要的**完美用户名**（这将直接成为新的文件夹名）。
    *   创建后，点击该账户，选择 **“更改账户类型”**，将其设置为 **“管理员”**。

2.  **迁移数据**
    *   **注销**当前账户，登录刚才创建的**新账户**。
    *   打开文件资源管理器，进入 `C:\Users\旧用户名`（旧的那 5 位字母文件夹）。
    *   复制你需要保留的文件（桌面、文档、图片、视频、下载等文件夹内的内容）。
    *   粘贴到 `C:\Users\新用户名` 对应的文件夹中。
    *   *注意：不要直接复制整个 AppData 文件夹，这会导致配置冲突，建议只迁移个人文件。*

3.  **关联微软账户（可选）**
    *   如果你希望新账户也同步微软的云盘和设置，进入 **“设置”** > **“账户”** > **“你的信息”**，点击 **“改用 Microsoft 账户登录”**，登录你的邮箱即可。

4.  **删除旧账户**
    *   确认新账户一切正常后，回到 **“设置”** > **“账户”** > **“其他用户”**，选中旧的那个 5 位字母的账户，点击 **“删除”**。

```bat
# Windows 软件自动化部署脚本
# 作者：尹浩宇
# 功能：批量静默安装常用软件，并记录日志

Write-Host "🚀 开始执行自动化安装脚本..." -ForegroundColor Green

# 定义软件列表
$packages = @(
    "Google.Chrome",
    "2dust.v2rayN",
    "GeekUninstaller.GeekUninstaller",
    "Yuanli.uTools",
    "Tencent.WeChat",
    "Tencent.WeType",
    "Kingsoft.WPSOffice.CN",
    "SoftDeluxe.FreeDownloadManager",
    "Logitech.GHUB",
    "Alibaba.aDrive",
    "Anthropic.Claude",
    "astral-sh.uv",
    "Rye.Rye",
    "ByteDance.Douyin",
    "ch.LosslessCut",
    "OpenMedia.4KVideoDownloaderPlus",
    "Eassos.DiskGenius",
    "Rufus.Rufus",
    "Blizzard.BattleNet",
    "Bilibili.Bilibili"
)

# 遍历安装
foreach ($pkg in $packages) {
    Write-Host "📦 正在安装: $pkg ..." -ForegroundColor Yellow
    
    # 核心安装命令：精确匹配 + 静默安装 + 等待完成
    winget install -e $pkg --silent --wait
    
    # 检查上一条命令是否成功
    if ($LASTEXITCODE -eq 0) {
        Write-Host "✅ $pkg 安装成功" -ForegroundColor Green
    } else {
        Write-Host "❌ $pkg 安装失败 (错误码: $LASTEXITCODE)" -ForegroundColor Red
    }
}

# 特殊处理：Microsoft Store 应用 (Raycast)
Write-Host "📦 正在安装 Microsoft Store 应用: Raycast ..." -ForegroundColor Yellow
winget install Raycast --source msstore --wait
if ($LASTEXITCODE -eq 0) {
    Write-Host "✅ Raycast 安装成功" -ForegroundColor Green
} else {
    Write-Host "❌ Raycast 安装失败" -ForegroundColor Red
}

Write-Host "🎉 脚本执行完毕！请检查日志。" -ForegroundColor Cyan
```
