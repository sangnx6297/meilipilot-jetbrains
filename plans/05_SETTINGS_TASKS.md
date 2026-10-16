# Phase 5 — Settings and Task Lifecycle

## Objective

Hoàn tất Community MVP bằng settings editor và central task monitor. Chuẩn hóa toàn bộ semantics của asynchronous operations, production safeguards và cache invalidation.

## Dependencies

- Phase 4 exit criteria.

## Deliverables

- Task domain/state machine/polling service.
- Tasks list/filter/detail/cancel.
- Settings viewer/editor/reset/update.
- Minimal patch preview và reindex warnings.
- Unified mutation outcome cho index/documents/settings.

## Tasks

### Task domain và API

- [ ] **TSK-001 (M):** `TaskUid`, `TaskStatus`, `TaskType`, `TaskInfo`, unknown status policy.
- [ ] **TSK-002 (M):** Task state machine và terminal outcome.
- [ ] **TSK-003 (M):** List/get tasks endpoints và filters.
- [ ] **TSK-004 (M):** Cancel/delete tasks capability-gated endpoints.
- [ ] **TSK-005 (M):** Error/details mapper giữ raw unknown data.

### Task monitor service

- [ ] **TSK-010 (L):** Project-scoped central `TaskMonitorService`.
- [ ] **TSK-011 (M):** Deduplicate polling theo connection/task UID.
- [ ] **TSK-012 (M):** Exponential backoff, cap, timeout và cancellation.
- [ ] **TSK-013 (M):** Terminal cache/retention và cleanup.
- [ ] **TSK-014 (M):** Publish task updates không chứa payload/secret.
- [ ] **TSK-015 (M):** Operation owner metadata để mở resource liên quan.
- [ ] **TSK-016 (M):** Project close/disconnect cleanup tests.

### Task UI

- [ ] **TSK-020 (L):** Task list editor với paging/filter/status/type/index/time.
- [ ] **TSK-021 (M):** Task detail editor: duration/details/error/link.
- [ ] **TSK-022 (M):** Active task badge trong explorer/status.
- [ ] **TSK-023 (M):** Cancel selected tasks với confirmation/capability.
- [ ] **TSK-024 (M):** Background completion/failure notification policy.
- [ ] **TSK-025 (S):** Unknown status UI không coi là success.

### Settings domain/API

- [ ] **SET-001 (L):** Settings model theo group + raw JSON preservation.
- [ ] **SET-002 (M):** Settings endpoints full/group get/update/reset.
- [ ] **SET-003 (M):** Version-aware DTO mapping và unknown fields.
- [ ] **SET-004 (L):** Settings validation/canonical representation baseline.
- [ ] **SET-005 (M):** Change classifier: low/medium/high/reindex risk.

### Settings editor

- [ ] **SET-010 (L):** Settings editor shell theo groups.
- [ ] **SET-011 (L):** Typed forms cho groups ổn định.
- [ ] **SET-012 (M):** Raw JSON editor và synchronization policy.
- [ ] **SET-013 (M):** Baseline/dirty state và Revert.
- [ ] **SET-014 (L):** Compute minimal PATCH và exact payload preview.
- [ ] **SET-015 (M):** Apply qua OperationGuard + TaskMonitor.
- [ ] **SET-016 (M):** Reset group/all strong confirmation.
- [ ] **SET-017 (M):** Reload baseline/cache khi task success.
- [ ] **SET-018 (M):** Conflict state nếu settings server thay đổi trong lúc editor dirty.

### Unified async semantics

- [ ] **TSK-030 (L):** Refactor index/document/settings mutations dùng chung `TaskHandle`.
- [ ] **TSK-031 (M):** UI wording `Accepted/Queued/Processing/Succeeded/Failed/Canceled` nhất quán.
- [ ] **TSK-032 (M):** Poll timeout chuyển sang background monitoring, không báo failure giả.
- [ ] **TSK-033 (M):** Aggregate outcome cho batch tasks.
- [ ] **TSK-034 (M):** Retry policy: không tự retry write không idempotent.

## Tests

- State machine cho mọi known/unknown status.
- Polling deduplicate và dừng đúng terminal/dispose/cancel.
- Task timeout không chuyển thành failed.
- Settings unchanged tạo empty patch.
- Order-sensitive settings giữ thứ tự.
- Reset/apply bị chặn đúng bởi read-only/production guard.
- Mutation của index/documents/settings có wording/outcome thống nhất.

## Exit criteria

- M3 Community MVP hoàn tất.
- Tất cả async mutations dùng central TaskMonitor.
- Settings workflow có preview, validation, confirmation và terminal result.
- Không còn đường write chuẩn nào bypass OperationGuard.

## Risks

- Meilisearch tasks API thay đổi field/filter: giữ raw + capability adapter.
- Settings form lag sau API update: raw JSON là fallback bắt buộc.

