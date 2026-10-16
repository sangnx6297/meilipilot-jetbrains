# Master Implementation Plan

> Phiên bản: 1.0  
> Baseline: 16/10/2026  
> Mục tiêu: Implement toàn bộ Community, Professional và backlog mở rộng của MeiliPilot JetBrains

## 1. Delivery strategy

Triển khai theo vertical slices trên một modular monolith:

```text
Foundation
  ↓
Connections + Transport + Security
  ↓
Explorer + Indexes
  ↓
Search + Documents
  ↓
Settings + Tasks
  ↓
Settings Diff + Migration + Search Debugger
  ↓
Advanced Network + Commercial/Team backlog
  ↓
Hardening + Release
```

Mỗi phase phải để lại plugin có thể build/chạy. Không tạo trước toàn bộ abstraction trừ khi phase kế tiếp sử dụng ngay.

## 2. Scope matrix

| Capability | Tier | Plan | Release target |
|---|---|---|---|
| Native Tool Window/editor/action architecture | Core | 01 | Alpha foundation |
| Connection profiles và test connection | Community | 02 | Alpha |
| Password Safe và redaction | Core security | 02 | Alpha |
| Multi-instance/environment/read-only | Community | 02 | Alpha |
| Index explorer/details/stats/CRUD | Community | 03 | Alpha |
| Search console/raw request-response | Community | 04 | Alpha |
| Query history | Community | 04 | MVP |
| Document browser/table/JSON | Community | 04 | MVP |
| Document add/update/replace/delete | Community | 04 | MVP |
| Settings viewer/editor/reset | Community | 05 | MVP |
| Task list/filter/poll/details/cancel | Community | 05 | MVP |
| Production safeguards | Core security | 02/05 | MVP |
| Semantic settings diff | Professional | 06 | Pro beta |
| Migration preview/selective apply/drift | Professional | 06 | Pro beta |
| Search run comparison | Professional | 06 | Pro beta |
| Saved presets/workspace templates | Professional | 07 | Post-MVP |
| Advanced proxy/custom CA | Professional | 07 | Post-MVP |
| SSH tunnel | Professional | 07 | Post-MVP |
| License gating/offline activation | Commercial | 07 | Post-traction |
| Shared presets/team policies | Team | 07 | Post-traction |
| Marketplace package/release | All | 08 | Mỗi release |

## 3. Milestones

### M0 — Architecture proof, target cuối Phase 1

- [ ] Build/run plugin bằng target IDE.
- [ ] Production package root và resource bundle được chuẩn hóa.
- [ ] Tool Window native mở được và dispose đúng.
- [ ] Custom Meili resource mở thành editor tab.
- [ ] Application/project light service POC pass lifecycle test.
- [ ] CI build, tests và verifier skeleton hoạt động.

### M1 — Connection vertical slice, target cuối Phase 2

- [ ] Tạo/sửa/xóa/test connection.
- [ ] API key chỉ ở Password Safe.
- [ ] HTTP transport hỗ trợ cancellation, timeout và redaction.
- [ ] Health/version/capability hiển thị đúng.
- [ ] Read-only và production session guard tồn tại ở application layer.

### M2 — Explorer alpha, target cuối Phase 3

- [ ] Tool Window hiển thị nhiều connections và indexes.
- [ ] Lazy refresh, loading/error/empty states.
- [ ] Index overview/stats/create/delete.
- [ ] Context actions và keyboard navigation hoạt động.

### M3 — Daily-use MVP, target cuối Phase 5

- [ ] Search, documents, settings và tasks dùng được end-to-end.
- [ ] Mọi async mutation theo dõi tới task terminal hoặc Task Monitor.
- [ ] Không freeze EDT và không lifecycle leak trong smoke tests.
- [ ] Production destructive actions có strong confirmation.

### M4 — Pro beta, target cuối Phase 6

- [ ] Semantic settings diff đúng order semantics.
- [ ] Migration preview/selective apply có drift detection.
- [ ] Search run comparison chỉ hiển thị metadata có thật.
- [ ] Export JSON/Markdown không chứa secret.

### M5 — Extended product, target cuối Phase 7

- [ ] Advanced network features có security review.
- [ ] Presets/templates ổn định.
- [ ] SSH/licensing/team features chỉ release khi acceptance gates riêng pass.

### M6 — Public release, target cuối Phase 8

- [ ] IDE compatibility matrix và Meilisearch matrix pass.
- [ ] Marketplace metadata/package/signing hoàn tất.
- [ ] User guide, privacy/security và diagnostics guide hoàn tất.
- [ ] Không còn P0 blocker.

## 4. Critical path

```text
FND-001 Build baseline
→ FND-004 Service/lifecycle baseline
→ NET-001 Transport spike
→ SEC-001 Credential facade
→ CON-004 Session/capability
→ EXP-003 Lazy explorer
→ SEA-004 Search vertical slice
→ TSK-003 Central task polling
→ DOC-008 Mutations
→ SET-007 Settings apply
→ DIF-005 Semantic diff
→ MIG-007 Migration executor
→ QA-010 Release gate
```

## 5. Cross-cutting workstreams

### Architecture/ADR

- [ ] ADR-001 client-only Kotlin/native UI.
- [ ] ADR-002 HTTP transport choice.
- [ ] ADR-003 service scopes/lifecycle.
- [ ] ADR-004 Password Safe and persisted metadata.
- [ ] ADR-005 custom editor resource strategy.
- [ ] ADR-006 async task state machine.
- [ ] ADR-007 settings diff/migration semantics.
- [ ] ADR-008 advanced TLS/SSH, trước Phase 7.
- [ ] ADR-009 licensing, trước commercial implementation.

### Security

- [ ] Threat model connection/credential/redirect/export.
- [ ] Central redaction tests.
- [ ] Dependency/license review.
- [ ] Destructive operation matrix.
- [ ] Diagnostic export review.

### Compatibility

- [ ] Chốt min/max IDE builds.
- [ ] Chốt Meilisearch version matrix.
- [ ] Fixtures cho unknown/new fields.
- [ ] Capability fallback policy.
- [ ] Remote Development support statement.

### Documentation

- [ ] Architecture overview.
- [ ] API compatibility matrix.
- [ ] Security model.
- [ ] User guide theo workflow.
- [ ] Troubleshooting/diagnostics.
- [ ] Release checklist/changelog.

## 6. Estimation model

Mỗi task được estimate theo ideal developer days sau technical spike:

- `S`: ≤ 1 ngày;
- `M`: 2–3 ngày;
- `L`: 4–5 ngày;
- `XL`: phải chia nhỏ trước khi implement.

Không cộng estimate thành release date trước khi hoàn tất Phase 1–2, vì HTTP/proxy/editor lifecycle là các uncertainty lớn nhất.

## 7. Definition of Ready

Task sẵn sàng khi:

- có user-visible behavior;
- biết dependency và owner;
- có API/extension point dự kiến;
- có acceptance criteria testable;
- có security/lifecycle impact;
- không còn câu hỏi kiến trúc làm thay đổi >30% implementation.

## 8. Definition of Done

Task hoàn tất khi:

- implementation không vi phạm dependency rule;
- không blocking I/O trên EDT;
- cancellation/disposal được xử lý;
- unit/platform/integration tests phù hợp pass;
- action state đúng read-only/capability;
- strings được localize qua bundle;
- errors sanitized;
- docs/compatibility được cập nhật;
- Plugin Verifier không phát sinh lỗi mới liên quan.

## 9. Release branching và feature flags

- Main branch luôn build được.
- Feature chưa hoàn tất được giấu bằng internal feature flag hoặc không đăng ký action/extension.
- Không để half-implemented write action xuất hiện trong production build.
- Schema/state migration có version và backward-compatibility test.
- Community core không phụ thuộc licensing service.

## 10. Completion criteria toàn chương trình

Chương trình được coi là implement đầy đủ khi tất cả capability trong scope matrix có một trong ba trạng thái:

1. released và đạt acceptance criteria;
2. deferred có ADR/issue, lý do và release target mới;
3. removed khỏi scope bằng quyết định sản phẩm được ghi lại.

