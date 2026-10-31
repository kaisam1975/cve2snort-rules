<div align="center">

# cve2snort-rules

**Snort 2 偵測規則，一個 CVE 一個資料夾，可個別下載**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Snort 2](https://img.shields.io/badge/Snort-2-E01E5A)](#如何把規則載入-snort)

由 [cve2snort](https://github.com/kaisam1975/cve2snort) 產生，經人工審閱後發布。不含完整漏洞報告。MIT 授權。

</div>

---

## 如何把規則載入 Snort

每個 CVE 資料夾裡有：

- `<CVE>.rules` — Snort 2 規則（放到目標的 `rules/` 即可載入）
- `rules-doc.md` — 規則說明（sid、偵測範圍、限制）
- `vulnerability.md` — 公開版摘要（不是完整報告）

不必 clone 整個 repo。此映像載入 `/rules/*.rules`，**不必改** `snort.conf`。

### 1. 下載 `.rules`

```bash
# 把 CVE-2025-55182 換成你要的編號
CVE=CVE-2025-55182
curl -fsSL -o "${CVE}.rules" \
  "https://raw.githubusercontent.com/kaisam1975/cve2snort-rules/main/${CVE}/${CVE}.rules"
```

也可在 GitHub 檔案頁按 Download / Raw 另存。

### 2. 確認 sid 不衝突

打開檔案，看 `sid:` 是否已出現在目標 `rules/*.rules`。本專案自訂區段形如 `1004xxx`、`1005xxx`。重複的 sid 不要直接覆蓋。

### 3. 放到 `rules/` 並重啟

```bash
# 語法檢查（映像名與路徑依你的環境調整）
docker run --rm -v /path/to/snort/rules:/rules:ro local/snort2:2.9.20 -T

# 載入
docker restart snort2
```

`snort -T` 失敗就不要重啟。遠端機器請把檔案拷到該機的 `rules/` 再做同樣檢查與重啟。

---

## 規則一覽

| CVE | 簡介 | 規則檔 | 說明 |
| --- | --- | --- | --- |
| [CVE-2025-55182](CVE-2025-55182/) | React2Shell：React Server Components（RSC）在處理 Flight 協定時的不安全反序列化漏洞（CWE-502） | [CVE-2025-55182.rules](CVE-2025-55182/CVE-2025-55182.rules) | [規則說明](CVE-2025-55182/rules-doc.md) |
| [CVE-2026-103663](CVE-2026-103663/) | Ollama 模型拉取 layer digest 路徑穿越：Ollama 在 /api/pull 模型拉取流程中 | [CVE-2026-103663.rules](CVE-2026-103663/CVE-2026-103663.rules) | [規則說明](CVE-2026-103663/rules-doc.md) |
