# Funcionário Infinito knowledge

Installed skills are grouped by their manifest's `module` key. Each module's
knowledge is read from that manifest's `knowledge` value: free-form text
saying where the module's knowledge lives or what it is. Follow it for the
module the question concerns. This document is what the `method` and
`toolbox` manifests point at; another module points elsewhere, and nothing
below describes it.

## The method and toolbox modules

A cohesive collection of skills for software development, helping the user
turn an intent of any size into working software. Route the user to the
smallest path that safely fits the work; never march them through every skill.

### The skills and their places in the flow

Shaping and planning:

- `funcionario-spec` — condenses any input into a short spec, and can break a spec
  into an ordered story list. The entry point for epic-sized (2-10 coding
  sessions) work and for existing material (notes, transcripts, PRDs from
  elsewhere).
- `funcionario-product-brief` and `funcionario-prfaq` — two alternative ways to shape a
  product concept; use one, never both.
- `funcionario-prd` — turns a shaped concept into product requirements.
- `funcionario-ux` — records user experience decisions; belongs after the PRD when a
  UI is a significant part of the work.
- `funcionario-architecture` — records the how-to-build decisions that keep
  separately built parts consistent; comes before epics and stories.
- `funcionario-create-epics-and-stories` — breaks the PRD and architecture into
  epics and stories.
- `funcionario-sprint-planning` — checks the planning is complete enough to
  implement and generates the sprint status file; its status action
  summarizes sprint state at any time.
- `funcionario-preview-ticketing` — preview of the ticket tree: slices an
  initiative into epics, incepts an epic into a breakdown of stories,
  spikes, and bugs, refines tickets when pulled, and runs the board on a git-backed
  store or a tracker. An alternative to `funcionario-create-epics-and-stories`
  plus `funcionario-sprint-planning`, not a companion to them.
- `funcionario-project-context` — sets up or refreshes the repo's agent
  instructions; useful any time, in any path.

Implementation and quality:

- `funcionario-build` — one session-sized unit of delivery: clarifies the intent,
  plans as needed, implements, reviews, and presents. The implementation unit
  every path shares.
- `funcionario-build-auto` — one unattended Build unit; the worker an orchestrated
  loop dispatches. Do not choose it for attended work.
- `funcionario-code-review` — optional extra review of any change, on top of
  Build's built-in review.
- `funcionario-walkthrough` — guided human review of a commit, PR, file, or directory.
- `funcionario-qa-generate-e2e-tests` — generates API and end-to-end tests for
  implemented code.
- `funcionario-retrospective` — judges a completed epic as a whole against its spec.
- `funcionario-correct-course` — assesses a significant midstream change and
  proposes where to resume.

Agent personas (optional):

- `funcionario-agent-analyst`, `funcionario-agent-architect`, `funcionario-agent-dev`,
  `funcionario-agent-pm`, `funcionario-agent-ux-designer` — conversations with a single
  named perspective. No path above needs them; the flow skills already do
  this work. Offer one only when the user asks to talk to a specific role
  or wants one perspective's take without running a full skill.

Support skills (standalone):

- `funcionario-brainstorming` — facilitated ideation across many creative
  techniques.
- `funcionario-forge-idea` — stress-tests a half-formed idea in a questioning
  conversation until the user can act on it or drop it.
- `funcionario-deep-recon` — research to support a decision: drafts a research
  prompt for the user's own tool, or runs the research itself.
- `funcionario-advanced-elicitation` — pushes recent output to be reconsidered
  and improved through a chosen critique method.
- `funcionario-review` — runs installed review lenses (adversarial critique, edge
  cases, verification gaps, structure, prose) over any artifact and reports
  triaged findings.
- `funcionario-party-mode` — a lively group discussion between installed agents or
  custom personas.
- `funcionario-customize` — authors customization overrides for installed Funcionário Infinito
  skills.

These belong to no path and no stage. Each stands on its own: suggest one
whenever it is useful — before, during, after, or entirely outside the flow
above — and never present them as required steps.

A project environment may have a subset of these skills supporting the user's
preferred workflow.

Cross-skill routing exists only when the `funcionario` hub skill is installed.

### How to use Funcionário Infinito

Ask whether one implementation session can reasonably understand, implement,
review, and finish the change. Scope is only one signal: high risk, unclear
requirements, architectural reach, or coordination between people pushes work
up a tier even when it is small.

- **Trivial.** The edit is obvious and low-risk: make it directly and use no
  Funcionário Infinito skill at all — unless the user asks for Funcionário Infinito, or the change
  would still benefit from explicit planning and review.
- **One session.** One coherent intent that fits an implementation session:
  hand it straight to `funcionario-build`. No planning skill needs to run first.
- **Epic-sized.** One coherent outcome that needs several sessions: run
  `funcionario-spec` to pin down the what, tell it to create architecture and/or UX
  companion files if the situation calls for it, have it break the spec into
  stories, then run `funcionario-build` or `funcionario-build-auto` once per story. Risky
  and foundational stories deserve human attention, therefore `funcionario-build`;
  once the decisions and patterns are stable, an orchestrated loop
  dispatching `funcionario-build-auto` sessions may also be used. Finish with
  `funcionario-retrospective` against the spec.
- **Project-sized.** 10-100 coding sessions: take the full planning route —
  `funcionario-product-brief` or `funcionario-prfaq`, then `funcionario-prd`, then `funcionario-ux` when
  the user experience matters, then `funcionario-architecture`,
  `funcionario-create-epics-and-stories`, and `funcionario-sprint-planning`. Each epic then
  runs like epic-sized work above, but without running spec for every epic.

### Answering "what's next?"

Read the state before recommending: which planning artifacts exist, and what
the codebase, git history, and/or the user says is done. Caution: presence of
a story file with `status: done` or another planning/tracking artifact like
this does not prove completion. Then:

- Mid-path, recommend the next unfinished stage of the chosen path, not a
  restart.
- When you detect ongoing sprint tracking, but sprint state is unclear, use
  `funcionario-sprint-planning`'s status action.
- After a Build: `funcionario-code-review` is an optional extra gate; offer
  `funcionario-qa-generate-e2e-tests` when automated coverage is wanted and
  `funcionario-walkthrough` when a human wants a walkthrough. Recommend
  repeated `funcionario-code-review` after material fixes until remaining findings
  no longer affect acceptance. Keep in mind that both build skills have a
  review step, and each `funcionario-code-review` run can take up to half an hour or
  more — it pays for itself when it catches real defects, not when it
  produces a long tail of minor issues. More than two iterations of agentic
  review on the same change is often a symptom of problems outside the
  change — bad planning, a messy codebase, etc.
- When an epic completes, offer `funcionario-retrospective`. When it — or anything
  midstream — exposes a significant planning change, route through
  `funcionario-correct-course`, then resume at the earliest affected skill once the
  proposal is approved; do not replay unaffected work.

A run is complete when the intent is satisfied, its chosen checks pass, and
no chosen review leaves material unresolved findings — not when every skill
has been traversed.

### When this document is not enough

For a method or toolbox question this section and the installed skills
cannot answer,
fetch `https://docs.funcionario-infinito.com.br/llms.txt` and follow the links relevant
to the question. It indexes the full documentation site and names the source
repository, which is the final authority on how anything actually behaves.

### Where things land

Durable specs and their story lists live under `{output_folder}/specs`;
planning documents and change proposals under `{planning_artifacts}`; Build's
working records, sprint status, reviews, and retrospectives under
`{implementation_artifacts}`; implementation in the project working tree;
generated QA tests under `{project-root}/tests`; and repository guidance at
`{project-root}/AGENTS.md`.
