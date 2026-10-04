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
- supersedes: "Axes freeze before the first plan" (run-logic §4),
  `/ufo` fleet prefix, swe-2 swarm routing note. Sub-clauses since
  superseded: planner-declared axes → L1-declared (:186-191); hard-coded
  swarm routes → global-alias table (:206-225); `spawns: []` leaf spelling
  → omit-the-key (:129-151); "no plan size limit" → `MAX_PLAN_ARTIFACT_BYTES`
  4 MiB (agents/planner.md, run-logic §5).
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
- supersedes: `docs/SWARM-PARITY.md` A1 is now explicit dated 2026-09-19 doctrine;
  A6 is the current global-only cutover pointer. The former project/overlay
  tables and w4/w7 spawn aliases remain dated requested-route evidence, never
  current authority or served-model proof.
- rationale: configured values are not served-model proof; the parity ledger
  must not present requested routes or overlay tables as current authority.
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
  global-alias cutover (alias set and chain shape unchanged). The
  parenthetical seat binding "(executor, simplifier)" was the 2026-09-21
  snapshot — superseded by the later seat-table redelegations (simplifier
  rides `@m_flash` at nc5 HEAD); the alias's model choice stands.
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
  path-scoped cursor-origin commits. The `origin.cursor.com` wording was
  narrowed by the AGENTS.md commit-trail doctrine: cursor `origin` in the
  canonical repo, a local bare `origin` inside the isolation root in
  ephemeral fleets — never GitHub either way.
- rationale: operator directive — code is ephemeral, commits pushed to
  cursor origin are the auditable trail; stale artifacts and review theater
  are laggard; GitHub rate limits never apply on the cursor remote
- evidence: fleet `lean` L0 map `.ufo/scopes/lean/l0-wwkd-plan.md`;
  `AGENTS.md` commit-trail doctrine; SKILL.md ship section; annotated
  `docs/AUTO-SHIP.md` and `docs/EPHEMERAL-L1-MISSIONS.md`; pushed range
  recorded in the lean-flush mission receipt

## 2026-09-21 — maxConcurrentL1 16→32; wave band 16–100; no L1-alias allowlist
- decision: live fleet admission is `sighting.dispatch.maxConcurrentL1 = 32`
  and `sighting.dispatch.swarm.waveMinLanes`/`waveMaxLanes` = 16/100
  (`waveMinLanes` stays 16). `globalRunnerCeiling` is 1056 (= 32 L1s + 1024
  L2 lanes). Timeless run-logic header and §8.2 / SKILL.md / AGENTS.md
  state 32 and 16–100. Every L1 selects any bare alias that resolves in
  the fd-bound global OMP config; there is no project allowlist.
  The 2026-09-20 NC2 CHANGELOG entry remains the historical decision that
  first set 16 live L1s, a 16–32 wave band, and an `[m_daybreak, m_swe]`
  example set.
- supersedes: the then-current 16 live-L1 cap, 16–32 wave band, and
  L1-alias allowed-set wording named in the 2026-09-20 NC2 standard and
  wave-band amendment entries (those entries stay dated history, not
  rewritten)
- rationale: operator raise in commit `91cc18fe` so 32 L1s fit under
  ceiling 1056 with 16–100 waves; allowlist relaxation is already
  timeless in SKILL/AGENTS/§8.2
- evidence: commit `91cc18fe`; `config/ufo.json` `maxConcurrentL1` and
  `swarm.waveMinLanes`/`waveMaxLanes`; run-logic §8.2 item 1; SKILL.md
  fleet block; AGENTS.md NC2 item 1 and "any bare alias"


## 2026-09-21 — planner seat → `@m_swe`
- decision: the live global OMP planner seat is `@m_swe` (`devin/swe-2:max`,
  terminal empty chain). The remaining flash cohort is six seats
  (revenger, scout, labrat, mutation-tester, scribe, distiller) on
  `@m_flash`. Timeless `AGENTS.md` Routing authority table splits planner
  onto `@m_swe` and leaves those six on `@m_flash`.
- supersedes: the live-law reading of planner as a member of the seven-flash
  cohort named in the 2026-09-20 NC2 seat-distribution sentence and
  reaffirmed as census in the 2026-09-21 composer-variant entry (those
  entries stay dated history, not rewritten)
- rationale: live `~/.omp/agent/config.yml` `task.agentModelOverrides.planner`
  is `@m_swe`; the AGENTS table is a present-tense summary of that authority
  and went stale after the live flip
- evidence: live `~/.omp/agent/config.yml` planner override; bundled
  `omp-seat-routing.json` planner alias `m_swe`; `AGENTS.md` Routing
  authority table


## 2026-09-21 — planner seat → `@m_grok47`; seat table is a dated observation
- decision: the live global OMP planner seat is `@m_grok47`
  (`xai-oauth/grok-4.7:high`, chain `cursor/grok-4.7-high:high` →
  `xai/grok-4.7:high` → `devin/grok-4.7:high`). The `AGENTS.md` Routing
  authority table is a dated observation of the live global config — never a
  timeless contract — and is re-pinned whenever the live table moves.
- supersedes: the same-day "planner seat → `@m_swe`" entry above, which
  recorded the pre-`a3e15b36` table and mislabeled the AGENTS table as
  timeless (that entry stays dated history, not rewritten)
- rationale: live `~/.omp/agent/config.yml` `task.agentModelOverrides.planner`
  is `@m_grok47` (config sha `1ac071d3`); commit `b21a5aa1` established the
  dated-observation caption after the table went stale twice in one day
- evidence: live `~/.omp/agent/config.yml` planner override; bundled
  `omp-seat-routing.json` planner alias `m_grok47`; `AGENTS.md` Routing
  authority table caption; commits `a3e15b36`, `b21a5aa1`, `2c99e546`


## 2026-09-21 — r13 repairs: wave-unit sentence restored; wwkd source path scoped
- decision: run-logic §4.3's wave-cap sentence regains its subject ("The unit
  is a *wave*; `fleet` stays the mission class. The wave cap is its own
  ceiling, distinct from the wave band that sizes each dispatch.") — the r12
  16-lane repair clipped the subject and left an orphan clause. wwkd
  SKILL.md's `~/wikillm/…` citation is now labeled the external authoring
  source, not a runtime dependency (absent on fleet hosts; SKILL.md is
  self-contained).
- supersedes: none (r12 collateral repair, not a decision reversal)
- rationale: prose integrity is a claims axis — an orphaned clause reads as
  normative text with a missing referent; a host-dead path stated as live
  source is a falsifiable claim.
- evidence: `git show 103357d5` hunk at run-logic.md:666 (clipped subject);
  `ls ~/wikillm` absent; sync `--check` green post-edit; ufo-deps.lock wwkd
  pins re-stamped (`d6ed6310`, `7d252ac2`).

## 2026-09-21 — L2 seat table redelegated to a four-alias split
- decision: the live global OMP seat table is four aliases — planner →
  `@m_grok47` (`xai-oauth/grok-4.7:high`, chain
  `cursor/grok-4.7-high:high` → `xai/grok-4.7:high` → `devin/grok-4.7:high`);
  reviewer + connector → `@m_swe` (`devin/swe-2:max`, terminal empty chain);
  critic + sentinel → `@m_luna` (`openai-codex/gpt-5.6-luna:low`, chain
  `devin/gpt-5-6-luna:low` → `cursor/gpt-5.6-luna:low` →
  `cursor/gpt-5.6-luna-fast:low`); the remaining eight seats (revenger,
  scout, executor, labrat, mutation-tester, simplifier, scribe, distiller) →
  `@m_zfl` (`zai/glm-5.3-flash:max`, chain `charm-hyper/glm-5.3-flash:max` →
  `opencode-go/glm-5.3-flash:max` → `devin/glm-5-3-flash-1m:max`). The prior
  seat distribution (`@m_composer` ×2, `@m_flash` ×7, `@m_grok` ×4,
  `@m_daybreak`/`@m_luna` planner/reviewer/critic) is fully superseded —
  those aliases still resolve in the global config but bind no seat. The
  `AGENTS.md` Routing authority table stays a dated observation and matches
  this table; the bundled `omp-seat-routing.json` mirror carries it and
  `routes:equivalence` holds for 14 seats. The L1 alias table is separate
  and unchanged (`missionFormat.l1Alias` default `m_daybreak`; any bare
  alias resolving in the fd-bound global config is selectable).
- supersedes: the seat distributions recorded in the 2026-09-20 NC2 entry,
  the 2026-09-21 composer-variant entry, and the two same-day planner-flip
  entries (those entries stay dated history, not rewritten — this entry
  closes the same-day redelegation sequence they recorded mid-flight). The
  four-alias live-table claim itself is superseded by the nc4-era seat
  table (`cbb685ad`, 2026-09-23 — the AGENTS.md dated observation read
  2026-09-23 records it: planner `m_sol6`, reviewer `m_luna6f`,
  critic/sentinel `m_grok`, connector `m_antigravity`, scout/executor/
  scribe `m_composer`, revenger/labrat/mutation-tester `m_zfl`,
  simplifier/distiller `m_flash`).
- rationale: operator redelegation consolidated the L2 seats onto four
  aliases; the dated-decision log must record the settled table, not only
  the intermediate flips
- evidence: live `~/.omp/agent/config.yml` `task.agentModelOverrides` +
  `retry.fallbackChains`; bundled
  `crates/ufo-core-runtime/bundled/omp-seat-routing.json`; `AGENTS.md`
  Routing authority table; `.ufo/scopes/nc3/l0-wwkd-plan.md` routing note
  ("post-15:30Z redelegation")

## 2026-09-22 — run-logic §8 codifications: third L0 surface, receipt contract, deferred-continue
- decision: three normative codifications landed in `run-logic.md` §8,
  each closing a discoverability gap where the normative layer lagged
  shipped behavior. (a) §8.1 names the third L0-owned healing surface —
  `scripts/ufo-night-watchdog.sh` heals the SUBSTRATE (wall tmux recovery,
  hung-client reaper, daemon singleton+respawn, bounded repend) where the
  two monitor carriers heal lane state (commits `1e07756e` codification +
  `154ae417` normative text). (b) §8.2 item 6 carries the
  dispatch-binding/receipt contract — binding fields, `ufo-task-receipt-v1`
  exact-keys rule, `promptSha256` sidecar-verbatim rule, iterate decision
  set, and optional `reason`/`nativeVerdict`/`blockedAudit` fields that
  `AGENTS.md` documented and `fleet-dispatcher.mjs` minted but the
  normative spec omitted (commit `ff87d9b2`). (c) Iterate chains gain
  deferred-continue semantics — an occupied-scope successor mint records
  `deferred: "scope_occupied"` + `scopeOccupiedBy` on the parent
  `iterationOutcome`, mints no row, and `reconcileQueue` re-attempts each
  pass once the blocker drains; successor identity is pure in (parent,
  round, priorReceiptSha256) (commit `fd4f0451`, codifying dissection r16
  `63952cc0`).
- supersedes: none (gap closures, not reversals — each section previously
  under-described already-shipped behavior)
- rationale: this file's contract is "every dated decision lives here";
  the three §8.x codifications are dated normative decisions and the log
  skipped them. A lane reading only the dated history could not discover
  that deferred-continue, the receipt contract, or the watchdog surface
  are normative.
- evidence: commits `1e07756e`, `154ae417`, `ff87d9b2`, `fd4f0451`;
  `run-logic.md` §8.1 third-surface paragraph, §8.2 item 6 binding
  paragraph, iterate-chain deferred paragraph; dispatcher
  `fleet-dispatcher.mjs` `iterationOutcome.deferred`/`scopeOccupiedBy`
  (:4806-4814, :5979-5995) and `validateTaskReceipt` optional-key
  admission

## 2026-09-22 — run-logic §8.1 session-hook single-flight codification
- decision: §8.1's description of the `.omp/hooks/pre/ufo-l0-monitor.js`
  session hook now records the mechanisms the hook actually runs:
  coverage-aware freshness (a run counts only when its recorded `fleets`
  set covers the hook's own; `null` unscoped covers all; absent field
  fails open), the `O_EXCL` claim file `.ufo/l0-monitor-claim.json`
  serializing concurrent sessions (stale past spawn timeout + 10s), the
  `UFO_L0_MONITOR_FLEETS` / `UFO_L0_MONITOR_INTERVAL_MS` operator knobs
  (defaults `nc3` / 120s, 5s floor, malformed fleets falls back), and the
  tick schedule (session start + interval + every turn end) with the
  `l0mon` status segment. Codifies hook behavior landed in tooling r32
  (`b53e7f9b`, coverage-aware throttle) and r36 (`c02c4ee7`, claim file).
- supersedes: none (gap closure — the section previously named only the
  shared-state throttle). The `nc3` default-fleet knob recorded here is
  superseded: nc5-guidance r01 rebound `UFO_L0_MONITOR_FLEETS` to `nc5`
  (run-logic §8.1 and `.omp/hooks/pre/ufo-l0-monitor.js` `DEFAULT_FLEETS`
  both read `nc5` at nc5 HEAD).
- rationale: the normative layer lagged shipped hook behavior; a lane
  reading §8.1 could not discover the single-flight claim, the
  coverage-aware freshness rule, or the operator knobs.
- evidence: `.omp/hooks/pre/ufo-l0-monitor.js` `isFresh` (:96-115),
  `claimRun`/`releaseClaim` (:165-206), `normalizeFleets`/
  `normalizeIntervalMs` (:54-77), `tick`/`session_start`/`turn_end`
  (:216-254); commits `b53e7f9b`, `c02c4ee7`

## 2026-09-22 — run-logic §8.1 watch respawn/seal/whip codification
- decision: §8.1's description of the `scripts/ufo-l0-watch.mjs` night
  watch now records the respawn arm's bounds and seal semantics the code
  actually runs: hourly enqueue caps (global `--max-enqueues-hour`
  default 48; per-lane `--max-lane-enqueues-hour` default 4), the
  `no_alias` / `bad_result_path` skip reasons (`no_alias` stays unsealed
  so a later `l1Alias` backfill can still respawn), the deferred seal
  that arms `done`/`donePath` only once a queue read confirms the
  successor row is visible, the per-tick done-seal re-check (reopen iff
  the successor is `failed`, or absent with no receipt or a `continue`
  receipt; stay sealed on a live non-failed successor, a terminal or
  unreadable receipt, or a pre-successor seal), and the per-lane whip
  cooldown (`--whip-cooldown-min`, default 15 minutes) that a skipped
  whip never starts.
- supersedes: none (gap closure — the section previously named only the
  heal/respawn/whip duties, not their bounds or seal rules)
- rationale: the normative layer lagged shipped watch behavior; a lane
  reading §8.1 could not discover the respawn budget, the seal
  re-check rules, or the whip cooldown — the same under-description
  class the 2026-09-22 session-hook entry closed for the first carrier.
- evidence: `scripts/ufo-l0-watch.mjs` `MAX_ENQUEUES_HOUR`/
  `MAX_LANE_ENQUEUES_HOUR`/`WHIP_COOLDOWN_MS` (:87-91, argv :1563-1565),
  skip reasons (:1045-1058), budget gates (:1071-1077), deferred seal
  (:1091-1130), done-seal re-check (:920-971), whip cooldown
  (:1169-1176)

## 2026-09-22 — run-logic §4.3 launch-ramp and minLanes codification
- decision: §4.3's swarm-wave dispatch doctrine now records the declared
  launch ramp and the repo `minLanes` value the code actually ships: the
  plan's `policy` block carries `rampBatchSize`/`rampIntervalMs`
  (`sighting.dispatch.swarm.*`, built-in defaults 5 lanes per 700 ms,
  kimi AgentSwarm parity) as pacing policy for substrates that pace
  manually — on OMP the single `task` call is the wave and the harness
  queues lanes beyond its concurrency window, so the ramp never splits
  or delays a dispatch — and the band-less `minLanes` floor now names
  both the built-in default (2, kimi-parity minimum) and the repo
  policy's declared 64 (a round-floor doctrine the planner does not
  gate).
- supersedes: none (gap closure — the section previously named the wave
  band and member ceiling but never the ramp keys or the repo minLanes)
- rationale: the normative layer lagged shipped planner behavior; a lane
  reading §4.3 could not discover the ramp constants recorded in every
  emitted plan or the repo's declared round floor — the same
  under-description class the 2026-09-22 §8.1 entries closed for the
  watch carriers.
- evidence: `scripts/ufo-swarm-wave.mjs` `SWARM_RAMP_BATCH_SIZE`/
  `SWARM_RAMP_INTERVAL_MS` (:170-171), config-key validation (:395-408),
  plan `policy` emission (:1078-1079), ramp semantics comment (:34-37);
  `config/ufo.json` `sighting.dispatch.swarm.minLanes` = 64

## 2026-09-22 — run-logic §8.2 receipt mint affordance and validation split codification
- decision: §8.2's receipt contract now records the shipped mint affordance
  and the validation split the code enforces: `create-receipt` accepts an
  optional `reportPath` input key (stripped before schema validation, never
  a receipt key) that hashes the report file's raw bytes at mint and fills
  `reportSha256` — refusing `""`/`"-"`/`--*` as `invalid_type` and a
  disagreeing declared digest as `receipt_mismatch` — and `validate-receipt`
  is shape-only while acceptance is the dispatcher's expected-bag
  cross-check binding the six digests/ids to the task that produced it.
- supersedes: none (gap closure — the section previously named the schema
  and the three digest rules but never the mint affordance or the
  shape-vs-acceptance split)
- rationale: the normative layer lagged shipped tooling; a lane reading
  §8.2 could not discover the `reportPath` mint path — the hand-computed
  digest it implied is exactly the stale-digest class the affordance
  exists to close — nor that `validate-receipt` exit 0 says nothing about
  fleet acceptance. Same under-description class the 2026-09-22 §4.3 and
  §8.1 entries closed for the ramp and watch carriers.
- evidence: `scripts/ufo-mission-result.mjs` `reportPath` destructure +
  refusals (:735-768), raw-bytes hashing comment (:676-679), usage +
  shape-only/expected-bag text (:686-690, :778-784)

## 2026-09-22 — run-logic §4.3 axes/milestone judgment binding codification
- decision: §4.3 now records the per-atom judgment binding the wave planner
  ships: spawn items may declare `axes` (1..8 distinct nonempty names ≤256
  bytes each, else `invalid_spec`) and `milestone` (nonempty ≤256 bytes);
  `spec.axes`/`spec.milestone` are wave defaults an item-level declaration
  overrides outright (never merges); absent at both levels the lane is
  judged on the round's axes; the binding renders into the spawn prompt as
  `Judged on:`/`Milestone:` lines ahead of the reportDir suffix and
  persists on the member's registry row; resume lanes inherit the
  spawn-minted binding and may not restate either key
  (`resume_meta_forbidden`), while the resume member's registry row copies
  it forward so collect still attributes the verdict.
- supersedes: none (gap closure — the section previously named the wave
  band, member ceiling, ramp, and registry mechanics but never the
  per-atom judgment binding)
- rationale: the normative layer lagged shipped planner behavior; a lane
  reading §4.3 to dissect a wave could not discover that atoms carry
  their own scoring axes — the mechanism the dissection-quality mission
  goal is built on. Same under-description class the 2026-09-22 §4.3,
  §8.1, and §8.2 entries closed for the ramp, watch, and receipt-mint
  carriers.
- evidence: `scripts/ufo-swarm-wave.mjs` `MAX_LANE_AXES`/
  `MAX_LANE_META_BYTES` (:242-243), `validateLaneMeta` bounds + absent
  semantics (:663-686), item-over-spec resolution (:847-848),
  `laneBindingSuffix` render (:694-702), registry member persistence
  (:1117-1121), resume-member copy-forward (:1112-1113),
  `resume_meta_forbidden` (:809-814)

## 2026-09-22 — run-logic §4.3 collect contract and registry/collect seam codification
- decision: §4.3 now names the aggregation bridge
  (`scripts/ufo-swarm-collect.mjs`) and records its join contract plus the
  registry/collect seam mechanics the planner and collector ship:
  persisting over an existing registry surfaces every displaced handle on
  the dispatch payload as `handlesReset`
  (`{name, previousAgentId, agentId}` — a re-run's `agentId: null` reset
  and a resume re-point to a different handle both kill the old handle's
  only ownership row); the collect join is fail-closed
  (`unmapped_member`/`unexpected_member`/`duplicate_member`); identity
  evidence is three-way — registry (authority) > results row >
  resume-derived — with distinct non-null values `conflicting_member` and
  an unresolvable resume id `missing_agent_id`; `resumeSends[].resume` is
  shape-validated at join (nonempty string ≤256 bytes, else
  `invalid_wave`) so a malformed record cannot silently disable a leg of
  the three-way check; absent `--registry` the wave record's own
  `registry.path` is the default join under the artifact-path gate
  (root-relative, beneath the project root — `invalid_wave` /
  `EXEC_PATH_OUTSIDE_ROOT`); `reportDir` resolves registry-file-copy
  first then the wave record's `registry.reportDir`, both through the
  same trust gate (relative, segment-clean, beneath root, no symlink —
  untrusted degrades to "no reportDir", never a failure); `reportPresent`
  surfaces only under a trusted reportDir via an `lstat` regular-file
  check; the registry is the sole authority for the judgment binding on
  the emitted entry.
- supersedes: none (gap closure — the section named "collect" twice but
  never the collector, its join contract, or the seam mechanics)
- rationale: the normative layer lagged shipped collector behavior; a
  lane reading §4.3 could not discover how settled outcomes join back
  onto the dispatch record, what identity evidence wins, or that a resume
  re-point surfaces on the payload — the seam the dissection-quality
  mission goal depends on for resume attribution. Same under-description
  class the 2026-09-22 §4.3, §8.1, and §8.2 entries closed for the ramp,
  watch, receipt-mint, and judgment-binding carriers.
- evidence: `scripts/ufo-swarm-wave.mjs` `persistWaveRegistry`
  `handlesReset` (:1252-1258), payload emission (:1151);
  `scripts/ufo-swarm-collect.mjs` `resumeSends[].resume` shape check
  (:285-295), `waveRegistryDefaultPath` gate (:328-380), `registryMembers`
  authority + reportDir trust (:465-516), `trustedReportDir` (:521-531),
  `collectEntries` fail-closed join + three-way identity + `reportPresent`
  lstat (:592-680), reportDir fallback (:756-765)

## 2026-09-22 — run-logic §8.1 display-projection pipeline codification
- decision: §8.1 now names the observation trio and records the
  display-evidence contract the L0 surface serves:
  `scripts/ufo-mission-lifecycle.mjs` projects a wall-manifest and/or
  queue task row into the five-phase vocabulary `queued | working |
  suspended | completed | failed` (live wall supersedes stale queue
  suspension; queue `paused`/`blocked` → `suspended` carrying the
  blocker's `code`/`failureClass`; queue terminal beats a `stopped` wall;
  crossed identities and live-vs-terminal contradictions fail closed;
  `resumed` is an observed resume dispatch, `resumeHint` advisory only, no
  terminal-outcome override); `scripts/ufo-mission-activity.mjs` attaches
  sanitized bounded display text (C0/C1, ANSI/OSC, bidi stripped; tmux
  format tokens neutralized; activity ≤240 and label ≤280 code points;
  terminal phases render `finalNote`); `scripts/ufo-mission-observation.mjs`
  is the single reconciled snapshot the dispatcher persists to
  `.ufo/sighting/observations.json` (`activity`/`label` redacted, tmp +
  rename, unchanged-content skip, projection failure never blocks
  reconciliation) with `task.route` as live activity for `working`/`queued`;
  `ufo-sighting` reads the sidecar fail-open through `loadObservations`
  (symlink/size/identity/vocabulary guards) with `statusPhase` as the
  raw-status fallback. Display evidence only — the wall and dispatcher own
  every lifecycle mutation; no observation row drives routing or
  acceptance.
- supersedes: none (gap closure — the section documented the heal
  surfaces but never the projection the same surface serves; the trio had
  zero mentions in the corpus)
- rationale: the normative layer lagged shipped display behavior; a lane
  reading §8.1 could not discover the five-phase vocabulary, the
  precedence rules, the sidecar contract, or that the projection is
  display-only — the same under-description class the 2026-09-22 §4.3,
  §8.1, and §8.2 entries closed for the ramp, watch, receipt-mint,
  judgment-binding, and collect carriers.
- evidence: `scripts/ufo-mission-lifecycle.mjs` phase precedence +
  conflict refusals (:83-160), `resumed`/`resumeHint` (:162-170),
  `readBoundedJsonInput` (:186-262); `scripts/ufo-mission-activity.mjs`
  `sanitizeDisplayText` (:51-73), bounds (:16-19), `buildLabel` (:96-106);
  `scripts/ufo-mission-observation.mjs` `reconcileObservation` + live-route
  activity (:36-69); `scripts/fleet-dispatcher.mjs` projection call
  (:6265), `observationsPath`/`persistObservations` redaction + tmp/rename
  + cache skip (:6294-6358); `scripts/ufo-sighting.mjs` `loadObservations`
  guards (:1953-2000), `statusPhase` fallback (:4437-4444,
  :2006/:2015/:2906/:4478).

## 2026-09-22 — run-logic §8.1 stall-admission contract codification
- decision: §8.1 now names the monitor's `findStalled` admission contract
  the whip gate stands on — which queue rows can be STALLED at all, not
  just when a STALLED row is whipped. Admission is deliberately narrower
  than `settle` (detection, never acceptance): in scope
  (`--fleet`/`--match`), state `running`/`launching`, runId matching the
  dispatcher's `gq<hex16>` contract (malformed → DEAD via `diagnose`,
  never whipped), `resultPath` beneath the repo root, a parseable object
  receipt, `taskKey`/`runId` binding, and `reportSha256` equal to the
  current report bytes — prompt/config drift is more reason to inspect,
  never a skip reason, but a drifted or foreign receipt makes the row
  invisible to stall detection entirely. Liveness is the transcript mtime
  under `.ufo/sessions/<runId>/` (shared lstat-based `newestMtime`,
  `.jsonl`-filtered), not the row state; scan faults surface flagged
  `scanError` and are never whipped blind; future-dated mtimes surface as
  idle-unknown (`idleMinutes: null`); otherwise idle ≥
  `--stale-after-min` (default 10, finite > 0). The whip fires only on
  `decision === "continue"` (`whipSkipReason`: `terminal_*` /
  `no_continue`), skips log once per reason without starting the
  cooldown, and only a fired whip cools down.
- supersedes: none at writing (gap closure — the section documented the
  whip gate but never the admission contract beneath it); the
  foreign/drift-receipt "invisible to stall detection" clause was
  superseded by the 2026-09-22 stall-anomaly-flags entry below
  (`efee9fe4` — flags on the stall signal, not admission gates).
- rationale: the normative layer lagged shipped detection behavior; a
  lane reading §8.1 could not discover that a drifted or foreign receipt
  hides a dead-ended row from stall detection, that liveness is
  transcript mtime rather than row state, or that scan faults and
  future-dated mtimes surface flagged instead of silently reading as
  fresh — the same under-description class the 2026-09-22 §4.3, §8.1, and
  §8.2 entries closed for the ramp, watch, receipt-mint,
  judgment-binding, collect, and display-projection carriers.
- evidence: `scripts/ufo-l0-monitor.mjs` `findStalled` gates
  (:1029-1090), `transcriptScan`/`newestMtime` (:1010-1022), `diagnose`
  invalid_run_id (:450-470), `absPath` root gate (:382-395),
  `--stale-after-min` validation (:1184-1187); `scripts/ufo-l0-watch.mjs`
  `whipSkipReason` (:164-170), scanError skip + once-per-reason dedupe +
  cooldown ordering (:1140-1210).

## 2026-09-22 — run-logic §8.1 stall-anomaly flags + WHIP_DRIFT codification
- decision: §8.1 re-codified for the landed stall-detection
  evidence-honesty change (nc3-swarm r37, `efee9fe4`): the
  `taskKey`/`runId` binding and `reportSha256` legs are anomaly flags,
  not admission gates — a foreign receipt surfaces flagged
  `receiptMismatch` (`decision` nulled; its fields are untrusted), a
  stale or unreadable report digest surfaces flagged `reportDrift`
  (`mismatch` | `unreadable`; the digest is computed only for non-foreign
  receipts), and a future-dated transcript surfaces flagged
  `futureMtime`; the flags ride the stall signal (`scanError` or idle ≥
  `--stale-after-min`) rather than stalling a row by themselves. The
  watch walks each stalled row in order — malformed runId → `scanError`
  skip → foreign-receipt skip (deduped once per reason) → `reportDrift`
  `WHIP_DRIFT` steer bypassing the decision gate (re-mint the receipt
  against current report bytes, then `ufo-sighting complete`; a terminal
  decision needs the same re-mint) → `whipSkipReason` decision gate →
  cooldown → steer — and `steer()` now returns `{ok,fault}` so a failed
  whip carries its child fault on the action line. The STALLED display
  carries the anomaly tags (`foreign-receipt` / `drift:<kind>` /
  `future-mtime` / `scan:<err>`). AGENTS.md's L0-duty bullets were
  amended the same round.
- supersedes: the 2026-09-22 stall-admission entry's invisibility claim
  ("a drifted or foreign receipt makes the row invisible to stall
  detection entirely") and its "whip fires only on `continue`" gate —
  both accurate when written, falsified by `efee9fe4`
- rationale: the normative layer documented pre-change semantics; the
  landed code made drifted and foreign receipts visible flagged rows and
  added a decision-blind evidence-repair steer — a lane reading the old
  text would believe a dead-ended row rides invisible until acceptance
  marks it missing and that no whip can fire on a terminal decision.
- evidence: `scripts/ufo-l0-monitor.mjs` `findStalled` flags + export
  (:1035-1103), STALLED display anomaly tags (:1299-1317);
  `scripts/ufo-l0-watch.mjs` `WHIP_DRIFT` (:158-165), stall-loop ordering
  (:1150-1216), `steer` `{ok,fault}` (:759-770), `whipSkipReason`
  (:172-178).

## 2026-09-22 — prior-evidence heal contract codified
- decision: run-logic §8.1's repair duty now documents the
  `prior_evidence_drift` heal as a two-legged contract — the bound
  digest lives in the PARENT's receipt, so the heal rewrites the
  terminal parent's receipt `promptSha256`/`configSha256` to the
  child's current bytes (refusing `no_parent`, `parent_not_terminal`,
  `parent_child_paths_diverge`, `no_parent_receipt`,
  `parent_receipt_invalid`, `digest_unreadable`), then rebinds the
  row's `priorReceiptSha256` AND every non-terminal sibling sharing
  that parent receipt path in the same locked pass (`reboundSiblings`
  attribution; terminal siblings keep their checked digest). The
  prompt/config-drift leg refreshes `priorReceiptSha256` when the
  parent receipt is readable; the live leg (`live_digest_drift` on
  non-blocked rows, healed by `--rebind`) is codified; the rebound
  digest is computed over the `validateTaskReceipt`-normalized object
  (dispatcher parity). AGENTS.md's L0-duty bullet amended the same
  round.
- supersedes: §8.1's single-row "rebind the row's digests to the
  CURRENT bytes" — accurate for prompt/config drift, silently wrong
  for prior-evidence drift (the mechanism predates the nc3 chain;
  the sibling-cohort rebind landed as `a2a4c8ef`, nc3-swarm r55)
- rationale: a lane reading the old text would believe the monitor
  only re-points a row's own digests — it would not expect the heal
  to mutate a terminal parent's receipt, refuse on live/divergent/
  missing parents, or fan the rebind out to a sibling cohort; one
  parent-receipt rewrite without the cohort rebind manufactures N
  serial `prior_evidence_drift` blocks.
- evidence: `scripts/ufo-l0-monitor.mjs` `repair()` prior-evidence
  branch + refusal taxonomy (:631-708), sibling-rebind loop
  (:677-700), prompt/config leg prior-binding refresh (:715-724),
  `rebind()` prior leg (:932-948), `diagnose()` live prior-evidence
  leg (:558-600); `scripts/fleet-dispatcher.mjs` prior-evidence
  re-verification at dispatch (:4463-4489), successor binding
  (:4574-4664).

## 2026-09-22 — drift-kind steer selection codified
- decision: run-logic §8.1 and AGENTS.md's L0-duty bullets now document
  the watch's drift steer as kind-selected, not a single text: the
  monitor's `reportDrift` flag is a typed kind (`mismatch`, or
  `unreadable` when the report cannot be read), and the watch's
  `driftWhipText(kind)` selects `WHIP_DRIFT_UNREADABLE` for
  `unreadable` (restore a readable report at the lane-owned result
  path first — the generic re-mint is unfulfillable because
  create-receipt throws `unreadable_input` on a missing report — then
  re-mint, then complete) and `WHIP_DRIFT` for every other kind
  (`mismatch` today, any future kind — the safer default when bytes
  exist to hash). Both arms stay decision-blind (a terminal decision
  needs the same re-mint to settle); the action line carries the kind
  (`whip_drift:<kind> ok|failed`); `driftWhipText` is exported for the
  owned probe suite alongside `whipSkipReason`.
- supersedes: §8.1's "the decision-blind `WHIP_DRIFT` re-mint steer"
  as the single drift text — accurate for `mismatch`, silently wrong
  for `unreadable` (a lane whipped into a re-mint that cannot succeed
  would be re-whipped every cooldown).
- rationale: the unreadable dead-end needs restore-then-remint, not
  remint; codifying the kind selection keeps the steer honest for the
  failure mode the flag was typed to distinguish.
- evidence: `scripts/ufo-l0-watch.mjs` `WHIP_DRIFT_UNREADABLE` +
  `driftWhipText` (:166-184), tick selection + `whip_drift:<kind>`
  action line (:1199-1237); `scripts/ufo-l0-monitor.mjs` `reportDrift`
  typing (:1085-1096).

## 2026-09-22 — monitor single-lock heal, watch tick isolation + bounded logs, collect emit taxonomy codified
- decision: run-logic §8.1 now documents the monitor heal pass's atomicity
  contract — one queue-lock acquisition and one bounded queue read for
  `--rebind`/`--settle`/`--repair` executed sequentially inside
  `withQueueLock`, repair re-diagnosing under the lock (the pre-lock
  findings snapshot can be stale — TOCTOU), per-step `writeQueue`
  preserved so a mid-pass fault leaves earlier steps durable, and
  `repend` outside the lock (it spawns the dispatcher — non-reentrant);
  the watch daemon's per-tick fault isolation (`tick_error` to the action
  log, cadence preserved; `--once` unguarded) and both surfaces' bounded
  action logs (1 MiB + one `.1` generation, O_NOFOLLOW|O_NONBLOCK
  appends, whitespace-collapsed lines, `log_rotated` /
  `log_rotate_failed code=<errno>` inline); and §4.3 now documents
  collect's emit-path taxonomy — `--out -` is stdout, errno-coded fs
  faults on `--out` (`ENOENT`/`ENOTDIR`/`ELOOP`/`EACCES`/`EPERM`/`EISDIR`)
  surface `invalid_out`, resource faults stay internal, and typed
  `MissionResultError`s (`invalid_xml_text` on a lone-surrogate body)
  wrap as `invalid_envelope`. AGENTS.md's L0-duty bullets carry the
  single-lock heal and tick-isolation/bounded-log lines in parallel.
- supersedes: §8.1's heal-duty list (which named the lock as the safe
  mutation point but never the single-acquisition pass shape or the
  in-lock re-diagnosis), the carrier paragraph's silence on daemon
  resilience and log bounds, and §4.3's join-only collect contract.
- rationale: the same under-description class as the 2026-09-22 §4.3,
  §8.1, and §8.2 codifications — normative text lagged shipped mechanism;
  a reader could not discover the atomicity, resilience, or error
  taxonomy contracts from the normative layer.
- evidence: `scripts/ufo-l0-monitor.mjs` single-lock heal pass
  (:1249-1286), `appendLog` bound (:786-835); `scripts/ufo-l0-watch.mjs`
  tick fault isolation (:1744-1759), `log()` bound (:385-445);
  `scripts/ufo-swarm-collect.mjs` emit-path wraps (:777-817).

## 2026-09-22 — monitor artifact_unreadable live-row finding class codified
- decision: run-logic §8.1's live-drift paragraph now documents the
  `artifact_unreadable` finding class alongside `live_digest_drift`: a
  live row whose prompt/config/prior-receipt artifact cannot be digested
  at all (path escapes root, file missing, or read failing under the
  bounded digest) is named `artifact_unreadable` and never repaired —
  a missing artifact is at least as dead-ended as an unreadable one
  because the row fails its next dispatch. All four cannot-digest
  branches share one shape: live rows are named; blocked rows keep
  their blocker code and gain `repairable=false` plus the reason (the
  missing-file arms previously skipped blocked non-drift rows
  entirely). AGENTS.md's L0-duty monitor bullet carries the class in
  parallel.
- supersedes: §8.1's live-drift paragraph naming only
  `live_digest_drift` — the unreadable-artifact arm was codified
  earlier, but the missing-file and escapes-root arms produced no
  finding on live rows until nc3-swarm r57 (`9de5e861`).
- rationale: same codification-lag class as the day's §8.1 entries —
  normative text lagged shipped mechanism; a reader could not discover
  the dead-end naming contract from the normative layer.
- evidence: `scripts/ufo-l0-monitor.mjs` `diagnose()` cannot-digest
  branches (:486-621); sibling commit `9de5e861` (nc3-swarm r57).

## 2026-09-22 — monitor settle() admission + finish() parity, watch respawn outcome taxonomy codified; godspeed-core README judge-load-path repair
- decision: three normative repairs. (a) run-logic §8.1 gains the `--settle`
  arm's contract — it completes only rows blocked on
  `acceptance_evidence_missing` whose on-disk receipt satisfies the
  dispatcher's expected bag (taskKey/runId/sessionId/promptSha256/
  configSha256/reportSha256, either-binding prompt digest: stored first,
  then the dispatch-snapshot sidecar), and records `iterationOutcome` in
  dispatcher `finish()` shape — `reason` through the verbatim
  `redact`/`CREDENTIAL_SHAPE` copy, `nativeVerdict`/`blockedAudit`
  passthrough — so a monitor-settled row is indistinguishable from a
  dispatcher-settled one (nc3-swarm r58 `84b0f77f`; AGENTS.md bullet
  carries it in parallel). (b) `ssot/godspeed-core/README.md` +
  `skills/godspeed-core/README.md` (byte-identical pair): the
  judge-load-path paragraph named `ssot/godspeed-core/` then called
  "copies sitting beside this README" undeclared origin documents —
  self-contradictory in the ssot copy — and omitted the operative path
  `~/.agents/godspeed-core/` that `fleet-dispatcher.mjs` mints into fleet
  prompts. Rewritten location-neutrally: authored halves at `ssot/` +
  declared bundled mirror, operative host path named, vendored copies
  declared upstream-pinned non-mirrors, and the consequence stated —
  vendored `filter.md` retains phrasing the ssot bridge note marks
  self-contradictory vs `gate.rs` (admit iff ≥1 axis improves and none
  regress). (c) §8.1's respawn paragraph gains the action-line outcome
  taxonomy (nc3-swarm r59 `72a34cac`): `enqueued`/`deduped` arm the
  deferred seal; `respawn_failed` is a dispatcher refusal (usageError);
  `respawn_unparseable`/`respawn_invalid_payload` are exit-0 dispatcher
  contract violations — the report shape is the suspect, never the spec;
  `budget_lane`/`budget_global` are the hourly caps;
  `respawn_skipped_*` are the skip arms; outcomes dedupe per lane via
  `lastRespawnResult`. AGENTS.md's watch bullet carries the taxonomy.
- supersedes: §8.1's heal-pass description naming `--settle` only as a
  lock participant and its respawn paragraph silent on outcome names; the
  README's relative "copies beside this README" reference.
- rationale: same codification-lag class — normative text lagged shipped
  mechanism (settle parity, respawn outcome names) and the dispatch
  binding (operative judge path); a reader could not discover any of the
  three contracts from the normative layer.
- evidence: `scripts/ufo-l0-monitor.mjs` `settle()` (:1044-1103),
  `redact`/`CREDENTIAL_SHAPE` local copies (:60-89);
  `scripts/ufo-l0-watch.mjs` `enqueue()` outcome arms (:744-783) and
  respawn note taxonomy (:1095-1160); sibling commits `84b0f77f`,
  `72a34cac`; `scripts/fleet-dispatcher.mjs` minted-prompt path (:4542);
  `crates/ufo-core-runtime/src/gate.rs` Pareto admission (:38).

## 2026-09-22 — run-logic §4.3 registry-lock contract codification
- decision: §4.3 now records the `withRegistryLock` fence (nc3-swarm r60
  `979f90eb`): both registry writers (`persistWaveRegistry` at `run`,
  `mainRecord` at `record`) serialize their load→mutate→write under
  `<registry>.lock` — mkdir claim, `owner.json` pid+token binding
  (O_EXCL/O_NOFOLLOW, 0o600, fsync'd), fenced stale break (dead-pid, or
  unreadable-owner past a 30s freshness grace; future-dated mtime still
  attempts the break) via quarantine rename + seized-token restore,
  token-checked release, 30s acquire deadline, unsafe-path refusal.
  Read-only loads stay lock-free; `record` on a missing registry still
  fails `invalid_registry` (parent dir created before the claim).
- supersedes: none (gap closure — the section named the registry as the
  resume-ownership authority and its write mechanics but never the
  cross-process fence that makes concurrent writers safe).
- rationale: same codification-lag class — normative text lagged shipped
  mechanism; a reader could not discover from §4.3 that two concurrent
  registry writers are fenced by `withRegistryLock` rather than racing
  the load→mutate→write.
- evidence: `scripts/ufo-swarm-wave.mjs` `withRegistryLock` (:753-805),
  `breakStaleRegistryLock` (:675-727), `writeRegistryLockOwner`
  (:730-750), `persistWaveRegistry` wrap (:1407), `mainRecord` wrap
  (:1484); sibling commit `979f90eb`.

## 2026-09-22 — run-logic §8.1 canonical durability-leaf codification
- decision: §8.1 now names `scripts/ufo-mission-result.mjs` as the
  fleet's single canonical leaf for bounded-read and atomic-publish
  primitives (nc3-swarm r61 `5048f4ed`): `readBoundedFd` (fstat pin,
  stat-size + 1 slack, mid-read-grow `changed`, EAGAIN retry on
  non-regular fds only, post-read fstat), `readBoundedFile`
  (`O_NOFOLLOW|O_NONBLOCK`, `not_regular`), `readBoundedStdin`
  (`read_error` wrap), `writeFileAtomic` (random `pid+UUID` O_EXCL tmp
  0o600, fsync-before-rename, directory fsync, unlink-on-error, no
  parent mkdir). Callers supply `fail(message, kind)` so every typed
  error contract survives byte-identically; kinds are `too_large` |
  `not_regular` | `changed` | `read_error`. `readBoundedJsonInput` is
  recorded as a thin adapter, not a second implementation.
- supersedes: §8.1's pre-consolidation silence — the paragraph named
  `readBoundedJsonInput` as the shared bounded reader while seven
  near-identical private copies and ~6 atomic-write bodies still
  existed across the owned surface; the consolidation collapsed them
  (-214 net lines, 3 new import edges, acyclic) and the normative
  layer never named the leaf.
- rationale: same codification-lag class as the registry-lock entry —
  normative text lagged shipped mechanism; a reader could not discover
  from §8.1 where the canonical bounded-read/atomic-write contract
  lives or that private copies are prohibited.
- evidence: `scripts/ufo-mission-result.mjs` `readBoundedFd` (:631),
  `readBoundedFile` (:687), `readBoundedStdin` (:703),
  `writeFileAtomic` (:718); import edges at
  `ufo-mission-lifecycle.mjs:6`, `ufo-l0-monitor.mjs:37`,
  `ufo-l0-watch.mjs:60`, `ufo-stale-watchdog.mjs:55`,
  `ufo-swarm-collect.mjs:52`, `ufo-swarm-wave.mjs:86`,
  `fleet-dispatcher.mjs:29`; `readBoundedJsonInput` delegation at
  `ufo-mission-lifecycle.mjs:204,215,221`; sibling commit `5048f4ed`.

## 2026-09-22 — run-logic §8.1 canonical-leaf extension: lock protocols
- decision: §8.1's canonical-leaf paragraph now also names the shared
  lock machinery consolidated into `scripts/ufo-mission-result.mjs`
  (nc3-swarm r62 `836d9dcb`): `withDirLock` (mkdir-claimed dir mutex,
  dispatcher/monitor queue-lock parity — pid+token `owner.json`
  O_EXCL/O_NOFOLLOW 0o600 fsync'd, fenced quarantine break on dead-pid
  or unreadable-owner past the 30s freshness grace, proven-string token
  compare, token-checked release, 30s acquire bound, symlink/non-dir
  refusal; callers keep token/messages/readOwner — monitor keeps
  `assertQueueParent`, wave keeps `invalid_registry` owner reads) and
  `acquireSingletonLock` (`.takeover` ticket, inode-bound owner links
  with pid/starttime/bootId, owner states
  dead/stale/live/foreign_live, `foreign_live` quarantined `.bad.*`,
  8-attempt bound) shared by `ufo-l0-watch` + `ufo-stale-watchdog`;
  `pidIsAlive` + proc-identity helpers deduped from five byte-identical
  copies. Dispatcher queue lock and `ufo-sighting` `operation.lock`
  keep private bodies — the dispatcher copy is the parity source.
- supersedes: §8.1's post-r64 scope — the paragraph named only
  bounded-read/atomic-publish primitives while ~380 lines of
  near-verbatim lock machinery still lived in four scripts; the
  consolidation collapsed them (-386 net lines) and the normative
  layer did not name the lock home.
- rationale: same codification-lag class as the durability-leaf entry —
  a reader could not discover from §8.1 that the dir-lock and
  singleton-lock protocols are single-sourced or which callers keep
  private bodies.
- evidence: `scripts/ufo-mission-result.mjs` `acquireSingletonLock`
  (:865), `withDirLock` (:1123), `pidIsAlive` (:743); import edges at
  `ufo-l0-monitor.mjs:37`, `ufo-l0-watch.mjs:53`,
  `ufo-stale-watchdog.mjs:48`, `ufo-swarm-wave.mjs:86`; private copies
  at `fleet-dispatcher.mjs:4122+`, `ufo-sighting.mjs:2229+`; sibling
  commit `836d9dcb`.

## 2026-09-22 — run-logic §8.1 canonical-leaf extension: log + state-publish primitives
- decision: §8.1 gains a third canonical-leaf paragraph codifying
  `appendRotatingLog` (O_NOFOLLOW|O_NONBLOCK|O_APPEND open at 0o600,
  one-generation `.1` rename at `maxBytes`, soft-bound fallback writing
  `rotateFailedLine` to the still-open old fd on rename failure, inline
  `rotatedLine` on the fresh fd — non-reentrant) and
  `writeFileAtomicIfChanged` (bounded compare-read + `Buffer.equals`
  skip → `writeFileAtomic` publish; invalid-UTF-8 never aliases onto
  U+FFFD) — shared by `ufo-l0-watch` (LOG/STATE), `ufo-stale-watchdog`
  (telemetry/state), and `ufo-l0-monitor` (`appendLog`); callers keep
  stamped bodies and rotation-line contracts.
- supersedes: §8.1's post-r67 scope — the leaf paragraphs named
  bounded-read/atomic-publish and lock protocols while ~200 lines of
  near-verbatim rotate-on-size and quiet-tick-skip machinery still
  lived in three scripts; the consolidation collapsed them and the
  normative layer did not name the new primitives.
- rationale: same codification-lag class as the durability-leaf and
  lock-protocol entries — a reader could not discover from §8.1 that
  log rotation and quiet-tick publish are single-sourced or which
  contracts stay caller-owned.
- evidence: `scripts/ufo-mission-result.mjs` `appendRotatingLog`,
  `writeFileAtomicIfChanged`; import edges at `ufo-l0-watch.mjs:51-52`,
  `ufo-stale-watchdog.mjs:46-47`, `ufo-l0-monitor.mjs:37`; callsites
  `ufo-l0-watch.mjs:344/:375`, `ufo-stale-watchdog.mjs:158/:431`,
  `ufo-l0-monitor.mjs:683`; sibling commit `8f098cc8`.

## 2026-09-22 — run-logic §8.1 canonical-leaf extension: path-containment + credential gates
- decision: §8.1 gains a fourth canonical-leaf paragraph codifying
  `beneath` (S-04: realpath-anchored root with ENOENT-only
  `resolve(root)` fallback, `..`/absolute escape rejection,
  per-component symlink refusal with ENOENT skip), `CREDENTIAL_SHAPE` +
  `redact` (S-06: key=value credential keys incl. cookie/set-cookie,
  bearer/basic blobs, provider key prefixes, AWS AKIA/ASIA ids, JWTs,
  PEM blocks → typed `[REDACTED_*]` placeholders), and `optionValue`
  (wave-family argv reader: duplicate flag and missing/`--`-leading
  value → caller's typed `fail()`) — `beneath`/`CREDENTIAL_SHAPE`/
  `redact` shared by `ufo-swarm-wave`, `ufo-swarm-collect`,
  `ufo-l0-watch`, `ufo-l0-monitor`, and `ufo-stale-watchdog`;
  `optionValue` was codified with zero importers (collect moved to
  `parseDeclaredArgv` one round later — §8.1 names it a parity leaf
  with no consumers); the dispatcher's copies stay its own parity
  source (importing it remains forbidden).
- supersedes: §8.1's post-r69 scope — the leaf paragraphs named
  durability, lock, and log/state primitives while ~240 lines of
  byte-identical containment/redaction/argv machinery still lived in
  five scripts; the consolidation collapsed them (-97 net lines) and
  the normative layer did not name the new gates. The adopter roster in
  the decision above is superseded by the current §8.1 text
  (run-logic.md:1576-1584): `beneath` adopters are wave/collect/watch/
  monitor while the `CREDENTIAL_SHAPE`/`redact` pair is monitor +
  watchdog only — collect/watch no longer ride the S-06 trio.
- rationale: same codification-lag class as the prior leaf entries —
  and the drift class was realized, not hypothetical: the stale
  watchdog's private `redact` lacked the AWS AKIA/ASIA line the
  dispatcher canonical carries, so its telemetry could persist a key
  the monitor redacts.
- evidence: `scripts/ufo-mission-result.mjs` `beneath` (:749),
  `CREDENTIAL_SHAPE` (:777), `redact` (:780), `optionValue` (:1435);
  import edges at `ufo-swarm-wave.mjs:86`, `ufo-swarm-collect.mjs:52`,
  `ufo-l0-monitor.mjs:37`, `ufo-stale-watchdog.mjs:44`; dispatcher
  parity copies at `fleet-dispatcher.mjs:213` (CREDENTIAL_SHAPE),
  `:336` (redact), `:435` (beneath); sibling commit `b0173d15`.

## 2026-09-22 — run-logic §8.1 canonical-leaf extension: queue-row trust-boundary primitives
- decision: §8.1 gains a fifth canonical-leaf paragraph codifying
  `MAX_QUEUE_BYTES` (shared 4 MiB bound, dispatcher parity — acceptance
  reads report/receipt under the same bound), `ALLOW_EXTERNAL_TOOLS`
  (S-04 escape flag bound at module load), `isQueueRunId`
  (dispatcher-minted `gq<16 hex>` contract; strict pattern makes the
  inherited-name probe redundant), `containedJoin` (root join through
  `beneath` + escape flag, null-returning), `statSignature` (lstat-based
  memo key — mtimeNs/ctimeNs/size/ino; null = absent/unreadable),
  `readQueueFile` (bounded read + `tasks` array-of-objects shape
  validation through the caller's typed `fail()`), and
  `dispatchSnapshotPromptPath` (relative snapshot layout, caller-gated
  through `containedJoin`) — shared by `ufo-l0-monitor`, `ufo-l0-watch`,
  `ufo-swarm-wave`, and `ufo-swarm-collect`; the stale watchdog's
  `isSafeRunId` stays deliberately broader, and the dispatcher's copies
  stay its own parity source (importing it remains forbidden).
- supersedes: §8.1's post-r70 scope — the leaf paragraphs named
  durability, lock, log/state, and containment/credential primitives
  while ~120 lines of byte-identical queue-row gating still lived in
  the monitor and watch; the consolidation collapsed them and the
  normative layer did not name the new primitives.
- rationale: same codification-lag class as the prior leaf entries —
  a reader could not discover from §8.1 that queue-row path fields,
  runId shape, and the snapshot prompt layout are single-sourced or
  which contracts stay caller-owned.
- evidence: `scripts/ufo-mission-result.mjs` `MAX_QUEUE_BYTES` (:1460),
  `ALLOW_EXTERNAL_TOOLS` (:1465), `isQueueRunId` (:1474),
  `containedJoin` (:1488), `statSignature` (:1512), `readQueueFile`
  (:1531), `dispatchSnapshotPromptPath` (:1551); import edges at
  `ufo-l0-monitor.mjs:37`, `ufo-l0-watch.mjs:52-59`,
  `ufo-swarm-wave.mjs:86`, `ufo-swarm-collect.mjs:52`; dispatcher
  parity copies at `fleet-dispatcher.mjs:100` (MAX_QUEUE_BYTES),
  `:236` (QUEUE_RUN_ID_PATTERN), `:7196/:7342` (snapshot layout);
  stale-watchdog broader `isSafeRunId` at `ufo-stale-watchdog.mjs:101/:108`;
  sibling commit `d0dd958a`.

## 2026-09-22 — run-logic §8.1 leaf-paragraph convention + sixth family
- decision: §8.1 gains a convention paragraph naming the codification
  rule itself — one leaf paragraph per consolidation family, appended in
  landing order; each names the primitives and their callers, the
  contracts callers keep, the consolidating commit, and the dispatcher
  parity source where one exists; codification waits for the
  consolidating commit to land (staged-but-uncommitted consolidation is
  not named); a dated CHANGELOG entry and regenerated mirrors ride every
  codification; the dispatcher's own copies stay its own parity source
  and importing it remains forbidden. §8.1 also gains a sixth
  canonical-leaf paragraph codifying `writeWithMkdirRetry`
  (ENOENT-mkdir retry for fixed-path writes — one retry after
  recreating the parent, non-ENOENT faults propagate or drop under
  `swallow`) and `appendStampedLog` (whitespace-collapsed ISO-stamped
  lines through `appendRotatingLog` under the retry) — shared by the
  monitor's `appendLog`/`writeState` and the watch's `log`/`writeState`;
  `swallow` selects the doctrine (monitor propagates; watch swallows
  log faults but propagates state-write faults to the tick-level catch
  that logs `tick_error` and keeps cadence). The stale watchdog keeps
  its own `appendRotatingLog` telemetry path and the shell night
  watchdog's `say` stays a printf append outside the leaf.
- supersedes: §8.1's post-r72 scope — the leaf paragraphs named five
  families while the convention that produced them lived only in round
  reports (a fresh session re-derived the trigger rule each round), and
  ~78 lines of byte-identical mkdir-retry/stamped-log bodies still
  lived in the monitor and watch until `f9d67284` collapsed them.
- rationale: same codification-lag class as the prior leaf entries —
  plus a self-iteration gap: the trigger rule (codify on the
  consolidating commit, never on WIP) was carried in reports, not in
  the normative layer it maintains.
- evidence: `scripts/ufo-mission-result.mjs` `writeWithMkdirRetry`
  (:1411), `appendStampedLog` (:1450); import edges at
  `ufo-l0-monitor.mjs:37`, `ufo-l0-watch.mjs:50-51`; caller doctrines
  at `ufo-l0-monitor.mjs:590` (propagate), `:601` (state propagate),
  `ufo-l0-watch.mjs:353` (state propagate → tick catch :1299),
  `:370` (log swallow); stale-watchdog telemetry at
  `ufo-stale-watchdog.mjs:130`; shell watchdog `say` at
  `ufo-night-watchdog.sh:51`; sibling commit `f9d67284`.

## 2026-09-22 — tracked mirror set named in the §8.1 convention
- decision: the convention paragraph now names the committable mirror
  set — every `skillTargets` copy in `scripts/sync-ufo-contracts.mjs`
  except the two gitignored `.devin/` projections — and calls out
  `.omp/skills/ufo` as tracked; a regeneration left unstaged is
  gate-invisible because the sync gate checks the working tree, so the
  codification commit must stage the whole set.
- supersedes: the same-day convention text, which said "regenerated
  mirrors ride every codification" without enumerating the set — the
  r73 codification commit staged 10 of 11 tracked copies and dropped
  `.omp/skills/ufo` (regenerated, byte-identical, never committed).
- rationale: the convention is executed by a fresh session each round;
  an unenumerated set is re-derived per round and one member outside
  `skills/`/`.cursor/`/`packages/` was silently missed.
- evidence: `skillTargets` at `scripts/sync-ufo-contracts.mjs:89-102`
  (13 copies; `project-omp` → `.omp/skills/ufo` tracked; `project-devin`
  and `devin-native` → gitignored `.devin/` projections); r73 commit
  `077c1f1f` file set (23 files, no `.omp/skills`); `.devin/` ignore
  rule (`git check-ignore`).

## 2026-09-22 — run-logic §8.1 canonical-leaf extension: bounded artifact digest
- decision: §8.1 gains a seventh canonical-leaf paragraph codifying
  `sha256File` — `createHash("sha256")` over `readBoundedFile(path,
  maximum, label)`, the bounded artifact digest the monitor and watch
  each carried privately. The monitor keeps its `statSignature`-memoized
  wrapper (aliased import; memo key `maximum:signature`; null signature
  → unmemoized; failures never memoized so per-row fault isolation
  holds). The watch calls the primitive directly — bound and label are
  caller arguments, so the watch/monitor prompt-bound divergence is now
  visible per call site (watch `MAX_QUEUE_BYTES` vs monitor
  `MAX_PROMPT_BYTES` on snapshot prompts) rather than buried in two
  private copies. The dispatcher's inline `digest(readBoundedFile(...))`
  compositions stay its own parity source; importing it remains
  forbidden.
- supersedes: §8.1's post-r74 scope — the leaf paragraphs named six
  families while the watch still carried a verbatim `createHash` copy
  of the monitor's digest and the monitor carried the digest line
  inline, until `f3a078b2` collapsed them.
- rationale: same codification-lag class as the prior leaf entries —
  the normative layer names each consolidation family as its commit
  lands so a fresh session never re-derives which primitives are
  canonical.
- evidence: `scripts/ufo-mission-result.mjs` `sha256File` (:1603);
  import edges at `ufo-l0-monitor.mjs:37` (aliased `sharedSha256File`),
  `ufo-l0-watch.mjs:59`; monitor memoized wrapper at
  `ufo-l0-monitor.mjs:99-113`; watch call sites at
  `ufo-l0-watch.mjs:579` (`snapshotPromptSha256`, label "snapshot
  prompt"), `:895` (respawn report digest); dispatcher parity
  compositions at `fleet-dispatcher.mjs:5500`, `:5606`; sibling commit
  `f3a078b2`.

## 2026-09-22 — run-logic §8.1 canonical-leaf extension: direct-entry guard
- decision: §8.1 gains an eighth canonical-leaf paragraph codifying
  `isMainModule(moduleUrl)` — the direct-entry guard eight CLIs carried
  as verbatim watchdog-guard copies (monitor, L0 watch, the three
  mission-* projection CLIs, stale watchdog, swarm-collect, wave
  planner; the leaf guards its own CLI too). The contract: an
  `execArgv` screen refuses `-e`/`-p`/`--eval`/`--print` entrypoints
  (an eval-import puts the module path in argv[1] and would run the
  whole CLI), a missing argv[1] is not a direct invocation, and the
  comparison realpaths BOTH sides with any fault fail-closed to false.
  The lift realized and fixed a drift class: the old copies realpathed
  only argv[1], so under `--preserve-symlinks` an intentional symlinked
  launch silently refused to run. The paragraph also names the
  non-adopter census as visible-per-call-site divergence: the
  dispatcher keeps its own guard (no execArgv screen — parity source,
  importing forbidden); `ufo-sighting`, `sync-global-routing`, and
  `fleet-ledger-rotate` compare without realpathing argv[1] (symlinked
  launch exits 0); `run-omp-native-trial`, `the-tick-ping`, and
  `ufo-ground-handler` realpath only argv[1] (the refusal class);
  `prepare-ephemeral-l1` realpaths argv[1] against a load-time
  fileURLToPath'd MODULE_PATH (leaf-equivalent under default
  resolution, minus the execArgv screen).
- supersedes: §8.1's post-r75 scope — the leaf paragraphs named seven
  families while eight CLIs still carried verbatim watchdog-guard
  copies, until `02897376` collapsed them.
- rationale: same codification-lag class as the prior leaf entries —
  the normative layer names each consolidation family as its commit
  lands so a fresh session never re-derives which primitives are
  canonical; the non-adopter census records the remaining guard
  variants so the divergence is surveyed, not rediscovered per round.
- evidence: `scripts/ufo-mission-result.mjs` `isMainModule` (:1654);
  call sites at `ufo-l0-monitor.mjs:879`, `ufo-l0-watch.mjs:1140`,
  `ufo-mission-activity.mjs:200`, `ufo-mission-lifecycle.mjs:237`,
  `ufo-mission-observation.mjs:79`, `ufo-stale-watchdog.mjs:885`,
  `ufo-swarm-collect.mjs:730`, `ufo-swarm-wave.mjs:1402`,
  `ufo-mission-result.mjs:1816`; non-adopters at
  `fleet-dispatcher.mjs:8379`, `ufo-sighting.mjs:6633`,
  `sync-global-routing.mjs:294`, `fleet-ledger-rotate.mjs:1036`,
  `run-omp-native-trial.mjs:4244`, `the-tick-ping.mjs:703`,
  `ufo-ground-handler.mjs:755`, `prepare-ephemeral-l1.mjs:872`;
  sibling commit `02897376`.

## 2026-09-22 — run-logic §8.1 canonical-leaf extension: snapshot-prompt digest
- decision: §8.1 gains a ninth canonical-leaf paragraph codifying
  `snapshotPromptSha256(root, runId, attempt, digest = sha256File)` —
  the receipt-validation fallback both L0 daemons carried verbatim
  (monitor, watch). A receipt may bind the snapshot prompt bytes the
  lane received (skill lines + binding overlay) instead of the drifting
  source file; the dispatcher accepts either digest via the
  `dispatch_snapshot` bindingSource. The contract: the queue-row runId
  is gated through `containedJoin` like every other row path field, any
  digest fault returns null rather than throwing out of the settle
  pass, and the bound is `MAX_QUEUE_BYTES` — the dispatcher's own
  snapshot bound. The lift realized and fixed a drift class: the
  monitor's private copy digested under `MAX_PROMPT_BYTES`, which would
  have false-nulled the fallback on a >512 KiB snapshot the dispatcher
  accepts. The optional `digest` parameter keeps per-pass memoization
  caller-owned (monitor passes its `statSignature`-memoized wrapper;
  watch calls the primitive directly). The paragraph also names the
  set-vs-single divergence now visible per call site: the dispatcher's
  `dispatchSnapshotPromptSha256` accepts a receipt bound to ANY
  attempt's snapshot (presence-based set over every
  `dispatch-snapshot-*` dir, superseded renames included) while the
  daemon fallbacks validate only the row's current attempt. The
  seventh-paragraph bound-divergence sentence was amended in the same
  pass — the monitor no longer digests snapshot prompts under
  `MAX_PROMPT_BYTES`.
- supersedes: §8.1's post-r76 scope — the leaf paragraphs named eight
  families while both daemons still carried verbatim snapshot-digest
  copies, until `da2b38d2` collapsed them.
- rationale: same codification-lag class as the prior leaf entries —
  the normative layer names each consolidation family as its commit
  lands so a fresh session never re-derives which primitives are
  canonical; the bound-drift fix is recorded so the >512 KiB
  false-null class is surveyed, not rediscovered per round.
- evidence: `scripts/ufo-mission-result.mjs` `snapshotPromptSha256`
  (:1663); call sites at `ufo-l0-monitor.mjs:696` (memoized wrapper)
  and `ufo-l0-watch.mjs:577` (direct); dispatcher parity source at
  `fleet-dispatcher.mjs:5517` (`dispatchSnapshotPromptSha256` over
  `dispatchSnapshotDigests` :5488, membership accepted at :5652);
  sibling commit `da2b38d2`.

## 2026-09-22 — run-logic §8.1 canonical-leaf extension: plain-object predicate
- decision: §8.1 gains a tenth canonical-leaf paragraph codifying
  `isPlainObject(value)` — the non-throwing shape half of the leaf's
  `plainObject` guard (`value !== null && typeof value === "object" &&
  !Array.isArray(value)`), shared so every artifact/state/report
  boundary names the same check. The predicate inspects no prototype —
  a class instance or null-prototype object passes — so it answers
  "record-shaped", never "literal `{}`"; callers needing the stricter
  contract keep their own check. The lift collapsed four verbatim
  private bodies (`ufo-mission-activity`, stale watchdog,
  swarm-collect, wave planner) plus a dozen inline expansions (monitor,
  L0 watch, `ufo-mission-lifecycle`, `ufo-mission-observation`, and the
  leaf's own queue-shape/JSON-input checks). The collapsed spellings
  were semantically identical but textually divergent — null-first,
  falsy-first, and positive forms side by side — the drift class the
  lift fixed: a future semantic fix would have had to find and edit
  sixteen spellings. The paragraph names the parity source
  (`fleet-dispatcher.mjs:2755`, importing forbidden) and the
  non-adopter census now visible per call site:
  `ufo-state-retention.mjs:328` (verbatim private copy, imports nothing
  from the leaf), `prepare-ephemeral-l1.mjs:56` (STRICTER contract —
  adds `Object.getPrototypeOf` rejection of class instances and
  null-prototype objects), and the inline expansions outside the lift's
  adopt scope (`collect-omp-native-handoff.mjs` 36 sites,
  `run-omp-native-trial.mjs`, `probe-ufo-route-health.mjs`,
  `project-devin-subagents.mjs`, `local-helper.mjs`,
  `omp-native-shutdown.mjs`, `omp-role-work.mjs`,
  `fleet-dispatcher.test.mjs`) — unconsolidated, not wrong.
- supersedes: §8.1's post-r77 scope — the leaf paragraphs named nine
  families while sixteen spellings of the same predicate lived across
  the swarm/monitor/watch/watchdog/mission-* files, until `1ebc7323`
  collapsed them.
- rationale: same codification-lag class as the prior leaf entries —
  the normative layer names each consolidation family as its commit
  lands so a fresh session never re-derives which primitives are
  canonical; the prototype-blind contract is recorded so a caller
  needing literal-`{}` strictness does not mistake the predicate for
  `prepare-ephemeral-l1`'s guard.
- evidence: `scripts/ufo-mission-result.mjs` `isPlainObject` (:133);
  adopters `ufo-l0-monitor.mjs:37`, `ufo-l0-watch.mjs:61`,
  `ufo-mission-activity.mjs`, `ufo-mission-lifecycle.mjs`,
  `ufo-mission-observation.mjs`, `ufo-stale-watchdog.mjs`,
  `ufo-swarm-collect.mjs`, `ufo-swarm-wave.mjs`; parity source
  `fleet-dispatcher.mjs:2755`; non-adopters
  `ufo-state-retention.mjs:328`, `prepare-ephemeral-l1.mjs:56`;
  sibling commit `1ebc7323`.

## 2026-09-22 — run-logic §8.1 canonical-leaf extension: either-binding receipt validation
- decision: §8.1 gains an eleventh canonical-leaf paragraph codifying
  `validateTaskReceiptEitherBinding(parsed, expected, snapshotDigest)` —
  the acceptance contract both L0 daemons carried verbatim (one 9-line
  block each: monitor `settle` admission, watch hole verdict). A receipt
  may bind the SOURCE prompt digest (queue-row `promptSha256`) or the
  dispatch-snapshot digest (the prompt the lane actually received — the
  dispatcher's `dispatch_snapshot` bindingSource). Source binding first;
  on a `receipt_mismatch` whose `details.field` is `promptSha256` the
  snapshot digest is resolved and the receipt retried — but only when
  the row resolves one: a null snapshot digest rethrows the
  source-binding error, so a missing snapshot never masks the real
  mismatch, and any other first-path failure (schema, another field,
  iteration shape) is final without a retry.
  `snapshotDigest` is a caller-supplied thunk,
  not a leaf-resolved path — row-context resolution stays caller-owned
  like the leaf's other injected dependencies. The paragraph names the
  dispatcher parity source (set-membership over every
  `dispatch-snapshot-*` dir, superseded renames included) and the
  stricter subset the helper encodes: the daemons' single
  current-attempt fallback still rejects a receipt the dispatcher would
  accept on a superseded attempt — the set-vs-single divergence now
  visible as a typed helper boundary, not two hand-rolled try/catch
  ladders.
- supersedes: §8.1's post-r78 scope — the leaf paragraphs named ten
  families while both daemons still carried verbatim either-binding
  copies, until `5e6dd1bc` collapsed them.
- rationale: same codification-lag class as the prior leaf entries —
  the normative layer names each consolidation family as its commit
  lands so a fresh session never re-derives which primitives are
  canonical; the null-rethrow contract is recorded so a caller does not
  mistake a missing snapshot for a masking path.
- evidence: `scripts/ufo-mission-result.mjs`
  `validateTaskReceiptEitherBinding` (:1702); call sites at
  `ufo-l0-monitor.mjs:728` (settle) and `ufo-l0-watch.mjs:893` (hole
  verdict); dispatcher parity source `fleet-dispatcher.mjs:5517`
  (`dispatchSnapshotPromptSha256` over `dispatchSnapshotDigests` :5488,
  membership accepted at :5652); sibling commit `5e6dd1bc`.

## 2026-09-22 — run-logic §8.1 eighth-paragraph census re-pin
- decision: the isMainModule non-adopter census (§8.1 eighth paragraph,
  r76) re-pins four line references that drifted under sibling commits —
  the cited files shrank and three pins pointed past EOF:
  `ufo-sighting.mjs` 6633→6529, `run-omp-native-trial.mjs` 4244→4196,
  `the-tick-ping.mjs` 703→695, `ufo-ground-handler.mjs` 755→744. No
  semantic change: every census claim was re-verified at the corrected
  pins (no-realpath trio, one-sided-realpath trio, dispatcher parity
  source, prepare-ephemeral MODULE_PATH guard all confirmed verbatim).
- supersedes: the r76 pins as written — stale within five rounds of
  sibling churn on the cited files.
- rationale: the census is a living claim about HEAD, not a historical
  record; a pin past EOF silently reads as a wrong claim. CHANGELOG
  evidence refs stay historical and are never re-pinned.
- evidence: HEAD `dfc42bc6`; guards at `ufo-sighting.mjs:6529`,
  `run-omp-native-trial.mjs:4196`, `the-tick-ping.mjs:695`,
  `ufo-ground-handler.mjs:744`; unchanged refs re-verified at
  `fleet-dispatcher.mjs:8379`, `sync-global-routing.mjs:294`,
  `fleet-ledger-rotate.mjs:1036`, `prepare-ephemeral-l1.mjs:872`.

## 2026-09-22 — run-logic §8.1 canonical-leaf extension: declared-argv walk
- decision: §8.1 gains a twelfth canonical-leaf paragraph codifying
  `parseDeclaredArgv(args, flagNames, valueNames)` — the declared-argv
  surface walk both L0 daemons carried per-file (monitor option binding,
  watch daemon-option binding). One pass returns `{ flags, values,
  faults }`: declared flags consume nothing; value options fault
  `duplicate <name>` on seen-ever re-appearance (the watch's stricter
  arm), fault `<name> requires a value` when the next argument is absent
  or itself declared (a swallowed flag is never a value), consume a
  present value so it is never re-walked, and keep the first valid
  value; anything else faults `unsupported argument: <arg>`. The caller
  owns the refusal — daemons append value-domain checks and emit one
  typed usage error before any queue read, lock, or mutation. The same
  sibling commit unexported `dispatchSnapshotPromptPath` — the leaf's
  public surface stays the digest primitive alone (ninth-paragraph
  amendment).
- supersedes: §8.1's post-r80 scope — the leaf paragraphs named eleven
  families while both daemons still carried private declared-argv
  walks, until `f74b7fae` collapsed them.
- rationale: same codification-lag class as the prior leaf entries —
  the normative layer names each consolidation family as its commit
  lands so a fresh session never re-derives which primitives are
  canonical; the union semantics (seen-ever duplicates, first-valid
  value) are recorded so a caller does not mistake the leaf for either
  private copy's narrower fault set.
- evidence: `scripts/ufo-mission-result.mjs` `parseDeclaredArgv`
  (:1553); call sites `ufo-l0-monitor.mjs:885`, `ufo-l0-watch.mjs:1142`;
  dispatcher parity source `fleet-dispatcher.mjs:8102-8118`
  (throw-on-first-fault, not collect-then-refuse); drift classes fixed —
  watch `option()` returned the raw next argument unvalidated, monitor
  emitted fewer faults on `--x --x a`; sibling commit `f74b7fae`.

## 2026-09-22 — run-logic §8.1 twelfth-paragraph re-pin + HEAD-anchor convention
- decision: the `the-tick-ping.mjs` declared-argv census pin moves
  `:549`→`:541` — HEAD carries the requires-a-value throw inside the
  `take` helper at `:541`; `:549` at HEAD is the `--health`
  duplicate-check. The pin had been minted against the working tree,
  where sibling WIP (a `--` terminator + `seen` pre-pass, +8 lines)
  coincidentally lands the throw back at `:549`. Same-pass amendment:
  the twelfth paragraph now states the anchor convention — every census
  pin in §8.1 cites COMMITTED bytes (HEAD), never the working tree;
  sibling WIP shifts lines without drifting a claim, and a pin verified
  against uncommitted bytes is wrong the moment it is written.
- supersedes: the `:549` pin minted in the r81b twelfth paragraph.
- rationale: pins exist so a fresh session can verify a claim against
  durable bytes; WIP is ephemeral by definition — a pin anchored to it
  silently re-points when the WIP commits, reverts, or grows. Naming
  the convention closes the drift class, not just the instance.
- evidence: `git show HEAD:scripts/the-tick-ping.mjs` — `:541` throws
  `${name} requires a value`, `:549` throws `duplicate --health`;
  working-tree `:549` is the same requires-a-value throw shifted +8 by
  uncommitted sibling WIP. All other §8.1 census pins re-verified at
  HEAD this round.

## 2026-09-22 — run-logic §9 `.cursor/` managed/unmanaged boundary
- decision: §9 gains a paragraph naming the `.cursor/` split — ten of
  twelve tracked files are managed (six via the `project-cursor` skill
  target, three via dependency mirrors whose package root is `.cursor`
  itself, one via the godspeed directive channel); two are unmanaged:
  `.cursor/skills/godspeed/SKILL.md` (byte-identical copy of
  `skills/godspeed/SKILL.md`; source SHA256SUMS-pinned but outside
  `canonicalSources`, so the copy drifts invisibly to `--check`) and
  `.cursor/rules/godspeed-always.mdc` (cursor-native always-apply rule,
  no canonical counterpart). Register-or-delete is mirror-map-owned.
- supersedes: the nc3-guidance r82 report's "5 files" unmanaged census —
  it counted the managed `.cursor/skills/godspeed/directive.md` among
  the unmanaged copies.
- rationale: a lane reading `.cursor/` as fully managed (or fully
  unmanaged) misjudges both halves; the boundary is derivable only from
  the mirror map, not from `--check` output, so the contract names it.
- evidence: `git ls-files .cursor/` (12 files); mirror-map derivation —
  `skillTargets["project-cursor"]` + `packagedDependencyMirrors` +
  `godspeedDirectiveMirrors` cover 10; byte-identity verified for all
  five copy pairs this round.

## 2026-09-22 — run-logic argv-reader adopter-set correction
- decision: §8.1 re-scopes `optionValue` from "the shared argv reader
  for the wave-family CLIs" to `ufo-swarm-collect.mjs` alone, and the
  declared-argv paragraph names the wave CLI as a third
  `parseDeclaredArgv` adopter (sibling `78e6c13e`, nc3-swarm r56) with
  its stricter arm — a bound value leading with `--` faults
  `requires a value` even when the next argument is not a declared
  name, restated per call site for `optionValue` parity.
- supersedes: the wave-family-CLIs framing — true while both wave CLIs
  read argv through `optionValue`; stale the moment the wave CLI moved
  to the declared-argv walk.
- rationale: adopter-set claims drift when a sibling migrates a CLI
  between readers; the census names adopters, not just non-adopters,
  so a migration lands as a visible edit instead of silent drift. The
  leaf's own `optionValue` docstring
  (`ufo-mission-result.mjs:1507`) still carries the stale wave-family
  claim — sibling-owned, recorded as a hand-off.
- evidence: `git show 78e6c13e` — `ufo-swarm-wave.mjs` drops the
  `optionValue` import, adopts `parseDeclaredArgv` at `record` and at
  the `plan`/`run` spec surface, and re-arms the `--`-leading-value
  refusal on bound options; `grep -ln optionValue scripts/*.mjs` —
  `ufo-swarm-collect.mjs` is the sole leaf importer.

## 2026-09-22 — run-logic argv-reader adopter-set correction (collect adoption)
- decision: §8.1 re-scopes `optionValue` from "the shared argv reader
  for `ufo-swarm-collect.mjs`" to a parity leaf with no consumers —
  collect, its last importer, adopted `parseDeclaredArgv` (sibling
  `a9e89555`, nc3-swarm r57), retiring the leaf's importer set. The
  declared-argv paragraph names collect as the fourth adopter with a
  second stricter arm the leaf does not have: a duplicate `--emit-xml`
  is refused at the precedence the private walk kept (after the
  value-option faults, before the required checks), while the leaf
  records a declared flag idempotently and dedupes it silently.
- supersedes: the sole-importer framing — true for one round; stale
  the moment collect migrated. Second consecutive round this claim
  class drifted (r84 wave, r85 collect): sibling argv migrations land
  as visible edits, not silent drift.
- rationale: the leaf stays exported but unimported — the parity
  source each adopter restates per call site, not a dead helper to
  delete (the dispatcher's and fake-omp's private same-name helpers
  are unrelated copies with different signatures). The leaf's own
  `optionValue` docstring (`ufo-mission-result.mjs:1507`) still
  carries the stale wave-family claim — sibling-owned, hand-off
  re-armed.
- evidence: `git show a9e89555` — `ufo-swarm-collect.mjs` drops the
  `optionValue` import, adopts `parseDeclaredArgv` for its six value
  options plus `--emit-xml`, re-arms the `--`-leading-value refusal,
  and keeps the duplicate-flag refusal the leaf dedupes;
  `grep -n optionValue scripts/*.mjs` — zero leaf imports (only
  comment-residue mentions and unrelated private same-name helpers in
  `fleet-dispatcher.mjs:8092` and `fake-omp.mjs:108`);
  `ufo-l0-monitor.mjs` `digestDriftLeg` extraction is
  behavior-preserving — §8.1's diagnose claims name finding classes,
  not internals, so no drift there.

## 2026-09-22 — §8.1 codifies `plainObjectRows`; watchdog argv pin re-anchored
- decision: §8.1 names the leaf's malformed-element row filter
  `plainObjectRows(value, onMalformed)` (sibling `eb723399`, nc3-swarm
  r59) — the consolidation of the watch's `malformedReportMembers` walk
  and the stale watchdog's `malformedMissionElements` walk. The
  paragraph names both adopters, the caller-owned descriptor contract
  (watch `member[i]`; watchdog `missions[i]:<type>`), the watchdog's
  private `jsonTypeName` precision fix (a null member now reports
  `"null"`, not `"object"`), and the dispatcher `:840` divergence —
  it admits null rows, so it is NOT this family's parity source.
  `receiptCoreFields` is recorded as module-private dedup, not a fleet
  primitive. The same edit re-anchors the stale-watchdog argv census
  pin `:913` → `:918` (r59's import + helper additions shifted it).
- supersedes: the `:913` pin (correct at `b5b16f25`, stale at
  `eb723399`); the implicit "each daemon hand-rolls its element
  filter" state — never codified, now closed. The evidence bullet's
  `fleet-dispatcher.mjs:840` "verified at HEAD" clause is stale: the
  null-admit was removed in `82d08c49` (nc3-dissection r17); the gate is
  `isPlainObject(row)` only at `fleet-dispatcher.mjs:1087` (nc5 HEAD).
- rationale: §8.1's convention names each consolidated primitive
  family in landing order; `plainObjectRows` is the newest family.
  The dispatcher divergence is named explicitly because its
  null-admitting contract is the first leaf family where the
  dispatcher is NOT the parity source — recording that prevents a
  future round from "fixing" the leaf to match.
- evidence: `git show eb723399` — `ufo-mission-result.mjs:150` exports
  `plainObjectRows`; `ufo-l0-watch.mjs` and `ufo-stale-watchdog.mjs`
  adopt it; `git show eb723399:scripts/ufo-stale-watchdog.mjs |
  sed -n '918p'` names the argv refusal; `fleet-dispatcher.mjs:840`
  `row === null || isPlainObject(row)` verified at HEAD.

## 2026-09-22 — §8.1 records collect-bridge private dedups
- decision: §8.1 names `optionalBoundedString`
  (`ufo-swarm-collect.mjs:189`) and `soleEvidence`
  (`ufo-swarm-collect.mjs:481`) as module-private dedups inside the
  collect bridge (sibling `068fa666`, nc3-swarm r60) — five
  bounded-string call sites and two distinct-non-null conflict walks
  collapsed, per-call-site code/label/cap preserved, join contract
  (`conflicting_member`, `missing_agent_id`, bijection) unchanged.
  Recorded as private, not fleet primitives: the parity source for any
  future adopter is the join contract, not the helpers.
- supersedes: none (new census entry; the implicit "collect hand-rolls
  its checks" state — never codified, now closed).
- rationale: §8.1's convention records each committed dedup so a later
  round resolves primitive-vs-private from the doc instead of
  re-diffing the sibling commit; same class as `receiptCoreFields`.
- evidence: `git show 068fa666` — `ufo-swarm-collect.mjs` gains both
  helpers; `grep -n optionalBoundedString\|soleEvidence
  scripts/ufo-swarm-collect.mjs` pins `:189`/`:481` at HEAD; helper
  comments say "nc3-swarm r77" vs commit r60 — sibling-internal
  numbering, recorded not reconciled.

## 2026-09-22 — run-logic §8.1 sighting launch-detector codification
- decision: §8.1 records the sighting surface's dispatch-attestation
  internals — the factored `shellLaunches`/`appearsToLaunch` pair
  (`ufo-sighting.mjs:652-720`), the `INDIRECT_OMP_DISPATCH` refusal
  (`:985`) mirroring `INDIRECT_OPENCODE_DISPATCH`, the 30s `runTmux`
  bound, the live-cmdline `isIdlePane` check, and the `operation.lock`
  owner-null restore arm (a seized lock whose `owner.json` is unreadable
  is quarantined and renamed back, never deleted; `EEXIST`/`ENOTEMPTY`
  on restore proves a contender's fresh `mkdir` and makes deletion
  safe). The session-hook paragraph gains the `claimRun` mtime fallback
  (a malformed or future-dated claim must not suppress the monitor
  forever); §4.2 gains the trial launcher's routing-authority clause
  (provider admission is the fd-bound global snapshot's, never a
  launcher-side allowlist) and the collector's judge-parity clauses
  (empty-string provider/model dies at collection; `argv_sanitized`
  screened by the wider sensitive-shape gate; evidence files persist
  only after every die-capable check).
- supersedes: the armed-trigger state — the launch-detector doctrine was
  carried in guidance-lane reports for 20 rounds pending the commit.
- rationale: same codification-lag class as the prior leaf entries —
  the trigger rule (codify on the consolidating commit, never on WIP)
  fired when `5289d1a6` landed.
- evidence: `scripts/ufo-sighting.mjs` `shellLaunches`/`appearsToLaunch`
  (:652-720), `INDIRECT_OMP_DISPATCH` (:985), `acquireOperationLock`
  owner-null restore (:2229+), `TMUX_TIMEOUT_MS` (:2384), `isIdlePane`
  (:2528); `.omp/hooks/pre/ufo-l0-monitor.js` `claimRun` mtime fallback
  (:182-186); `scripts/collect-omp-native-handoff.mjs` judge-parity dies
  (:2074+) + `persistEvidenceWrites` ordering (:5458);
  `scripts/run-omp-native-trial.mjs` provider-allowlist removal;
  census pins re-located at HEAD (`ufo-sighting.mjs:6633`,
  `run-omp-native-trial.mjs:4244`, `the-tick-ping.mjs:703`,
  `ufo-ground-handler.mjs:755`, `fleet-dispatcher.mjs:8381`/`:5519`);
  sibling commit `5289d1a6`; sync `--check` green post-edit.

## 2026-09-22 — run-logic §8.1 census re-pin: ufo-sighting lib split
- decision: the living census pins re-home to committed bytes after
  sibling `7fba1db0` (nc3-tooling r38) split `ufo-sighting.mjs`
  (6635→4650 lines) under the 256 KiB `MAX_CONTRACT_FILE_BYTES` bound
  into `scripts/ufo-sighting-lib/{base,argv,observe,surface}.mjs`, the
  entry re-exporting the moved names. Re-pins: entry guard
  `ufo-sighting.mjs:6633`→`:4640`; `shellLaunches`/`appearsToLaunch`
  `:652-720`→`ufo-sighting-lib/argv.mjs:139-204`; `INDIRECT_OMP_DISPATCH`
  `:985`→`argv.mjs:467`; `optionValue` `:540-545`→`argv.mjs:22-35`;
  collect `optionalBoundedString` `:189`→`:196`, `soleEvidence`
  `:481`→`:497`; dispatcher `isPlainObject` `:2755`→`:2757` (off-by-2
  drift). The collect paragraph's private-dedup census also extends to
  the now-committed `c0c373b8` helpers (`OPERATOR_PATH_ERRNOS` :144,
  `resolveAgentId` :472, `requireArray` :485), and the §-level sighting
  claim now names the hash-bound `.mjs` module family.
- supersedes: the r98/r99 pins as written — stale the moment `7fba1db0`
  landed (the r99 armed re-pin trigger fired on this commit).
- rationale: same doctrine as the eighth-paragraph re-pin — the census
  is a living claim about HEAD; CHANGELOG evidence refs stay historical.
- evidence: HEAD `7fba1db0`; every re-pin verified against committed
  bytes (`git show`); unchanged census pins re-verified at
  `fleet-dispatcher.mjs:8381`/`:5519`/`:840`/`:8102-8118`,
  `sync-global-routing.mjs:294`, `fleet-ledger-rotate.mjs:1036`,
  `run-omp-native-trial.mjs:4244`, `the-tick-ping.mjs:703`/`:541`,
  `ufo-ground-handler.mjs:755`, `prepare-ephemeral-l1.mjs:872`/`:844`,
  `ufo-state-retention.mjs:328`, `ufo-stale-watchdog.mjs:918`,
  `ufo-mission-activity.mjs:159`, `collect-omp-native-handoff.mjs:312`,
  `fake-omp.mjs:130`, `probe-ufo-route-health.mjs:102-148`; sync
  `--check` green post-regen.

## 2026-09-22 — run-logic §8.1 census: watchdog re-pin + leaf primitives
- decision: the argv-fault census pin for the stale watchdog re-homes
  `ufo-stale-watchdog.mjs:918` → `:946` — the pin was already stale at
  the r100 verification (committed bytes identical; `:918` carries
  `isMainModule`, the typed `ufo-stale-watchdog-error-v1` `code:"usage"`
  + exit-64 fault sits at `:946-955`). The same section's census
  extends to sibling `232f0cef` (nc3-swarm r64): the leaf now hosts
  `spinWait` (five adoptions — three internal bounded-wait loops plus
  the L0 watch and stale watchdog ticks) and `emitJson` (six — four
  `main()` sites plus the wave CLI's two outputs) as shared
  primitives, with `rethrowInputError` and the `validateTaskReceipt`
  expected-bag cross-check table recorded as module-private dedups.
- supersedes: the r100 `:918` pin as written — stale on arrival;
  line-existence verification passed it, semantic verification caught
  it this round.
- rationale: same living-claim doctrine as the prior re-pins — the
  census describes committed bytes at HEAD; the trigger rule (codify
  on the consolidating commit, never on WIP) fired when `232f0cef`
  landed.
- evidence: HEAD `1675463d`; every pin re-verified semantically
  against committed bytes (`git show`) — entry guards
  `fleet-dispatcher.mjs:8381` (no execArgv screen),
  `ufo-sighting.mjs:4640`, `sync-global-routing.mjs:294`,
  `fleet-ledger-rotate.mjs:1036`, `run-omp-native-trial.mjs:4244`,
  `the-tick-ping.mjs:703`, `ufo-ground-handler.mjs:755`,
  `prepare-ephemeral-l1.mjs:872`; argv surfaces
  `fleet-dispatcher.mjs:8102-8118`, `prepare-ephemeral-l1.mjs:844`,
  `the-tick-ping.mjs:541`, `probe-ufo-route-health.mjs:102-148`,
  `ufo-sighting-lib/argv.mjs:22-35`, `collect-omp-native-handoff.mjs:312`,
  `fake-omp.mjs:130`, `ufo-mission-activity.mjs:159`,
  `ufo-stale-watchdog.mjs:946`; dedup census
  `fleet-dispatcher.mjs:2757`/`:5519`/`:840`,
  `ufo-state-retention.mjs:328`, `prepare-ephemeral-l1.mjs:56`,
  `ufo-swarm-collect.mjs:196`/`:497`/`:144`/`:472`/`:485`; sighting
  internals `ufo-sighting-lib/argv.mjs:139-204`/`:455`/`:467`;
  `spinWait` `ufo-mission-result.mjs:658`, `emitJson` `:1637`,
  `rethrowInputError` `:1893`, expected-bag table `:615-623`; sibling
  commit `232f0cef`; sync `--check` green post-regen.

## 2026-09-22 — godspeed-core README: stale AGENTS.md §6 ref + undeclared twin
- decision: the fleet-judge fusion paragraph in
  `skills/godspeed-core/README.md` and `ssot/godspeed-core/README.md`
  cited "AGENTS.md §6" — a numbered-section reference that no longer
  resolves: AGENTS.md carries named headings only ("NC2 fleet dispatch
  protocol" item 6 is the doctrine the citation meant). Both copies
  re-anchored to the named section + item. The two READMEs are
  byte-identical twins with no declared mirror relationship in
  `sync-ufo-contracts.mjs` — drift between them is invisible to
  `--check`; recorded as an undeclared-duplication flag for the
  mirror-map owner rather than reconciled unilaterally.
- supersedes: the `fefde4c2` (r22) citation form — the doctrine it
  pointed at is unchanged; only the anchor went stale when AGENTS.md
  moved to named headings.
- rationale: living-claim doctrine — a section reference must resolve
  against committed bytes at HEAD; "§6" resolved to nothing.
- evidence: HEAD `e2667bc9`; AGENTS.md headings enumerated (no numbered
  sections); `run-logic §4.3` ref re-verified correct (fleet-L1
  mission-internal Pareto doctrine at §4.3 tail); twin byte-identity
  confirmed by `diff`; mirror-map absence confirmed by grep of
  `scripts/sync-ufo-contracts.mjs`; `skills/SHA256SUMS` regenerated;
  sync `--check` green post-regen.

## 2026-09-22 — §8.1 census: collect-omp-native-handoff lib split re-anchor
- decision: sibling `4046cc06` (nc3-tooling r39) split
  `collect-omp-native-handoff.mjs` (3883→1796 lines) into
  `collect-omp-native-handoff-lib/{base,screening,events,policy,evidence}.mjs`.
  Two living census pins re-anchored: the isPlainObject non-adopter count
  moved from the entry file to the module family (36 sites re-verified
  exactly — entry 5, base 1, events 1, evidence 7, policy 22, screening 0),
  and the usage-text pin moved `:312` → `:118-141` (COLLECTOR_USAGE
  constant + three emit sites). Semantic claims unchanged: the
  current-user/non-symlink contract (§377) and SKILL.md:243 collector
  description still hold across the family; `config/ufo.json` glob
  `collect-omp-native-handoff*` covers the lib dir.
- supersedes: the pre-split single-file anchors — the doctrine is
  unchanged; only the file shape moved.
- rationale: living-claim doctrine — census pins cite committed bytes at
  HEAD; a pin naming the old monolith misleads the next census.
- evidence: HEAD `4046cc06`; per-file expansion counts via grep
  (`typeof.*"object".*Array\.isArray`); usage sites at
  `collect-omp-native-handoff.mjs:118`/`:122`/`:133`/`:141`; sibling WIP
  excluded (dispatcher +5 trigger, `readBoundedJson` leaf, swarm-script
  adoptions still uncommitted); `skills/SHA256SUMS` regenerated; sync
  `--check` green post-regen.

## 2026-09-22 — §8.1 census: ufo-sighting entry-guard re-pin after de-export
- decision: sibling `d3e7f36b` (nc3-tooling r40) removed 3 unused
  `node:fs` imports (`fstatSync`, `mkdtempSync`, `readSync`) from
  `scripts/ufo-sighting.mjs`, shifting every line below the import block
  −3. The living census pin for the entry guard moved
  `ufo-sighting.mjs:4640` → `:4637`. The same commit de-exported 83
  internal-only names across `collect-omp-native-handoff-lib/` (63) and
  `ufo-sighting-lib/` (20); the entry re-export tail at
  `ufo-sighting.mjs:4644-4647` still re-exports the same public names, so
  the "public surface unchanged" claim holds and no census claim about
  the lib surface drifts. `sighting.surfaceDigest` re-chartered
  `bfedffea`→`4a851d60` by the sibling (config-owned; no guidance ref).
- supersedes: the `:4640` anchor minted at the r38 lib split — the
  doctrine is unchanged; only the line moved.
- rationale: living-claim doctrine — census pins cite committed bytes at
  HEAD; a pin naming the pre-de-export line misleads the next census.
- evidence: HEAD `d3e7f36b`; entry guard verified at
  `ufo-sighting.mjs:4637` (`if (SIGHTING_CONFIG !== null &&
  import.meta.url === pathToFileURL(process.argv[1] || "").href)`);
  `ufo-sighting-lib/argv.mjs` untouched by r40 — pins `:22-35`,
  `:139-204`, `:455`, `:467` re-verified; dispatcher pins `:8381`,
  `:5519`, `:2757`, `:840`, `:8102-8118` and collect `:118-141`
  re-verified at HEAD (sibling WIP excluded — pins cite committed bytes);
  `skills/SHA256SUMS` regenerated; sync `--check` green post-regen.

## 2026-09-22 — §8.1 census: residue primitives codified (nc3-swarm r65)
- decision: sibling `d3998f39` (nc3-swarm r65) collapsed the last
  hand-rolled spellings across the nine wave-family CLIs into the
  `ufo-mission-result.mjs` leaf — `readBoundedJson` (11 call sites:
  monitor 4, watch 3, wave 2, leaf `readQueueFile` + `withDirLock`
  readOwner default), `collapseWhitespace` (7 sites), `emitErrorJson`
  (15 sites across 9 files), `TERMINAL_QUEUE_STATES` (monitor `TERMINAL`
  + watch `TERMINAL_QUEUE_STATES_LOCAL` aliases; dispatcher `:134` and
  `ufo-state-retention.mjs:126` keep private copies),
  `MAX_EVIDENCE_LOG_BYTES` (monitor/watch/watchdog `MAX_LOG_BYTES`
  aliases), `expectedReceiptBag` (monitor settle `:728`, watch hole
  verdict `:913`), `nonStringFields` (wave `:499`/`:520`), and
  module-private `buildRegistryDoc` (wave `:576`, not a leaf export).
  Non-adoptions documented at site: collect `readJsonInput`, wave
  `loadRegistry`, watchdog `readBoundedFile`, watch `readState`
  lane-field loop (`:336`), watch `writeSync(1,…)`, watchdog
  `writeSync(2,…)`, `ufo-ground-handler.mjs:345` same-name private.
- supersedes: none (new census paragraph; the r105 `readBoundedJson`
  census candidate hand-off is discharged).
- rationale: living-claim doctrine — codification waits for the
  consolidating commit; the paragraph names verified call sites and
  per-site divergences so the next census reads committed bytes, not
  the commit message's aggregate counts.
- evidence: HEAD `e340e667`; all counts re-verified against committed
  bytes (commit message's "10 sites"/"12 across 8 CLIs" aggregates
  differ from the call-site census — the paragraph cites the census);
  prior pins re-verified unchanged (dispatcher `:134/:840/:2757/:5519/
  :8102-8118/:8381`, sighting `:4637`, collect `:118-141/:144/:196/
  :472/:485/:497`, watchdog `:946`, activity `:159`, state-retention
  `:328`, prepare-ephemeral `:56/:844/:872`, tick-ping `:541/:703`,
  sync-global-routing `:294`, fleet-ledger-rotate `:1036`,
  run-omp-native-trial `:4244`, ground-handler `:755`, fake-omp `:130`,
  probe `:102`, argv.mjs `:22-35/:139-204/:455/:467`); `skills/
  SHA256SUMS` regenerated; sync `--check` green post-regen.

## 2026-09-22 — godspeed-core README twin pair declared at site
- decision: `ssot/godspeed-core/README.md` and
  `skills/godspeed-core/README.md` are byte-identical twins absent from
  the `sync-ufo-contracts.mjs` mirror map — drift between them was
  invisible to `--check` (flagged 2026-09-22 r102). A paragraph appended
  to both copies declares the pair at site: byte-identical at 6234
  bytes (2026-09-22 census), edit-both-identically rule until the
  mirror-map owner declares the pair. Both copies rewritten
  byte-identically post-edit (6634 bytes).
- supersedes: none (the r102 flag is discharged; the mirror-map gap
  itself stays mirror-map-owner scope).
- rationale: living-claim doctrine — an undeclared twin pair drifts
  silently; the declaration belongs at the site an editor touches, not
  only in a changelog.
- evidence: `cmp` byte-identical pre- and post-edit; mirror map
  (`scripts/sync-ufo-contracts.mjs` `skillTargets` +
  `godspeedDirectiveMirrors` + `bundledAssetMirrors`) contains no
  README entry; `skills/SHA256SUMS` regenerated; sync `--check` green
  post-regen.

## 2026-09-22 — always-on.md declared in README twins; census count corrected
- decision: `skills/godspeed-core/always-on.md` (tracked, repo-authored
  host always-on install doctrine, r23-scoped) was absent from the
  README twins' Files list — every other file in the directory was
  enumerated. A Files entry added to both twins declares it
  skills-distribution-only: deliberately absent from the vendored roots
  (`godspeed-core/`, `skills/ufo/references/godspeed-core/`), `ssot/`,
  and the sync mirror map. The twin-declaration paragraph's "6234
  bytes at the 2026-09-22 census" corrected to "6234 bytes each at the
  2026-09-22 pre-declaration census" (post-declaration files were
  already 6634B — the count read as current). Both copies rewritten
  byte-identically post-edit (7027 bytes).
- supersedes: none (the mirror-map gap stays mirror-map-owner scope).
- rationale: census completeness — an undeclared file in a declared
  family drifts silently; the declaration belongs at the site an
  editor touches.
- evidence: `md5sum` byte-identical twins pre- and post-edit;
  `git ls-files` confirms always-on.md tracked only under
  `skills/godspeed-core/`; mirror map contains no always-on/README
  entry; `skills/SHA256SUMS` regenerated; sync `--check` green
  post-regen.

## 2026-09-22 — §8.1 census re-pin + r67 argv primitives codified
- decision: five pin groups in run-logic §8.1's residue-primitives
  paragraph drifted when sibling `56201bf4` (nc3-swarm r66: repair()
  rowDigests dedup + wave policy-check fold) shifted monitor and wave
  lines after the r106 census was written. Re-pinned to HEAD bytes:
  monitor `readBoundedJson` receipt reads `:465/:636/:727/:810` →
  `:482/:645/:736/:819`; monitor `collapseWhitespace` repend-fault clip
  `:574` → `:583`; monitor `MAX_LOG_BYTES` alias `:586` → `:595`;
  monitor `expectedReceiptBag` settle `:728` → `:737`; wave
  `buildRegistryDoc` rewrites `:1193/:1307` → `:1183/:1293`. Sibling
  `eb37076b` (nc3-swarm r67) landed mid-round and lifted the argv
  paragraph's two stricter arms into the leaf: `rejectFlagLikeValues`
  (the `--`-leading-bound-value refusal; wave `:1219`/`:1326`, collect
  `:619`) and `hasDuplicateArg` (the duplicate-flag refusal; collect
  `--emit-xml` `:626`, wave `--emit-tasks` `:1345`) — the paragraph now
  codifies both as shared primitives instead of per-call-site
  restatements. All other §8.1 pins re-verified at HEAD (`eb37076b`)
  and hold; the `emitErrorJson` 15-site/9-file count re-counted and
  holds.
- supersedes: none (re-pin + codification, not a contract change).
- rationale: census pins cite committed bytes; a sibling commit that
  shifts lines without drifting semantics still falsifies the pin —
  re-verification must cover the whole census set, not only the pins a
  round happened to list. A mid-round sibling landing is integrated the
  same round, not carried as a hand-off.
- evidence: `git show HEAD:<file> | sed -n '<pin>p'` per new pin;
  `git log` attributes the shifts to `56201bf4`/`eb37076b`; leaf
  helpers at `ufo-mission-result.mjs:1684/:1702`; sync `--check` green
  post-regen.

## 2026-09-22 — §8.1 census: isPlainObject non-adopter count corrected
- decision: the isPlainObject paragraph's non-adopter census claimed "36
  sites across the module family — entry 5, base 1, events 1, evidence 7,
  policy 22, screening 0". A structural recount (if-condition scan +
  pure-predicate filter, not grep) gives 38 sites — entry 7, base 1,
  events 1, evidence 7, policy 22, screening 0. The delta is two entry
  sites the original grep-based count missed: a multi-line falsy-first
  condition (`snapshot.assignment_hashes`, entry :190) and a
  positive-falsy condition (`canonicalProfile.seatTiers`, entry :441) —
  the latter a FOURTH collapsed spelling (`x && typeof x === "object" &&
  !Array.isArray(x)`) the three-spelling enumeration did not carry.
  Semantically identical to `isPlainObject` for every value (0/""/NaN/
  false/null all reject), so the "semantically identical" claim survives;
  only the count and the spelling enumeration were wrong. The paragraph
  now names the count basis: a site is a condition that IS the predicate,
  not one containing it. Both sites predate the r39 lib split (monolith
  :3153/:4134) — the original "36" was a miscount, re-anchored verbatim
  by r103 (`310c9507`).
- supersedes: none (count correction, not a contract change).
- rationale: a census claim must be verifiable by the method it names;
  grep counts lines, not conditions — multi-line and positive-form
  predicates are invisible to it. The count basis is now stated at site
  so the next re-verification counts the same set.
- evidence: structural recount script (if-condition scan + pure-predicate
  regex over `git show HEAD:` bytes): entry 7 (:183/:190/:441/:1251/
  :1296/:1447/:1452), base 1 (:909), events 1 (:200), evidence 7
  (:540/:566/:630/:637/:695/:717/:813), policy 22, screening 0; pre-split
  monolith recount at `4046cc06^` gives the same 38. Sibling `2ef45bed`
  (nc3-swarm r68: `stalledIdleText` leaf lift + `rejectDuplicate`
  wave-private dedup) landed mid-round and was integrated the same
  round: 9 wave pins re-pinned (`:301/:612`→`:318/:629`, `:499/:520`→
  `:516/:537`, `:576`→`:593`, `:1183/:1293`→`:1195`/`:1304`,
  `:1219/:1326`→`:1231/:1337`, `:1345`→`:1356`), 10 watch pins +1
  (`:266/:856/:912`→`:267/:857/:913`, `:242/:246/:455`→`:243/:247/:456`,
  `:108`→`:109`, `:384`→`:385`, `:913`→`:914`, `:336`→`:337`), both new
  primitives codified at site; monitor and collect pins hold. All §8.1
  pins re-verified at HEAD `2ef45bed`; emitErrorJson 15/9, emitJson 6,
  spinWait 5, readBoundedJson 11, collapseWhitespace 7 counts hold;
  sync `--check` green post-regen.

## 2026-09-22 — SKILL.md L3 chain claim corrected; §8.1 re-pin for r69
- decision: SKILL.md's Sekhmet/L3 paragraph claimed the shelved spark
  chain "lives in `config/ufo.json` `l3Evidence`" — stale since the
  routing-authority cutover. The canonical chain is the Rust literal
  `CANONICAL_L3_CHAIN` (`crates/ufo-core-runtime/src/l3_swarm.rs`),
  supplied by `L3EvidenceConfig::canonical()`; config `l3Evidence`
  carries only `transport`/`authority`/`concurrencyCeiling`, and a
  `chain` field there is forbidden project model authority the sync gate
  rejects (`sync-ufo-contracts.mjs` `PROJECT_MODEL_AUTHORITY_SUBFIELDS`).
  Sibling `3854da5c` (nc3-swarm r69: `checkComposedText` +
  `reportInstruction` composition tail, `memberEntries` single-pass
  task+registry mint, `atRest` ownership index) landed mid-round and was
  integrated the same round: 9 wave pins re-pinned (`:318/:629`→
  `:336/:647`, `:516/:537`→`:534/:555`, `:593`→`:611`, `:1195/:1304`→
  `:1203/:1321`, `:274`→`:292`, `:894/:901`→`:912/:919`, `:1260`→
  `:1268`), all four new primitives codified at site.
- supersedes: none (claim correction + pin maintenance, not a contract
  change).
- rationale: a guidance claim must name the authority the code actually
  enforces; post-cutover the chain is a Rust literal and config is
  forbidden from carrying it — the sentence described the pre-cutover
  arrangement.
- evidence: systematic AGENTS.md + SKILL.md claim-vs-code audit (~65
  claims verified against `ufo-swarm-wave.mjs`, `ufo-sighting-lib/*`,
  `run-omp-native-trial.mjs`, `ufo-night-watchdog.sh`, `config/ufo.json`,
  `config/the-tick.machine.json`, `fleet-dispatcher.mjs`,
  `ufo-mission-result.mjs`, `~/.omp/agent/config.yml` — one drift found);
  `L3EvidenceConfig::canonical()` at `l3_swarm.rs:322`; forbidden-field
  gate at `sync-ufo-contracts.mjs:447`; sync `--check` green post-regen.

## 2026-09-22 — §8.1 re-pin for r70 + five primitives codified; argv pin miss corrected
- decision: sibling `eb147b51` (nc3-swarm r70: single-pass lane classify +
  payload split, canonical-once scope overlap, lazy seal/sibling indexes)
  landed all three armed WIP files in one commit — wave +34, monitor +22,
  watch +39. 24 §8.1 pins re-pinned to HEAD `f6ebc5da`: monitor
  readBoundedJson `:482/:645/:736/:819`→`:487/:659/:750/:833`, watch
  readBoundedJson `:267/:857/:913`→`:274/:881/:937`, monitor
  collapseWhitespace `:583`→`:597`, watch collapseWhitespace
  `:243/:247/:456`→`:250/:254/:463`, monitor MAX_LOG_BYTES `:595`→`:609`,
  watch `:385`→`:392`, monitor expectedReceiptBag `:737`→`:751`, watch
  `:914`→`:938`, watch readState loop `:337`→`:347`, monitor
  stalledIdleText `:1043`→`:1057`, watch `:1093`→`:1116`, wave
  buildRegistryDoc calls `:1203/:1321`→`:1221/:1339`, wave
  rejectDuplicate sites `:912/:919/:1268`→`:923/:930/:1286`, wave r69
  pins `:996→:1007`, `:1021→:1032`, `:1004→:1015`, `:1034→:1045`,
  `:972→:983`, `:989→:1000`, `:1014→:1025`, `:1083→:1094`, `:1284→:1302`.
  Five r70 module-private dedups codified at site: `file()` single-pass
  classify, `planToDispatchPayload` single-pass split (both-fields → both
  lists preserved), monitor `siblingsByReceipt` lazy index
  (`ufo-l0-monitor.mjs:429`), watch `canonicalScopesOverlap` +
  canonical-once `occupied` (`ufo-l0-watch.mjs:145`, `:793/:1005`), watch
  `successorByResultPath` lazy index (`:776`). Separately, the r111b
  re-pin missed the `rejectFlagLikeValues`/`hasDuplicateArg` call-site
  trio — pins `:1231/:1337/:1356` were already stale at r112 HEAD (+8/
  +17/+17 drift from r69's memberEntries insertion); corrected to
  `:1257/:1372/:1391`. All §8.1 pins re-verified at HEAD `f6ebc5da`.
- supersedes: none (pin maintenance + codification, not a contract
  change).
- rationale: census pins cite committed bytes; a sibling landing shifts
  lines without drifting claims, and the normative layer names each
  consolidated primitive family in landing order.
- evidence: per-pin line-content verification (38 pin targets grepped at
  HEAD); r70 diff `eb147b51`; sync `--check` green post-regen.

## 2026-09-22 — §8.1 re-pin for r17/r71 + dispatcher element-check contract rewrite
- decision: sibling `82d08c49` (nc3-dissection r17: wave-a defect settle,
  18-lane patch wave) landed `fleet-dispatcher.mjs` +552/-144,
  `fleet-ledger-rotate.mjs` +75, `prepare-ephemeral-l1.mjs` +72; sibling
  `feb4958c` (nc3-swarm r71: wave-context geometry) touched no §8.1
  pinned file. 9 §8.1 pins re-pinned to HEAD `feb4958c`: dispatcher
  entry guard `:8381`→`:8705`, `dispatchSnapshotPromptSha256`
  `:5519`→`:5704`, `isPlainObject` `:2757`→`:2827`, argv walk
  `:8102-8118`→`:8399-8420`, element check `:840`→`:873`,
  `TERMINAL_QUEUE_STATES` `:134`→`:138`, ledger-rotate entry guard
  `:1036`→`:1101`, ephemeral `parseOptions` `:844`→`:855`, ephemeral
  entry guard `:872`→`:898`. One claim REWRITTEN, not just re-pinned:
  r17's manifest-rows null filter changed the dispatcher's element
  check from `row === null || isPlainObject(row)` (admitted null rows)
  to `status.missions.every((row) => isPlainObject(row))` — the
  divergence claim now names the fail-the-whole-status shape vs the
  leaf's skip-malformed filter, with the pre-r17 spelling recorded.
  Two r17 module-private dedups codified at site: `beneath()`
  realpath-anchored stat-keyed containment (`fleet-dispatcher.mjs:439`,
  8 call sites) and `clearLatched()` emit-latched clear (6 sites).
- supersedes: the element-check divergence claim (null-admission arm
  removed by sibling `82d08c49`).
- rationale: census pins cite committed bytes; a sibling landing shifts
  lines without drifting claims, and a contract change inside a pinned
  file rewrites the claim, not just the pin.
- evidence: per-pin line-content verification at HEAD `feb4958c`; r17
  diff `82d08c49` (`row === null ||` arm deleted); sync `--check`
  green post-regen.

## 2026-09-24 — nc5-guidance r01: post-baseline claim-fidelity audit + repair
- decision: nc5 baselines `3c35abf3` (defaultIterateRounds 8→1024) and
  `74da1e8b` (watchdog/monitor fleet wiring nc4→nc5, env-overridable)
  drifted owned guidance. 20-lane read-only audit wave verified all 75
  §8.1 pins plus claim families against HEAD `74da1e8b`. Repairs landed:
  (a) iterate-rounds claims — run-logic §8.2 + AGENTS.md said "8-round
  iteration"; the live default is `missionFormat.defaultIterateRounds`
  (a ceiling, not a target); (b) `UFO_L0_MONITOR_FLEETS` default
  `nc4`→`nc5` (run-logic :1245, hook `DEFAULT_FLEETS`); (c) §3 gates
  battery claim rewritten — compile/boot/probe discharge through the
  canonical runtime's `pareto_gate_mutation_smoke` phase-0 report
  (`ufo gates`/`ufo self-iter`), not a `cargo build`/`ufo status`/
  per-seat-fixture chain inside `gates.sh`; (d) §4.1 critical-seat list
  corrected — `native.rs` `is_critical` is Main|Planner|Distiller|Labrat;
  the probeParent is a proposal seat, not critical; (e) ~25 §8.1 pins
  re-anchored to HEAD (wave primitives ~-28 lines post-nc3 landings:
  buildRegistryDoc :611→:535, reportInstruction :206→:203,
  checkComposedText :214→:211, memberEntries :983→:948, atRest
  :1302→:1342, rejectDuplicate sites :923/:930/:1286→:888/:895/:1326,
  rejectFlagLikeValues :1257/:1372→:1297/:1444, hasDuplicateArg
  :1391→:1463, collect :619/:626→:639/:646, soleEvidence :497→:517,
  resolveAgentId :472→:492, requireArray :485→:505, isPlainObject
  retention :328→:350, ephemeral guard :898→:918 + parseOptions
  :855→:879, entry guards sighting :4637→:4702, sync-global :294→:358,
  ledger-rotate :1249→:1265, ground-handler :755→:761 + :345→:347,
  stale-watchdog :990-996→:932-938, watch canonicalScopesOverlap
  :145→:150, readState :348→:352, occupied :793/:1005→:859/:1096,
  successorByResultPath :776→:837, stalledIdleText :1057/:1116→:1095/
  :1210, collapseWhitespace :302/:597/:250/:254/:463/:65→:324/:627/
  :255/:259/:471/:67, expectedReceiptBag :751/:938→:789/:1009,
  nonStringFields :534/:555→:446/:467, monitor TERMINAL :75→:97,
  MAX_EVIDENCE_LOG_BYTES :609/:392/:109→:639/:397/:116, emitErrorJson
  count 15→17 across 9 files, watch TERMINAL_QUEUE_STATES_LOCAL alias
  claim removed — direct import since nc4-swarm r01); (f)
  agents/executor.md trigger-normalization ref SKILL.md→
  `ufo-sighting.mjs` `normalizeTrigger`.
- supersedes: none (pin maintenance + claim repair, not a contract
  change).
- rationale: census pins cite committed bytes; baselines and sibling
  landings shift lines without drifting claims.
- evidence: 20-lane audit reports under `.ufo/scopes/nc5-guidance/
  r01-audit/`; per-pin line-content verification at HEAD `74da1e8b`;
  sync `--check` green post-regen modulo the sibling-owned
  `sighting.surfaceDigest` drift (nc5-primeagent in-flight
  `ufo-sighting.mjs` edits — re-charters on their commit).
  Cross-scope findings recorded, not edited: `ufo-night-watchdog.sh`
  stale nc3/nc4 comments (:25,:167), `config/mission-nightcall.yml`
  header "16-32 lane waves" vs live 16-100 band, test fixtures pinning
  `defaultIterateRounds: 8` (fleet-dispatcher.test.mjs:176).

## 2026-09-24 — nc5-guidance r02: §8.1 semantic-claim audit + repair
- decision: 26-lane read-only audit wave verified §8.1 semantic (non-pin)
  claims, AGENTS.md non-routing claims, the SKILL↔run-logic↔AGENTS
  duplication map, and CHANGELOG dated-prose classification at HEAD.
  Fifteen stale claims repaired: (a) §8.1 detect leg "blocked iterate
  rows"→"blocked rows" (no iterate filter in diagnose); (b) retired-fleet
  mechanism → fleet-set scoping; (c) respawn action tokens
  `enqueued`/`deduped`→`respawned`/`respawn_deduped`; (d) watchdog repend
  age 10min→240s (run-logic + AGENTS.md); (e) `loadObservations` fail-open
  distinguishes `unavailable`-tagged Map; (f) durability leaf "every
  script imports"→adopting scripts + named private-copy exceptions;
  (g) proc-helper dedup notes sighting/retention private copies;
  (h) S-06 pair shared by monitor only (stale watchdog adopts `redact`
  alone); (i) leaf `redact` lacks dispatcher quoted-value arm —
  documented; (j) snapshot layout `ompChildArgv`→`dispatchQueuedTask`;
  (k) pure-predicate census 38/entry-7→36/entry-5; (l) either-binding
  retry "ANY validation failure"→`receipt_mismatch` on `promptSha256`
  only; (m) `prepare-ephemeral-l1.mjs` pin :879→:884; (n)
  `expectedReceiptBag` five-field→six-field (`promptSha256`/`configSha256`
  ride the bag); (o) SKILL.md D1a retry set drops `probeParent`
  (is_critical = Main|Planner|Distiller|Labrat) and :316 renamed
  admission-critical; ssot+skills godspeed-core README twin pair:
  directive.md IS a declared contract-sync mirror.
- supersedes: none (claim repair, not a contract change).
- rationale: semantic claims drift independently of pins; dated
  CHANGELOG entries stay historical.
- evidence: 26 lane reports under `.ufo/scopes/nc5-guidance/r02-audit/`;
  per-claim verification at HEAD `f96e8e11`; sync `--check` green on
  owned scope modulo sibling-owned `sighting.surfaceDigest` drift
  (nc5-primeagent in-flight). Cross-scope findings recorded, not edited:
  `ufo-night-watchdog.sh` stale ">10min" comment (:25) and wedged-kill
  header (:12-15) vs 240s code — nc5-swarm.

## 2026-09-24 — nc5-guidance r03: full-corpus semantic audit + pin re-anchor
- decision: 26-lane read-only audit wave verified ~430 claims across
  run-logic §§0-11, SKILL.md, agents/*.md frontmatter, AGENTS.md, README
  twins, and the CHANGELOG head. Repairs landed: (a) axes-dynamic claims
  scoped to the fleet-mission path — judged native freezes `config.axes`
  at launch (run-logic §4 + §1 + SKILL.md); (b) I1 adapter-guard claim →
  config serde `deny_unknown_fields` (drill `d-i1-second-l1` records the
  gap); (c) §2.1 enforcement rewritten — `argvContainsForbiddenSelector`
  + `resolveExactMission` identity binding, no dedicated planner→L1
  guard; (d) §3 compile/boot/probe are doctrine, phase-0 report =
  mutation smoke only, gates.sh order corrected; (e) D1a scoped to the
  fixture distiller seat (native admission deferred); (f) collector
  route binding → global seat-routing mirror; (g) truncated
  manifest-telemetry sentence completed; (h) plan artifact 4 MiB cap
  (`MAX_PLAN_ARTIFACT_BYTES`); (i) exit code reflects verdict
  persistence, not `loop_stop`; (j) §8.2 prompt contract gains
  `/skill:godspeed` second line; (k) §10 pseudocode annotated
  contract-shape; (l) SKILL.md `lane_failure` typing + handler-reuse =
  supervisor duty + expansion ban scoped to manual re-expansion; (m)
  AGENTS.md membrane/authority_boundary note; (n) 24 §8.1 pins
  re-anchored (10 `file:NNN` + 14 bare `:NNN`).
- supersedes: none (claim repair, not a contract change).
- rationale: same class as r01/r02 — semantic claims drift independently
  of pins; dated CHANGELOG entries stay historical.
- evidence: 26 lane reports under `.ufo/scopes/nc5-guidance/r03-audit/`;
  per-claim verification at HEAD `9ea39c8a`-era tree; sync `--check`
  green on owned scope modulo sibling-owned `sighting.surfaceDigest`
  drift (nc5-primeagent in-flight). Cross-scope findings recorded, not
  edited: `.omp/hooks/pre/ufo-godspeed-inject.js:17` comment names
  `pre/` only (nc5-tooling); `config/mission-nightcall.yml:3` "16-32
  lane waves" stale comment (config owner);
  `fleet-dispatcher.test.mjs:176` fixture `defaultIterateRounds: 8`
  (tests owner).

## 2026-09-24 — nc5-guidance r04: §8.1 prose + dated-entry audit + agents body depth
- decision: 23-lane read-only audit wave verified ~350 claims across §8.1
  prose, CHANGELOG dated entries, and agent-card bodies at HEAD. Fourteen
  repairs landed (`40771445`): CHANGELOG truncated rationale completed
  (:933), either-binding "ANY failure" narrowed to promptSha256-only
  (:1325), the missing r03 dated entry retro-added, the stall-admission
  entry's invisibility clause annotated superseded by `efee9fe4` (:705),
  `optionValue` zero-importer corrected (:1040); planner.md plan-cap 4 MiB;
  run-logic retention `readBootId` scope, `emitErrorJson` 17→18 (monitor
  3→4), `stalledIdleText` :1331→:1349, tick-ping :703→:716,
  ground-handler :777→:779, activity :159→:159-166, HEAD-anchor example
  re-anchored, and the bare-`:NNN` pin-spelling convention declared
  (:1894-1901); watchdog hub-row claim annotated with the setsid arm
  (run-logic + AGENTS.md).
- supersedes: none (claim repair, not a contract change). This entry itself
  was omitted at ship time and retro-added by r06 — same drift class as the
  missing r03 entry r04 repaired.
- rationale: same class as r01/r02 — semantic claims drift independently of
  pins; dated CHANGELOG entries stay historical.
- evidence: 23 lane reports under `.ufo/scopes/nc5-guidance/r04-audit/`;
  verdict `.ufo/scopes/nc5-guidance/r04-verdict.md`; commit `40771445`;
  sync `--check` green on owned scope modulo sibling-owned
  `sighting.surfaceDigest` drift (nc5-primeagent in-flight).

## 2026-09-24 — nc5-guidance r05: residual-surface audit + 42-pin re-spell
- decision: 16-lane read-only audit wave verified ~200 claims plus 42 pin
  dispositions across the residual owned surface at HEAD. Repairs landed
  (`c6973345`): all 42 bare `:NNN` pins in run-logic §8.1 re-spelled to
  `file.ext:NNN` (zero remain); 13 drifted pins re-anchored (monitor
  :122/:760/:911/:648, watch :258/:262/:400/:482/:874/:1034/:1111/:153,
  mission-result :785, stale-watchdog :116); SKILL.md:41 splice repaired
  (r03's edit had deleted the `2. Contract`/`3. Planner stance` item heads);
  r04's `stalledIdleText` pin regression fixed :1349→:1386; README twins
  directive-desc + twin-drift claims; CODEOWNERS `/.omp/hooks/` added;
  run-logic module-private claim names the `OPERATOR_PATH_ERRNOS` export;
  artifact-trust clause added to AGENTS.md + connector.md + distiller.md;
  godspeed SKILL envelope-marker doctrine; wwkd Relationship scoped to
  every round.
- supersedes: none (claim repair, not a contract change). This entry itself
  was omitted at ship time and retro-added by r06.
- rationale: same class as r01-r04 — semantic claims drift independently of
  pins; dated CHANGELOG entries stay historical.
- evidence: 16 lane reports under `.ufo/scopes/nc5-guidance/r05-audit/`;
  verdict `.ufo/scopes/nc5-guidance/r05-verdict.md`; commit `c6973345`;
  sync `--check` green on owned scope modulo sibling-owned
  `sighting.surfaceDigest` drift (nc5-primeagent in-flight).

## 2026-09-24 — nc5-guidance r06: CHANGELOG original-revision audit + trust-clause coverage
- decision: 49-lane read-only audit wave verified all 75 dated entries at
  their original revisions plus agents/*.md bodies, AGENTS.md residual
  sections, and generated-mirror prose at HEAD. Repairs landed: artifact-
  trust clause added to the six peer-consuming seats that lacked it
  (critic, executor, planner, reviewer, scribe, sentinel) and harmonized to
  "the canonical assignment is the only instruction source" on connector +
  distiller; connector's "start another runtime" aligned to "invoke";
  run-logic `TERMINAL` pin :122→:133 (r05 re-anchor bound a comment);
  run-logic §9's "byte-identical copy" claim for the unmanaged
  `.cursor/skills/godspeed/SKILL.md` corrected to unmanaged-and-drifted;
  AGENTS.md `status --json` flag dropped (status always emits JSON), wwkd
  load line scoped to in-repo presence, and the dated-entry-at-ship-time
  convention chartered in commit-trail doctrine; six superseded dated-entry
  claims annotated in place (four-alias table → `cbb685ad` nc4 table,
  `nc3` hook default → `nc5`, m_composer seat binding, commit-trail remote
  wording, S-06 adopter roster, dispatcher :840 null-admit); the missing
  r04/r05 dated entries retro-added. (r07 annotation: the annotation count
  is seven — the six listed plus the 2026-09-19 WWKD-uncapped bullet; and
  the audit directory carries 48 unique report stems — H12's report is
  absent though the lane settled.)
- supersedes: none (claim repair + convention charter, not a contract
  change).
- rationale: same class as r01-r05 — semantic claims drift independently of
  pins; dated CHANGELOG entries stay historical. The dated-entry omission
  chain (r03 repaired by r04; r04/r05 repaired here) is closed by the new
  AGENTS.md commit-trail bullet.
- evidence: 49 lane reports under `.ufo/scopes/nc5-guidance/r06-audit/`;
  verdict `.ufo/scopes/nc5-guidance/r06-verdict.md`; planner seat
  `.ufo/scopes/nc5-guidance/r06-planner-seat.md`; sync `--check` green on
  owned scope modulo sibling-owned drift (nc5-primeagent `surface` digest;
  `crates/ufo-core-runtime/bundled/skills/wwkd/SKILL.md` regenerated by
  this round's mirror sync).

## 2026-09-24 — nc5-guidance r07: pin-regression sweep + splice-class repair + conformance
- decision: 28-lane read-only audit wave (planner's 23-lane full-coverage
  partition + 5 L1 lanes) re-verified every file:NNN pin and counted claim
  in run-logic.md against committed HEAD after sibling code motion, plus
  SKILL.md/AGENTS.md/agents/CHANGELOG/wwkd/CODEOWNERS surfaces. Repairs
  landed: 31 pin re-anchors across run-logic §8.1 (ufo-swarm-wave.mjs ×20,
  ufo-l0-monitor.mjs ×5, ufo-l0-watch.mjs ×4, sync-global-routing.mjs ×1,
  native_evidence.rs ×1 — the loop_driver.rs:2381 D1a pin moved to
  native_evidence.rs:2715); three deletion-splice seams healed
  (run-logic:2000-2001 `noteInvalidRunId pair and` ×2 collapsed;
  :2030-2031 `keeps its` ×2 restored to the aba4e8b1 original — the
  watchdog's `readBoundedFile` clause, fixing a misattribution to the
  wave's `loadRegistry`; :2040-2041 `added / field —` restored to the
  24f331ebd original — `stalledIdleText(row, suffix)` name + "two more"
  count); eight §8.1 prose enumerations corrected (durability commit cite
  + non-adopter pairing, fail-seam over-breadth, still-private probe
  enumeration, appendRotatingLog callers post-f9d67284, caller-kept
  stamped bodies, beneath callers post-d0dd958a, redact placeholder
  typing, same-name helper enumeration); watchdog repend cap re-scoped to
  continuously-blocked rows; observation row bound re-united to UTF-16
  code units; AGENTS.md resume-key null-as-absent, QUEUE_INVALID
  daemon-survival nuance, too_many_lanes/wave_too_wide ordering, wwkd
  every-round cadence, prompt_evidence_invalid unpinned-string fix;
  SKILL.md retirement/wall-open/axes-milestone/cursor-origin/I10/exit-2
  repairs; wwkd epigraph label deleted; CODEOWNERS gained /.omp/agents/ +
  /.omp/ssot/; connector frontmatter scoped native-vs-fleet; reviewer
  clause noun aligned to assigned-diff; r06 entry annotated in place for
  its six-vs-seven count and absent H12 report.
- supersedes: none (claim repair + convention alignment, not a contract
  change).
- rationale: same class as r01-r06 — sibling code motion drifts §8.1 pins
  and prose enumerations; the r05 re-anchor commit itself wrote ≥10 pins
  already wrong at its own tree (RL09 provenance finding), so pin audits
  must re-verify, not trust, prior anchors.
- evidence: 28 lane reports under `.ufo/scopes/nc5-guidance/r07-audit/`;
  verdict `.ufo/scopes/nc5-guidance/r07-verdict.md`; planner seat
  `.ufo/scopes/nc5-guidance/r07-planner-seat.md`; sync `--check` green on
  owned scope modulo sibling-owned drift (nc5-primeagent `surface`
  digest).

## 2026-09-24 — nc5-guidance r08: post-refactor pin regression sweep
- decision: after sibling crates r06 (`f8e1dce1`) split `loop_driver.rs`
  (6335→5832 + new `loop_driver_judge.rs`, 521L) and touched `native.rs`,
  `native_evidence.rs`, `lib.rs`, `local_ship.rs`, `godspeed.rs`, and
  `ufo-cli`, a census of all 245 `file.ext:N` pins in the owned corpus
  (34 unique targets) intersected the changed-file set at exactly three
  references. One was stale: §4.1's D1a deferral pin
  `native_evidence.rs:2715` now names the deadline-reciprocity guard;
  re-anchored to `native_evidence.rs:2734` (the `/// D1a grants one
  same-identity retry on the substrate (deferred…)` doc comment above
  `reject_critical_lane_timeout`). Verified live: `native.rs`
  `is_critical` still Main|Planner|Distiller|Labrat (`native.rs:399`),
  `loop_driver.rs:51` still `MAX_PLAN_ARTIFACT_BYTES`. No new pins into
  `loop_driver_judge.rs` — the moved judge-cluster symbols
  (`judge_wave`, `AdmittedProposal`, `ProposalVerdict`,
  `rejection_reason_code`) are described symbolically, never pinned.
  Bare-relative-pin sweep (`:NNN` without filename) found zero hits.
- supersedes: none (claim repair, not a contract change).
- rationale: same class as r07 — sibling code motion drifts pins; audits
  re-verify against committed HEAD, never trust prior anchors. The r07
  dated entry's `native_evidence.rs:2715` anchor stays historical — it
  was correct at its own revision.
- evidence: planner seat `.ufo/scopes/nc5-guidance/r08-planner-seat.md`;
  plan `.ufo/scopes/nc5-guidance/r08-plan.md`; verdict
  `.ufo/scopes/nc5-guidance/r08-verdict.md`; sync `--check` green on
  owned scope modulo sibling-owned `surface` digest.

## 2026-09-24 — nc5-guidance r09: watchdog-repend extraction + splice seam
- decision: nc5-swarm r07 extracted the night watchdog's repend duty into
  `scripts/ufo-watchdog-repend.mjs` (refusal-aware: `mission_stale_registered`
  suppressed inside a 900s signature-bound quiet floor; refused/failed
  repends never consume the cap; cap is 3 successful repends per
  continuously blocked row key, state pruned on unblock). §8.1's watchdog
  paragraph now names the helper and its suppression semantics, and
  AGENTS.md's parallel clause is corrected from "capped 3 per row per
  watchdog lifetime" (stale — the state file persists across watchdog
  restarts) to the same per-row-key successful-only semantics. The same
  edit healed a fourth splice seam introduced by r07's own repend-cap
  re-scope: the replacement had dropped "pending >15min, watch state
  >6min), and repends blocked fleet rows older", leaving "(dispatcher
  than 240s" dangling — the daemon staleness thresholds are restored.
  AGENTS.md's routing observation re-dated to 2026-09-24 and now records
  that every `m_*` chain terminates on `stepfun/step-5-preview:high`
  (`m_step`; baseline `51d75c2c`). The same rotation made three
  "terminal" route claims stale — `m_daybreak`, `m_swe`, and
  `m_kimi_devin_high` each carry one fallback hop now, so the
  non-cascading sense of terminal no longer holds: run-logic §4.2's
  "terminal fallback does not silently change models" now names the
  one-hop chain and its typed-capacity-only advance, and the
  "terminal … not a project allowlist" phrasing in §6 and AGENTS.md
  drops the stale qualifier. Live pin census into sibling-changed
  targets re-verified at HEAD: `fleet-dispatcher.mjs:138`,
  `collect-omp-native-handoff.mjs:118-141`, `run-omp-native-trial.mjs:4244`,
  `native_evidence.rs:2734`, `loop_driver.rs:51`, `native.rs:399` — all
  hold; dirty-worktree line drift (crates r07 in flight) is record-only.
  Cross-scope finding handed to L0, not edited: sibling-owned
  `ufo-night-watchdog.sh:25-28` header still says "per watchdog
  lifetime" and its wall-recovery comment overclaims killing a wedged
  server.
- supersedes: none (claim repair + seam heal, not a contract change).
- rationale: same class as r07-r08 — sibling extraction drifts §8.1 prose;
  the r07 seam proves even repair commits need re-verification.
- evidence: planner seat `.ufo/scopes/nc5-guidance/r09-planner-seat.md`;
  plan `.ufo/scopes/nc5-guidance/r09-plan.md`; verdict
  `.ufo/scopes/nc5-guidance/r09-verdict.md`; sync `--check` green on
  owned scope modulo sibling-owned `surface` digest.

## 2026-09-24 — nc5-guidance r10: post-extraction pin re-anchor + seam coverage
- decision: sibling churn since r09 (`4e721eaa` → `0f5dbb6c8`) — crates
  r15–r19 contract-file extraction and swarm r21–r27 — drifted ~30 live
  pins in run-logic §9's call-site censuses and moved two named symbols.
  Re-anchored: `is_critical` now lives in `native_schema.rs` (was
  `native.rs`); the deferred native-seat D1a admission is
  `native_telemetry.rs` `reject_critical_lane_timeout` (was
  `native_evidence.rs:2734`, file now 450 lines); `MAX_PLAN_ARTIFACT_BYTES`
  is `loop_driver.rs:112` (was :51). The §9 censuses re-anchor to HEAD
  `0f5db6c8`: isMainModule sites (run-omp `:4293`, ledger-rotate `:1324`,
  prepare `:939`, retention `:350`), argv surfaces (wave record `:1569`,
  plan/run `:1748`, `--emit-tasks` `:1767`; collect `:676`, `--emit-xml`
  `:683`; activity `:158-183`, stale-watchdog `:971-972`), collect helpers
  (`optionalBoundedString` `:213`, `soleEvidence` `:554`, `resolveAgentId`
  `:529`, `requireArray` `:542`, `OPERATOR_PATH_ERRNOS` `:879`), and the
  residue/monitor/watch/wave primitives (`collapseWhitespace` sites,
  `MAX_EVIDENCE_LOG_BYTES` aliases, `expectedReceiptBag`,
  `nonStringFields`, `buildRegistryDoc`, `stalledIdleText`,
  `rejectDuplicate`, `reportInstruction`, `checkComposedText`,
  `memberEntries`, `atRest`, `siblingsByReceipt`, `canonicalScopesOverlap`,
  `successorByResultPath`). Two seams gained coverage: §4.3's registry
  paragraph now names `wave_registry_collision` — a different wave
  identity persisting over an existing registry refuses BEFORE the write
  when an overlapping member name would displace an assigned handle
  (claimed resume handles excluded; unknown-wave registries keep reset
  semantics) — and the emit paragraph names `--emit-xml`'s
  render-before-publish plus `writeFilePairAtomic` two-file commit
  (sidecar-first rename, best-effort retract on primary-rename fault,
  kill -9 window documented). `reportInstruction`/`checkComposedText`
  gained their third composition site (schema-v2 compact prompt).
- supersedes: none (claim repair + seam coverage, not a contract change).
- rationale: same class as r07–r09 — sibling extraction drifts §9 census
  pins; HEAD moved mid-edit (`2eb4de41e` → `0f5dbb6c8`), so pins bind the
  landing HEAD. Pins cite committed bytes only; the dirty worktree
  (`ufo-mission-observation.mjs`, `ufo-swarm-collect.mjs` WIP) is
  sibling-owned and never pinned.
- evidence: planner seat `.ufo/scopes/nc5-guidance/r10-planner-seat.md`;
  plan `.ufo/scopes/nc5-guidance/r10-plan.md`; pin ledger
  `.ufo/scopes/nc5-guidance/r10-audit/pins.json`; verdict
  `.ufo/scopes/nc5-guidance/r10-verdict.md`; sync `--check` green on
  owned scope modulo sibling-owned `surface` digest.

## 2026-09-24 — nc5-guidance r11: post-census seam repairs (r26/r27 landings)
- decision: zero pin drift vs r10's verified HEAD (only docs r77–r82
  landed since `a89826b5d`; pinned files byte-identical). Three seams
  from swarm r26/r27 — landed before r10 shipped but after its census
  window closed — gained or corrected coverage: the observation
  paragraph's route precedence was stale (`task.route` first for
  working seats); r27 flipped it — `working` prefers the attested
  `lastDispatch.route` (the dispatcher writes `outcome.activeRoute` on
  every accepted launch; `task.route` stays the configured chain head a
  fallback hop leaves behind), `queued` keeps configured `task.route`
  authoritative over a stale `lastDispatch` record, non-string entries
  skipped. The collect join paragraph gains `MAX_REGISTRY_BYTES` (1 MiB,
  typed `invalid_registry`) on both the explicit `--registry` read and
  the default join — matching the wave authority's `loadRegistry` bound
  so an over-bound registry cannot join silently in collect while
  refusing every resume wave. The activity paragraph gains the
  `buildLabel` dedup rule: the appended activity dedupes against phase,
  `resumed`, the suspended reason, AND the reason's own 240-cp
  truncation (the activity channel's bound), closing the 240–280 window
  where an untruncated-reason dedup appended a visible duplicated head
  fragment.
- supersedes: none (claim repair + seam coverage, not a contract change).
- rationale: same class as r07–r10 — sibling landings drift §8.1/§9
  prose; pins cite committed bytes only. HEAD moved mid-round
  (`8b713e2e1` → `1ec07ab2e`, docs-only) — no code drift. AGENTS.md's
  lane-width paragraph self-contradicted (64-lane floor "enforced
  (`too_few_lanes`, `wave_too_wide`)" then "not gate-enforced");
  repaired to name `minLanes` 64 as the declared round floor and
  `waveMinLanes`/`waveMaxLanes` 16-100 as the gated wave band, matching
  run-logic §8.1. Record-only:
  `ufo-night-watchdog.sh` header duty-5 still says "max 3 repends per
  row per watchdog lifetime" (helper is per-row-key refusal-aware; body
  comment correct) — sibling-owned, re-flagged to L0.
- evidence: planner seat `.ufo/scopes/nc5-guidance/r11-planner-seat.md`;
  plan `.ufo/scopes/nc5-guidance/r11-plan.md`; verdict
  `.ufo/scopes/nc5-guidance/r11-verdict.md`; sync `--check` green on
  owned scope modulo sibling-owned `surface` digest; focused
  `node scripts/ufo-mission-activity.test.mjs` 5/5 green.

## 2026-09-24 — nc5-guidance r12: seal-justification repair + monitor recovery seam coverage
- decision: three stale/absent seams in run-logic §8.1 repaired against
  HEAD `861da8094`. (1) The blocked-successor seal justification was the
  pre-r28 claim "a `blocked` successor keeps its scope" — swarm r28
  (`ac887ec3d`, landed inside r11's census window) corrected the code
  comment: the watch's occupancy scan excludes blocked rows
  (`ufo-l0-watch.mjs:1088-1096`), so a respawn could land; the seal holds
  because recovery ownership is the monitor's (`:1163-1177`) — reopening
  would mint a second chain head. Prose now carries the corrected
  justification plus the operator-owned unrecoverable class. (2) The
  monitor's recovery seam was undocumented: `--repair` entails `--settle`
  (`ufo-l0-monitor.mjs:1421-1431`), healed rows are journaled BEFORE the
  queue publish through the fault-guarded accessor (`:1442-1459`), repend
  drains the whole journal outside the lock (`:1489-1516`), and
  `forgeSuccessor` (`:1094-1194`) mints fresh-root successors for
  torn/absent-receipt blocked rows with `iterationOutcome.kind` =
  `decision_missing` (never a fabricated `continue`), licensed only by a
  present non-empty report plus torn receipt or absent receipt under
  `acceptance_receipt_missing` — a valid receipt stays settle()'s job;
  dedupe is round-occupancy. (3) The statusline claim was stale: the hook
  never reads the sidecar — it spawns `ufo-sighting status [--lite]`
  through `node` (3s SIGKILL, 1 MiB stdout cap), shares the result through
  the 5s `statusline-cache.json` + `wx`-token lock with rename-aside
  steal, and gates render+cache on `isStatusEnvelope` (levels/phaseCounts
  objects + string hatch) — drifted output publishes CLOSED and is never
  cached (nc5-tooling r15). (4) Private `readBoundedFile` parity recorded:
  all copies now carry `O_NOFOLLOW|O_NONBLOCK` except
  `ufo-state-retention.mjs` (:195, :591 — `O_NOFOLLOW`-only; FIFO-wedge
  residual flagged to tooling).
- supersedes: none (claim repair + seam coverage, not a contract change).
- rationale: same class as r07–r11 — sibling landings drift §8.1 prose;
  pins cite committed bytes only. Planner's `m_sol6` route-mismatch claim
  rejected on direct read (isolated `config.yml:42` = `gpt-6-sol:high`,
  AGENTS.md row correct). Record-only cross-scope flags:
  `ufo-state-retention.mjs` missing `O_NONBLOCK` (tooling);
  `ufo-night-watchdog.sh` header staleness (still open);
  `docs/L2-L3-ROUTING.md` stale terminal-alias rows (docs);
  `ufo-l0-watch.test.mjs:912` stale comment (swarm); `.cursor/` unmanaged
  pair (mirror-map-owned decision).
- evidence: planner seat `.ufo/scopes/nc5-guidance/r12-planner-seat.md`;
  plan `.ufo/scopes/nc5-guidance/r12-plan.md`; verdict
  `.ufo/scopes/nc5-guidance/r12-verdict.md`; sync `--check` green on
  owned scope modulo sibling-owned `surface` digest; focused
  `node scripts/ufo-l0-watch.test.mjs` + `ufo-l0-monitor-hook.test.mjs`
  green.

## 2026-09-24 — nc5-guidance r13: swarm-hoist + receipt-gate + tick + queue seams
- decision: four undocumented seams in run-logic repaired against HEAD
  `6ab824d27` (owned paths unchanged since r12 `3881f3b96`; no sibling
  script/crate landings since verified base `af25ed7b2`). (1) §4.3 gains
  the schema-v2 template hoist (nc5-swarm r13): `spec.hoist` default
  `true` lifts the byte-identical `{{item}}` template into shared
  `taskCall.context`; compact tasks keep item/binding/reportDir/
  invocation inline; legacy expansion validated first at old precedence;
  all-or-nothing decision (`MAX_CONTEXT_BYTES` 64 KiB,
  `MIN_HOIST_SAVINGS` 512) with bypass reasons `disabled`/
  `template_invocation`/`template_marker`/`context_bound`/`no_savings`
  in `plan.compaction`; `savedBytes` is net wave delta, not per-seat
  `hoistedBytes`; hoisted `plan --emit-tasks` emits `{context,tasks}`
  (`ufo-swarm-wave.mjs:151,197-212,225,273,808-817,1062-1205,1785-1793`).
  (2) §8.2 item 6: `validate-receipt` qualified shape-only BY DEFAULT —
  `--iterate` gates `iteration.decision`, repeatable `--expected
  key=value` binds the six acceptance fields (malformed/unknown/
  duplicate → exit 64), and `--expected` equality never proves fleet
  acceptance; `create-receipt --out` atomic publish (tmp+fsync+rename+
  dir-fsync, refuses `-`/empty/`--*`) documented
  (`ufo-mission-result.mjs:2622-2708,2722-2745`). (3) §8.1 tail gains
  the tick verdict arms: `--fresh` (`fresh`0/`heartbeat_stale`1/
  `deadline`2), `--health` (`ok`0 all runners / `degraded`7 partial),
  runner faults never synthesize; ground handler accepts exactly four
  exact-schema ops (`health`, `chat`, `freshness_ping`, `path_ping`),
  `chat` never a completion proof; `protocol_error`4 vs socket-fault
  `unavailable`3 split (`the-tick-ping.mjs:15-41,153-159`;
  `ufo-ground-handler.mjs:90-150`). (4) §8.2 gains the queue-integrity
  seam: `validateQueue` schema + safe-integer `revision` <
  `MAX_SAFE_INTEGER`, per-row `validateQueueTask`, uniqueness across
  keys/runIds/sessionIds/resultPaths, dependency edges never
  self/dangle/cycle (archive-backed completed keys satisfied leaves;
  chain member on own resolved root = self-edge), typed attribution
  (`taskIndex` always, `queueRevision` when safe, `taskKey` only when
  minted-shaped), failed read → `QUEUE_INVALID` → `queue_invalid`,
  malformed input never mutates the queue
  (`fleet-dispatcher.mjs:398-413,4704-4813,4823-4851,9615-9626`).
- supersedes: none (seam coverage, not a contract change).
- rationale: same class as r07–r12 — sibling landings drift prose;
  pins cite committed bytes only. Planner seat's P5 (SKILL.md catalog
  trim) rejected: SKILL.md is the packaged operational digest whose
  §4.3-referenced workflow is the designed two-layer structure, not
  drift. Record-only cross-scope flags unchanged from r12:
  `ufo-state-retention.mjs` missing `O_NONBLOCK` (tooling);
  `ufo-night-watchdog.sh` header staleness (L0);
  `docs/L2-L3-ROUTING.md` stale terminal-alias rows (docs);
  `ufo-l0-watch.test.mjs:912` stale comment (swarm); `.cursor/`
  unmanaged pair (mirror-map-owned decision).
- evidence: planner seat `.ufo/scopes/nc5-guidance/r13-planner-seat.md`;
  plan `.ufo/scopes/nc5-guidance/r13-plan.md`; verdict
  `.ufo/scopes/nc5-guidance/r13-verdict.md`; sync `--check` green;
  focused `ufo-swarm-wave.mjs plan` hoist probe + `validate-receipt`
  `--iterate`/`--expected` probe green.

## 2026-09-24 — nc5-guidance r14: gate-tier + native-helper + drill-seam coverage
- decision: four undocumented seams in run-logic repaired against HEAD
  `30cc15900` (zero code drift since r13 verified base; docs-only commits
  on main). (1) §3 gains the `UFO_GATES` tier: `fast` default, `full` runs
  every stage, invalid exits 2; `gates-plan.mjs` selects `fleet`/`retention`
  groups from the touched-path set (worktree + untracked + ahead-of-
  `origin/main`, empty-tree fallback; `UFO_GATES_TOUCHED`/`--touched-file`
  override); guidance/docs/mirror paths ignored for selection; unreadable,
  explicitly empty, or unmapped touched set fails safe to all groups;
  unselected stages record `SKIP` under full label; `fleet` group named
  (`fleet-dispatcher`/`fleet-ledger-read`/`fleet-ledger-rotate` tests +
  `fleet-selfheal-verify.mjs` e2e fixture harness); `dev-verify.sh` exec
  alias (`gates.sh:54-61,586-601,699-715,749`; `gates-plan.mjs:20-46,95-183`).
  (2) §4.2 gains the shared native helpers: `ufo-native-names.mjs`
  derivations (`seatId` `role:N`, `seatLabel` `role-NN`,
  `canonicalDispatchName` `u<sha256(runId)[:8]>-role-NN`, `sha256:`-
  prefixed correlation/unavailability groups; `NATIVE_CONTRACT_FILES`
  member `native_contract.rs:80`; Rust twin `native_seats.rs`) and
  `ufo-credential-screen.mjs` two-tier screen (narrow
  `containsCredentialShape` mirror of `detail_contains_credential` in
  `native_admission_text.rs` + wider `containsSensitiveShape`), explicitly
  NOT contract-hash-bound — parity by convention and test
  (`ufo-native-names.mjs:38-81`; `ufo-credential-screen.mjs:1-54`).
  (3) §8 tail gains the drill harness mechanics: charter-sign `drills`
  stage is unfiltered `node scripts/ufo-drills.mjs` (`main.rs:965-967`),
  distinct from the `gates.sh` battery; six executors (`self-iter`,
  `sync-check`, `cargo-test`, `node-test`, `judge-handoff`, `shell`);
  statuses `wired`/`pending-mechanism`/`referenced`; coverage ratchet
  (no placeholder class may outnumber wired; unfiltered runs only);
  `--only` diagnostic skips the invariant and writes `summary-<id>.json`;
  `--list`/`--self-test` read-only; pending-without-reason and
  unresolved-references fail closed at load (`ufo-drills.mjs:4-33,86-117,
  1493-1600,1680-1715`). (4) §3 names `fleet-selfheal-verify.mjs` inside
  the fleet group (folded into (1)).
- supersedes: none (seam coverage, not a contract change).
- rationale: same class as r07–r13 — sibling landings drift prose; pins
  cite committed bytes only. Planner seat converged with inline data walk.
  Rejected: `nc5-seat-watch.sh` promotion (nc5-only occupancy logger, not
  canonical machinery); `probe-redact.mjs` dedup (deliberate standalone
  fixture copy); CHANGELOG/run-logic bulk deletion (no proven-safe
  duplicate). Record-only cross-scope flags: `ufo-credential-screen.mjs`
  absent from `NATIVE_CONTRACT_FILES` (crates/tooling owner);
  `native_admission_text.rs:42` comment still names
  `collect-omp-native-handoff.mjs` as `containsSensitiveShape` home
  (crates); `sync-ufo-contracts.mjs:1372-1385` stale `drills.enabled`
  diagnostic (tooling); plus r13's carried flags.
- evidence: planner seat `.ufo/scopes/nc5-guidance/r14-planner-seat.md`;
  plan `.ufo/scopes/nc5-guidance/r14-plan.md`; verdict
  `.ufo/scopes/nc5-guidance/r14-verdict.md`; `gates-plan.mjs` probes
  (guidance→none, dispatcher→fleet, unmapped/empty→both);
  `ufo-drills.mjs --list` (51 wired / 11 pending / 5 referenced);
  `ufo-native-names.mjs` probe (`executor:2`/`executor-02`/
  `ucae0aa92-executor-02`); sync `--check` green.

## 2026-09-24 — nc5-guidance r15: ledger-sibling seam coverage + one-claim debloat
- decision: two repairs against HEAD `ff0879a0a` (zero owned-path drift
  since r14; 84-pin census clean). (1) §8.2 gains the fleet lifecycle
  ledger sibling seam: `.ufo/fleet-ledger.jsonl`
  (`UFO_FLEET_LEDGER_PATH` under `beneath(UFO_STATE, …)`, schema
  `ufo-process-lifecycle-v1`) appended under the ledger lock by
  `appendLifecycleEvents`; `fleet-ledger-read.mjs` is the dispatcher's
  preferred streaming reader (dedupe-in-pass, per-segment coverage,
  pre-dedupe `processIndex`, no total-size cap — superset shape
  normalized, failure degrades to the inline reader with typed
  `ledger_*_module_error` telemetry); `fleet-ledger-rotate.mjs` the same
  optional-sibling class invoked `prelocked`;
  `UFO_FLEET_DISABLE_LEDGER_MODULES=1` forces inline paths;
  `ufo-state-retention.mjs` statically imports `loadLifecycleLedger` for
  fail-closed `readLedgerActivity` (`fleet-dispatcher.mjs:283-330,
  511,995-1003,1987-1998,2125`; `fleet-ledger-read.mjs:2-76`;
  `ufo-state-retention.mjs:74,746-749`). (2) debloat: the `isPlainObject`
  paragraph's verbatim restatement of the dispatcher import-ban +
  parity-source rule (already global at the leaf convention) trimmed to
  the family attribution alone — every other restatement carries
  family-specific facts and stays.
- supersedes: none (seam coverage + duplicate-claim removal).
- rationale: pin census found zero drift — no manufactured repairs.
  Rejected: `omp-wave-context.mjs` citation (ZERO production importers —
  only `tests/omp-wave-context.test.js`; the wave planner's own
  `spec.hoist` is the live mechanism — naming it would be a false claim;
  record-only flag to swarm); `primeagent-{recovery-assess,
  refinement-ledger}.mjs` (primeagent-owned mission CLIs, no L0 caller);
  `probe-token-plan-{kimi,models,shared}.mjs` (operator diagnostic probes,
  deliberately uncited per probe-redact precedent); broad refrain
  deletion (family-specific attributions are load-bearing).
- evidence: planner seat `.ufo/scopes/nc5-guidance/r15-planner-seat.md`;
  plan `.ufo/scopes/nc5-guidance/r15-plan.md`; verdict
  `.ufo/scopes/nc5-guidance/r15-verdict.md`; 84-pin HEAD census clean;
  `git show HEAD:` byte verification of every ledger claim; sync
  `--check` green.

## 2026-09-24 — nc5-guidance r16: seal-mechanism inversion repair + 3 stale pins + false privacy claim
- decision: three claim-fidelity repairs against HEAD `33be4d428`
  (only post-r15 landing is primeagent r24, outside owned paths).
  (1) §8.1 respawn-arm prose inverted the seal mechanism: a successful
  enqueue ARMS the seal synchronously (`done` + `donePath` on the
  dispatcher's admission answer, `ufo-l0-watch.mjs:1259-1260`), then the
  tick's deferred `readQueue()` confirms or releases it — visible
  successor keeps the seal, absent releases (`seal_pending`), read fault
  leaves the armed seal (`seal_check_failed`); the net guarantee
  (accepted-but-lost never permanently seals) is unchanged. (2) Three
  stale pins: `occupied.push(canonicalScopes(...))` moved to
  `ufo-l0-watch.mjs:1106` (holeCandidates held-row loop) and `:1247`
  (respawnHole post-enqueue); `successorByResultPath` index pinned to
  its declaration `:1084` (`:1072` was `holeCandidates`' def line).
  (3) "All five are module-private: not exports" was false — the five
  eb147b51 dedup patterns are module-internal, but
  `canonicalScopesOverlap` and `holeCandidates` are exported watch test
  seams from the r29 suite de-mirroring.
- supersedes: none (claim repairs only).
- rationale: planner seat + L1 construct-level census found the drift a
  range-only pin check misses (all pins were in-range; three named the
  wrong construct). Rejected: new seam codification (r29 exports are
  test seams, not leaf-family consolidations; primeagent r24 `--json`
  CLI has no L0 caller); debloat (zero verbatim duplicates this round);
  `omp-wave-context.mjs` citation (still zero production importers).
- evidence: planner seat `.ufo/scopes/nc5-guidance/r16-planner-seat.md`;
  plan `.ufo/scopes/nc5-guidance/r16-plan.md`; verdict
  `.ufo/scopes/nc5-guidance/r16-verdict.md`; every edited clause
  verified against `git show HEAD:` bytes; sync `--check` green.

## 2026-09-24 — nc5-guidance r17: §8.1 pin re-points (verified, landed by nc5-final r01)
- decision: nine stale `ufo-l0-watch.mjs` pins in the §8.1 tail re-pointed
  to the constructs' current lines: `noteInvalidRunId` collapse pair
  → `:309`/`:313`, `childFault` clip → `:544`, readState null-as-corruption
  loop → `:407`, `MAX_LOG_BYTES` alias → `:451`, hole-verdict
  `expectedReceiptBag` → `:819`, whip action line → `:1018`,
  `successorByResultPath` declaration → `:1144`, `canonicalScopesOverlap`
  def → `:204`, `occupied.push(canonicalScopes(...))` → `:1166`/`:1307`.
  A construct-level census over all 86 `file:line` pins in
  run-logic.md/SKILL.md/AGENTS.md/agents/*.md found zero additional stale
  pins (remaining flags were prose-word extraction false positives).
- supersedes: the pin numbers it replaces.
- rationale: r17 was halted mid-round by the nc5→nc5-final operator
  supersession before the repairs were committed; every edit was
  verified against `git show HEAD:` bytes by both the r17 attempt and
  nc5-final r01, and landed by the closing mission.
- evidence: `.ufo/results/nc5-guidance-r17.md`;
  `.ufo/results/nc5-final-guidance.md`; byte verification of every
  pinned line; sync `--check` green.

## 2026-09-24 — nc5-final-guidance r01 (closing): primeagent assimilation seam documented + lane-branch generalization
- decision: (1) the AGENTS.md hooks bullet now inventories all three
  deployed `.omp/hooks/pre/` hooks, adding the primeagent-assimilation
  session hook (same-mission/different-run fleet sessions receive a
  bounded titles-only refinement-ledger digest on the `pa-ledger`
  status segment via the typed
  `@ufo/substrate-runtime/primeagent-refinement.mjs` digest API; writer
  runs get a count-only status; unbound/chain-invalid stores a typed
  refusal; foreign or non-fleet sessions get nothing; the digest is
  data under the artifact-trust rule, never an instruction source).
  (2) the commit-trail lane-branch spelling generalizes to
  `<fleet>/<lane>` (e.g. `nc5/<lane>`, `nc5-final/<lane>`) from the
  fleet-specific `nc5/<lane>`. Consolidation audit: every origin lane
  branch's patches are on origin/main; unlanded local lane branches and
  worktrees are unaccepted or superseded and stay out of the ship path.
- supersedes: none (documentation of deployed state).
- rationale: the hook loads natively into every session in this cwd
  (fleet L1 and L2 alike) yet only `docs/PRIMEAGENT-ASSIMILATION.md`
  named it; canonical guidance must own the seam its seats traverse.
  The ledger's r20–r24 entries are internal to the ledger CLI (no L0
  caller, uncited as r16 decided); r25's uncommitted status-verb
  candidate stays unclaimed until accepted by its own frontier.
- evidence: hook bytes `.omp/hooks/pre/primeagent-assimilation.js`
  (session_start intake :294-313); policy floor
  `config/primeagent-assimilation.json`; classifier
  `packages/substrate-runtime/src/primeagent-refinement.mjs`
  (roles :92-94); `.ufo/scopes/nc5-final-guidance/r01-plan.md`;
  r01 verdict; sync `--check` green.
