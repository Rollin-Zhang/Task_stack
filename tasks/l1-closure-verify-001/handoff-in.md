# Handoff-In: l1-closure-verify-001

## Metadata

| 欄位 | 值 |
|---|---|
| task_id | `l1-closure-verify-001` |
| handoff_direction | `mac → windows` |
| handoff_at | `2026-04-01T06:15:00+08:00` |
| handoff_type | `dispatch` |

## 交接摘要

Mac 主控端透過 Task_stack task-plane 將本任務 dispatch 給 Windows 執行端。

## 交接內容

- **任務類型：** probe（純探測，不需實際執行）
- **Windows 需完成：** claim + 生成 claim-receipt.json + push 回 Task_stack
- **不需要：** 實際任務執行、execution log、handoff-out

## 前置條件

| 項目 | 狀態 |
|---|---|
| P3-A（Windows claim receipt 能力） | ✅ 已驗證 |
| P3-B（Task_stack ingress 能力） | ✅ 已驗證 |
| Task_stack Git push 能力 | ✅ git push --dry-run 已通過 |

## 預期回傳

Windows 在 claim 後，應將 `runs/l1-closure-verify-001/claim-receipt.json` push 回 Task_stack，供 Mac 端驗證。
