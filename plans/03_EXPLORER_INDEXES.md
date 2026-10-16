# Phase 3 — Explorer and Index Management

## Objective

Xây trải nghiệm điều hướng giống Database Explorer: cây connections/indexes lazy-load, actions theo context, index overview/stats và index CRUD an toàn.

## Dependencies

- Phase 2 exit criteria.

## Deliverables

- Explorer tree production.
- Stable node model, loading/error/empty states.
- Refresh/cancellation/stale result protection.
- Index list/details/stats/create/delete.
- Context menus, toolbar, shortcuts và editor navigation.

## Tasks

### Explorer model

- [ ] **EXP-001 (M):** Sealed `ExplorerNode` và stable `NodeId`.
- [ ] **EXP-002 (M):** Tree model phân cấp connection/index/feature/tasks.
- [ ] **EXP-003 (L):** Lazy child loader bằng coroutine và node lifecycle.
- [ ] **EXP-004 (M):** Loading, empty, permission, disconnected và error nodes.
- [ ] **EXP-005 (M):** Refresh generation/revision để bỏ stale result.
- [ ] **EXP-006 (M):** Cache/TTL và manual refresh bypass.
- [ ] **EXP-007 (M):** Preserve expanded/selection state sau refresh.
- [ ] **EXP-008 (S):** Tree speed search và keyboard navigation.

### Explorer presentation

- [ ] **EXP-010 (M):** Native tree cell renderer theo theme.
- [ ] **EXP-011 (S):** Environment/read-only/disconnected/task badges.
- [ ] **EXP-012 (M):** Tool Window toolbar actions.
- [ ] **EXP-013 (M):** Context menu qua Action System/DataKeys.
- [ ] **EXP-014 (S):** Double-click/Enter mở resource editor.
- [ ] **EXP-015 (M):** Accessibility names, focus và high-contrast review.

### Index API/domain

- [ ] **IDX-001 (M):** Index DTO/domain mapper và pagination metadata.
- [ ] **IDX-002 (M):** List/get/create/update/delete endpoints.
- [ ] **IDX-003 (S):** Stats endpoint và unknown fields.
- [ ] **IDX-004 (M):** Mutation result luôn thành `TaskHandle` khi async.
- [ ] **IDX-005 (M):** Primary key/create validation.

### Index UI/use cases

- [ ] **IDX-010 (M):** Index overview editor.
- [ ] **IDX-011 (M):** Index stats panel với loading/error/refresh.
- [ ] **IDX-012 (M):** Create Index dialog + exact request preview.
- [ ] **IDX-013 (M):** Delete Index strong confirmation nhập lại UID.
- [ ] **IDX-014 (M):** Open Documents/Search/Settings actions.
- [ ] **IDX-015 (S):** Copy index UID/request info.
- [ ] **IDX-016 (M):** Invalidate explorer/session cache sau mutation terminal.

## Tests

- 100+ index nodes không freeze UI.
- Expand/collapse/refresh giữ selection hợp lý.
- Slow refresh cũ không overwrite refresh mới.
- Permission error ở một connection không làm hỏng toàn tree.
- Create/delete gọi OperationGuard.
- Delete confirmation target gồm environment, endpoint và UID.
- Index mutation trả task handle, không báo hoàn tất sớm.

## Exit criteria

- M2 hoàn tất.
- Explorer dùng được bằng mouse và keyboard.
- Có thể quản lý index cơ bản mà không rời IDE.
- Tree/editor dispose không để background job sống sót.

## Risks

- Dynamic tree update gây selection flicker: dùng stable IDs và minimal model update.
- Server có hàng nghìn indexes: paging/lazy strategy và search/filter local có giới hạn.

