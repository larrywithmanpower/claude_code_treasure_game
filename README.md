# MCP 圖片工具伺服器

🌐 **線上網站：** https://larrywithmanpower.github.io/claude-mcp-image-processor/

這是一個基於 MCP（Model Context Protocol）的圖片處理伺服器，透過 Docker 容器運行，並整合至 Claude Code 中使用。

## 功能介紹

| 工具 | 說明 |
|------|------|
| `fetch_toy_image` | 透過 DuckDuckGo 搜尋並下載圖片 |
| `resize_image` | 調整圖片尺寸，支援保持長寬比 |
| `remove_background_as_png` | AI 自動去背，輸出透明 PNG |

## 技術架構

- **FastMCP** — MCP 伺服器框架
- **Pillow** — 圖片處理
- **rembg + onnxruntime** — AI 去背模型（U2Net）
- **DuckDuckGo Search** — 圖片搜尋
- **Docker** — 容器化部署

## 快速開始

### 建置 Docker 映像檔

```bash
docker build -t mcp-toy-image-tools-server .
```

### 在 Claude Code 中使用

1. 確認 `.mcp.json` 設定正確
2. 在 Claude Code 執行 `/mcp`
3. 連線至 `image-tools-server-docker`

## 目錄結構

```
.
├── server.py                          # MCP 伺服器主程式
├── Dockerfile                         # Docker 容器設定
├── requirements.txt                   # Python 套件需求
├── .mcp.json                          # MCP 伺服器設定
├── images/                            # 圖片工作目錄
└── .claude/commands/
    └── deploy_github_page.md          # 一鍵部署至 GitHub Pages 指令
```

## 部署至 GitHub Pages

在 Claude Code 中執行：

```
/deploy_github_page
```

指令會自動：
1. 檢查 GitHub 登入狀態
2. 建立 GitHub Repo（若不存在）
3. 部署至 GitHub Pages

## 線上展示

- 網站：https://larrywithmanpower.github.io/claude-mcp-image-processor/
- 程式碼：https://github.com/larrywithmanpower/claude-mcp-image-processor
