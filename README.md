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
