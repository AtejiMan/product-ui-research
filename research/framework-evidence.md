# Finished React admin workflows: adoption evidence

> **Recommendation update, same day:** The later requirement prioritizes a single complete application template for development, with predefined page types. The current recommendation is Ant Design Pro **full**, with the complete React-admin E-commerce example as the alternative. See [the visual template decision](2026-11-06-template-choice.md). The source findings below remain evidence; the earlier Atomic CRM transplantation recommendation is historical.

**Checked:** 2026-11-06 (Asia/Seoul)  
**Scope:** public official documentation and public source code only. This review reports source inspection; the candidates were not installed, implemented, purchased, deployed, or benchmarked against a target product.

## Decision

**Recommendation — inferred:** For a resource-oriented operations dashboard, choose the **React-admin / ra-core ecosystem**, and use **Atomic CRM's implemented workflows plus Shadcn Admin Kit** as the concrete source to transplant when its visual presentation fits. Adopt the list-to-detail-to-edit flow, its state ownership, and its data-provider boundary together. Copying its CSS or screenshots while recreating those behaviors would discard much of the benefit.

This is one ecosystem recommendation, with an important distinction: current Atomic CRM uses **React, Shadcn Admin Kit, and Supabase**; it is not a drop-in Material UI React-admin application. Shadcn Admin Kit uses `ra-core`. React-admin's default UI and Atomic CRM's UI are separate presentation layers. [S01][S02]

**Condition:** Apply this choice to CRUD/resource-management routes. Do not replace a long-form, offline document editor with an admin framework. Keeping an existing Mantine-based editor is compatible with adopting a different, complete admin flow in a bounded route group, but the integration itself still requires engineering. The sources do not establish that any framework is universally the most usable or fastest.

The most valuable change is the unit of reuse: **a working product flow and its state behavior**, rather than a collection of buttons or a page image. This is a recommendation derived from the documented differences below, not an independently measured UX ranking.

## Evidence labels

- **Verified:** directly supported by the cited public documentation or inspected source.
- **Inferred:** an engineering judgment based on those facts.
- **Unverified:** not established by this research, particularly end-to-end behavior under a different application's data and device conditions.

Default-branch source was inspected separately from released-package documentation. A default-branch implementation can be newer than the published version. Commit-pinned links record the code actually inspected.

## 1. What each candidate already supplies

| Candidate | Verified delivery level | Work still owned by the application | Suitability judgment |
| --- | --- | --- | --- |
| React-admin / ra-core, with Atomic CRM and Shadcn Admin Kit | React-admin supplies connected CRUD controllers and views. Shadcn Admin Kit's `List` connects fetching, list context, a header, filters, and pagination; `DataTable` supplies sorting, selection, row navigation, bulk actions, and column controls. Atomic CRM supplies real contact, company, task, and deal flows. [S01][S02][S03][S04] | Choose product fields and relationships, implement or adapt the data provider, and retain the intended interaction flow. Atomic CRM is a CRM donor, not a generic operations app with the domain already replaced. | **Inferred:** strongest fit here for reducing both presentation invention and repeated CRUD-state plumbing. |
| Refine | Headless CRUD framework covering routing, data operations, access, and state, with UI integration packages. `useTable` manages filtering, sorting, pagination, and optional URL synchronization. [S10][S11] | Assemble the actual screen, select the table and form implementation, choose persistence behavior, and supply providers. A UI integration is not the complete product information architecture. | **Inferred:** strong when preserving custom UI freedom matters; weaker for a requirement to minimize fresh layout and behavior decisions. |
| Ant Design Pro + ProComponents | A complete React enterprise-app scaffold plus page-level components. ProTable includes a request contract, query form, pagination, density controls, column controls, and reload actions. ProLayout supplies the application layout/menu layer. [S15][S16] | Connect domain services; implement product-specific detail/edit flows and cross-route persistence beyond each component's documented scope. ProComponents alone is not the same artifact as the complete Ant Design Pro scaffold. | **Inferred:** credible close alternative for dense, table-heavy admin products, particularly when adopting its Ant Design/Umi stack is acceptable. |
| Cloudscape | AWS-origin design system with complete resource-view, detail, filtering, density, and refresh patterns, plus React components. Client-side collection hooks cover local filtering, sorting, and pagination. [S20][S21][S22] | Official guidance explicitly leaves server-side fetching, filtering, selection, pagination, and sorting to the application. [S20] | **Inferred:** excellent source of coherent cloud-console interaction patterns, but less complete as a ready data/application runtime. |

**Verified:** The current Ant Design Pro repository describes a React 19 / Umi Max 4 / Ant Design 6 stack. This is a larger application-stack choice than installing a new table component. [S15]

**Unverified:** GitHub popularity, vendor deployment counts, and polished demo screenshots do not establish comparative usability, menu latency, or error rates. None is used as proof of a UX winner in this recommendation.

## 2. Refreshing data without resetting the user's workspace

A background update, a user-requested new query, a pagination action, and opening a different record are different operations. The existing implementations provide concrete distinctions.

### React-admin / ra-core

**Verified:** `useRefresh` calls TanStack Query's `queryClient.invalidateQueries()`; it does not call `window.location.reload()`. The inspected `useListController` passes `placeholderData: previousData => previousData` to its query. Data invalidation and initial empty loading therefore need not be treated as the same screen state. [S05][S06]

**Verified:** The default list stores sort, pagination, and filters in localStorage. `storeKey` provides separate identities for list parameters and, in the inspected current implementation, selection too: `useListController` passes it to `useRecordSelection`, which stores selected IDs under `${storeKey || resource}.selectedIds`. Distinct explicit keys therefore support independent selections for lists of the same resource. Setting `storeKey` to `false` disables store synchronization. Older versions or cached documentation may describe resource-only selection; that limitation should not be asserted for this pinned implementation. The parameter code merges URL values, stored values, and defaults. [S06][S07][S08][S36]

**Verified:** `useListParams` marks explicit page changes with `_scrollToTop: action.type === SET_PAGE`. This demonstrates an intentional distinction between paging and other parameter changes. It is not a universal scroll-position guarantee. [S08]

**Inferred:** For a list refresh defect, transplant the controller and stable record rendering rather than recreating the entire page when data arrives. Preserve the mounted list shell and the current query. However, record deletion, reordering, changing row heights, remounting by a changing React key, or application-level navigation can still change the visible position.

### Atomic CRM: product code beyond a library promise

At commit `7bd2136a270a1374226b69a50892a3bc83fa6d85`:

- **Verified:** `ContactList.tsx` uses a desktop `List` with 25 items per page and a separate mobile `InfiniteListBase`. The actual list content, filters, actions, and bulk actions are implemented, not left as a screenshot. [S09a]
- **Verified:** `ContactListContent.tsx` uses record IDs as React keys. It implements row navigation and selection, including shift-click range selection on desktop. [S09b]
- **Verified:** `layout/useRefreshData.ts` awaits query invalidation, prevents overlapping refresh calls, and holds a refresh indicator for at least 400 ms. The same hook supports mobile refresh affordances. This is actual data-refresh code, not a browser reload. [S09c]
- **Verified:** Mobile behavior is deliberately different: the contact list clears a desktop/URL name-search filter because mobile uses the header's global search. Therefore, copying a polished product still means understanding its interaction decisions. [S09a]

**Inferred:** This is the level of source reuse that can replace repeatedly improvised UX. The donor includes what happens during loading, refresh, selection, empty results, and mobile navigation—not just its appearance.

**Unverified:** Atomic CRM's live demo was reachable, but the text retrieval exposed only its JavaScript loading shell. No interactive demo performance or scroll-retention result is claimed.

### Refine

**Verified:** Refine's `useList` uses TanStack Query and a provider's `getList`. `useInvalidate` invalidates resource query state. A Live Provider with automatic mode invalidates and refetches related queries after events. This is data-query refresh, not a browser-page reload. [S12][S13][S14]

**Verified:** `useTable` can synchronize filters, sort order, and pagination with URL query parameters, but this feature is disabled by default in the documented core hook. [S11]

**Inferred:** Refine offers a sound refresh and URL-state foundation, but choosing it does not itself fix selection persistence, scroll anchoring, or a custom component that replaces all rows with a spinner during every refetch.

### Ant Design Pro / ProTable

**Verified:** ProTable distinguishes `reload()`, `reloadAndRest()`, and `reset()`. Normal reload refreshes the table; requesting a reset also changes page/form state according to the selected method. Column visibility/order persistence is separately configured with `persistenceKey` and localStorage/sessionStorage. [S16]

**Verified:** The inspected `src/table/useFetchData.tsx` has separate reload and pagination-reset paths. Reload invokes its fetch operation; reset rewrites pagination state. [S17]

**Verified:** Underlying Ant Design Table supports controlled selected row keys, `preserveSelectedRowKeys`, virtual rendering, and `scrollToFirstRowOnChange` for paging/sorting/filtering. These are configuration surfaces with specific scopes, not a promise to preserve every piece of view state automatically. [S18]

### Cloudscape

**Verified:** The official refresh pattern says to keep existing data visible and usable while refresh is in progress. Initial loading has a separate skeleton state. [S22]

**Verified:** Its table-view pattern exposes page size, visible columns, column order, sticky columns, and table/card preferences. It also intentionally resets visible-row selection after certain operations, including pagination and sorting. [S21]

**Inferred:** A complete pattern includes which actions preserve or clear state. Blindly demanding that every state always survive every action is different from preserving the user's position during an automatic data refresh.

## 3. Persistence is several separate problems

| State | Verified support | Boundary |
| --- | --- | --- |
| Filters, sort, current page | React-admin list store and URL behavior; Refine opt-in URL synchronization. [S07][S08][S11] | URL state is not automatically the same as a saved view across devices. |
| Column visibility/order | Shadcn Admin Kit column controls; ProTable configurable column persistence; Cloudscape preferences pattern. [S03][S16][S21] | The presence of a control does not prove durable persistence unless that behavior is implemented. |
| Record selection | Current React-admin selection supports explicit `storeKey` isolation with a resource fallback; Ant Design controlled selection/preserved keys; Atomic CRM actual selection code. [S06][S36][S09b][S18] | Configuration and application event semantics still determine when selections are cleared. |
| Scroll offset / visible anchor | Explicit paging and scroll APIs are visible in the reviewed code and docs. [S08][S18] | **Unverified:** none of the checked sources promises arbitrary-scroll preservation under every background insertion, deletion, resize, or custom render. |
| Editor caret, composition, undo history | ProseMirror models document, selection, marks, and transactions. [S25] | An admin-list query cache is not the editor's transaction state. |

**Inferred:** A practical transplant should retain the donor's event distinctions: refresh the data already being viewed, navigate when the user navigates, and reset only when the operation calls for a reset. This follows existing implementations; it does not require inventing another general-purpose rule system.

## 4. Virtualization and responsiveness

**Verified:** Ant Design Table has a virtual mode. React-admin's documented `DatagridAG` integration includes DOM virtualization but belongs to Enterprise Edition; ordinary React-admin list pagination and the AG Grid integration are different features. [S18][S19]

**Verified:** Atomic CRM's inspected mobile contact screen uses infinite pagination, while the desktop screen uses a 25-record page. The reviewed code does not justify calling its contact list virtualized. [S09a][S09b]

**Inferred:** Virtualization reduces rendered-item work for large collections. It does not resolve an application that remounts its layout, runs a blocking computation while opening a menu, or resets state whenever a network response arrives. A mature list implementation reduces the amount of custom work; it cannot make unrelated application code fast automatically.

**Unverified:** No candidate was benchmarked against the same data, device, menu interaction, or editing workload. Claims such as “this migration eliminates menu stutter” would exceed the evidence.

## 5. Existing Mantine code: retain it where it is useful

**Verified:** Refine's current Mantine integration documentation still specifies Mantine v5. The inspected `@refinedev/mantine` package has `^5.10.4` peer dependencies for its Mantine packages. Therefore “Refine supports Mantine” does not establish compatibility with an arbitrary newer Mantine installation. [S23][S24]

**Inferred:** Retaining Mantine is technically possible by using a headless data/controller layer and writing the presentation adapter. That route keeps existing UI work but also retains more assembly work. It should not be sold as importing the completed Atomic CRM or Ant Design Pro experience.

A bounded migration can preserve an existing editor or specialized workflow while adopting complete admin routes elsewhere. The boundary should follow the type of work, not a desire to make every product look identical.

## 6. Offline document editing is a different workload

**Verified:** ProseMirror stores document content, selection, and stored marks in editor state and applies normal edits as transactions. Selection is mapped through those transactions, and scrolling the selection into view is an explicit transaction capability. [S25]

**Inferred:** A long-form writer needs continuity of document identity, input composition, caret position, undo history, and offline synchronization. The reviewed admin frameworks supply CRUD and collection behavior; they do not supply a complete replacement for that editor lifecycle. Reusing their browser-shell conventions or a library screen can be sensible. Replacing the document editor with a CRUD form in order to obtain a consistent dashboard template would address the wrong problem.

## 7. Cost and licensing

| Artifact | Verified license / cost boundary |
| --- | --- |
| React-admin open-source core | MIT; no software license fee for the open-source edition. [S26] |
| Atomic CRM | MIT. Its source is free to reuse subject to its license; hosting/backend operations are separate. [S01][S27] |
| Shadcn Admin Kit | MIT. [S28] |
| Refine core | MIT. Paid services or other products should not be conflated with the core license. [S29] |
| Ant Design Pro and ProComponents | MIT. [S15][S30] |
| Cloudscape components | Apache-2.0. [S31] |
| React-admin Enterprise | Official Team plan starts at EUR 145/month, billed annually, for up to two developers. The ready-made `@react-admin/ra-realtime` live-update hooks and `DatagridAG` are paid capabilities. Ordinary `useRefresh` / query invalidation does not require this purchase. AG Grid Enterprise features may require a separate AG Grid license. [S04][S19][S32][S35] |

No purchase is recommended merely to solve ordinary refresh/state-reset defects.

## 8. What a complete transplant means

**Recommendation — inferred:**

1. Select the donor flow that matches the task: collection, search/filter, row action, detail, editing, and return.
2. Preserve its navigation, data-query, loading, refresh, selection, and preference behavior while replacing domain fields through a data/provider adapter.
3. Keep its actual layout hierarchy and responsive decisions until there is a concrete domain mismatch. Avoid rebuilding equivalent shells independently on every route.
4. Keep specialized editing and offline state in their existing dedicated subsystem.
5. Describe remaining differences precisely. A copied list without its detail route, persisted query, or refresh semantics is a partial transplant.

This is a reuse decision, not another owner-approval loop. The choice reduces fresh design decisions and repeated state plumbing; it does not claim automatic perfect design.

## 9. Atomic CRM's bundled agent harness

**Verified:** Atomic CRM includes a Claude Code harness in the same repository as the working product. The documented pipeline uses specialized planning, development, review, and documentation roles. Simple changes take a shorter path; complex requests are decomposed into coordinated work. Its documentation describes automatic merging and a session-specific diff/revert facility. These documents do not prescribe a repeated owner screenshot-approval loop. [S33]

**Verified:** This is not only a generic instruction to “review the UI.” The frontend reference names actual repository boundaries and existing components: admin inputs versus UI primitives, `ra-core` data hooks, the CRM resource registration point, shared create/edit inputs, existing filter controls, and distinct mobile list/page components. Those instructions correspond to the source files inspected above. [S34]

**Inferred:** The useful transferable idea is a product-specific development workflow attached to a finished product and its actual implementations. Copying only the agent-role names or the review pipeline into another repository would lose that grounding. The harness does not establish that the resulting design is optimal, and adopting all of its hooks is not required to reuse the product's UI behavior.

**Limit:** Only the harness overview and frontend reference were inspected for this addition, not every hook, permission path, planner prompt, or merge operation. The harness was not run. No blanket claim of approval-free operation, safe automatic merging, or correct design is made.

## Sources

All sources were checked on 2026-11-06. Official documentation URLs can change; code links below are pinned where source was inspected.

- **S01:** [Atomic CRM README and stack](https://github.com/marmelab/atomic-crm/blob/7bd2136a270a1374226b69a50892a3bc83fa6d85/README.md).
- **S02:** [Shadcn Admin Kit List](https://marmelab.com/shadcn-admin-kit/docs/list/).
- **S03:** [Shadcn Admin Kit DataTable](https://marmelab.com/shadcn-admin-kit/docs/datatable/).
- **S04:** [React-admin overview](https://marmelab.com/react-admin/index.html).
- **S05:** [ra-core useRefresh source](https://github.com/marmelab/react-admin/blob/67914cd9572336d0926d719d0021f7e1835f799c/packages/ra-core/src/dataProvider/useRefresh.ts).
- **S06:** [ra-core useListController source](https://github.com/marmelab/react-admin/blob/67914cd9572336d0926d719d0021f7e1835f799c/packages/ra-core/src/controller/list/useListController.ts).
- **S07:** [React-admin List](https://marmelab.com/react-admin/List.html).
- **S08:** [ra-core useListParams source](https://github.com/marmelab/react-admin/blob/67914cd9572336d0926d719d0021f7e1835f799c/packages/ra-core/src/controller/list/useListParams.ts).
- **S09a:** [Atomic CRM ContactList source](https://github.com/marmelab/atomic-crm/blob/7bd2136a270a1374226b69a50892a3bc83fa6d85/src/components/atomic-crm/contacts/ContactList.tsx).
- **S09b:** [Atomic CRM ContactListContent source](https://github.com/marmelab/atomic-crm/blob/7bd2136a270a1374226b69a50892a3bc83fa6d85/src/components/atomic-crm/contacts/ContactListContent.tsx).
- **S09c:** [Atomic CRM useRefreshData source](https://github.com/marmelab/atomic-crm/blob/7bd2136a270a1374226b69a50892a3bc83fa6d85/src/components/atomic-crm/layout/useRefreshData.ts).
- **S10:** [Refine core overview](https://refine.dev/core/docs/).
- **S11:** [Refine core useTable](https://refine.dev/core/docs/data/hooks/use-table/).
- **S12:** [Refine useList source](https://github.com/refinedev/refine/blob/0d6d062e73189aa196a5ffbd9a8939134f88bd2d/packages/core/src/hooks/data/useList.ts).
- **S13:** [Refine useInvalidate](https://refine.dev/core/docs/data/hooks/use-invalidate/).
- **S14:** [Refine Live Provider](https://refine.dev/core/docs/realtime/live-provider/).
- **S15:** [Ant Design Pro official repository](https://github.com/ant-design/ant-design-pro).
- **S16:** [ProTable official documentation](https://pro-components.antdigital.dev/en-US/components/table).
- **S17:** [ProTable useFetchData source](https://github.com/ant-design/pro-components/blob/546b6d01b76b32487a4d0688c690a1e48fa10995/src/table/useFetchData.tsx).
- **S18:** [Ant Design Table](https://ant.design/components/table/?locale=en-US).
- **S19:** [React-admin DatagridAG](https://marmelab.com/react-admin/DatagridAG.html).
- **S20:** [Cloudscape collection hooks](https://cloudscape.design/get-started/dev-guides/collection-hooks/).
- **S21:** [Cloudscape table-view pattern](https://cloudscape.design/patterns/resource-management/view/table-view/).
- **S22:** [Cloudscape loading and refreshing](https://cloudscape.design/patterns/general/loading-and-refreshing/).
- **S23:** [Refine Mantine integration](https://refine.dev/core/docs/ui-integrations/mantine/introduction).
- **S24:** [Refine Mantine package peer dependencies](https://github.com/refinedev/refine/blob/0d6d062e73189aa196a5ffbd9a8939134f88bd2d/packages/mantine/package.json).
- **S25:** [ProseMirror guide](https://prosemirror.net/docs/guide/) and [transaction source](https://github.com/ProseMirror/prosemirror-state/blob/master/src/transaction.ts).
- **S26:** [React-admin MIT license](https://github.com/marmelab/react-admin/blob/67914cd9572336d0926d719d0021f7e1835f799c/LICENSE.md).
- **S27:** [Atomic CRM MIT license](https://github.com/marmelab/atomic-crm/blob/7bd2136a270a1374226b69a50892a3bc83fa6d85/LICENSE.md).
- **S28:** [Shadcn Admin Kit MIT license](https://github.com/marmelab/shadcn-admin-kit/blob/main/LICENSE).
- **S29:** [Refine MIT license](https://github.com/refinedev/refine/blob/0d6d062e73189aa196a5ffbd9a8939134f88bd2d/LICENSE).
- **S30:** [ProComponents MIT license](https://github.com/ant-design/pro-components/blob/546b6d01b76b32487a4d0688c690a1e48fa10995/LICENSE.md).
- **S31:** [Cloudscape Apache-2.0 license](https://github.com/cloudscape-design/components/blob/main/LICENSE).
- **S32:** [React-admin Enterprise pricing](https://marmelab.com/ra-enterprise/).
- **S33:** [Atomic CRM agent-harness overview](https://github.com/marmelab/atomic-crm/blob/7bd2136a270a1374226b69a50892a3bc83fa6d85/doc/src/content/docs/developers/agent-harness.mdx).
- **S34:** [Atomic CRM frontend development reference](https://github.com/marmelab/atomic-crm/blob/7bd2136a270a1374226b69a50892a3bc83fa6d85/.claude/skills/frontend-dev/SKILL.md).
- **S35:** [React-admin useGetList, live-update hook package](https://marmelab.com/react-admin/useGetList.html).
- **S36:** [ra-core useRecordSelection source](https://github.com/marmelab/react-admin/blob/67914cd9572336d0926d719d0021f7e1835f799c/packages/ra-core/src/controller/list/useRecordSelection.ts).
- **Demo:** [Atomic CRM](https://marmelab.com/atomic-crm-demo/) — reached, but interactive behavior was not evaluated in this research.

