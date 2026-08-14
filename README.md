# Grok API Pool 部署指南 · 負載均衡與 Key 輪詢實戰

> 開放 API 實戰指南 — 用 LiteLLM / Nginx+Lua / 自建 FastAPI 閘道三套方案，做 Grok API 的多 Key 負載均衡、健康檢查、熔斷與監控。

**線上頁面** → https://forumdata-collab.github.io/grok-api-pool-guide/

## 這份指南講什麼

| 章節 | 內容 |
|---|---|
| 為什麼需要 Pool | 速率限制、單點故障、用量盲區、被封風險 |
| 核心機制 | Round-Robin 輪詢、加權輪詢、健康檢查、熔斷、緩存層、日誌監控 |
| 方案一：LiteLLM | config.yaml 多 Key 輪詢 + 健康檢查 + 熔斷、.env、systemd、實測驗證 |
| 方案二：Nginx+Lua | OpenResty、完整 nginx.conf 模板（Key 池 + 輪詢 + 熔斷 + 入口鑒權） |
| 方案三：自建閘道 | gateway.py 主程式、Docker 部署（可選） |
| 安全硬性要求 | 佔位符命名規則、HTTPS + 鑒權 |
| 運維 | logrotate 日誌輪替、Prometheus 指標 |
| 帳號註冊流程 | registration-workflow 頁面：批次註冊、驗證、防封 |

## 技術摘要

- **閘道方案**：LiteLLM（最快上線）/ Nginx+Lua（輕量）/ 自建 FastAPI（完全可控）三選一
- **負載均衡**：Round-Robin + 加權輪詢；健康檢查剔除失效率 Key；熔斷保護
- **安全**：入口強制 HTTPS + Bearer 鑒權；全部敏感值用佔位符
- **監控**：logrotate + Prometheus `/metrics`
- **實測**：每章附驗證步驟（輪詢 + 熔斷實測）

## 目錄結構

```
grok-api-pool-guide/
├── index.html                 # 主指南（部署 + 三大方案 + 運維）
├── registration-workflow.html # 帳號批次註冊流程
└── README.md                  # 本文件
```

## 本地開發 / 預覽

```bash
# 改完直接 push 即自動更新 Pages
git add . && git commit -m "update" && git push

# 本地預覽
python3 -m http.server 8080
# → http://localhost:8080
```

## 相關兄弟指南

- [夸克網盤 × GDrive 同步教學](https://forumdata-collab.github.io/quark-gdrive-sync-guide/)
- [Hermes CF 教學](https://forumdata-collab.github.io/hermes-cf-guide/)
- [Hermes Oracle 教學](https://forumdata-collab.github.io/hermes-oracle-guide/)

## 授權

內容以 CC BY-NC 形式分享，歡迎引用並註明出處。