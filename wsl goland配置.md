# wsl goland配置
## 预置条件
Windows 10 内部版本 19044+ 或 Windows 11 

## 现有wsl安装
```bash
# 避免update卡死
wsl --shutdown
wsl --update
wsl
```

## 软件安装

安装文本编辑器, 文件管理器
```bash
sudo apt install gedit -y
sudo apt install nautilus -y
```

安装edge
[下载 Microsoft Edge Insider Channels](https://www.microsoftedgeinsider.com/zh-cn/download?platform=linux-deb)
`sudo apt-get install ./<xxx.deb>`

安装gpu驱动
[GPU in Windows Subsystem for Linux (WSL) | NVIDIA Developer](https://developer.nvidia.com/cuda/wsl)

安装goland
[Download GoLand: A Go IDE with extended support for JavaScript, TypeScript, and databases](https://www.jetbrains.com/go/download/#section=linux)

下载后需解压, 进入bin运行`goland.sh`即可; 学生版配置license需要安装edge等浏览器

## 参考资料

[使用 WSL 运行 Linux GUI 应用 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/tutorials/gui-apps)

## TroubleShooting
WSL (11) ERROR: UtilTranslatePathList:2671: Failed to translate

windows环境变量对应的目录不存在了, 导致挂卷失败, 删除环境变量, `wsl --shutdown`, 重新打开windows terminal即可
