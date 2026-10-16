# MeiliPilot JetBrains — Implementation Plans

Thư mục này chứa kế hoạch triển khai toàn bộ tính năng được mô tả trong:

- `MEILIPILOT_JETBRAINS_DEVELOPMENT_PLAN.md`;
- `docs/MEILIPILOT_TECHNICAL_OVERVIEW.md`.

## Thứ tự thực hiện

| Thứ tự | Plan | Phạm vi |
|---:|---|---|
| 0 | `00_MASTER_IMPLEMENTATION_PLAN.md` | Milestones, dependency graph, governance và Definition of Done |
| 1 | `01_PLATFORM_FOUNDATION.md` | Build, package boundaries, plugin descriptor, services, editor/tool window POC, CI |
| 2 | `02_CONNECTIONS_SECURITY.md` | Profiles, Password Safe, HTTP transport, capability, errors, safe operations |
| 3 | `03_EXPLORER_INDEXES.md` | Tool Window explorer, index CRUD, overview, stats, actions |
| 4 | `04_SEARCH_DOCUMENTS.md` | Search console, history, document browser/editor và mutations |
| 5 | `05_SETTINGS_TASKS.md` | Settings editor, task monitor, async operation lifecycle |
| 6 | `06_DIFF_MIGRATION_SEARCH_DEBUGGER.md` | Semantic diff, migration plan/executor và search comparison |
| 7 | `07_ADVANCED_NETWORK_COMMERCIAL.md` | Custom CA/proxy, SSH, presets/templates, licensing/team backlog |
| 8 | `08_QA_RELEASE.md` | Test matrix, hardening, accessibility, Marketplace/release |

## Quy ước trạng thái

- `[ ]` chưa bắt đầu;
- `[~]` đang thực hiện;
- `[x]` hoàn tất và đạt acceptance criteria;
- `[!]` blocked, phải ghi nguyên nhân và owner;
- `[D]` deferred có chủ đích, phải có ADR hoặc issue tham chiếu.

## Quy ước ID

- `FND`: platform foundation;
- `CON`: connection;
- `SEC`: security/safety;
- `NET`: transport/network;
- `EXP`: explorer;
- `IDX`: index;
- `SEA`: search;
- `DOC`: documents;
- `SET`: settings;
- `TSK`: tasks;
- `DIF`: settings diff;
- `MIG`: migration;
- `DBG`: search debugger;
- `ADV`: advanced features;
- `QA`: quality/release.

## Quy tắc thực thi

1. Không bắt đầu feature phase khi foundation gate liên quan chưa pass.
2. Mỗi vertical slice phải bao gồm domain, use case, infrastructure, UI, tests và docs.
3. Mọi write operation bắt buộc đi qua `OperationGuard` và task handling chung.
4. Không gọi network hoặc Password Safe trên EDT.
5. Không thêm IntelliJ internal API nếu chưa có ADR và Plugin Verifier coverage.
6. Không đưa Go/Wails binary hoặc runtime vào plugin.
7. Task chỉ được đánh dấu `[x]` khi acceptance criteria và tests tương ứng pass.

