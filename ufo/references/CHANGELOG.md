# UFO-FSD CHANGELOG

Dated re-charter history, extracted from normative prose per improvement-pack
spec 08 §1. Normative text in SKILL.md and run-logic.md stays timeless; every
dated decision lives here. Entry format: date / decision / supersedes /
rationale / evidence. This file is a tracked canonical doc: it rides the
contract-sync mirror set and the native contract hash.

## 2026-09-11 — dispatch-time output policy
- decision: English natural-language output with unchanged English JSON
  contract keys; `--print-thoughts` controls output visibility ONLY (not
  reasoning effort, verbosity, tool access, or auto-approval); no
  model-specific reasoning-language instruction
- supersedes: none (initial statement)
- rationale: admission relies on observable actions and artifacts; hidden
  reasoning is never required evidence
- evidence: SKILL.md OMP native profile; corrected wording 2026-09-17

## 2026-09-11 — Sekhmet/L3 shelved
- decision: Sekhmet/L3 is shelved — no sparks as routes, fallback
  transports, proposal seats, or prerequisites; the retained
  evidence-only implementation and its 64-worker ceiling are
  compatibility data, and no spark output enters a NativeRoundHandoff
- supersedes: L3 as an active dispatch tier
- rationale: operator doctrine; the OMP native profile carries dispatch
- evidence: SKILL.md role section; run-logic §4.2; `l3Evidence` config

## 2026-09-12 — SWE-2-everywhere route contract
- decision: all seats on `devin/swe-2`, including a same-day flash-main
  interlude
- supersedes: initial mixed routing
- rationale: uniform seat routing under Devin OAuth
- evidence: superseded 2026-09-15; git history

## 2026-09-15 — OMP-only re-charter; route table frozen
- decision: OMP is the only automatic substrate (`automaticSubstrate` stays
  `omp`; the other six adapters are compatibility surfaces); per-seat route
  table frozen — Main, fleet L1s, and thinking seats on `devin/swe-2:max`
  with empty fallbacks; distiller and the six mechanical seats on pinned
  flash chains; advisor disabled (absent from `omp-native-v1`);
  `xai/grok-4-fast` removed from all chains; Kimi Code OAuth de-chained
  (installed, no active chain)
- supersedes: 2026-09-12 SWE-2-everywhere
- rationale (token-poor, operator): the Token Plan carries ~15 USD of
  credits, so paid flash capacity fronts the high-throughput mechanical
  seats while unmetered SWE-2 covers Main and the thinking seats
- evidence: config/ufo.json pins; git history

## 2026-09-16 — planner-seat override
- decision: planner seat primary `alibaba-token-plan/qwen3.8-max:xhigh`,
  empty fallback — the only deviation from the frozen 2026-09-15 table
- supersedes: planner on `devin/swe-2:max` (2026-09-15)
- rationale: operator directive; planner quality on the xhigh effort tier
- evidence: config/ufo.json `modelRoutes.planner`

## 2026-09-17 — improvement pack re-charter (PC + P3 + P4)
- decision: admission profiles split (strict v1/v2 + resilient attempt
  ledger); failure-action matrix + backpressure under
  `nativeProfiles.*.recovery`; effective-launch attestation; token budgets
  (`budgets.*`, `honesty_brake`/`interrupted` emitted); route table gains
  tier indirection (`routeTiers`/`seatTiers`) + `failureDomains` +
  `routes:equivalence` gate + per-domain Phase 0 probes + lane-health
  ledger; prose route table deleted from run-logic §6/SKILL.md (config is
  the sole statement); drill matrix harness + dependency closure
- supersedes: prose-restated route table (config was already authoritative)
- rationale: three re-charters in five days proved the table is the
  most-volatile artifact in the most expensive format; correctness core
  before efficiency per the pack's merged phase order
- evidence: docs/advisory/2026-09-17-ufo-improvement-pack/; commits
  4043a7e7 (PC-A), 1bddc7b3 (PC-B), c166c8cd (PC-C), 2c087de6 (P3),
  285fc692 (P8-structural)

## 2026-09-18 — improvement pack judgment/enforcement/hygiene (P5–P7)
- decision: membrane sign-off (`authority_boundary` + TTY-gated
  `ufo charter sign` + Phase 0 re-pass) with artifact-trust screening;
  executable/evidence/subjective axis measurements with computed deltas
  outranking advisory scores; writer lease with fencing epochs,
  journaled transactional apply, and raw+derived evidence digests;
  bounded round digests (`ufo-round-digest-v1`) with the clean-round
  saturation rule and plan-digest binding with wave-drift provenance
- supersedes: prompt-text-only enforcement boundaries; advisory-only
  axis scoring; unbounded cache carry; saturates-on-any-zero-accept
- rationale: judgment integrity requires mechanism below the prompt
  (F09–F12, F18); computed measurement beats narrated improvement
- evidence: docs/advisory/2026-09-17-ufo-improvement-pack/; commits
  52898c0b + 5bd0584d (P5), 1d1f95d4 (P6), 241ec3a2 (P7)

## 2026-09-19 — swarmport contract amendments (kimi /swarm port)
- decision: axes are dynamic — declared per round by the planner,
  externally visible, stable within a round, free to evolve between
  rounds, never frozen at Phase 0; fleet dispatch prompts begin with the
  literal `/skill:ufo` line; the WWKD posture is uncapped (no milestone
  cap, no plan size limit); swarm members are leaf profiles — no
  task/hub/jobs tooling, no delegation, no background jobs — enforced by
  the member agent definition: OMP `tools:` frontmatter is an allowlist,
  so a leaf profile excludes `task`/`hub`/`jobs` and sets `spawns: []`
  (no per-agent `tools_deny` exists; `tools.approval` deny is
  session-scoped); swarm lane routing — thinking roles to
  `xai-oauth/grok-4.5:low`, mechanical roles to `cursor/composer-2.5-fast`,
  `devin/swe-2` never a swarm lane; the wave election rule — a wave procs
  only on unjudged fleet scope with >=2 same-shape plan items, judged
  rounds keep the frozen proposal topology, wave output is advisory
  evidence only; vocabulary — the unit is a *wave*, `fleet` stays the
  mission class, and the wave cap is distinct from the "up to 16 L2 lanes
  per L1" fan-out doctrine
- supersedes: "Axes freeze before the first plan" (run-logic §4),
  `/ufo` fleet prefix, swe-2 swarm routing note
- rationale: operator amendments to the kimi /swarm → OMP ufo-fsd port
  (swarmport-contract mission); connector-synthesis C1/C2/C3/C9
  resolutions
- evidence: skills/ufo/SKILL.md, skills/ufo/references/run-logic.md,
  agents/planner.md, config/ufo.json `sighting.dispatch.swarm.note`

## 2026-09-20 — L1-orchestrator loop doctrine (nightcall-swarm-evidence)
- decision: codify the unjudged fleet mission loop — a fleet L1 is an
  autonomous, self-iterating orchestrator and its own judge on unjudged
  missions; a mission is a loop of WWKD-planned, axes-governed wave
  dispatches (plan → dissect + dispatch → judge → ship + loop), never a
  one-shot task; the loop stops honestly (saturated / blocked / budget)
  with the stop state emitted
- supersedes: none (the 2026-09-19 amendments defined wave mechanics; this
  defines the mission-level loop those waves serve)
- rationale: operator dispatch binding for the nightcall fleet; waves
  without the loop doctrine read as one-shot fan-out
- evidence: run-logic §4.3 closing block; SKILL.md dispatch-contract swarm
  text; mission scope .ufo/scopes/nightcall-swarm-evidence/ (r01 plan +
  verdict)

## 2026-09-20 — swarm ledger re-anchor + lifecycle/routing doctrine (nc2-evidence r01)
- decision: SWARM-PARITY re-anchored to HEAD 953c6050 (committed
  registry/record/priorRegistry/collect landings); D5 split into landed
  ownership vs deferred idle/dead-agent checks; V6 corrected — ufo emits
  `stop_reason` on any row carrying `stopReason`, not completed rows only;
  V7 added — `message`/`prompt` surface split (spawn_message_forbidden,
  message_with_prompt, duplicate_resume_id, duplicate_name); A6 records
  the final nightcall fleet map (planner/critic/connector daybreak;
  scout/executor composer; remaining L2 roles grok; no swe-2 L2) without
  touching canonical pins; leaf-profile enforcement claim corrected: the live OMP binary
  consumes tools:/spawns: (leaf-by-default via absent spawns:; spawns: []
  is a footgun → wildcard *); executor is the declared non-leaf exception
  (spawns: labrat); jobs is a hub op, not a tool name;
  record/priorRegistry lifecycle codified in SKILL.md swarm list item 5
  and run-logic §4.3 item 4; L0 fleet-monitor duty codified in run-logic
  §8.1 with a SKILL.md pointer (drift detect → queue-locked current-byte
  digest rebind → repend → liveness re-verify; never fabricate evidence or
  resurrect retired-fleet rows); run-immutable-axis wording replaced with
  dynamically discovered per round; swarm-wave payload now prefixes every
  spawned lane with `/skill:godspeed`
- supersedes: "leaf profiles enforced by the member agent definition"
  (wrong mechanism details: tools:/spawns: exist in the live binary;
  enforcement is taxonomy + instructions + spawn-policy default)
- rationale: doctrine must not claim enforcement that does not exist;
  fleet overrides are recorded, never silently globalized
- evidence: .ufo/scopes/nc2-evidence/w1/ lane reports;
  conformance/vectors/swarm-parity 55/55 (incl. 10 sp-collect-* rejections
  + 6 sp-record-* pins); evidence/nc2-evidence/r01-*.json


## 2026-09-20 — wave-band floor + godspeed-hook mechanism doctrine (nc2-evidence v3r01)
- decision: SKILL.md swarm item 3 and run-logic §4.3 item 2 replace the
  falsified "at least two lanes unless every lane is a resume" claim with
  the configured wave band (`waveMinLanes`/`waveMaxLanes`, repo 16–32,
  `too_few_lanes`/`wave_too_wide`; resume-only waves exempt; a config
  policy declaring no wave band falls back to the swarm band, so the
  band-less floor is `minLanes`, default 2 — the kimi-parity minimum).
  SKILL.md swarm item 1 and run-logic §4.3 correct the godspeed-injection
  mechanism: the `.omp/hooks/pre/ufo-godspeed-inject.js`
  `tool_call` hook injects the leading `/skill:godspeed` into every
  `task`-tool dispatch (idempotent); only surfaces bypassing `tool_call`
  (eval-kernel `agent()`/`workpool()`) prepend it themselves. SWARM-PARITY
  A6 re-anchored to the live global delegation table (executor/simplifier
  → `@m_flash` per `cf186b88`; connector/sentinel → `@m_grok` per
  `bb92fa6c`)
- supersedes: "direct `task`/topology-seat dispatches prepend it
  themselves" (the hook is now the injector for all `task`-tool
  dispatches; manual prepend is redundant-but-idempotent outside the
  eval kernel)
- rationale: doctrine must describe the enforced floor and the actual
  injection mechanism; a falsified floor claim teaches L1s to plan
  illegal waves
- evidence: `node scripts/ufo-swarm-wave.mjs plan` on a 2-lane spec →
  `too_few_lanes` (floor 16); `.omp/hooks/pre/ufo-godspeed-inject.js`;
  `~/.omp/agent/config.yml:39-52`; `.ufo/scopes/nc2-evidence/w2/` lane
  reports (SwarmCritic14 C1/C2, SwarmConnector13 §c, SwarmScribe16 R16-R18)

## 2026-09-20 — axes authority: planner proposes, L1 declares
- decision: the round's task axes are proposed by the planner seat and
  declared by the L1 in the per-round WWKD plan it writes
  (`ufo-round-plan-v1`); the set stays stable within the round and free to
  evolve between rounds
- supersedes: the 2026-09-19 entry's "axes are dynamic — declared per round
  by the planner" wording — the planner proposes the axis set, the L1
  declares it (the rest of that amendment stands)
- rationale: the declaration owner is the L1-authored plan, so the
  2026-09-19 phrasing names the wrong seat for the declaration and
  contradicts the canonical carriers
- evidence: `agents/planner.md` ("Propose the round's task axes … the L1
  declares the set in that plan per round"); `skills/ufo/references/run-logic.md`
  §5 ("The plan is written by the one L1"; "Every declared axis names its
  measurement … declared with the round's axis set") and §8 ("axes are
  dynamically discovered per round and declared by the L1 in its WWKD plan");
  `skills/ufo/SKILL.md` dispatch contract ("L1 writes exactly one WWKD plan
  before each judged round") + WWKD-planned, axes-governed loop; `AGENTS.md`
  per-round dynamic axes

## 2026-09-20 — global-alias routing cutover
- decision: seat routes leave the project. Global OMP config
  (`~/.omp/agent/config.yml` `task.agentModelOverrides` + `modelRoles` +
  `retry.fallbackChains`) is the only seat-route authority; launcher resolves
  at dispatch; generated `crates/ufo-core-runtime/bundled/omp-seat-routing.json`
  mirrors into the compiled runtime. Project `config/ufo.json` drops
  `modelRoutes`/`modelFallbacks`/`routeTiers`/`seatTiers`/`failureDomains`.
  Verified seats: planner/revenger → `@m_daybreak` =
  `openai-codex/gpt-daybreak-blue-latest:max` `[]`; reviewer/critic →
  `@m_luna` = `openai-codex/gpt-5.6-luna:low` + Luna cascade; connector/
  sentinel/scout/labrat/mutation-tester/scribe/distiller → `@m_grok` =
  `xai-oauth/grok-4.5:low` + Grok cascade; executor/simplifier → `@m_flash` =
  `alibaba-token-plan/deepseek-v4.1-flash:max` + flash cascade
  (`opencode-go` first hop). Main/fleet L1 stays dispatch `route`
  `devin/swe-2:max`. Retry policy
  `usageAwareFallback=false`/`fallbackRevertPolicy=never` and `l1Context`
  capability metadata remain project-owned.
- supersedes: 2026-09-15/16 project pin table; 2026-09-17
  `routeTiers`/`seatTiers` indirection as live authority; 2026-09-19 swarm
  prose that hard-coded thinking→grok / mechanical→`composer-2.5-fast`
- rationale: operator directive — no project-level model declarations or
  delegations; a fleet overlay once silently overrode the global table
- evidence: `AGENTS.md` Routing authority; `.ufo/scopes/global-routing-cutover/contract.md`;
  docs/L2-L3-ROUTING.md; live `~/.omp/agent/config.yml`

## 2026-09-20 — NC2/nightcall declared the standard fleet dispatch protocol
- decision: NC2 is the standard shape of every UFO-FSD fleet dispatch — the
  observed Nightcall fleet graph, not a newly invented topology. L0 maps the
  whole fleet first (one WWKD map, disjoint scopes), then batch-enqueues the
  independent self-iterating L1 frontiers — crates, tooling, tests, docs,
  packages, evidence, verify — each with `requestedRunners: 1` and 8-round
  iteration. Verify is a concurrent read-only frontier; later
  iterate/integration receipts may add dependencies (no skeleton-first or
  mandatory initial verify binding). One L1 per mission, at most 16 live L1s
  globally (`sighting.dispatch.maxConcurrentL1`); new fleet enqueues default
  to `config/mission-nightcall.yml` with 8-round iteration
  (`sighting.dispatch.missionFormat`). Every mission is one fresh L1 whose
  prompt begins `/skill:ufo`; every fresh L2 task text begins
  `/skill:godspeed` (the invocation, never bare shorthand); L0 is the sole
  operator↔mission interaction and monitor surface and never judges inside a
  mission. Every L1 — a fleet mission and a canonical native-trial Main alike
  — selects a global L1 alias from the allowed set `[m_daybreak, m_swe]`
  (`missionFormat.l1Alias`, default `m_daybreak` → `openai-codex/gpt-daybreak-blue-latest:max`;
  `m_swe` = `devin/swe-2:max`; both terminal). The observed NC2 split is
  crates/tests on `m_swe` and tooling/docs/packages/evidence/verify on
  `m_daybreak`, with native Main on the default. Every L2 seat resolves
  routing and cascades only through the global OMP alias table — per-project
  and per-mission concrete model declarations are prohibited; a mission spec
  selects an alias, never a concrete route (the `fleetL1Route` key is
  removed). Global L2 seat distribution: 7 `@m_flash` (planner, revenger,
  scout, labrat, mutation-tester, scribe, distiller), 4 `@m_grok` (reviewer,
  critic, connector, sentinel), 2 terminal `@m_composer` (executor,
  simplifier).
  `task.maxConcurrency: 0` everywhere means no OMP
  host secondary cap; the finite UFO bounds are independent: ≤100 atomized L2
  members per L1 in sequential 16–32 waves, under the configured global runner
  ceiling. Standard lane families: crates, tooling, tests, docs, packages,
  evidence, verify (subset follows the disjoint decomposition; verify is
  read-only integration unless given ownership). Prompt and mechanics
  contract: `/skill:ufo`, exact directive bytes, explicit scope/acceptance,
  report + receipt per round, one terminal marker, OMP-native task/Hub
  self-iteration with dynamic per-round axes; contract freeze and
  same-identity reroute unchanged.
- supersedes: any reading of nightcall as one special fleet, fleet-scoped
  route pins over the global table, the interim guidance split that kept a
  native-trial Main on a project `devin/swe-2:max` route, and the kimi-parity
  128 population constant as the live swarm ceiling (the planner's
  `MAX_SWARM_LANES` hard bound now backs the 100-member policy cap); the
  64-lane round floor stays declared policy
- rationale: operator directive — the proven nightcall/NC2 shape is the
  standard for every future fleet; per-fleet route binds re-open the
  split-routing failure, and a wider population ceiling misstates the
  enforced bounds
- evidence: `.ufo/scopes/nc2-standard/l0-wwkd-plan.md`; `AGENTS.md` NC2
  section; `skills/ufo/SKILL.md` fleet subsection; run-logic §8.2; config
  `sighting.dispatch.missionFormat`/`maxConcurrentL1`/`swarm`

## 2026-09-20 — routing provenance and parity-ledger reclassification
- decision: preserve the global OMP alias table as the only L2 seat-route and
  cascade authority while distinguishing its operator-global retry flag from
  the hash-bound project/native launch projection. Only typed capacity
  evidence authorizes a hop; neither configured value proves a served route.
- ledger: `docs/SWARM-PARITY.md` A1 is now explicit dated 2026-09-19 doctrine;
  A6 is the current global-only cutover pointer. The former project/overlay
  tables and w4/w7 spawn aliases remain dated requested-route evidence, never
  current authority or served-model proof.
- evidence: live `~/.omp/agent/config.yml`; generated
  `crates/ufo-core-runtime/bundled/omp-seat-routing.json`; `AGENTS.md` Routing
  authority; nightcall-swarm-evidence r11 wave A.

## 2026-09-21 — m_composer moved to the non-fast composer variant
- decision: the global OMP alias `m_composer` (executor, simplifier) resolves
  `cursor/composer-2.5` instead of `cursor/composer-2.5-fast`; the alias's
  terminal empty chain, the seat distribution (2 `@m_composer`, 7 `@m_flash`,
  4 `@m_grok`), and every other seat route are unchanged. The derived seat
  mirror, the execution-profile vector/test, the native-handoff fixture, and
  the repo routing docs were re-derived from the live global table
- supersedes: the `cursor/composer-2.5-fast` mechanical/composer route named
  in the 2026-09-19 swarm-routing prose and carried by the 2026-09-20
  global-alias cutover (alias set and chain shape unchanged)
- rationale: operator directive — the bounded code-execution seats run the
  normal composer variant, not the fast one
- evidence: live `~/.omp/agent/config.yml` (modelRoles.m_composer);
  regenerated `crates/ufo-core-runtime/bundled/omp-seat-routing.json`;
  `conformance/fixtures/native-handoff`; `docs/L2-L3-ROUTING.md`

## 2026-09-21 — commits are the trail; artifacts are ephemeral
- decision: finished fleet work is committed path-scoped
  (`git add -- <paths>` + `git commit -- <paths>`) and pushed to the cursor
  `origin` remote (`origin.cursor.com`) — never GitHub — so the pushed
  history is the auditable trail by itself. Run artifacts (`.ufo/` sessions,
  scopes, results, dispatch snapshots) are ephemeral: gitignored, pruned at
  completion, never the record. Validation is proof-by-doing on the changed
  surface — the smallest real observation that shows the change works — not
  a repeated full gate battery. There is no review-theater seat: no fleet
  lane exists to re-review what a landed commit already proved. The runtime
  ship path stays unarmed (run-logic §10 unchanged): no runtime mechanism
  commits or pushes; the L1 agent's own git operations are the trail, and
  public publishing stays operator-owned.
- supersedes: mission prompts minted with a "No git commits" line (the line
  lived only in prompt bytes under gitignored `.ufo/`, never in tracked
  guidance); any reading of AUTO-SHIP.md's "does not commit or push" or
  "operator retains every publish decision" as a ban on the L1's own
  path-scoped cursor-origin commits
- rationale: operator directive — code is ephemeral, commits pushed to
  cursor origin are the auditable trail; stale artifacts and review theater
  are laggard; GitHub rate limits never apply on the cursor remote
- evidence: fleet `lean` L0 map `.ufo/scopes/lean/l0-wwkd-plan.md`;
  `AGENTS.md` commit-trail doctrine; SKILL.md ship section; annotated
  `docs/AUTO-SHIP.md` and `docs/EPHEMERAL-L1-MISSIONS.md`; pushed range
  recorded in the lean-flush mission receipt
