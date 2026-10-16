# Phase 7 — Advanced Network and Extended Product Features

## Objective

Triển khai các tính năng sau MVP/Pro beta: presets/templates, advanced TLS/proxy, SSH tunnel và hạ tầng commercial/team. Mỗi nhóm phải qua gate riêng; không được làm suy yếu Community core.

## Dependencies

- Phase 6 exit criteria cho product workflow.
- Security ADR/threat model tương ứng trước từng network/commercial feature.

## Workstream A — Saved presets và workspace templates

### Deliverables

- Search presets.
- Workspace template mapping connections/indexes/views.
- Import/export qua file/Git không chứa secret.

### Tasks

- [ ] **ADV-001 (M):** Preset schema/version và stable identifiers.
- [ ] **ADV-002 (M):** Save/apply/rename/delete search preset.
- [ ] **ADV-003 (M):** Import/export preset JSON sanitized.
- [ ] **ADV-004 (M):** Workspace template schema.
- [ ] **ADV-005 (L):** Apply template với missing connection/index handling.
- [ ] **ADV-006 (M):** Git-friendly deterministic serialization.
- [ ] **ADV-007 (M):** Schema migration/backward compatibility tests.

## Workstream B — Advanced proxy và custom CA

### Gate

- HTTP transport đã có proxy/TLS test coverage.
- Threat model và ADR được duyệt.

### Tasks

- [ ] **NET-020 (M):** Phân biệt IDE proxy, system proxy và per-connection override.
- [ ] **NET-021 (M):** Proxy credentials qua secure store.
- [ ] **NET-022 (L):** Custom CA/trust material per connection hoặc profile.
- [ ] **NET-023 (M):** Không có global trust-all switch.
- [ ] **NET-024 (M):** TLS error diagnostics không lộ secret.
- [ ] **NET-025 (M):** Certificate rotation/update UX.
- [ ] **NET-026 (L):** Tests self-signed/custom CA/proxy auth/redirect.

## Workstream C — SSH tunnel

### Gate

- ADR library/process model.
- Host-key verification design.
- Credential storage design.
- Cleanup/lifecycle POC.

### Tasks

- [ ] **ADV-020 (L):** `SshProfile` metadata và secure credential references.
- [ ] **ADV-021 (L):** SSH client/tunnel adapter abstraction.
- [ ] **ADV-022 (M):** Host key verification/known host workflow.
- [ ] **ADV-023 (M):** Local port allocation và collision handling.
- [ ] **ADV-024 (L):** Tunnel lifecycle gắn ConnectionSession/project.
- [ ] **ADV-025 (M):** Reconnect/backoff và user-visible state.
- [ ] **ADV-026 (M):** Cleanup khi disconnect/project close/IDE exit.
- [ ] **ADV-027 (M):** Không truyền passphrase/private key qua command line/log.
- [ ] **ADV-028 (L):** Integration tests với disposable SSH server.

## Workstream D — Licensing/commercial gating

### Gate

- Product decision và legal/privacy review.
- ADR chứng minh Community core hoạt động không cần licensing/network.

### Tasks

- [ ] **ADV-040 (M):** `EntitlementService` port, default Community implementation.
- [ ] **ADV-041 (M):** Feature capability mapping Community/Pro/Team.
- [ ] **ADV-042 (L):** Signed license verification local nếu chọn offline payload.
- [ ] **ADV-043 (M):** Grace/expiration UX không khóa dữ liệu user.
- [ ] **ADV-044 (M):** License state persistence không chứa payment data.
- [ ] **ADV-045 (M):** Offline/no-network behavior.
- [ ] **ADV-046 (M):** Tests Community features không gọi licensing backend.
- [ ] **ADV-047 (M):** Marketplace/legal text và privacy update.

## Workstream E — Team policies/shared configuration

- [ ] **ADV-060 (M):** Policy template schema và version.
- [ ] **ADV-061 (M):** Read-only/production defaults từ project file.
- [ ] **ADV-062 (M):** Merge local override với team policy rõ ràng.
- [ ] **ADV-063 (M):** Shared migration plan via Git.
- [ ] **ADV-064 (M):** Secret scanner từ chối import/export có credential.
- [ ] **ADV-065 (L):** Approval workflow chỉ sau validated customer demand.

## Tests

- Preset/template deterministic và không chứa secret.
- Custom CA chỉ tác động connection/profile dự kiến.
- SSH tunnel cleanup không còn process/socket/port.
- Host key mismatch fail closed.
- Community mode vẫn dùng được core feature khi licensing unavailable.
- Expired license không xóa hoặc khóa export dữ liệu user.

## Exit criteria

- M5 chỉ hoàn tất với các workstream đã được product chọn release.
- Workstream chưa release phải ở trạng thái deferred có ADR/issue, không để UI nửa vời.
- Không advanced feature nào bypass transport, Password Safe, OperationGuard hoặc lifecycle model.

## Risks

- SSH/TLS tăng attack surface: tách release và security review.
- Licensing làm giảm reliability: dependency đảo chiều để core không phụ thuộc commercial service.
- Team policies có thể trở thành backend SaaS ngoài scope: ưu tiên file/Git local-first.

