# Phase 2 — Connections, Transport and Security

## Objective

Hoàn thành vertical slice kết nối trực tiếp Meilisearch: profile metadata, Password Safe, HTTP transport, typed system/index probes, capability detection, error taxonomy và operation guard.

## Dependencies

- Phase 1 exit criteria.

## Deliverables

- Connection CRUD/test UI.
- Persisted profile metadata không có secret.
- Password Safe credential facade.
- Cancellable HTTP transport.
- Health/version/index-list client tối thiểu.
- Connection sessions/capabilities.
- Read-only/production operation guard.
- Redacted diagnostics.

## Tasks

### Domain và persistence

- [ ] **CON-001 (S):** `ConnectionId`, `ConnectionProfile`, `EnvironmentType`, validation rules.
- [ ] **CON-002 (M):** Application-level `ConnectionProfileService` với custom storage/roaming disabled.
- [ ] **CON-003 (M):** State schema version và migration test cho profile.
- [ ] **CON-004 (S):** Endpoint normalization: scheme, trailing slash, path prefix và display URL.
- [ ] **CON-005 (S):** Không cho credential trong equality/toString/copy diagnostics.

### Credential security

- [ ] **SEC-001 (M):** `CredentialStore` port và `PasswordSafeCredentialStore` adapter.
- [ ] **SEC-002 (S):** Credential attributes từ immutable connection ID.
- [ ] **SEC-003 (M):** Save/load/delete trên `Dispatchers.IO`, không EDT.
- [ ] **SEC-004 (M):** Rename/delete profile semantics và orphan cleanup tests.
- [ ] **SEC-005 (M):** `RedactionService` cho header, URL, error và diagnostic payload.
- [ ] **SEC-006 (S):** Secret leakage test với canary API key.

### HTTP transport spike

- [ ] **NET-001 (L):** So sánh Ktor/JDK/khả năng Platform theo cancellation, proxy, TLS, size và classloader.
- [ ] **NET-002 (S):** Ghi ADR lựa chọn transport.
- [ ] **NET-003 (L):** Implement `HttpTransport` production và fake transport.
- [ ] **NET-004 (M):** Timeouts, cancellation, response size limit và redirect-origin rule.
- [ ] **NET-005 (M):** IDE proxy behavior smoke test.
- [ ] **NET-006 (M):** Request/response summary sanitized.

### API và capability

- [ ] **CON-010 (M):** JSON DTO/mapping baseline và unknown-field policy.
- [ ] **CON-011 (S):** `SystemApi` health/version.
- [ ] **CON-012 (S):** `IndexApi.list()` dùng cho vertical slice.
- [ ] **CON-013 (M):** Central `ApiErrorMapper` và `MeiliFailure` taxonomy.
- [ ] **CON-014 (M):** `CapabilityDetector` + session cache.
- [ ] **CON-015 (M):** `ConnectionSessionManager` project service.
- [ ] **CON-016 (M):** Test limited/missing key và phân biệt 401/403/network/TLS.

### Connection UI

- [ ] **CON-020 (M):** Add/Edit Connection `DialogWrapper` bằng Kotlin UI DSL.
- [ ] **CON-021 (M):** Test Connection background action với progress/cancel.
- [ ] **CON-022 (M):** Connections list/empty state trong Tool Window.
- [ ] **CON-023 (S):** Edit/remove/copy endpoint actions.
- [ ] **CON-024 (S):** Environment badge và non-TLS warning.
- [ ] **CON-025 (M):** Connection overview editor hiển thị endpoint/version/latency/capability.

### Operation safety

- [ ] **SEC-010 (M):** `OperationGuard` domain/application policy.
- [ ] **SEC-011 (S):** Read-only reject trước transport.
- [ ] **SEC-012 (M):** Project/session-scoped production write unlock, không persist.
- [ ] **SEC-013 (M):** Risk/target confirmation model tái sử dụng.
- [ ] **SEC-014 (M):** Tests chứng minh action và use case không bypass guard.

## Tests

- Profile persistence round-trip không có API key.
- Password Safe adapter không chạy trên EDT.
- Redirect khác origin không giữ Authorization.
- Cancellation hủy transport request.
- Error taxonomy đúng cho timeout/TLS/401/403/404/429/5xx/decode.
- Test connection không suy diễn CRUD permission từ `/health`.
- Production unlock reset khi project/session kết thúc.

## Exit criteria

- M1 hoàn tất.
- User có thể thêm connection, lưu key an toàn, test và xem version/index count.
- Logs/state/notification không chứa secret canary.
- HTTP transport và editor/project lifecycle đã được chứng minh bằng tests.

## Risks

- IDE proxy/custom certificate behavior khác OS: document known behavior, custom CA chuyển Phase 7.
- Remote Development Password Safe behavior chưa đủ bằng chứng: không công bố support trước Phase 8 matrix.

