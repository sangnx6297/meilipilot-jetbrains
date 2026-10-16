# Phase 4 — Search and Documents

## Objective

Implement hai workflow hằng ngày quan trọng nhất: search console và document browser/editor, gồm raw JSON, history, paging, validation và mutation theo task semantics.

## Dependencies

- Phase 3 exit criteria.
- Task handle abstraction từ Index phase; polling hoàn chỉnh ở Phase 5.

## Deliverables

- Search editor typed + advanced JSON.
- Result table/raw/metadata.
- Query history và privacy controls.
- Document paging/table/JSON/detail editor.
- Add/update/replace/delete mutations với preview và guard.

## Tasks

### Search domain/API

- [ ] **SEA-001 (M):** `SearchRequest`, common options và raw extension fields.
- [ ] **SEA-002 (M):** `SearchResult`, hit, facet và metadata models.
- [ ] **SEA-003 (M):** Search DTO mapping giữ unknown fields/raw payload có limit.
- [ ] **SEA-004 (M):** `SearchApi` và `ExecuteSearchUseCase` cancellable.
- [ ] **SEA-005 (M):** Filter/sort/facet validation tối thiểu, không over-validate server syntax.

### Search editor

- [ ] **SEA-010 (M):** Query/basic options toolbar.
- [ ] **SEA-011 (L):** Advanced JSON editor dùng IntelliJ Editor API.
- [ ] **SEA-012 (M):** Compose typed fields + advanced JSON với conflict rules rõ ràng.
- [ ] **SEA-013 (L):** Result `JBTable` với dynamic columns và paging controls.
- [ ] **SEA-014 (M):** Raw request/response viewer, format/copy/export.
- [ ] **SEA-015 (S):** Metadata: latency, processing time, hit counts, payload size.
- [ ] **SEA-016 (M):** Run/Cancel actions và `Ctrl+Enter` shortcut.
- [ ] **SEA-017 (M):** Stale result protection khi chạy query liên tiếp.
- [ ] **SEA-018 (M):** Loading/empty/error/rate-limit states.

### Query history

- [ ] **SEA-020 (M):** Project-scoped `QueryHistoryService` với retention limit.
- [ ] **SEA-021 (S):** Privacy setting: off/clear history.
- [ ] **SEA-022 (M):** History UI, rerun và remove item.
- [ ] **SEA-023 (M):** Sanitization: không lưu key/header và có policy cho query payload.
- [ ] **SEA-024 (S):** Persist schema/version tests.

### Documents domain/API

- [ ] **DOC-001 (M):** Document identity và JSON representation policy.
- [ ] **DOC-002 (M):** Page request/result models.
- [ ] **DOC-003 (L):** List/get documents endpoints và filter/paging options.
- [ ] **DOC-004 (L):** Add/update, add/replace, delete IDs, delete filter endpoints.
- [ ] **DOC-005 (M):** Batch/response size limits.
- [ ] **DOC-006 (M):** Primary key ambiguity/error mapping.

### Document browser/editor

- [ ] **DOC-010 (L):** Documents editor shell và page state.
- [ ] **DOC-011 (L):** Dynamic table columns từ page sample.
- [ ] **DOC-012 (M):** JSON page/raw view luôn khả dụng.
- [ ] **DOC-013 (M):** Document detail JSON editor, format và validation.
- [ ] **DOC-014 (M):** Dirty state, Apply/Revert/close confirmation.
- [ ] **DOC-015 (M):** Add/update mutation preview.
- [ ] **DOC-016 (M):** Replace warning về field removal semantics.
- [ ] **DOC-017 (M):** Delete IDs preview/strong confirmation.
- [ ] **DOC-018 (L):** Delete by filter preview, capability gate và high-risk confirmation.
- [ ] **DOC-019 (M):** Mutation handoff sang Task Monitor.
- [ ] **DOC-020 (M):** Reload/invalidate page sau task success.

### Export/copy

- [ ] **DOC-030 (M):** Export current page JSON/NDJSON.
- [ ] **DOC-031 (M):** Streaming export design cho phạm vi lớn; chưa bật nếu không đạt memory/cancel tests.
- [ ] **DOC-032 (S):** Clipboard actions có size warning.

## Tests

- Search request composition không mất advanced fields.
- Cancel search không render late result.
- History respects disabled/retention/clear.
- Dynamic document table chịu nested/array/Unicode/missing fields.
- JSON invalid không được gửi.
- Update và replace tạo payload/endpoint khác nhau đúng semantics.
- Delete by filter bị chặn ở read-only/unsupported connection.
- Page size/response limit ngăn memory blow-up.

## Exit criteria

- Search và document read workflow usable end-to-end.
- Write workflow tạo task handle và không hiển thị success sớm.
- Không full-index load trong browser.
- Raw request/response giúp debug nhưng đã redact và giới hạn size.

## Risks

- Dynamic schema làm table khó dùng: JSON view là source of truth.
- JSON editor bridge phức tạp: giữ text editor và form state độc lập, merge rõ ràng.

