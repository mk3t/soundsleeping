# 核对下载文件的 SHA-256

SHA-256 用于比较文件内容。下载后算出的值与发布清单中同名文件一致，表示下载内容与发布文件一致。大小写不影响比较。

## Windows：核对安卓轻量版

在保存 APK 的文件夹中打开 PowerShell：可以在文件管理器地址栏输入 `powershell` 后回车。运行以下命令：

```powershell
(Get-FileHash -LiteralPath '.\SoundSleeping-Android-0.2.1.apk' -Algorithm SHA256).Hash -eq 'fec6a5dfe03680ad442f322e5652a47405fa3e7a2230596fafa12770c2c8dd2a'
```

输出 `True` 表示一致；`False` 表示不一致。若提示找不到文件，确认当前文件夹和文件名，例如重复下载可能让文件名多出 `(1)`。这时修改命令中的文件名即可。

## 核对其他文件

从 [v0.2.1 Release](https://github.com/mk3t/soundsleeping/releases/tag/v0.2.1) 同时下载 `SHA256SUMS.txt`。在 PowerShell 中计算想核对的文件，例如电脑版轻量版：

```powershell
(Get-FileHash -LiteralPath '.\SoundSleeping-Desktop-0.2.1.zip' -Algorithm SHA256).Hash
```

用记事本打开 `SHA256SUMS.txt`，找到同名文件所在行，将行首的完整 64 位值与命令结果比较。只需核对自己下载的文件，无需下载全部附件。

请核对下载的 APK / ZIP 文件本身，而不是安装后的程序或解压后的目录。未来版本使用各自 Release 的清单，不能沿用此页中 0.2.1 APK 的固定值。

这用于核对内容一致性，不是软件功能或安全性的检测。[Microsoft Get-FileHash 官方说明](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash)
