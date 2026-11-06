# Reusable UI design-to-implementation processes: primary-source evidence

Checked: **2026-11-06**. Scope: public repositories, their command files, official documentation, and clearly identified first-person public reports. No private project information is included. None of these tools was installed or run against a product during this review.

## Decision

**Inferred recommendation: Design OS is the closest reusable process among the candidates examined.** It supplies a coherent sequence from product definition and data relationships through section requirements and rendered React components to a concrete implementation handoff. Its most useful property is the handoff of the actual component source, alongside requirements and behavior specifications. This is materially more than a collection of style prompts. [D1][D2][D3][D4]

**Runner-up: the current Superdesign skill and hosted product**, especially when the main job is extending an existing interface or deriving a visual direction from a reference website. It has more explicit existing-codebase discovery and reference-extraction workflows. However, its upstream workflow still expects user design feedback and approval, and its public skill is not the source code of the hosted design engine. [S1][S2][S3][S4]

**No examined candidate is verified as an out-of-the-box, owner-independent process covering research, information architecture, good design judgment, production integration, and runtime behavior.** Design OS is the best process to transplant, not proof that installing it removes all design decisions. Substituting an agent's decisions for the original human questionnaire would be an adaptation; its success is not established by upstream evidence.

**Recommendation scope:** this ranking is among the process candidates examined here. It is not a recommendation to generate a new interface when a suitable working product or licensed template can be adopted directly. Design OS preserves generated component code during its downstream handoff; its upstream design stage still generates new components from specifications and references. Supplying a reference screenshot is not the same as importing and retaining that reference product's actual component tree, interactions, state model, or runtime. [D2][D7][D11]

Agent OS v3 is not the preferred alternative for this purpose: it deliberately narrowed its role to standards and specification support, leaving implementation orchestration to the host coding agent. OOUX/ORCA is a relevant information-architecture method, not an executable screen-to-code pipeline. [A1][A2][O1]

## Comparison

| Candidate | Verified deliverable | Existing-product support | Human involvement in the upstream process | Main gap for this use case |
| --- | --- | --- | --- | --- |
| **Design OS** | Product and section specifications, sample data, TypeScript props, shell and section TSX components, tokens, handoff instructions, UI behavior test specifications | Export into a target React/Tailwind codebase; references can be supplied during design conversations | Product questions, color/type choices, shell approval, section questions, optional view-selection questions, implementation clarification | No automatic migration of an existing application; runtime and autonomous design judgment remain outside the package |
| **Superdesign skill + service** | Extracted design context, reusable design-system files, reference material, canvas drafts, related flow pages, downloadable draft HTML | Explicit discovery of existing routes, components, shell, styles, and a separate path for new features in an existing codebase | Constraints/direction questions, canvas feedback, implementation after user approval unless explicitly instructed to skip design | Hosted service dependency; UI approval remains central; exported visual drafts do not constitute an integrated application |
| **Agent OS v3** | Standards files and index; persistent plan, shaping notes, references, standards, and supplied visuals | Extracts conventions from existing code | Questions and confirmation for individual standards; shaping and plan approval | Does not produce the missing UI design layer or a complete UI component handoff by itself |
| **OOUX / ORCA** | Object and relationship models, object-associated actions and attributes, prioritized information structure | Can begin with existing screens, product materials, and research | Collaborative discovery and requirements work | Method rather than coding software; no UI library, production renderer, or application runtime |

Sources for this table: [D1–D10], [S1–S4], [A1–A4], [O1–O2]. The last column is an inference from each documented scope, not a comparative performance test.

## 1. Design OS: what is actually reusable

### The pipeline and its artifacts

**Verified:** the current `product-vision` command collects product problems, features, major sections, and domain nouns/relationships. Once enough context exists, it writes the overview, roadmap, and data-shape files without a separate draft-approval step. These are UI planning artifacts rather than a final database model. [D5]

**Verified:** `shape-section` specifies user actions, information to display, user flows, UI requirements, and scope. It generates a section specification, representative JSON data, and TypeScript interfaces. Its sample-data instructions include varied text lengths and statuses, empty collections, and a long description. Actions become callback props. [D6]

**Verified:** `design-screen` builds actual props-based React components. It requires data and callbacks through props, separates the preview wrapper from exportable components, and directs the agent to use the section's types. The preview uses sample data and logging callbacks; this demonstrates why a functioning preview is not proof of completed production behavior. [D7]

**Verified:** the export command assembles a `product-plan/` package with product context, implementation prompts, incremental instructions, design tokens, UI data contracts, shell components, section components, and section behavior specifications. Screenshots are optional. The handoff includes source code, rather than asking the implementation agent to recreate the design from a picture. [D3][D4]

**Verified:** the implementation guide directs the recipient to connect the provided components instead of rebuilding them. Backend architecture, data fetching, routing, state management, and executable tests belong to the implementation stage. The project's description of its components as production-ready is the maintainer's claim, not an independently verified guarantee. [D2]

### Information architecture and placement of new features

**Verified:** the original process establishes product sections and domain relationships, then an application shell, then the views needed by each section. The shell command discusses navigation pattern, default view, user-menu position, and responsive behavior. This gives subsequent features a place in a larger product structure. [D5][D8]

**Important limit:** the design-token command primarily specifies colors and fonts. It is not, by itself, a complete product design system covering density, component behavior, all navigation decisions, and information prioritization. Moreover, the screen command permits default styling when tokens are absent and standalone rendering when no shell exists. The sequence is encouraged, but not all foundations are enforced prerequisites. [D7][D9]

**Inferred:** this makes Design OS a useful upstream process to adopt, but it does not justify assuming that every newly generated feature will automatically occupy the correct place. That decision still comes from the product/section definition and the executing agent.

### Existing products and reference designs

**Verified:** the documented target requirements are React 18+ and Tailwind CSS v4; the backend is unrestricted. A target application using a different styling system does not receive a verified automatic adapter from the reviewed instructions. [D10]

**Verified, limited first-person evidence:** in the repository's discussion about existing designs, the maintainer recommends supplying screenshots during shell/section/screen conversations. A community participant reports having supplied Stitch HTML/CSS mockups and obtained a successful shell. This is evidence that somebody used the reference-to-component path, but it is one unmeasured self-report, not a repeatability study or proof of ongoing production adoption. [D11]

**Not established:** a general automated importer that understands an arbitrary existing application's information architecture, preserves its behavior, and migrates all screens to a chosen template. The reviewed documentation supplies a handoff and reference workflow, not that migration capability.

**Inferred consequence:** when the requirement is to retain an already-solved interface, the original product/template code remains the important asset. Passing it through a reference-to-new-design generation step may reintroduce the interpretation work that direct adoption was meant to avoid. Design OS is strongest as a source-code handoff process when a new design phase is actually needed; it should not be presented as a mandatory extra layer over a working UI foundation.

### How much human input remains?

| Upstream stage | Verified behavior |
| --- | --- |
| Product vision | Initial notes and follow-up questions; then automatic creation of three planning files |
| Tokens | Color and typography choices; approval before writing token files |
| Shell | Navigation and responsive-design questions; iteration until approved |
| Section shaping | Instructions call for 4–6 targeted questions, generally asked one or two at a time; then automatic specification/data/type generation |
| Screen creation | Conditional section/view selection questions when multiple choices exist |
| Implementation handoff | Clarifying questions, followed by implementation; incremental review is recommended |

Sources: [D2][D5–D9]. This is not a fixed number of human turns; the prompts make the number dependent on ambiguity and product scope.

**Verified:** the February 2026 change removed some draft-approval gates in planning and section shaping. It did not remove the human conversations or all design approval. The August 2026 change mostly standardized agent instruction locations. [D12]

**Inferred adaptation boundary:** existing decisions, a selected template, product requirements, and code evidence can be supplied as inputs instead of repeatedly asking a product owner to invent the design. Using that context to let an agent answer the remaining design questions is a reasonable adaptation when authorized. It should not be described as an upstream, proven hands-off mode.

### Runtime, cache, and scrolling

**Verified:** exported UI callbacks still need implementation. Loading, error, and empty states are explicitly part of integration work. The generated `tests.md` files describe UI behavior to test; they are not an already-running executable suite. [D2][D4]

**Not found in the reviewed design and export commands:** a complete application-cache policy, cache invalidation implementation, offline synchronization, scroll-position restoration, virtualized-list integration, mobile keyboard behavior, or proof of performance with production-sized data. These need to be part of the target application's implementation requirements. Their absence is not a defect in a package that explicitly limits itself to UI design, but it prevents calling the package an end-to-end application solution.

## 2. Superdesign: a stronger existing-interface workflow, with a different handoff

### Current project identity

**Verified:** the old `superdesigndev/superdesign` IDE-extension repository says it is retained for history and no longer actively maintained. Its README points to the web product and `superdesign-skill`. The old repository's open-source status must not be attributed to the entire current hosted service. [S5]

**Verified:** the current skill repository is MIT-licensed. It drives a hosted product using a CLI and account login. The vendor separately describes the current service as not open source. [S1][S6][S7]

### Existing code, new pages, and visual references

**Verified:** the skill has separate routes for an existing screen, a new target inside an existing codebase, and a new product. Existing-project analysis records reusable UI context. A new target uses surrounding shell/layout and relevant components as context rather than pretending a new page already exists. A saved resume state can preserve project/draft/context information across authoring sessions. [S2][S3]

**Verified:** the workflow establishes or extracts a design-system document, can reproduce the current page as a baseline, and then iterates or creates related flow pages. This is directly relevant to placing new work in an existing interface. [S3]

**Verified:** reference-site extraction can provide a style guide, tokens, content structure, brand information, or a static clone. The CLI documentation explicitly limits its recreation path to a style-informed rebuild. Faithful editable on-canvas cloning is assigned to the web application. A static CLI clone is a visual reference, not an editable generation input. [S4]

**Inferred:** these facilities make Superdesign the better runner-up where the central task is preserving or extending an existing visual environment. They are not evidence that it performs domain information architecture better than Design OS.

### Human effort and runtime limits

**Verified:** the current reference instructions require design on the canvas before code implementation, followed by user approval unless the user explicitly directs skipping design. Other instructions request feedback on drafts and confirmation of flow-page plans. The README also includes direction-selection questions. The upstream default therefore does not satisfy a requirement to eliminate repeated owner design decisions. [S1][S3]

**Verified:** the repository exposes fetching draft HTML and creating flow pages. It does not itself prove that the resulting target application has completed API integration, cache behavior, scrolling behavior, or state persistence. Saved authoring context in `.superdesign/resume.json` should not be confused with the built application's runtime cache. [S1][S2]

**Pricing uncertainty:** a vendor article advertises a free tier and a flat paid plan, while the current skill repeatedly describes generation credits. The direct pricing page returned no readable content during this review. Current checkout terms and the practical generation allowance were not verified, so no firm monthly-cost or unlimited-generation claim is made here. [S3][S7][S8]

**Adoption limit:** the examined materials establish a maintained public integration and vendor demonstrations. They do not establish a measured reduction in owner review effort or a named production deployment with independently verified design outcomes. Repository popularity is not used as proof of that result.

## 3. Why Agent OS is not the whole process

**Verified:** Agent OS v3 refocused the project on extracting and injecting standards and improving specifications. Its changelog explicitly retires implementation/orchestration phases in favor of host-agent capabilities. Descriptions of the older six-phase workflow should not be presented as its current architecture. [A1]

**Verified:** `shape-spec` gathers the feature, visuals, similar code, product alignment, and relevant standards. It persists a plan, shaping notes, standards, references, and supplied visuals. It does not generate a finished UI component package equivalent to Design OS. [A2][A3]

**Verified:** `discover-standards` asks users to select patterns, explain why they exist, and approve drafts one standard at a time. This is particularly poorly matched to eliminating repeated owner decisions if adopted unchanged. [A4]

**Inferred:** Agent OS can preserve known implementation conventions downstream, but adding it as the centerpiece would chiefly add another specification/standards process. It does not replace the missing design production phase.

## 4. What OOUX / ORCA can and cannot supply

**Verified:** creator Sophia Prater describes ORCA as Objects, Relationships, Calls-to-action, and Attributes, organized into four iterative rounds and fifteen steps. It turns research into an information-architecture foundation before screen and interaction design. It can start from existing product labels, research, documentation, and competitor material. [O1]

**Verified:** the method includes explicit prioritization and requirements work, not merely listing database entities. This is useful for questions such as which objects deserve first-class views, how related objects connect, and which actions belong to each object. [O2]

**Inferred:** it can help where a visual template supplies attractive components but leaves the product's conceptual structure unresolved. It cannot supply application code or runtime behavior, and the reviewed sources do not document an official Design OS–OOUX integration. Combining them would be a new implementation choice, not a ready-made proven pipeline. Do not present an invented combination as an established end-to-end product.

## 5. Licensing and maintenance snapshot

| Repository | Verified main commit | Commit time (UTC) | License and maintenance notes |
| --- | --- | --- | --- |
| buildermethods/design-os | `2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1` | 2026-10-07 04:19:20 | MIT; not archived. Current changelog includes 2026.8.10 instruction-location changes and the 2026.2.9 workflow/handoff changes. |
| buildermethods/agent-os | `e892e61d322759165e7d9173e92c1010406c9f4d` | 2026-10-07 04:18:58 | MIT; not archived. v3 dated 2026-01-20; installation fixes listed as unreleased. |
| superdesigndev/superdesign-skill | `f9f05cd988c247dce6c072eaf9ac6b162f2ffc4b` | 2026-08-21 05:23:23 | MIT for the skill repository; not archived. Changelog contains version 0.6.0. Hosted service licensing is separate. |

Sources: [M1–M6], [D12], [A1], [S6]. Recent configuration/packaging commits establish repository activity, not recent improvements to design quality. MIT licensing of these repositories does not license unrelated reference sites, brands, or third-party assets.

## Evidence register

All sources below were accessed on **2026-11-06**. Repository command and documentation links are pinned to the observed main commit for reproducibility. Links to service pages and discussions remain live references.

### Design OS

- **D1:** [Official workflow](https://buildermethods.com/design-os/usage).
- **D2:** [Codebase implementation guide](https://github.com/buildermethods/design-os/blob/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1/docs/codebase-implementation.md).
- **D3:** [Repository export documentation](https://github.com/buildermethods/design-os/blob/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1/docs/export.md).
- **D4:** [Actual export-product command](https://github.com/buildermethods/design-os/blob/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1/.claude/commands/design-os/export-product.md).
- **D5:** [Actual product-vision command](https://github.com/buildermethods/design-os/blob/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1/.claude/commands/design-os/product-vision.md).
- **D6:** [Actual shape-section command](https://github.com/buildermethods/design-os/blob/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1/.claude/commands/design-os/shape-section.md).
- **D7:** [Actual design-screen command](https://github.com/buildermethods/design-os/blob/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1/.claude/commands/design-os/design-screen.md).
- **D8:** [Actual design-shell command](https://github.com/buildermethods/design-os/blob/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1/.claude/commands/design-os/design-shell.md).
- **D9:** [Actual design-tokens command](https://github.com/buildermethods/design-os/blob/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1/.claude/commands/design-os/design-tokens.md).
- **D10:** [Target requirements](https://github.com/buildermethods/design-os/blob/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1/docs/requirements.md).
- **D11:** [First-person existing-design discussion](https://github.com/buildermethods/design-os/discussions/4).
- **D12:** [Changelog](https://github.com/buildermethods/design-os/blob/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1/CHANGELOG.md).

### Superdesign

- **S1:** [Current skill README](https://github.com/superdesigndev/superdesign-skill/blob/f9f05cd988c247dce6c072eaf9ac6b162f2ffc4b/README.md).
- **S2:** [Current skill entrypoint](https://github.com/superdesigndev/superdesign-skill/blob/f9f05cd988c247dce6c072eaf9ac6b162f2ffc4b/skills/superdesign/SKILL.md).
- **S3:** [Actual design workflow and approval instructions](https://github.com/superdesigndev/superdesign-skill/blob/f9f05cd988c247dce6c072eaf9ac6b162f2ffc4b/skills/superdesign/references/SUPERDESIGN.md).
- **S4:** [Website extraction workflow and scope boundaries](https://github.com/superdesigndev/superdesign-skill/blob/f9f05cd988c247dce6c072eaf9ac6b162f2ffc4b/skills/superdesign/references/WEBSITE.md).
- **S5:** [Legacy IDE-extension repository and maintenance notice](https://github.com/superdesigndev/superdesign).
- **S6:** [Skill license](https://github.com/superdesigndev/superdesign-skill/blob/f9f05cd988c247dce6c072eaf9ac6b162f2ffc4b/LICENSE) and [changelog](https://github.com/superdesigndev/superdesign-skill/blob/f9f05cd988c247dce6c072eaf9ac6b162f2ffc4b/CHANGELOG.md).
- **S7:** [Vendor article discussing code export, commercial plan, and service licensing](https://superdesign.dev/blog/ai-ui-generator-exports-code).
- **S8:** [Pricing page attempted; no readable content returned](https://superdesign.dev/pricing).

### Agent OS

- **A1:** [v3 changelog](https://github.com/buildermethods/agent-os/blob/e892e61d322759165e7d9173e92c1010406c9f4d/CHANGELOG.md).
- **A2:** [Actual shape-spec command](https://github.com/buildermethods/agent-os/blob/e892e61d322759165e7d9173e92c1010406c9f4d/commands/agent-os/shape-spec.md).
- **A3:** [Official shaping workflow](https://buildermethods.com/agent-os/shape-spec).
- **A4:** [Actual discover-standards command](https://github.com/buildermethods/agent-os/blob/e892e61d322759165e7d9173e92c1010406c9f4d/commands/agent-os/discover-standards.md).

### OOUX / ORCA

- **O1:** [Sophia Prater, How to Sell UX Research with Two Simple Questions](https://alistapart.com/article/how-to-sell-ux-research/), 2021-10-21. Original method author's explanation; not a new software release.
- **O2:** [Sophia Prater, Prioritizing Prioritization for Product Designers](https://sophiavux.medium.com/prioritizing-prioritization-for-product-designers-91e78a28f62e). Original author's account of the process's requirements and prioritization rounds.

### Repository metadata and licenses

- **M1:** [Design OS repository metadata](https://api.github.com/repos/buildermethods/design-os) and [commit](https://github.com/buildermethods/design-os/commit/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1).
- **M2:** [Design OS MIT license](https://github.com/buildermethods/design-os/blob/2f14c4611f06e0d866b1fba02f1bfb27d3ef1ef1/LICENSE).
- **M3:** [Agent OS repository metadata](https://api.github.com/repos/buildermethods/agent-os) and [commit](https://github.com/buildermethods/agent-os/commit/e892e61d322759165e7d9173e92c1010406c9f4d).
- **M4:** [Agent OS MIT license](https://github.com/buildermethods/agent-os/blob/e892e61d322759165e7d9173e92c1010406c9f4d/LICENSE).
- **M5:** [Superdesign skill repository metadata](https://api.github.com/repos/superdesigndev/superdesign-skill) and [commit](https://github.com/superdesigndev/superdesign-skill/commit/f9f05cd988c247dce6c072eaf9ac6b162f2ffc4b).
- **M6:** [Superdesign skill MIT license](https://github.com/superdesigndev/superdesign-skill/blob/f9f05cd988c247dce6c072eaf9ac6b162f2ffc4b/LICENSE).

## Review limits

This review verified source artifacts and instructions. It did not benchmark rendered output, purchase hosted services, execute generation, measure runtime behavior, or establish independent comparative success rates. A public command that asks an agent to create an artifact is evidence of an available workflow, not proof that every execution will produce a good artifact. The recommendation concerns which existing process is most directly reusable; it does not claim that any candidate eliminates all design uncertainty.
