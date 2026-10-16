# Phase 1 — Platform Foundation

## Objective

Tạo nền tảng IntelliJ Platform production-ready: build, package boundaries, plugin descriptor, services, Tool Window/editor proof, lifecycle và CI. Phase này chưa implement Meilisearch business feature ngoài fake adapter phục vụ vertical slice.

## Dependencies

- Không có.

## Deliverables

- Source/package structure production.
- Plugin metadata/resource bundle/icon chuẩn.
- Tool Window shell.
- `MeiliResourceKey`, editor registry và `FileEditorProvider` POC.
- Application/project light service lifecycle POC.
- Base UI state/result model.
- Test/verification pipeline.
- ADR foundation.

## Tasks

### Build và project structure

- [ ] **FND-001 (S):** Chuẩn hóa `group`, plugin name, vendor, description và version strategy.
- [ ] **FND-002 (M):** Chuyển demo classes vào `nxs.meili.meilipilot` và tạo package boundaries theo technical overview.
- [ ] **FND-003 (S):** Tạo `MeiliPilotBundle`, rename message keys và thay icon placeholder.
- [ ] **FND-004 (M):** Bổ sung version catalog cho serialization, HTTP candidate, test và quality tools.
- [ ] **FND-005 (S):** Cấu hình Java/Kotlin toolchain phù hợp target Platform.
- [ ] **FND-006 (M):** Cấu hình `verifyPluginProjectConfiguration`, `verifyPluginStructure`, `verifyPlugin` và build ZIP.

### Platform services và lifecycle

- [ ] **FND-010 (M):** Tạo application light service mẫu, project light service mẫu và retrieval helpers.
- [ ] **FND-011 (M):** Chứng minh project close cancel child coroutine/jobs.
- [ ] **FND-012 (S):** Tạo base `UiState<T>`/operation state không phụ thuộc Swing.
- [ ] **FND-013 (S):** Tạo disposal utilities cho listener/subscription/editor.
- [ ] **FND-014 (M):** Lifecycle tests: project dispose, editor dispose, no global job.

### Tool Window shell

- [ ] **FND-020 (M):** Implement `MeiliPilotToolWindowFactory` bằng `SimpleToolWindowPanel`.
- [ ] **FND-021 (S):** Mark DumbAware và xác thực dùng được khi IDE indexing.
- [ ] **FND-022 (M):** Tạo toolbar/action group placeholder qua Action System.
- [ ] **FND-023 (M):** Tạo explorer empty state và fake tree data source.
- [ ] **FND-024 (S):** Gắn content disposer và focus component.

### Editor integration POC

- [ ] **FND-030 (M):** Tạo `MeiliResourceKey`, `ResourceType` và stable display rules.
- [ ] **FND-031 (M):** Tạo project-scoped `MeiliEditorManager`/LightVirtualFile registry.
- [ ] **FND-032 (M):** Implement `MeiliFileEditorProvider` và base `MeiliResourceFileEditor`.
- [ ] **FND-033 (S):** Implement custom editor tab title/tooltip provider.
- [ ] **FND-034 (M):** POC open/focus/reuse/close một fake index editor.
- [ ] **FND-035 (M):** Test dirty state, dispose và repeated open không tạo duplicate tab.

### Actions, settings, notifications skeleton

- [ ] **FND-040 (S):** Định nghĩa custom DataKeys cho connection/resource/tree selection.
- [ ] **FND-041 (M):** Base action classes và update-thread policy.
- [ ] **FND-042 (M):** Register application configurable skeleton.
- [ ] **FND-043 (S):** Register notification group và sanitized notification helper.

### ADR và CI

- [ ] **FND-050 (S):** ADR client-only Kotlin/native JetBrains UI.
- [ ] **FND-051 (S):** ADR service scopes/lifecycle.
- [ ] **FND-052 (S):** ADR LightVirtualFile + FileEditorProvider session strategy.
- [ ] **FND-053 (M):** CI build/test/verify artifacts.
- [ ] **FND-054 (S):** Contributor checks và local commands trong README.

## Tests

- Plugin descriptor loads.
- Tool Window factory creates one content and disposes subscriptions.
- Editor provider only accepts Meili virtual resources.
- Open same `MeiliResourceKey` reuses tab.
- Project disposal cancels scoped jobs.
- Actions update without network/heavy work.
- `verifyPluginStructure` và verifier baseline pass.

## Exit criteria

- M0 trong master plan hoàn tất.
- Demo random button bị loại bỏ.
- Plugin chạy được với shell UI production naming.
- Không còn package/class placeholder `My*`.
- Architecture tests đủ để Phase 2 thêm transport/services mà không đổi lifecycle model.

## Risks

- `FileEditorProvider`/LightVirtualFile không đáp ứng restore requirement: chấp nhận session-only trong MVP.
- Target duy nhất 2025.3 che lỗi compatibility: thêm verifier matrix tối thiểu ngay trong Phase 1.

