# Phase 6 — Settings Diff, Migration and Search Debugger

## Objective

Implement nhóm tính năng Professional tạo khác biệt: semantic settings diff, migration preview/selective apply/drift detection và search run comparison.

## Dependencies

- Phase 5 exit criteria.
- Compatibility fixtures đủ cho settings/task API.

## Deliverables

- Pure settings diff engine.
- Diff editor và export Markdown/JSON.
- Migration planner/executor an toàn.
- Search snapshots và comparison editor.

## Tasks

### Semantic diff engine

- [ ] **DIF-001 (M):** Định nghĩa `SettingsGroup`, path và comparison metadata.
- [ ] **DIF-002 (L):** Version-aware normalization không làm mất raw semantics.
- [ ] **DIF-003 (M):** Phân biệt unset/default/explicit khi có thể.
- [ ] **DIF-004 (M):** Order-sensitive strategy cho ranking rules và tương tự.
- [ ] **DIF-005 (L):** Pure `SettingsDiffEngine` và fixtures.
- [ ] **DIF-006 (M):** Diff severity/risk classification.
- [ ] **DIF-007 (M):** Canonical fingerprint ổn định.

### Diff UI và export

- [ ] **DIF-010 (M):** Source/target selector khác connection/index.
- [ ] **DIF-011 (L):** Side-by-side/grouped diff editor.
- [ ] **DIF-012 (M):** Select/unselect groups và dependency warnings.
- [ ] **DIF-013 (M):** Raw value inspection.
- [ ] **DIF-014 (M):** Export Markdown sanitized.
- [ ] **DIF-015 (M):** Export machine-readable JSON schema/version.

### Migration planner

- [ ] **MIG-001 (M):** `MigrationOperation`, `MigrationWarning`, `MigrationPlan`.
- [ ] **MIG-002 (M):** Plan từ selected diff groups.
- [ ] **MIG-003 (M):** Exact endpoint/payload/order preview.
- [ ] **MIG-004 (M):** Target baseline snapshot/fingerprint.
- [ ] **MIG-005 (M):** Capability/permission/read-only/preflight checks.
- [ ] **MIG-006 (M):** Reindex/production/high-risk labels.

### Migration executor

- [ ] **MIG-010 (M):** Re-fetch target và drift check ngay trước apply.
- [ ] **MIG-011 (M):** Strong confirmation gồm source/target/env/index.
- [ ] **MIG-012 (L):** Execute operations theo explicit order.
- [ ] **MIG-013 (M):** Handoff mọi async operation sang TaskMonitor.
- [ ] **MIG-014 (M):** Stop/continue policy khi partial failure.
- [ ] **MIG-015 (M):** Result report và manual restore guidance.
- [ ] **MIG-016 (M):** Không claim transaction/automatic rollback.
- [ ] **MIG-017 (M):** Migration editor lifecycle/reopen result.

### Search snapshots

- [ ] **DBG-001 (M):** `SearchSnapshot` sanitized schema.
- [ ] **DBG-002 (M):** Project-local storage và retention.
- [ ] **DBG-003 (M):** Capture latency/hit count/order/IDs/payload size.
- [ ] **DBG-004 (S):** Capture score/ranking metadata chỉ khi API trả về.
- [ ] **DBG-005 (M):** Explicit save hoặc policy auto-save có privacy control.

### Search comparison

- [ ] **DBG-010 (M):** Pure comparison engine.
- [ ] **DBG-011 (L):** Chọn hai runs và comparison editor.
- [ ] **DBG-012 (M):** Result order change, added/removed/moved documents.
- [ ] **DBG-013 (M):** Latency/count/metadata comparison.
- [ ] **DBG-014 (M):** Export sanitized comparison report.
- [ ] **DBG-015 (S):** UX nói rõ giới hạn không tái dựng ranking internals.

## Tests

- Semantic diff fixtures cho reordered object keys và order-sensitive arrays.
- Fingerprint ổn định và drift detection chính xác.
- Migration không apply khi target drift/read-only/capability thiếu.
- Partial failure report không tuyên bố rollback.
- Export không chứa credential/authorization.
- Search comparison đúng moved/added/removed result và missing metadata.

## Exit criteria

- M4 Pro beta hoàn tất.
- Diff có giá trị semantic, không chỉ JSON text diff.
- Migration luôn preview/recheck/confirm trước write.
- Search debugger chỉ báo dữ liệu có thật từ response.

## Risks

- Default/unset semantics không đủ từ API: hiển thị `unknown/effective` thay vì suy đoán.
- Multi-operation migration không atomic: report từng operation/task và dừng policy rõ ràng.

