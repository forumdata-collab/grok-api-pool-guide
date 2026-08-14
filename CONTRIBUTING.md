# CONTRIBUTING

提交前請確認 (checklist)：

- [ ] 全文佔位符統一為 `<YOUR_...>` 或 `YOUR_...` 格式，**禁止出現真實 Key / Token / 域名 / IP**
- [ ] 無真實 API Key 洩漏（`grep -rn "sk-" .`）
- [ ] `.env` 已加入 `.gitignore`，絕不提交
- [ ] 日期格式為 ISO 8601（`2026-08-15`）
- [ ] 新增腳本放 `tools/` 目錄
- [ ] 配置模板同步更新 `templates/`
- [ ] 本地 `python3 -m http.server 8080` 預覽正常
- [ ] 內容以實測為準，註明測試日期

CI 會在 push 時自動檢查 Key 洩漏與 `.env` 追蹤，紅線不過不放行。