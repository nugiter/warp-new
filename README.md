# WarpScout-Chain

Wails v2 + Go Windows GUI application.

## GitHub Actions 自动编译 Windows EXE

本仓库已经包含可直接运行的 GitHub Actions 工作流：

`.github/workflows/build-windows.yml`

### 方法一：手动编译

1. 将整个项目上传到 GitHub 仓库。
2. 打开仓库的 **Actions**。
3. 选择 **Build Windows EXE**。
4. 点击 **Run workflow**。
5. 等待 `Windows x64` job 完成。
6. 在该次运行页面的 **Artifacts** 中下载 `WarpScoutChain-Windows-x64`。

### 方法二：推送到 main/master 自动编译

工作流也会在 `main` 或 `master` 分支的 Go/Wails/前端相关文件发生变化时自动运行。

## 本地 Windows 编译

要求：

- Windows 10/11 x64
- Go 1.22.x
- Node.js 20.x
- Wails CLI v2.9.2
- Windows WebView2 Runtime

命令：

```powershell
go install github.com/wailsapp/wails/v2/cmd/wails@v2.9.2
go mod download
wails build -clean -platform windows/amd64 -ldflags "-s -w -H windowsgui"
```

生成文件：

```text
build/bin/WarpScoutChain.exe
```

## 项目结构

```text
WarpScout-Chain/
├── .github/
│   └── workflows/
│       └── build-windows.yml
├── frontend/
│   └── index.html
├── app.go
├── main.go
├── go.mod
├── wails.json
├── .gitignore
├── .gitattributes
└── README.md
```

> 当前项目的前端为纯 HTML/CSS/JavaScript，不需要 npm 构建步骤；Node.js 保留在 Actions 环境中以兼容 Wails 构建环境。
