# Phase 8 — QA, Hardening and Release

## Objective

Đưa plugin từ feature-complete sang release-ready: test matrix, performance, lifecycle, accessibility, compatibility, security, packaging, documentation và Marketplace.

## Dependencies

- Chạy liên tục từ Phase 1; final gate sau phase feature mục tiêu.

## Deliverables

- Automated test suites và CI gates.
- IDE/Meilisearch compatibility matrices.
- Performance/lifecycle/security evidence.
- Signed/verifiable plugin artifact.
- User/admin/developer documentation.
- Release/rollback/support process.

## Tasks

### Test infrastructure

- [ ] **QA-001 (M):** Unit test conventions và fixture helpers.
- [ ] **QA-002 (L):** Separate integration test source set/task.
- [ ] **QA-003 (L):** Meilisearch container/version matrix và deterministic seed.
- [ ] **QA-004 (M):** Limited API key fixtures.
- [ ] **QA-005 (M):** Fake clock/transport/credential store.
- [ ] **QA-006 (L):** Platform fixture tests cho services/actions/editors.
- [ ] **QA-007 (L):** E2E smoke workflow trong IDE sandbox.
- [ ] **QA-008 (M):** Test result/log artifact retention và redaction.

### CI quality gates

- [ ] **QA-010 (M):** Compile/unit/platform tests.
- [ ] **QA-011 (M):** Integration tests theo supported Meilisearch versions.
- [ ] **QA-012 (M):** `verifyPluginProjectConfiguration`.
- [ ] **QA-013 (M):** `verifyPluginStructure`.
- [ ] **QA-014 (L):** Plugin Verifier IDE matrix.
- [ ] **QA-015 (M):** Static analysis/format/license/dependency vulnerability checks.
- [ ] **QA-016 (M):** Canary secret scan trên logs/test artifacts/plugin ZIP.
- [ ] **QA-017 (S):** CI artifact: plugin ZIP, verifier report, test reports.

### Performance và lifecycle

- [ ] **QA-020 (M):** Explorer 100/1,000 indexes benchmark.
- [ ] **QA-021 (M):** Document pages với wide/nested JSON.
- [ ] **QA-022 (M):** Large raw response size-limit behavior.
- [ ] **QA-023 (M):** Repeated open/close editor leak test.
- [ ] **QA-024 (M):** Project close với active search/polling/tunnel.
- [ ] **QA-025 (M):** SlowOperations/internal mode smoke run.
- [ ] **QA-026 (M):** Startup impact: no eager network/service heavy init.

### UX/accessibility

- [ ] **QA-030 (M):** Light/dark/high-contrast icon/color review.
- [ ] **QA-031 (M):** Scaling 100/125/150/200%.
- [ ] **QA-032 (M):** Full keyboard path cho main workflows.
- [ ] **QA-033 (M):** Accessible names/labels/focus order.
- [ ] **QA-034 (M):** Loading/empty/disconnected/error states review.
- [ ] **QA-035 (M):** Destructive dialog copy/target/risk consistency.
- [ ] **QA-036 (M):** Localization bundle completeness; no hard-coded user strings.

### Compatibility

- [ ] **QA-040 (M):** Chốt supported IDE products/build range.
- [ ] **QA-041 (M):** Test Platform-only dependency trên từng product mục tiêu.
- [ ] **QA-042 (M):** Chốt Meilisearch versions/capability matrix.
- [ ] **QA-043 (M):** Unknown-field/new-status forward compatibility tests.
- [ ] **QA-044 (M):** Persisted state upgrade/migration tests.
- [ ] **QA-045 (M):** Remote Development test hoặc explicit unsupported statement.
- [ ] **QA-046 (M):** OS matrix cho Password Safe/network behavior.

### Security review

- [ ] **QA-050 (M):** Threat model review và unresolved findings.
- [ ] **QA-051 (M):** API key leakage audit.
- [ ] **QA-052 (M):** Redirect/proxy/TLS review.
- [ ] **QA-053 (M):** OperationGuard bypass review.
- [ ] **QA-054 (M):** Export/diagnostic privacy review.
- [ ] **QA-055 (M):** Dependency/SBOM/license review.
- [ ] **QA-056 (M):** Marketplace signing secrets handling.

### Documentation

- [ ] **QA-060 (M):** Installation/quick start.
- [ ] **QA-061 (L):** User guide: connections/explorer/search/documents/settings/tasks.
- [ ] **QA-062 (M):** Pro guide: diff/migration/search comparison.
- [ ] **QA-063 (M):** Security/privacy/credential behavior.
- [ ] **QA-064 (M):** Compatibility matrix/known issues.
- [ ] **QA-065 (M):** Troubleshooting và sanitized diagnostics.
- [ ] **QA-066 (S):** Developer architecture/ADR index.
- [ ] **QA-067 (S):** Changelog/release notes.

### Packaging và release

- [ ] **QA-070 (M):** Final plugin metadata/vendor/links/license.
- [ ] **QA-071 (M):** Marketplace description/screenshots/icon.
- [ ] **QA-072 (M):** Plugin signing configuration.
- [ ] **QA-073 (M):** Beta channel publish và install test từ clean IDE.
- [ ] **QA-074 (M):** Upgrade/uninstall/reinstall smoke tests.
- [ ] **QA-075 (M):** Stable release approval checklist.
- [ ] **QA-076 (M):** Rollback/yank/hotfix procedure.
- [ ] **QA-077 (M):** Issue templates và support diagnostics policy.

## Release gates

### Community MVP gate

- All P0 features pass.
- No credential/destructive/lifecycle blocker.
- Core E2E workflow pass.
- Verifier and compatibility matrix pass.
- Docs đủ cho external beta.

### Pro gate

- Diff/migration/search comparison tests pass.
- Drift/partial failure behavior được manual review.
- Export sanitized.
- Entitlement failure không phá Community core nếu licensing được bật.

### Advanced network gate

- Custom CA/SSH threat model và integration tests pass.
- Cleanup/host-key/credential behavior pass.
- Feature có thể disable độc lập.

## Exit criteria

- M6 hoàn tất cho release target đã chọn.
- Artifact có thể tải/cài/nâng cấp trên clean IDE.
- Không còn P0 blocker; P1/P2 có owner/release target.
- Compatibility/security/privacy claims có test hoặc tài liệu bằng chứng.

