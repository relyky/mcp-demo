# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 專案概述

這是一個 MCP (Model Context Protocol) 伺服器示範專案,使用 FastMCP 框架來建立工具和資源。

## 主要參考文件
- [使用 uv 輔助開發 MCP 伺服器並安裝到 Claude Desktop 與 VS Code](https://blog.miniasp.com/post/2025/04/01/Write-your-own-MCP-server-using-uv-and-Python)

## 開發環境

- Python 版本: >=3.14
- 套件管理工具: uv
- 主要依賴: mcp[cli]>=1.21.0

## 常用指令

### 安裝依賴
```bash
uv sync
```

### 執行 MCP 伺服器
測試時使用。將開啟 MCP Inspector 測試頁面。
```bash
uv run mcp dev server.py
```

安裝 server.py 這個 MCP Server 到 Claude Desktop 之中。
```bash
uv run mcp install server.py
```

或直接使用 Python:
```bash
python -m mcp.server.fastmcp server.py
```

### 執行主程式(單元測試)
```bash
uv run main.py
```

## 架構說明

### 核心檔案

- **server.py**: MCP 伺服器實作
  - 使用 `FastMCP` 建立伺服器實例
  - 透過 `@mcp.tool()` 裝飾器定義工具函數
  - 透過 `@mcp.resource()` 裝飾器定義動態資源,支援路徑參數

### MCP 伺服器模式

此專案使用 FastMCP 框架,特點:
- 工具函數使用 `@mcp.tool()` 裝飾器標記
- 資源使用 `@mcp.resource("uri://{param}")` 定義,支援 URI 模板
- 工具和資源的文檔字串會自動成為 MCP 介面的描述

### 擴展伺服器功能

1. 新增工具:在 server.py 中加入帶有 `@mcp.tool()` 的函數
2. 新增資源:使用 `@mcp.resource()` 定義資源 URI 模板和處理函數
