# Task Spec: l1-closure-verify-001

## Metadata

| 欄位 | 值 |
|---|---|
| task_id | `l1-closure-verify-001` |
| task_type | `probe` |
| source_node | `mac` |
| target_node | `windows` |
| dispatched_at | `2026-04-01T06:15:00+08:00` |
| state | `dispatched` |
| priority | `10` |
| purpose | Level 1 closure 雙端驗證探測任務 |

## 任務說明

本任務是 Level 1 closure 雙端驗證的專用探測任務。

**目的：** 驗證 Mac → Task_stack → Windows ingress → claim → receipt → Task_stack → Mac observe 完整鏈路。

**Windows 端預期動作：**

1. 從 Task_stack 偵測到本任務（git pull / ingress polling）
2. Claim 本任務（觸發 `TaskStore.claim_next_task()` 或手動 claim）
3. 生成 `runs/l1-closure-verify-001/claim-receipt.json`
4. 將 claim-receipt.json commit & push 回 Task_stack

**不需要實際執行任務內容。** 本任務是純探測任務，Windows 只需完成 claim 並回傳 receipt。

## Claim Receipt 預期欄位

Windows 生成的 `claim-receipt.json` 應至少包含：

| 欄位 | 預期值 |
|---|---|
| `task_id` | `l1-closure-verify-001` |
| `claimed_by` | Windows 節點識別（如 `windows-exec`） |
| `claimed_at` | ISO 8601 時間戳 |
| `state` | `claimed` |
| `source_node` | `mac` |
| `target_node` | `windows` |
| `receipt_version` | 非空版本號 |

## 驗收標準

Mac 端在 Task_stack 觀察到符合上述 schema 的 claim-receipt.json 時，Level 1 closure = PASS。
