# UFO-FSD — Run Logic

> Provenance: tracked local UFO-FSD contract, revised 2026-09-15.
> The original ignored `.ufo/local-dispatch/l1-speedrun-24h-three-prompts.md`
> is unavailable and has no Git history. The three guidance themes below are
> an evidence-backed semantic reconstruction from tracked launch and handoff
> material; they are not quoted or claimed byte-identical to the missing file.

Language-neutral contract for the one canonical runtime. Framework: UFO-FSD.
Posture: godspeed. Planner stance: wwkd.

Dispatch doctrine: OMP-only.
`automaticSubstrate` stays `omp`; the other six installed adapters remain
compatibility surfaces, never automatic fallback transports. Native `kimi`
and Sekhmet/L3 are not selected. The frozen per-seat route table is owned by
the global OMP config (`~/.omp/agent/config.yml`); the launcher resolves it
at dispatch and `omp-seat-routing.json` mirrors it into the compiled
runtime (seat→alias summary in `AGENTS.md`; history in CHANGELOG.md). §6
states the routing invariants; this header restates no pins.
Fleet dispatch standard: NC2/`nightcall` — one L1 per mission, at most 32
live L1s globally, the canonical nightcall overlay as the enqueue default,
and the global alias table as the only routing authority (§8.2).
Assignments use English natural-language output and unchanged JSON contract
keys; no model-specific reasoning-language instruction is injected.
Exactly one terminal `| godspeed` per assignment; fail-closed on drift.
One authored Godspeed source: `ssot/godspeed-core/directive.md`. Host and
packaged copies (e.g. `references/godspeed-core/directive.md`, repo-root
`godspeed-core/directive.md`, the bundled crate copy, and every packaged
skill target) are checked generated mirrors, not a second authority.

Load authored guidance once per unchanged session. A digest-bound assignment's
canonical directive prefix is already loaded posture; do not expand it from a
second skill or mirror. On fleet dispatch one leading `/skill:ufo` invocation
precedes overlays and the one directive prefix; omp-native assignments carry
no `/skill:ufo` and must begin with the directive bytes themselves. Mirror parity
is a sync check, not repeated reading.

## Operator guidance themes (reconstructed)

These identifiers are exact and durable:

1. **`phase0_lkg_gate`** — compare the local tree with its last-known-good
   base, retain only non-regressing moves, then pass contract, compile, boot,
   and probe checks before round 1.
2. **`same_essence_substrate_shape`** — keep runtime, judge, Pareto, telemetry,
   reroute, and stop semantics identical. Only command and packaging shape may
   differ across `omp`, `kimi`, `codex`, `cursor`, `opencode`, `grok`, and `devin`.
3. **`reroute_not_respawn`** — a local route failure keeps the same logical
   lane identity, prompt, and cache. It never mints a replacement logical
   agent or switches runtime, judge, or substrate.

The runtime exposes and tests exactly these identifiers.

---

## 0. Invariants

- **I1 — One judge.** One local L1 owns the run; only the canonical Rust
  runtime emits judgment. A second L1 or judge is rejected at the config
  layer (`second_judge` dies on `deny_unknown_fields` serde, drill
  `d-i1-second-l1`); no adapter-level guard exists — the drill records that
  spec-vs-implementation gap.
- **I2 — The L1 works.** L1 plans, executes, integrates, and submits evidence
  to Rust. It never waits for a specialist to become the orchestrator.
- **I3 — Degrade honestly.** One unavailable lane cannot kill a sound wave.
  Other lanes continue, and the failed lane continues on another implemented
  local route when one exists. If every lane is unavailable, halt with
  evidence; never manufacture convergence or a proposal.
- **I4 — Failure is data.** Route failures and unavailable lanes are typed
  telemetry with identity, cause, source route, destination route, and round.
- **I5 — Cache on dispatch.** Every logical lane receives the current cache.
  A child process is transport, not a new lane identity.
- **I6 — Reroute, do not respawn.** Recovery keeps lane identity and cache.
  A replacement logical agent is never created for the same work.
- **I7 — Runtime identity is immutable.** The run stays in
  `crates/ufo-core-runtime`, with one judge and one selected substrate.
- **I8 — Honesty outranks progress.** Zero accepted proposals is convergence
  only after a complete, sound round. No progress theater.
- **I9 — Tracked authority wins.** Canonical guidance and runtime source beat
  generated artifacts and mirrors. Drift halts and names both paths.
- **I10 — Local-first ship.** A target is verified only when its local command
  surface is invoked. Publishing and deployment remain operator-owned.

---

## 1. State

```
RunState {
  token:         RunToken
  task:          String
  runtime:       "crates/ufo-core-runtime"
  judge:         "single-local-l1"
  substrate:     omp | kimi | codex | cursor | opencode | grok | devin
  axes:          RoundAxisSet   // declared per round (fleet) or frozen at
                               //   launch from config.axes (judged native)
  baseline:      ScoreVector
  round:         Int
  lanes:         Map<LaneIdentity, Lane>
  cache:         RoundCache
  telemetry:     Vec<Event>
  reroutes:      Vec<RerouteRecord>
  contract_sync: ContractSyncReport
  stop:          RUNNING | SATURATED | BUDGET_HALT | BLOCKED
}

Lane {
  identity: LaneIdentity       // durable tuple, spec 11 §4:
                               //   logical_lane_id = <run_id>/<role>/<instance>
                               //   frozen_scope_hash    — distinguishes repeated roles
                               //   native_agent_id      — per actual spawn (OMP)
                               //   attempt_id           — per try on any route
                               //   wave_token           — per dispatch (spec 02)
  role:     SpecialistRole
  route:    LocalRoute
  allowed_routes: Vec<LocalRoute>
  state:    READY | UNAVAILABLE
  cache:    CacheRef
}
```

Field names are contractual, not literal struct members: `runtime`/`judge`
are pinned constants, `cache`/`telemetry`/`contract_sync` are digest fields
and `.ufo` artifacts rather than stored loop state, and lane availability is
computed per dispatch — a failed lane either
recovers on its typed chain or reports `UNAVAILABLE`. `cache` is physically
a chain of bounded round digests (`ufo-round-digest-v1`,
`.ufo/rounds/<runId>/r<NN>-digest.json`, bound `rounds.digest_max_bytes`,
default 32768, single-sourced in the runtime) plus hash references; raw
artifacts are re-fetched by hash on demand. Digests are the only
guaranteed carry-forward — every lane still receives prior-round context
(I5), as bounded digests and pointers, not raw accumulation.
`stop_reason` uses `running | round_cap | saturated | blocked` plus
`interrupted` (SIGINT/operator halt checkpointing a live round, spec 03),
`honesty_brake` (actual or projected budget exhaustion, spec 03 §4), and
`authority_boundary` (membrane-touching accepts awaiting operator sign-off,
spec 06) — all three emitted; `budget_halt` is the `LoopOutcome` name for
`round_cap`. Mapping: `stop` is the loop-state field; `loop_stop` (§8) drops `running`.
`stop_reason` is the checkpoint vocabulary, not a telemetry event.
The selected substrate is state, not a dispatch hint. It cannot change during
resume or reroute.
Within the loop this holds: resume restores the checkpointed substrate and
rejects route-provenance changes, and reroute stays on the same-substrate
chain. The Sighting mission-manifest `substrate` field is operator-
overridable at `resume` and is display/dispatch metadata, not loop state.

---

## 2. Boot and identity pin

```
fn boot(goal, substrate) -> RunState:
    assert substrate in [omp, kimi, codex, cursor, opencode, grok, devin]
    authorities = read([
        canonical_ufo_skill,
        canonical_run_logic,
        canonical_agent_cards,
        core_runtime_source,
        local_lkg_reference,
    ])
    assert authorities.operator_guidance == [
        phase0_lkg_gate,
        same_essence_substrate_shape,
        reroute_not_respawn,
    ]
    assert exactly_one_runtime("crates/ufo-core-runtime")
    assert exactly_one_judge("single-local-l1")
    state.substrate = substrate
    freeze(state.runtime, state.judge, state.substrate)
    return state
```
the concrete mechanism is the contract-sync mirror check plus the provenance
assert; uniqueness holds by construction (pinned constants), and the
guidance triple is emitted as `operatorGuidanceThemes` and asserted by
`scripts/smoke.sh` (the mutation-smoke battery's canonical-guidance check).

### 2.1 `resume_continuity_v1`

Before any run-state, pane, or child mutation on resume, the exact native
session MUST be selected explicitly by its stable native identifier; recency,
ordinal selection, and `--continue` MUST NOT select it. Observe the selected
session's agent identity and canonical cwd/project, and require both to match
the frozen L1 mission. Missing evidence or any mismatch fails closed with zero
mutation. A resumed session retains its existing role and MUST NOT promote a
planner or any other subordinate to L1.
Enforcement on the fleet OMP path is the dispatcher's argv guard
(`argvContainsForbiddenSelector` rejects `--continue`/`--twin` in the
child argv) plus `ufo-sighting resume`'s exact-identity binding
(`resolveExactMission` fails `IDENTITY_MISMATCH` on runId/sessionId
mismatch; `RESUME_COMPLETED`/`RESUME_LIVE`/`RESUME_UNSUPPORTED` gate the
row state). The `omp` native path verifies at dispatch preflight (exact
`--resume` session UUID plus session-record attestation; `--continue` is
rejected) and `opencode` verifies via `--session` plus export attestation.
The other five substrates carry no verified native resume; the machine map
records them as policy-assumption-only. No dedicated planner→L1 promotion
guard exists — the exact-session binding is the mechanism that keeps a
resumed session in its frozen role.

---

## 3. Phase 0 last-known-good gate

Phase 0 runs once before round 1.

```
fn phase0(state):
    diff = compare(local_tree, local_lkg_reference)
    review_each(diff, rule = improves_one_axis_and_regresses_none)
    reject_ambiguous_or_regressing_changes()

    contract_sync = verify_exact_guidance_and_agent_mirrors()
    require(contract_sync.ok)

    require(local_compile())
    require(local_boot())
    probe = require(local_probe(state.substrate))
    record(state.telemetry, Phase0Passed{contract_sync, probe})
```
The `local_lkg_reference` diff steps are L1 doctrine — no scripted baseline
ships in the repo, and `local_compile`/`local_boot`/`local_probe` are
doctrine too: the canonical runtime's phase-0 report discharges only the
mutation smoke battery (`ufo gates` runs `pareto_gate_mutation_smoke` into
`.ufo/rs-paper-gates.json`; `ufo self-iter` re-runs it before iterating and
writes the `phase0` block into `.ufo/rs-self-iter-report.json`) while
`scripts/gates.sh` carries the operator battery (wall probes →
`contracts:check` → fleet selfheal/ledger/retention suites → post-run
`contracts:check`) under the `UFO_GATES` tier (`fast` default, `full`
runs every stage; an invalid value exits 2 before any stage). In `fast`
mode `scripts/gates-plan.mjs` selects the conditional suite groups
(`fleet`, `retention`) from the touched-path set — worktree diff,
untracked files, and commits ahead of `origin/main` (or the empty tree
when no upstream exists), overridable by `UFO_GATES_TOUCHED` or
`--touched-file`. Guidance/docs/mirror paths are ignored for selection
(the always-on `contracts:check` already covers them); an unreadable,
explicitly empty, or unmapped touched set fails safe to all groups, and
every unselected stage records `SKIP` under its full label — never a
phantom `PASS`. The `fleet` group runs `fleet-dispatcher.test.mjs`,
`fleet-ledger-read.test.mjs`, `fleet-ledger-rotate.test.mjs`, and the
`fleet-selfheal-verify.mjs` end-to-end fixture harness (a typed `SKIP`
on retired pre-swap evidence, never a pass); `dev-verify.sh` is an exec
alias into the same runner. Emitted telemetry is the `phase0` block
`{contracts, gates, provenance}` of `.ufo/rs-self-iter-report.json` plus
the `.ufo/contract-sync/r00.json` record — there is no `Phase0Passed`
event.

No round starts from a broken or ambiguous base. Fix forward, rerun Phase 0,
then enter the loop.

---

## 4. Round loop

Axes are dynamic on the fleet-mission path: the L1 declares the round's
axis set in its WWKD plan per round, informed by the planner stance or
seat; the set is externally visible, stable within that round, free to
evolve between rounds, and never frozen at Phase 0. On the judged native
path the axis set is frozen at launch from `config.axes` (the runtime's
auto-written round plan prints it verbatim — "Axes are frozen before this
plan"), and a fleet L1's per-round axis declarations govern its own
unjudged rounds, never the frozen native contract. Every round then has
the same order.

```
fn run(state):
    phase0(state)
    loop:
        boundary = pre_dispatch_boundary_stop(state, state.round + 1)
        if boundary != CONTINUE:
            return boundary              // zero lanes dispatch for this round

        state.round += 1
        plan      = wwkd_plan(state)
        outputs   = parallel_dispatch(state.lanes, plan, state.cache)
        distilled = distill(outputs)
        verdict   = canonical_rust_pareto_judge(state.baseline, distilled)

        advance_frontier_only(verdict.accepted)
        persist(state, outputs, verdict)

        outcome = post_round_stop_condition(state, verdict)
        outcome = seal_if_membrane_accepts(outcome)
        outcome = blocked_audit_if_running(outcome)
        match outcome:
            SATURATED         -> return SATURATED
            BUDGET_HALT       -> return BUDGET_HALT
            HONESTY_BRAKE     -> return HONESTY_BRAKE
            AUTHORITY_BOUNDARY -> return AUTHORITY_BOUNDARY
            BLOCKED           -> return BLOCKED
            CONTINUE          -> append_round_digest_and_continue()
```

Rejects, route failures, and no-proposal results remain in the cache. The next
round consumes them; the current round never changes its frozen contract.

### 4.1 Lane execution

```
fn lane_execute(state, lane, task):
    result = lane.run_current_route(task, lane.cache)
    match result:                        // RouteAttemptOutcome (state.rs)
        Proposal(output) -> return output
        NoProposal(note) -> return NoProposal(note)
        CapacityFailure(cause) -> {
            record(state.telemetry, cause)
            // only capacity classes advance: usage_limit | rate_limit |
            // model_unavailable; other typed failures never probe a route
            next = cause.is_capacity_class()
                ? next_implemented_local_route(lane)
                : none
            if next is none:
                lane.state = UNAVAILABLE
                return LaneUnavailable(cause)
            return reroute_same_identity(state, lane, task, next, cause)
        }
        Unavailable(cause) -> {
            lane.state = UNAVAILABLE
            record(state.telemetry, cause)
            return LaneUnavailable(cause)
        }
        ProcessExit(cause) -> {
            record(state.telemetry, cause)
            if lane.is_critical && retry_remaining(lane):
                return retry_same_identity_same_route(state, lane, task)
            lane.state = UNAVAILABLE
            return LaneUnavailable(cause)
        }
        LaneTimeout(deadline) -> {
            // terminal cause = time; elapsed = ended_ms - started_ms
            record(state.telemetry, lane_timeout{...})
            // never a capacity event: the route chain does not advance (I6)
            if lane.is_critical && retry_remaining(lane):
                return retry_same_identity_same_route(state, lane, task)
            lane.state = UNAVAILABLE
            return LaneUnavailable(lane_timeout)
        }
```

An unexpected process exit is not disguised as a reroute. The remaining wave
continues; an all-lane failure aborts the run with a hard error (exit 1),
not the `BLOCKED` stop value.

Deadlines are per seat class, declared in
`nativeProfiles.omp-native-v1.deadlines`: main to `orchestratorMs`, planner to
`plannerMs`, distiller to `distillerMs`, labrat to `labratMs`, the thinking
proposal roles to `thinkingMs`, the mechanical proposal roles to
`mechanicalMs`. `elapsed = ended_ms - started_ms` is compared against the
class bound; an exceed is a terminal cause of time (`LaneTimeout`), recorded
as `lane_timeout` telemetry and never as a capacity event — the route chain
does not advance (I6). Re-charter D1a grants a critical seat (Main, planner,
distiller, labrat — `native_schema.rs` `is_critical`; the probeParent is a proposal
seat, not a critical seat) exactly ONE same-identity same-route retry on
`LaneTimeout` or `ProcessExit`; a second terminal failure makes the round
invalid for judgment while collection and provenance continue, and never
suppresses later reachable dispatch or its evidence. Implementation status:
the fixture loop grants the D1a retry to the critical distiller seat only
(`dispatch_critical_distiller_seat`); the native-seat D1a admission is
deferred (`native_telemetry.rs` `reject_critical_lane_timeout`). A non-critical seat reports `UNAVAILABLE`,
the wave continues, and its late output is inadmissible (doctrine — the
inadmissibility is enforced by collection pairing, not a dedicated gate).

Recovery actions beyond capacity advance are typed by the failure-action
matrix (`nativeProfiles.*.recovery`, spec 11): temporary classes
(`timeout`, `tool_failure`, `unknown`) take a bounded same-route retry
(`temporaryRetry.maxAttempts` total attempts, then `UNAVAILABLE`);
`authentication`/`permission_denied` report `authorization_unavailable`
with no retry and no hop (auth is not capacity); `invalid_request` is
`UNAVAILABLE` with no retry; capacity classes hop or retry per the chain;
`ProcessExit`/`LaneTimeout` keep the D1a rule above. Account-level
backpressure (`recovery.backpressure`): `herdThreshold` capacity failures
in one route-provider domain inside `herdWindowMs` cool the domain for
`domainCooldownMs` — lanes into a cooled domain record typed
`domain-cooldown` unavailability (waiting is an authorized action, never
a hop-storm); `maxConcurrentPerDomain` 0 is unlimited. Every action is
telemetry. No row authorizes a substrate, runtime, or judge change (I7),
a replacement identity (I6), or a weakened checker (I9).

### 4.2 OMP native evidence membrane

OMP owns native agent transport; Rust remains the only judge. The OMP host
builds a typed handoff — `omp-native-v2` by default, on the admission-profile
split below — after its task wave:

```
NativeRoundHandoff {
  profile, run_id, round, substrate, concurrency,
  concurrency_semantics, axes, axes_hash, contract_hash,
  contract_root, config_digest,
  proposal_seats: [NativeProposalSeat], probe_parent,
  agents: [NativeAgentProvenance],
  proposals: [NativeProposal],
  integrated_candidate, candidate_digest, candidate_receipt,
  baseline, provenance, telemetry,
  // additive OPTIONAL fields by profile (v1 carries none):
  plan_digest, acceptance_criteria,        // v2+ (A-07)
  effective_launch: [EffectiveLaunch],     // v2+ (spec 12)
  attempt_ledger, dispatch_attempts,       // resilient only (specs 10/11)
}
```

`scripts/run-omp-native-trial.mjs` requires canonical mirrors to match before
creating trial state, snapshots the Rust-computed contract hash, creates full
prompt artifacts, and invokes one interactive OMP Main by default. Explicit
headless and preparation-only paths never silently replace a failed visible
launch. The interactive Main shuts down after its final artifact and settled
tasks; the host then collects, judges, persists the outcome and retires the
pane. A stopped process or retired pane alone is not an admitted result.
Provider admission is whatever the fd-bound global OMP snapshot declares —
the launcher carries no provider-name allowlist (a launcher-side table
vetoed globally-declared routes), and substrate identity is enforced by
the substrate field, never by a provider table.
`scripts/ufo-sighting` and its hash-bound `.mjs` module family own the attached
UFO Sighting terminal, pane registry, exact layout, and independent twin launch
membrane. They add no judgment, orchestration, provider, or credential layer.
`scripts/collect-omp-native-handoff.mjs` accepts only current-user,
non-symlink files bounded by declared run and session roots; rejects
launch/current contract drift — the launch contract hash and, when
`config/ufo.json` is present under the contract root, a re-hash against the
launch config digest. Role routes are bound to the generated global
seat-routing mirror (`verifyLaunchSeatRouting` against
`omp-seat-routing.json`), not re-pinned from `ufo.json` — the canonical
profile config no longer declares seat routes.
It snapshots OMP JSONL transcripts into a normalized evidence copy (reused
task call ids are uniquified and oversized uninspected fields are truncated
to the judge's 128 KiB line bound before hashing); extracts observed route,
failure, successful task-yield, actual spawn identity, and timing evidence;
pairs each successful task call with the spawn records in its task result;
screens failure details for credential-shaped data; screens proposal and
report artifacts for override-shaped patterns
(`membrane.screening.classes`: canonical directive bytes inside an
artifact, terminal markers, judge-addressed imperatives, assignment-shaped
headers, and directive-looking task data) and attaches typed
`screening_flags` — flags are evidence surfaced in the verdict, never
auto-rejection, and artifact content never modifies contract, axes,
routes, or judgment; and emits the typed
handoff. The collector synthesizes `lane_failure` and
`correlated_unavailability` telemetry itself; the manifest `telemetry`
field must be empty at launch — lane failure events are emitted from
observed transcript evidence, never carried in the manifest.
None of these scripts judges. Assistant-response provider/model presence
is judge-parity (`Option<&str>`): an empty string is present-but-incomplete
evidence, so `("x","")`/`("","m")` die at collection with the seat named
rather than emitting a handoff the judge must reject; `argv_sanitized`
entries are screened by the wider sensitive-shape gate, not the narrow
credential mirror; and evidence files persist only after every die-capable
check has passed — the writes are `O_EXCL`, so a late die would burn the
output directory for any retry.

The collector asks the existing Rust runtime's `receipt-digests` command for
typed baseline, axes, and survivor-set hashes through bounded JSON stdin.
Rust owns structural serialization; JavaScript hashes only exact artifact
bytes. Digest generation is not admission: `judge-handoff` independently
recomputes and validates the receipt before judgment.

`skills/ufo/SKILL.md` owns the level vocabulary: Main is L1; every OMP
task/Agent Hub specialist descendant, including the depth-2 labrat, is L2;
only Sekhmet sparks are L3. Native parentage below therefore uses explicit
depths 0, 1, and 2 rather than treating depth as a level number.

The Rust `judge-handoff --input <path>` gate fails closed unless all of these
hold:

- one Main L1 orchestrator at depth 0; one depth-1 planner that completes
  before the proposal wave starts; Rust remains the judge;
- one frozen batched proposal wave of 6–16 depth-1 seats drawn from the
  ten-role proposal taxonomy; the launcher default is all 16 seats;
- `scout`, `reviewer`, `critic`, `connector`, `sentinel`, and `executor` each
  hold at least one mandatory seat; the default also includes
  `mutation-tester`, `revenger`, `simplifier`, and `scribe`; repeated roles use
  contiguous instances with distinct frozen assignment scopes and hashes;
- exactly one depth-2 `labrat`, parented by the frozen executor
  `probe_parent` — the handoff field for the dispatch seat `probeParent`,
  which the launcher designates as the first executor seat in blueprint
  order — and contained within that executor's interval; no other
  descendant;
- Main successfully spawns the planner, every frozen proposal seat in one
  batched call, and distiller; `probe_parent` successfully spawns exactly
  labrat; every other seat spawns zero tasks; non-spawning rejected tool calls
  do not create agents;
- one depth-1 distiller starts after the proposal wave settles and
  completes;
- the complete topology contains `proposal_wave_size + 4` seats and never
  exceeds 20;
- concurrency is in `1..=32`, counts live children including waiting parents
  and descendants, and reserves one descendant slot:
  `concurrency >= proposal_wave_size + 1`;
- observed proposal overlap is positive; the
  `min(proposal_wave_size, concurrency - 1)` upper bound is implied by the
  concurrency precondition above and needs no separate check;
- every actual agent id, job id, dispatch name, parent, depth, assignment,
  transcript, artifact, hash, status, interval, requested model, resolved
  model, fallback flag, and evidence kind is present and internally
  consistent; the labrat id is executor-qualified;
- every completed non-Main transcript binds exactly one OMP task `yield`
  call, which must succeed; its result timestamp is the seat's settlement
  endpoint even when a later process-disposal `session_exit` exists; the
  collector also requires the adjacent nonempty completion artifact before
  producing the handoff;
- every effective spawned assignment byte-matches the launcher-written
  canonical assignment and its SHA-256; only one task-call terminal newline
  may be normalized by OMP before the successful spawn result;
- every assignment begins with the canonical directive bytes, appears in its
  hashed OMP transcript, and contains exactly one terminal `| godspeed`;
- the project OMP skill and used agent cards are byte-identical mirrors, while
  `contract_hash` binds canonical guidance, routing, collector/launcher,
  attached entry point, Rust execution profile and judge source, and CLI
  source;
- the handoff freezes each requested model to the compiled canonical route
  (the collector binds the hash-bound launch manifest to the same routes);
  every transcript
  contains exactly one session envelope, one primary `model_change` (any
  further `model_change` must be a capacity-failure-justified fallback
  switch), the effort event matching that hop's declared effort suffix
  (never a clamped or assumed setting — the §6 effort rule types a
  clamped or unobservable setting as `effort_unverifiable`), and at least one served assistant
  provider/model observation; every non-Main transcript additionally
  contains exactly one `session_init` whose `resolvedModel` exactly echoes
  the full requested route including effort;
- Main selects the default global L1 alias (`missionFormat.l1Alias`,
  `@m_daybreak`), resolving to `openai-codex/gpt-daybreak-blue-latest:max` at
  max effort, and uses `extendedContext=true`; the 1,000,000-token `l1Context`
  catalog is capability metadata, not a gate on the configured Main, and no
  project route exception exists. Its fallback chain — one hop,
  `stepfun/step-5-preview:high` — advances only on typed capacity failure
  and never silently changes models;
- every L2 role requests its pinned route from the global OMP seat table
  (§6 routing invariants; seat→alias summary in `AGENTS.md`; history in
  CHANGELOG.md) — resolving to the base model id at the declared effort
  with the typed fallback chain. Repeated roles use the same pinned route.
  Each `model_change` has a false fallback flag. `opencode-go` is admitted
  only as an OMP-native cascade hop on global `retry.fallbackChains`, never
  as a primary or automatic transport. Explicit fleet L1 studies are labeled
  separately and do not masquerade as this canonical native handoff;
- a failed proposal seat is bound to an OMP error transcript and one typed
  `lane_failure` event, while completed proposal seats retain canonical
  proposal artifacts; critical Main, planner, the frozen `probe_parent`
  executor, labrat, and distiller seats must complete for admission, and at
  least one proposal must survive;
- critical failure does not suppress a later reachable topology dispatch;
  collection preserves the failed transcript before Rust rejects admission;
- each surviving proposal equals its hashed native artifact and its provenance
  fields bind the OMP task id; no producer supplies a candidate — the
  distiller seat composes it, and Rust alone re-validates admission,
  composition, and digests before emitting the candidate in its
  digest-bound verdict;
- the handoff declares exactly one admission profile on substrate `omp` —
  `omp-native-v1` (frozen conformance) or `omp-native-v2` (the strict default,
  plan_digest + acceptance_criteria), and `omp-native-resilient-v1` only on an
  operator re-charter (the "Admission profiles" split below); axes are
  nonempty with unique ids and recomputed hashes; `contract_root`
  canonicalizes to the trusted project root, `config_digest` recomputes
  over `config/ufo.json`, and provenance must equal the active honest
  provenance; `.omp/config.yml` must byte-equal the regenerated projection —
  projection parity binds the project file, while the `effective_launch`
  record (v2+, spec 12) binds what each seat actually inherited; both are
  required and neither substitutes for the other;
  telemetry is restricted to `lane_failure`, `correlated_unavailability`, and
  `lane_timeout` events under `omp-native-v1`, plus `domain_cooldown`
  (observed herd record, spec 11 §5) under v2 and resilient;
  `lane_timeout` carries the identical field set to
  `lane_failure` (the deadline and elapsed times ride inside its bounded
  `detail` string — the v1 handoff schema gains no field); every handoff
  struct denies unknown fields under the declared byte ceilings.

Admission profiles (spec 10): a handoff declares exactly ONE admission
profile, and the two strict profiles — `omp-native-v1` (frozen conformance)
and `omp-native-v2` (the default) — admit one shape of route evidence: a
completed seat carries no route continuity. The strict rejection of a fallback
completion on a completed seat is the collector's die
`role <role> completed with route continuity; exact-primary evidence cannot
include continuity`, which fires before the handoff reaches the judge; that
rejection is the DOCUMENTED behavior (T03), not a surprise, and the judge's
twin rule stays unreachable on the native path.

`omp-native-resilient-v1` is a THIRD admitted profile, never a relaxation of
the other two: it validates authorized transitions instead of pretending no
transition happened. It admits a fallback completion only through a complete
`attempt_ledger` entry for that seat — an additive OPTIONAL field under this
profile, REQUIRED for any seat whose completion involved a route hop, and a
typed rejection naming the freeze under `omp-native-v1` and `omp-native-v2`.
Each entry carries `logical_lane_id` (`<run_id>/<role>/<instance>`), `role`,
`instance`, the ordered `attempts` (each with `attempt_id`,
`requested_route` as provider/model:effort, `observed_model`,
`observed_effort`, `native_agent_id`, `typed_failure`, and
`authorized_next_hop` as route + reason), `final_attempt_id`, and
`output_digest`; the ledger keeps no `input_snapshot_hash` or
`evidence_digests` of its own (the spec's two extra digest fields were
dropped when the entry landed): the v2 handoff's existing digests are reused,
so the ledger adds hops, never a parallel evidence channel. Resilient
admission requires: every attempt's `requested_route` is declared in the
seat's typed chain and hops strictly forward — the chain_index/next_route
machinery reused, no wrap and no skip backward; every hop's `typed_failure`
is a capacity class that permits advance, since a non-capacity transition is
inadmissible; `frozen_scope_hash` and `assignment_hash` are identical across
the lane's attempts and equal the seat's frozen assignment hash (I5/I6) — the
two renderings are deliberate, `frozen_scope_hash` being `sha256:`-prefixed
while `assignment_hash` stays the bare-hex handoff digest; the final
attempt binds the seat's completing agent and its output passes the SAME
evidence gates as a strict completion; and `observed_effort` equals the
requested route's declared effort suffix, a mismatch being the typed
`effort_unverifiable` rejection of the §6 effort rule (T07) — never silent
clamping credited as exact effort. An empty chain stays a hard pin, an
undeclared model stays inadmissible, and a completed seat carrying hop
evidence WITHOUT a ledger entry is rejected under this profile too.

Under BOTH strict and resilient, undeclared routes, non-capacity transitions,
and relabeled evidence are inadmissible: setting fallback flags false,
relabeling a fallback as the primary, and normalizing an observed route to
the requested route are never "fixes" (T05). The strict profile stays the
default; resilient activation for any mission class is an operator
re-charter, like any route-table change, and selects the profile with the
launcher's `--profile omp-native-v2|omp-native-resilient-v1` (default
`omp-native-v2`), whose choice is pinned into the launch manifest and flows
to the collector's emission. The profile choice never changes exit codes.

The resilient profile also admits a pre-spawn failure as typed unavailable
evidence (spec 11 §3): a frozen proposal seat whose batched task call was
rejected before spawn carries a `dispatch_attempts` entry — resilient-only,
a typed rejection under both strict profiles — recording
`logical_lane_id`, `attempt_id`, `requested_route`, `typed_failure`,
bounded sanitized `detail`, and the attempt interval, with NO native agent
id (T12). A frozen proposal seat is covered by an agent XOR a dispatch
attempt; its `lane_failure` telemetry binds `agent_id` null, the attempt's
requested route and interval, and the same correlation group the seat's
agent would carry. Under the strict profiles a pre-spawn failure keeps its
existing failed-seat admission semantics; critical seats never appear in
`dispatch_attempts` — a critical pre-spawn failure keeps its invalidation.

`effective_launch` (spec 12) is the per-seat launch attestation bound into
the handoff under v2 and resilient — an additive OPTIONAL field, a typed
rejection under v1. Each `effective-launch-v1` record carries the seat's
ids (`logical_lane_id`, `attempt_id`, `wave_token`), host attestation
(OMP path/version/sha256, launcher rev, tmux), the resolved role card
(source, path, sha256 recomputed over `contract_root/agents/<role>.md`),
requested route + resolved model + fallback chain + retry policy, tool/
spawn/behavior policy (advisor absent), overlay digests, cwd, and
credential-screened argv. The launcher captures records at dispatch and
re-resolves the policy immediately before the batched call — drift
between plan time and dispatch time halts pre-mutation naming the layer
(T14). The collector's behavior census (T15) requires every transcript
model/session event to be accounted for by the seat's declared attempts;
an unaccounted switch or extra session envelope is unauthorized evidence
and dies.

Native deadline admission is post-hoc. Any seat whose interval exceeds its
seat-class bound is `failed` + `lane_timeout` evidence — the deadline breach
is the terminal cause it names, regardless of whether the seat had completed
or already failed (`lane_failure` is for failures inside the bound), and the
seat's provider-failure detail remains in its transcript. The Rust judge
independently recomputes `elapsed` against the same config deadlines,
rejecting a mismatch in either direction — an over-deadline seat without
`lane_timeout`, or a `lane_timeout` without an over-deadline interval.
Dispatch is idempotent per
wave: the launcher writes `.ufo/dispatch/<runId>/pre-dispatch-r<NN>.json`
(O_EXCL, 0600, no-follow) holding the intended topology, per-seat assignment
hashes, and `wave_token` before the batched task call, whose `context` carries
a literal `wave_token: <token>` line. Two successful batched proposal-wave
calls for one wave, or a context token that disagrees with the snapshot, is a
typed `double_dispatch` rejection naming both transcripts; a token absent from
the evidence is the pre-P2 legacy path and draws no new rejection. A resumed
Main that finds a snapshot with no settled collection never re-fires the wave —
it pairs live Hub agents against the snapshot and continues to collection, and a
frozen seat with no live agent is a typed `missing_seats` rejection, never a
respawn (I6). The token never enters `NativeRoundHandoff` as a field of its
own; the profiles that carry it do so only inside the per-seat
`effective_launch.ids` record above. Re-running a
crashed run under the same `--run-id` always resumes the anchored wave and
never re-fires it; a fresh wave requires a fresh `--run-id`.

Task and Agent Hub records are transport evidence only. They cannot accept a
move. The Rust verdict includes the handoff digest so later edits invalidate
the decision. Fixture reports and native handoffs are different evidence kinds
and never impersonate one another.

Role assignments require the behavior in `agents/*.md`, not prefilled
improvement vectors. Mutation evidence includes a local defect, detector
output and exact restoration; executor evidence exercises a bounded real
change. Concurrent writes stay in separately owned scratch paths. Scores are
advisory and cite actual observations; unknown axes stay at baseline.
Transport conformance and repository improvement are separate claims.

OMP's native credential manager owns actual credential use. The hash-bound
launch manifest is the requested-route evidence. The hashed task transcript's
`model_change`, `session_init`, effort event, and served assistant messages are
the resolved-route evidence. No external credential or slot selector is part
of the native profile.

Two shared modules single-source the launcher's and collector's native
derivations. `scripts/ufo-native-names.mjs` derives the seat identity
surface both sides must compute identically — `seatId` (`role:N`),
`seatLabel` (`role-NN`, zero-padded), `canonicalDispatchName`
(`u<sha256(runId)[:8]>-role-NN`), and the `sha256:`-prefixed
correlation/unavailability groups over version-tagged NUL-separated
material — with the Rust twin in `native_seats.rs`; the file is a
`NATIVE_CONTRACT_FILES` member, so drift invalidates in-flight trials by
contract hash. `scripts/ufo-credential-screen.mjs` single-sources the
two-tier evidence screen: the narrow `containsCredentialShape` mirror of
`detail_contains_credential` (`native_admission_text.rs` — three literal
needles plus `sk-`/`rk-`/`ak-`/`xai-` prefixes that count only with ≥12
token characters) and the wider `containsSensitiveShape` predicate that
adds the literal `api_key=`/`token=`/`xoxb-`/`AIza`/`PRIVATE KEY`/JWT
shapes `argv_sanitized` and evidence writes screen through. The
credential screen is NOT a `NATIVE_CONTRACT_FILES` member — its parity
with the Rust mirror is maintained by convention and test, not enforced
by the contract hash.


Sekhmet/L3 is shelved by operator doctrine. Its retained implementation and
stored capacity/chain are compatibility data, not active dispatch authority.
Do not launch sparks, replace missing OMP seats with L3 evidence, or make L3 a
prerequisite. Spark output never enters `NativeRoundHandoff` agents,
proposals, or telemetry.

### 4.3 Swarm wave dispatch

Fleet self-improvement missions dispatch L2 workers swarm-style under one
L1-owned scope. The shape is substrate-neutral semantics; the command
mapping is per-substrate plumbing (OMP batched `task` call, kimi
`AgentSwarm`, devin `run_subagent` batch). This section is L1 orchestration
doctrine. The swarm-wave planner `scripts/ufo-swarm-wave.mjs` validates a
wave spec and emits the single batched dispatch payload (OMP is the first
plumbing target); the `ufo-mission-result-v1` evidence envelope records
swarm-shaped results. The spec itself is declared by whichever source the
operator or L1 has in hand — a saved file (`--spec <wave.json>`), stdin
(`--spec -`), or an inline literal (`--spec-json <json>`); `plan` emits the
validated `ufo-swarm-wave-v1` plan; `run` renders
`ufo-swarm-wave-dispatch-v1`: `taskCall {context, tasks}` for spawn lanes
(`null` when the wave resumes only) plus `resumeSends`, one `hub send` entry per resume lane. Every fresh subagent session MUST receive
`/skill:godspeed` as the leading line of its task text. The swarm-wave
renderer injects it into every spawned lane; the
`.omp/hooks/pre/ufo-godspeed-inject.js` `tool_call` hook injects it into
every `task`-tool dispatch (idempotent — an already-invoked prompt
is left untouched). Dispatch surfaces that bypass `tool_call` (eval-kernel
`agent()`/`workpool()`) must still prepend it themselves. A trailing
`| godspeed` marker is envelope-only and loads nothing. Resume `hub send`
messages are continuity messages, not new sessions — never prefix them.
The election rule: a swarm wave procs only when the work is unjudged fleet
scope AND the plan yields enough same-shape items to fill the configured
wave band (16–100 under repo policy; `minLanes` — default 2 — under a band-less policy). Judged rounds keep
the frozen proposal topology — a wave inside a `NativeRoundHandoff` session
is invalid — and wave output is advisory evidence only, never a `Proposal`.
The unit is a *wave*; `fleet` stays the mission class. The wave cap is its
own ceiling, distinct from the wave band that sizes each dispatch. Swarm
members are leaf by default: no `task`/jobs tooling, no
delegation, no background jobs; executor is the explicit bounded exception
below. Leaf-ness is enforced today by the
planner's role taxonomy plus member instructions — and by the OMP
spawn-policy default: a member card with no `spawns:` key resolves to
spawn policy disabled (leaf-by-default). The live OMP binary consumes
frontmatter `tools:` (an allowlist; `yield` auto-added, `hub` auto-added
to any non-read-only list) and `spawns:` — but `spawns: []` collapses to
undefined and yields wildcard `*` when `task` is in tools, so `[]` is a
footgun, never the leaf spelling. Exception: `agents/executor.md`
declares `spawns: labrat` — the executor swarm role is not a leaf.
`jobs` is a `hub` op, not a tool name. OMP has no per-agent
`tools_deny`; `tools.approval` deny policies are session-scoped and
would bind the L1 itself (kimi parity: the `coder` profile lacks
`Agent`/`AgentSwarm`). The spawn-policy, `tools:`/`spawns:` frontmatter,
and kimi-profile claims in this paragraph are host-observed semantics of
the installed binaries — no in-tree consumer exists; they are verified
against the live OMP host, not repo bytes. Lane routing: each swarm lane takes its taxonomy role's pinned route from
the global OMP table (`AGENTS.md` Routing authority — a dated observation).


1. Explore the owned scope and partition it into concrete items before
   dispatch; workers never edit outside the L1 scope.
2. For a wave with spawn lanes, emit one batched task call carrying every
   spawn lane; for a resume-only wave, emit none. Never split a wave across
   task calls. The effective policy cap counts spawn items plus resumes: the
   member ceiling is 100 by repo policy (`sighting.dispatch.swarm.maxLanes`,
   and the planner's `MAX_SWARM_LANES` hard bound backs that cap), independent
   of the OMP host `task.maxConcurrency` (0 everywhere — no host secondary
   cap), the native profile `concurrencyCeiling`, and the 1056 global runner
   ceiling. Expanded item prompts must be pairwise distinct — a duplicated
   expansion fails the wave before any lane spawns; never dedupe silently.
   A wave carrying spawn lanes must also land inside the configured wave band
   — `sighting.dispatch.swarm.waveMinLanes`/`waveMaxLanes` (repo: 16–100) —
   else `too_few_lanes`/`wave_too_wide`; a wave whose lanes are all resumes
   is exempt. A spec `maxLanes` tightened below the wave floor makes the band
   unreachable and fails `impossible_band` before any lane spawns — raise the
   spec cap or dispatch resumes only. A config policy declaring no wave band falls back to the swarm
   band (`minLanes`/`maxLanes`), so the band-less floor remains `minLanes` (built-in default 2 — the kimi-parity
   minimum; the repo policy declares `minLanes` 64, a round-floor doctrine the
   planner does not gate). The plan also records the declared launch ramp —
   `sighting.dispatch.swarm.rampBatchSize`/`rampIntervalMs` (built-in
   defaults 5 lanes per 700 ms, kimi AgentSwarm parity) — in its `policy`
   block as pacing policy for substrates that pace manually; on OMP the
   single `task` call is the wave and the harness queues lanes beyond its
   concurrency window, so the ramp never splits or delays a dispatch.
   Spawn items MAY declare a judgment binding: `axes` (1..8 distinct
   nonempty names, ≤256 bytes each — `invalid_spec` otherwise) and
   `milestone` (a nonempty label ≤256 bytes). `spec.axes`/`spec.milestone`
   are the wave's defaults; an item-level declaration wins outright — a
   lane that declares its own axes is judged on exactly those, never a
   merged set. Absent at both levels the lane is judged on the round's
   axes. The binding renders into the spawn prompt as `Judged on:` /
   `Milestone:` lines ahead of the reportDir suffix, and persists on the
   member's registry row so a later resume wave inherits it and collect
   can attribute the verdict to the declared axes.
3. Waves run sequentially within a round: wave N+1 launches only as wave N
   settles. A wave settles when every dispatched lane has a recorded terminal
   outcome: `completed`, `failed`, or `aborted`. Typed failure classes such as
   `lane_timeout` and `unavailable` are annotations, not outcome values. A
   lane without a terminal outcome blocks the next wave; no native seat
   deadline is inherited by an unjudged task-wave lane. A swarm wave may
   accompany an unjudged fleet mission as reconnaissance; on the judged OMP
   native path the collector admits exactly three Main task calls (planner,
   proposal wave, distiller), so no swarm wave may appear in a
   `NativeRoundHandoff` session or substitute for a typed proposal seat.
4. Resume a failed lane on the same identity (I6); never mint a
   replacement. Per-item failure is typed lane telemetry. Resume
   ownership is fail-closed at plan time: the id must be a member of the
   wave's own registry or a declared `spec.priorRegistry` (≤16 entries,
   root-relative), else `resume_unknown_member` before any lane spawns —
   membership proves ownership, not liveness. `run` persists the wave's
   `ufo-swarm-registry-v1` at `<reportDir|.ufo/scopes/<wave>>/swarm-registry.json`
   before emitting the payload; spawn members land with `agentId: null`
   and `record --registry <path> --assignments '{"<name>": "<agentId>"}'`
   fills them post-spawn (same-id idempotent; a re-point dies
   `conflicting_assignment`). On id collision the wave's own registry
   wins; resume rows recover the owning member's name and persisted
   `item`. Persisting over an existing registry surfaces every displaced
   handle on the dispatch payload as `handlesReset`
   (`{name, previousAgentId, agentId}`): a re-run's `agentId: null` reset
   and a resume row re-pointing a member name to a different handle both
   kill the old handle's only ownership row — the displaced id becomes
   unresumable — so the payload names each one instead of letting
   ownership die silently.
   A DIFFERENT wave identity persisting over an existing registry refuses
   BEFORE the write as `wave_registry_collision` when an overlapping member
   name would displace an assigned handle — the displacement used to surface
   only post-persistence via `handlesReset`, after the ownership bytes were
   already gone. Handles a planned resume lane claims are excluded (the
   aliased-reset case is adjudicated under the lock by resume
   re-validation), and a registry with no recorded wave predates wave
   provenance — its same-scope resets keep the documented semantics.
   Both registry writers serialize their load→mutate→write under
   `<registry>.lock`, a mkdir-claimed directory beside the registry:
   `persistWaveRegistry` (`run`) and `record` are the only writers of
   `ufo-swarm-registry-v1`, so the lock covers every mutation — two
   concurrent `record` calls can no longer lose an assignment (a silently
   orphaned handle), and a `run` racing a `record` can neither drop
   members nor resurrect reset rows. The holder binds its claim with an
   `owner.json` (pid + token, O_EXCL/O_NOFOLLOW, 0o600, fsync'd before
   any contender can read it); a contender finding the lock held breaks
   it only when the owner pid is dead, or the owner record is unreadable
   once the dir passes a 30s freshness grace — a future-dated mtime
   proves nothing and still attempts the break. The break is fenced: the
   held dir is quarantined by rename, and a seized owner whose token
   differs is renamed back — only a proven-string token match deletes.
   Release removes the dir only while `owner.json` still carries the
   holder's token (a stolen-and-reacquired lock is never ours to
   remove), and acquisition gives up after 30s. A symlink or
   non-directory at the lock path fails the acquire. Read-only loads
   (prior-registry reads, resume resolution) stay lock-free — the atomic
   rename already hands them one consistent snapshot. `record` against a
   missing registry still fails `invalid_registry`: the lock's parent
   dir is created before the claim, so the failure stays typed, never
   ENOENT on the lock dir.
   Resume lanes inherit the member's spawn-minted binding and MUST NOT
   restate either key — `resume_meta_forbidden` fails the wave before any
   lane spawns; the registry is the authority, and restating would fork
   the contract. The resume member's own registry row copies the binding
   forward so collect still attributes it.
5. Aggregate lane findings without flattening; each lane emits a scoped
   report artifact, and cross-scope findings hand to the L1 integrator (no
   dedicated wrap-up seat exists in `agents/` or the configured lanes).
   The aggregation bridge is `scripts/ufo-swarm-collect.mjs`: it joins the
   dispatch record, the `ufo-swarm-results-v1` settled outcomes, and the
   member registry into the `ufo-mission-result-v1` evidence envelope —
   L1/L0 evidence only, never a judge input. The join is fail-closed:
   every dispatch member needs exactly one result row (`unmapped_member`)
   and every result row a dispatch member (`unexpected_member`), with
   duplicate member names refused (`duplicate_member`). Identity evidence
   is three-way — registry (authority) > results row > resume-derived id —
   and distinct non-null values are `conflicting_member`; a resume member
   with no resolvable id is `missing_agent_id`. `resumeSends[].resume` is
   shape-validated at join (nonempty string ≤256 bytes, else
   `invalid_wave`) — a missing or non-string value would degrade to a null
   derived id and silently disable one leg of the three-way check or fail
   late as `missing_agent_id`, a misleading code for a malformed record;
   the id pattern itself is not re-checked — URI-form ids legitimately
   normalize through `toLocalAgentId`. Absent `--registry`, the wave
   record's own `registry.path` is the default join — artifact bytes, not
   argv, so it must be root-relative and resolve beneath the project root
   (`invalid_wave` on shape violations, `EXEC_PATH_OUTSIDE_ROOT` on
   escape, `UFO_FLEET_ALLOW_EXTERNAL_TOOLS=1` the escape hatch); a missing
   file is empty evidence, malformed bytes fail closed. Both the explicit
   `--registry` read and the default join carry `MAX_REGISTRY_BYTES`
   (1 MiB, typed `invalid_registry`) — the same bound the wave authority's
   `loadRegistry` enforces, so a registry that grew past the write-side
   bound cannot join silently in collect while refusing every resume
   wave. `reportDir`
   evidence resolves registry-file-copy first, then the wave record's own
   `registry.reportDir` — planner-emitted at dispatch, the same artifact
   trust class as `registry.path` — both through the same trust gate:
   relative, segment-clean, beneath the root with no symlink component;
   untrusted bytes degrade to "no reportDir", never a failure. Only under
   a trusted reportDir does a member surface `reportPresent` — an `lstat`
   regular-file check, so a symlink swapped in cannot fabricate a present
   report. The registry is the sole authority for the judgment binding:
   entry `axes`/`milestone` come only from the member's registry row.
   The emit path is typed the same way: `--out -` is stdout (the input
   side's `-` convention — never a file literally named `-`); an
   errno-coded fs fault on the operator-named `--out` path is operator
   input, not an internal bug — `ENOENT`, `ENOTDIR`, `ELOOP`,
   `EACCES`/`EPERM`, `EISDIR` surface `invalid_out`, while resource faults
   (`ENOSPC`, `EDQUOT`, an `EEXIST` tmp collision) stay internal; a typed
   `MissionResultError` from `createMissionResult` or
   `renderMissionResultXml` (`invalid_xml_text` on a lone-surrogate body —
   reachable via results-row bytes) wraps as `invalid_envelope`.
   With `--emit-xml` the envelope renders before anything publishes — a
   render fault leaves no fresh JSON-only artifact — and the pair commits
   through `writeFilePairAtomic` (`ufo-mission-result.mjs`): both bodies
   stage as O_EXCL temps, the sidecar renames first so a reader gating on
   the primary never sees half the pair, and a primary-rename fault
   retracts the published sidecar best-effort. The one unclosable window
   is kill -9 between the two renames (no journal); overwrite
   destinations inherit `writeFileAtomic` semantics.
6. Swarm output is advisory evidence, never a `Proposal`: it enters no
   judge admission path and manufactures no frontier movement. A swarm
   wave's exhaustion is lane telemetry, never `SATURATED` or
   `BUDGET_HALT` on its own — I8 applies to rounds, not lanes.
7. Never spawn another L1 (I1), change substrate, add L3, or touch
   credentials.

The unjudged fleet mission loop: a fleet L1 is an autonomous, self-iterating
orchestrator that performs its own mission-internal Pareto integration over
settled lane evidence and emits no canonical Rust verdict; canonical judgment
remains the Rust runtime's alone (I1). A mission is never a one-shot task: it
iterates over WWKD-planned, axes-governed rounds with axes stable within the
round and free to evolve between rounds; it dissects and dispatches same-shape
items, judges settled lanes by Pareto, ships accepted work, and hands off.
**Self-iteration is respawn-per-round, never in-session looping: one session
runs exactly one round.** When the round's work is landed the lane writes its
report and receipt once and exits; a receipt `iteration.decision: continue`
releases the dispatcher to mint the successor — a fresh session on the same
identity with the prior report bound in through the prior-round cache. A lane
that starts a second round in-session has violated the contract; a lane that
exits without a receipt strands its chain (`acceptance_evidence_missing`).
`stop`, `blocked`, and `budget_halt` end the chain honestly — saturated,
blocked, or budget — never progress theater. Declared terminal
saturation uses receipt `iteration.decision: stop` with a reason naming saturation; `stop` alone is not a Rust convergence verdict.

---

## 5. WWKD plan

```
fn wwkd_plan(state) -> Plan:
    1. data walk         — inspect cache, telemetry, and local diff first
    2. skeleton first    — establish one end-to-end shape before capacity
    3. overfit one case  — prove one concrete path, then generalize one axis
    4. cheapest local check — use pattern checks before expensive local work
    5. verification gate — every milestone names its observable check
    6. least disruption  — order moves so each remains runnable in isolation
```

The plan is written by the one L1. A planner card may provide advice on hosts
that support it, but it never becomes a second judge or runtime. The WWKD
posture is uncapped on milestones; the plan artifact itself is read under
`MAX_PLAN_ARTIFACT_BYTES` (4 MiB, loop_driver.rs:112).

Every declared axis names its measurement (`Axis.measurement`, declared with
the round's axis set): `executable` axes are measured by the runtime
— the check runs in a bounded scratch copy of the baseline tree and of
the candidate tree (the proposal's declared `candidate_writes`), never
the live tree, and the judge consumes the computed direction-aware delta;
seat scores on an executable axis are advisory context and never override
a computed regression. `subjective` axes admit a claimed improvement only
through the recorded symmetric argument (for and against sides citing
role-appropriate evidence); one-sided claims are clamped to baseline and
flagged. `evidence` axes are computed by the judge from typed handoff
evidence and exist only on the native path — the fixture loop cannot
produce them and the native path cannot execute subprocess checks, so
each side rejects the other's kind at admission. A check that fails to
run measures UNKNOWN: never regression cover, never a phantom gain, and
UNKNOWN on a material axis blocks admission as `INSUFFICIENT_EVIDENCE`.
An axis with no measurement declaration fails the round's plan admission:
unmeasurable axes are not axes (verification-gate stance applied to the axis
set itself).
The verdict and round report carry the computed measurements and flags
as provenance.

---

## 6. Same-identity local reroute

Reroute is a runtime capability, not an operator paste and not a replacement
process presented as the original lane.

```
fn reroute_same_identity(state, lane, task, next, cause):
    // concrete gates: require_local_route admits only implemented local
    // routes; next must sit in the role's typed chain; per-record pins keep
    // runtime "crates/ufo-core-runtime" and the selected substrate
    assert next in lane.allowed_routes
    assert next.is_local && next.is_implemented
    assert state.runtime == "crates/ufo-core-runtime"
    assert state.substrate == selected_substrate

    before = {
        identity: lane.identity,
        cache: lane.cache,
        prompt: task,
    }
    output = lane.resume_same_lane(route = next)  // new attempt, same identity
    assert lane.identity == before.identity
    assert lane.cache == before.cache
    assert task == before.prompt

    from = lane.route
    lane.route = next
    lane.state = READY
    record(state.reroutes, RerouteRecord{
        round: state.round,
        reason: cause,   // lane identity is asserted at intake, not stored
        from,
        to: next,
    })
    return output
```

Current canonical routes are explicit local implementations:
`local/fixture-primary`, its in-invocation recovery route
`local/fixture-recovery`, optional local distillation `hvm/qwen-hvm`, and the
OMP-native evidence transport `omp/task`. The latter is admitted
only through `ufo judge-handoff`; Rust does not pretend it spawned OMP agents.
Any undeclared route fails closed.

Autonomous model routing (OMP native lanes): the operator never pinpoints a
model per dispatch. Each seat resolves its route from the global OMP config
(`~/.omp/agent/config.yml` `task.agentModelOverrides` + `modelRoles` +
`retry.fallbackChains`); the launcher freezes that resolution at dispatch
and the generated `crates/ufo-core-runtime/bundled/omp-seat-routing.json`
mirrors it into the compiled runtime (I9 drift fails closed). Seat→alias
summary: `AGENTS.md` Routing authority. Every L1 — a fleet mission and a
canonical native-trial Main alike — selects a bare alias that resolves in the
fd-bound global OMP config. `missionFormat.l1Alias` supplies only the
`m_daybreak` default (`openai-codex/gpt-daybreak-blue-latest:max`);
`m_swe` (`devin/swe-2:max`) and `m_kimi_devin_high`
(`devin/kimi-k3:high`) are examples, not a project allowlist. A
mission spec selects the alias, never a concrete route, and no mission overlay
declares an L1 route (§8.2).
Chains advance only on typed capacity
failures (I6), honor the exact effort declared for each hop (the effort
rule below), and halt honestly on exhaustion without wrapping. Empty
fallback arrays are explicit. Repeated roles in one seat class resolve
identically. The hash-bound project/native launch projection keeps
`retry.usageAwareFallback=false`; `fallbackRevertPolicy=never`. The
operator-global retry flag is separate host configuration, not seat-route
authority or hop-admission evidence. Unknown provider usage is not healthy
capacity. Proactive pinned fallback
would not satisfy exact-primary native handoff evidence. Re-chartering a
route is a global-config edit plus mirror regeneration and operator
sign-off; it is never a live project pin edit. The advisor stays DISABLED —
absent from `omp-native-v1`, not `enabled: false`; an advisor is never a
seat or judge. The `devin-native-v1` profile uses
`devin/subagent` transport and is never admitted by `judge-handoff`.
`l1Context` is capability metadata (a minimum-token declaration), never
available capacity. L0 selection is independent of this table.

Provider domains implied by the live global cascades (not project
`failureDomains` keys): the set is derived from the live seat table and its
typed chains — re-derive it from the global config, never from a frozen list.
Loss of a provider strands the
seats whose primary or hop sits on that provider. Phase 0 probes still fire
for domains serving critical seats:
one bounded minimal completion whose failure halts dispatch pre-spend,
naming the domain and the killed seats; a Devin OAuth probe proves
reachability at probe time only and stays operator-attested, never a quota
guarantee. Seat attempts append to the append-only
`.ufo/routing-health.jsonl` lane-health ledger (read by `ufo routing-health`,
display-only) so re-charters move on ledger data, not on vibes.

The effort rule: each hop honors the exact effort declared for that hop in
the typed chain. Role-level reasoning intent, requested effort, resolved
effort, and provider-observable execution settings are recorded separately.
An unobservable setting is an explicit typed outcome
(`effort_unverifiable`), never assumed compliance and
never silent clamping credited as exact effort (T07).

---

## 7. Priority ramp

Priority changes ordering, never Pareto admission:

1. restore and prove the core runtime;
2. prove observable behavior and failure paths;
3. prove self-iteration and reroute;
4. prove exact contract portability;
5. exercise all seven local command surfaces.

A later concern may veto an earlier move. No weighted sum, confidence score,
or target metric may admit a regression.

---

## 8. Stop conditions

```
fn pre_dispatch_boundary_stop(state, next_round):
    if external_interrupt:
        return INTERRUPTED
    if budgets.wallClockMsPerMission > 0
       && mission_wall_clock_elapsed >= budgets.wallClockMsPerMission:
        record(telemetry, wall_clock_budget{...})
        return HONESTY_BRAKE
    if budgets.tokensPerMission > 0:
        if cost_ledger.mission_cumulative >= budgets.tokensPerMission:
            record(telemetry, budget_exhaustion{...})
            return HONESTY_BRAKE
        if projected_wave_cost > remaining_mission_budget:
            record(telemetry, budget_projection{...})
            return HONESTY_BRAKE
    return CONTINUE

fn post_round_stop_condition(state, verdict):
    // An all-lane failure aborts before judgment. Unsound distill or binding
    // and critical-seat invalidation stop here as BLOCKED.
    if !sound_round:
        return BLOCKED
    if verdict.accepted.is_empty() && no pending_refinement:
        if round_is_clean:      // the round digest's lane_health block:
                                // zero capacity, zero lane_timeout, zero
                                // quality_degraded, zero unavailable
            return SATURATED    // saturation precedes every budget stop
        record(telemetry, saturation_inconclusive{lane_health})
        if configured_round_budget_exhausted:
            return BUDGET_HALT  // the cap survives saturation demotion
        return CONTINUE         // a degraded zero-accept round is not a
                                // plateau (spec 07 §5)
    // The post-round actual-token brake follows saturation and precedes the
    // round cap. Zero means unlimited.
    if budgets.tokensPerMission > 0
       && cost_ledger.mission_cumulative >= budgets.tokensPerMission:
        record(telemetry, budget_exhaustion{...})
        return HONESTY_BRAKE
    if configured_round_budget_exhausted:
        return BUDGET_HALT
    return CONTINUE
```

Every post-round `CONTINUE` re-enters through
`pre_dispatch_boundary_stop` before planning or lane dispatch, so an enabled
wall-clock, actual-token, or projected-token brake stops with zero lanes in
the next round. The three brake kinds retain distinct telemetry; zero disables
the corresponding budget.

A provisional `CONTINUE` is also subject to the landed blocked audit: the same
work-class blocker signature across three consecutive zero-accept rounds
becomes `BLOCKED`. Transport failures do not increment that streak, resume
starts a fresh count, and the audit never overrides a terminal outcome. This
stop transform is runtime doctrine, not a goal-authoring intake surface.

`SATURATED` describes the search, not the task. Terminal outcomes carry
`round_validity` (sound | unsound), `loop_stop` (`saturated` | `budget_halt`
| `blocked` | `interrupted` | `honesty_brake` | `authority_boundary`), and
`mission_goal` (`satisfied` | `incomplete` | `unverified`) independently. A
sound, saturated mission with unmet acceptance criteria reports
`saturated + incomplete` and is not task completion; unmeasurable criteria
report `unverified`. Neither field ever upgrades the other. On the native
launcher the exit code reflects verdict persistence, not `loop_stop`: any
parsed verdict exits 0 (`run-omp-native-trial.mjs` writes the verdict then
sets `finalExit = 0`), a rejected or unparseable verdict exits 2 — the
triple is reported in the verdict output and the mission envelope, never
folded into exit status.

`mission_goal` derives ONLY from the round plan's `acceptance_criteria`
(`ufo-round-plan-v1`, spec 07 A-07). Empty or absent criteria, or any
non-empty string criterion (unmeasurable by construction), report
`unverified`. Mechanical criteria of the form
`{kind: "axis_threshold", axis, op: ">=" | "<=" | ">" | "<" | "==", value}`
are evaluated against the final round scores: every such criterion met →
`satisfied`; any measured unmet → `incomplete`. Full measurement states
(OBSERVED / UNKNOWN / CONTRADICTED / NOT_APPLICABLE) and their axis contracts
are landed (spec 05, P5); a criterion is either mechanical or unverifiable,
and no placeholder ever counts as met.

`BUDGET_HALT` and `BLOCKED` are not convergence.
`CONTINUE` is loop control; it persists only as the non-terminal `running`
checkpoint marker and is never a terminal stop value (§1).


If any accepted proposal touches `membrane.paths` (config-declared senses:
runtime, CLI, collector, sync gate, launcher, sighting, routing/budget
config, contract docs, authored directive), the verdict emits
`authority_boundary` and the loop seals until the operator signs
(`ufo charter sign <runId>`, operator-interactive only) and its Phase 0
stages — contracts, build, drills — re-pass. The accepted work still lands
locally; the next round never
dispatches under a seal. The system may edit its own body under judgment;
edits to its own senses are operator-owned, like publishing (I10).

The `drills` stage is `node scripts/ufo-drills.mjs` run unfiltered — the
fixture-only drill matrix (`drills/*.drill.json`, spec 09 + A-09 tier 1),
not the `gates.sh` battery. Six executors cover the surfaces a drill can
exercise: `self-iter` (shadow contract tree + `ufo self-iter`),
`sync-check` (shadow + `sync-ufo-contracts.mjs --check`/`--review`),
`cargo-test` (one named Rust test for in-process mechanisms),
`node-test` (one `node --test` case under `tests/` with
`--test-name-pattern`), `judge-handoff` (persisted handoff fixture +
transcript patch through the real `ufo judge-handoff`), and `shell`
(argv with env overrides). Rows carry status `wired`,
`pending-mechanism`, or `referenced`; placeholder rows never execute and
a coverage ratchet fails the suite when either placeholder class
outnumbers the wired count — enforced on unfiltered runs only.
`--only <id>` is a diagnostic view of one drill: it skips the coverage
invariant and writes `summary-<id>.json` beside the durable unfiltered
`summary.json`, never overwriting it; `--list` and `--self-test` are
read-only and leave evidence untouched. A pending row without
`pendingReason`, or a referenced row whose references do not resolve
under the repo root, fails closed at load.

Fleet `iterate` chains are scheduling continuity, not additional judges.
Only validated result receipts may release successors, which retain the
frozen prompt, routes, scope and prior-round evidence; axes are dynamically
discovered per round and declared by the L1 in its WWKD plan, stable within
the round and free to evolve between rounds — never frozen for the run. A
bound converged outcome stops the chain. Within one chain, reaching the
declared round count is a budget halt unless the final round itself saturates;
neither terminal outcome releases a successor, and a genuinely converged
charter is never automatically re-armed.
Missing receipts, drift or rejected evidence remain recorded blockers.

A `continue` release is a mint attempt, not a guaranteed mint. When the
successor's scopes overlap a live non-terminal row's scopes — chain-edge and
dependency rows exempt — the dispatcher records a deferred `continue` on the
parent's `iterationOutcome` (`deferred: "scope_occupied"`, `scopeOccupiedBy`
naming the blocker) and mints no row; the parent stays settleable rather than
dying on a transient scheduling condition. `reconcileQueue` re-attempts the
mint on every pass once the recorded blocker drains — silently while it is
still live, and a different live row defers again under its own key. The
successor identity is a pure function of (parent, round, priorReceiptSha256),
so the eventual mint lands on the same key the dedupe path already
understands; a missing or invalid receipt simply keeps the defer parked.

### 8.1 L0 fleet monitor duty

The L0 monitor (`scripts/ufo-l0-monitor.mjs`, L0-owned — never edited by
missions) keeps `iterate` chains schedulable. Its duty is mechanical
rebinding, never judgment:

1. **Detect** blocked rows whose blocker is evidence drift:
   `prompt_drift`, `config_drift`, `prior_evidence_drift` — the bound
   digest no longer matches the bytes on disk.
2. **Rebind** under the queue lock (`sighting.dispatch.queuePath`) —
   the lock is the only safe mutation point; a rebinding outside it
   races the dispatcher. The heal is two-legged:
   - `prompt_drift`/`config_drift`: rebind the row's stored digests to
     the CURRENT bytes. The same pass refreshes `priorReceiptSha256`
     when the parent receipt is readable (diagnose folds prior-evidence
     drift into `fix`); a missing or invalid receipt leaves the binding
     untouched rather than clearing it.
   - `prior_evidence_drift`: the bound digest lives in the PARENT's
     receipt, not the row. The heal rewrites the terminal parent's
     receipt `promptSha256`/`configSha256` to the child's current
     bytes, then rebinds the row's `priorReceiptSha256` to the
     rewritten receipt — and, because every sibling successor binds
     the same parent receipt (`priorResultPath` = `parent.resultPath`,
     re-verified at dispatch), rebinds every non-terminal sibling
     sharing that receipt path in the same locked pass (`reboundSiblings`
     attribution on the repaired row; terminal siblings keep the digest
     their evidence was checked against; an unresolvable sibling path
     keeps its binding for diagnose to name). It refuses rather than
     rewriting history: `no_parent`, `parent_not_terminal` (a live
     parent may still be minting against those bytes),
     `parent_child_paths_diverge` (the successor builder reuses the
     parent's prompt/config verbatim — divergent paths would stamp the
     child's digests into the parent's receipt), `no_parent_receipt`,
     `parent_receipt_invalid`, `digest_unreadable`. The rebound digest
     is computed over the `validateTaskReceipt`-normalized object —
     dispatcher parity; a raw parse tree with different key order
     mints a digest the dispatcher never reproduces.
3. **Repend** the row so the dispatcher re-attempts dispatch on the next
   reconcile pass.
4. **Re-verify liveness**: the rebound row must register its mission
   (launch or resume) within the launch-miss budget; a row that stays
   `launching` without registering is re-pended with
   `blocker.code=launch_not_registered`, never silently dropped. (The
   re-pend mechanism lives in `scripts/fleet-dispatcher.mjs`
   `recordLaunchMiss`, `MAX_LAUNCH_MISSES=8` — the monitor's own liveness
   surface is `findStalled`, a different signal.)

The same drift classes surface live on non-blocked rows as
`live_digest_drift` (prompt, config, and prior-receipt legs); `--rebind`
re-points the stored digests to current bytes, skipping a row whose
parent receipt is missing or invalid — it never invents evidence and
never clears a binding it cannot recompute. A live row whose artifact
cannot be digested at all is a different finding class:
`artifact_unreadable` — prompt or config path escaping root, file
missing, or read failing (bounded digest), and the prior-receipt leg's
unresolvable-path and unreadable arms. A missing artifact is at least
as dead-ended as an unreadable one — the row fails its next dispatch —
so all four cannot-digest branches share one shape: live rows are named
`artifact_unreadable` and never repaired; blocked rows keep their
blocker code and gain `repairable=false` plus the reason (the
missing-file arms previously skipped blocked non-drift rows entirely).

The heal pass itself runs under ONE queue-lock acquisition and one bounded
queue read: `--rebind`, `--settle`, and `--repair` execute sequentially
inside the same `withQueueLock` (three serialized cycles whose separate
reads could only ever observe identical bytes — the lock fences mutation).
`--repair` re-diagnoses inside the lock because the pre-lock findings
snapshot can be stale by the time it is held (TOCTOU — a row may have been
repended or its blocker cleared between the report scan and the heal), and
the report reflects the fresh findings, not the stale snapshot. Per-step
`writeQueue` is preserved exactly: a mid-pass fault still leaves earlier
steps durable, identical to the sequential version. `repend` stays OUTSIDE
the lock — it spawns the dispatcher, which acquires the same lock itself
(non-reentrant).

`--settle` is the heal pass's bookkeeping arm, deliberately narrower than
acceptance: it completes only rows blocked on `acceptance_evidence_missing`
whose evidence is already on disk — report plus a receipt that satisfies
the SAME expected bag the dispatcher checks at acceptance
(taskKey/runId/sessionId/promptSha256/configSha256/reportSha256, with the
same either-binding prompt digest: the row's stored digest first, then the
dispatch-snapshot sidecar digest). Settling on report bytes alone would
mark completed a row whose receipt binds stale prompt/config digests the
dispatcher would still reject, so an unverifiable receipt leaves the row
blocked. A settled row records `iterationOutcome` indistinguishable in
shape from a dispatcher-settled one (the monitor mirrors `finish()`
verbatim — the dispatcher is unimportable, so the copy is by doctrine):
`reason` rides through the same verbatim `redact`/`CREDENTIAL_SHAPE`
screen, and `nativeVerdict`/`blockedAudit` pass through, so the
blocked-chain audit surface and the operator's trail see the same evidence
whichever writer settled the row.

Hard rules: never fabricate evidence to unblock a row — a rebound digest
must hash bytes that exist on disk at rebind time; never resurrect
retired-fleet rows (a fleet outside the monitor's fleet set stays
out of the queue); never edit the monitor executable from a mission —
it is L0-owned surface.

Runtime carriers: two L0-owned surfaces run the monitor. The
`.omp/hooks/pre/ufo-l0-monitor.js` session hook persists the whipper —
throttled by a shared state file whose freshness is coverage-aware: a run
counts only when its recorded `fleets` set covers the hook's own
(`null` = unscoped covers all; an absent field is unknown coverage and
fails open to a run), so a run scoped to another fleet never suppresses
this fleet's heal. On a stale/missing state it spawns the monitor with
`--fleet <fleets> --repair --repend --json` (report-only runs do not
satisfy the throttle). An `O_EXCL` claim file
(`.ufo/l0-monitor-claim.json`) serializes concurrent sessions so only one
margin is stale and may be broken; a malformed or future-dated claim
falls back to the claim file's mtime for that check — an unparseable
claim must not suppress the monitor forever. The fleet set and interval are
operator-tunable via `UFO_L0_MONITOR_FLEETS` /
`UFO_L0_MONITOR_INTERVAL_MS` (defaults `nc5` / 120s, floored at 5s; a
malformed fleets value falls back to the default rather than silently
narrowing scope). The hook ticks on session start, on the interval, and
on every turn end, and publishes a `l0mon` status segment. The unattended
night watch `scripts/ufo-l0-watch.mjs` is the second carrier: each tick it runs the
monitor with `--fleet <fleets> --rebind --repair --repend --settle --json`,
then respawns settled rows whose receipt decided `continue` and whips a
STALLED row when that receipt's decision is `continue` — or, for a row
flagged `reportDrift`, with the decision-blind drift steer selected by
kind (`driftWhipText`: `unreadable` → the restore-then-remint
`WHIP_DRIFT_UNREADABLE`, every other kind → the `WHIP_DRIFT` re-mint
steer; a `receiptMismatch` row is never whipped; the ordering is codified
below). The monitor's
`--match` filters task *titles*, not fleet names — fleet scoping is
`--fleet`.

The watch daemon is fault-isolated per tick: a throwing tick is recorded
to the action log as `tick_error` and the loop keeps its cadence — an
unguarded throw would leave the fleet's only unattended heal/respawn/whip
surface dead for hours with the state mtime frozen mid-tick. `--once`
stays unguarded: a single-shot run exits non-zero honestly. Both watch and
monitor action logs are bounded evidence: 1 MiB cap with one `.1`
generation (the rename replaces any prior segment — the loss bound is one
generation by design), appended O_NOFOLLOW|O_NONBLOCK so a symlink or FIFO
at the fixed path fails the write instead of redirecting it or hanging the
daemon, with whitespace collapsed at the boundary so queue-row bytes can
never inject a forged line; rotation reports `log_rotated` inline (or
`log_rotate_failed code=<errno>` when the segment cannot be installed —
the bound is soft there, appends continue on the old fd).

The watch's respawn arm is bounded and self-sealing. Enqueues are capped
per hour globally (`--max-enqueues-hour`, default 48) and per lane
(`--max-lane-enqueues-hour`, default 4 — without it one hole that keeps
failing to land burns the whole global budget on itself). A parent row
minted before `l1Alias` existed is skipped with `no_alias` and NOT sealed,
so a later backfill can still respawn it; an unparseable result path skips
with `bad_result_path`. A successful enqueue arms the seal synchronously
(`done` + `donePath` on the dispatcher's admission answer), then a deferred
queue read confirms or releases it: a visible successor row keeps the seal,
an absent one releases it (`seal_pending`) so the next tick re-detects and
re-enqueues, and a read fault leaves the armed seal in place
(`seal_check_failed`) — an accepted-but-lost enqueue never permanently
seals the hole.
Each tick then re-checks every sealed lane: it reopens iff the successor
is `failed`, or absent with no receipt or a `continue` receipt; it stays
sealed when the successor is present and not `failed`, absent with a
terminal or unreadable receipt, or the seal predates successor records. A
`blocked` successor stays sealed NOT because it occupies its scope — the
watch's occupancy scan excludes blocked rows, so a respawn could in fact
land — but because recovery ownership is the monitor's: rependable rows
are re-pended there, and a non-rependable evidence/receipt-missing row is
either settled (valid receipt) or forge-successored (torn/absent receipt,
report present) there; reopening while that recovery is still possible
would mint a second chain head on a scope the recovered successor still
owns. The one unrecoverable class — blocked `evidence_missing` whose
report never landed — is surfaced by the monitor's own blocked-row report
and stays operator-owned. The whip carries its own per-lane
cooldown (`--whip-cooldown-min`, default 15 minutes); a skipped whip
(`stop` / `blocked` / `budget_halt` / absent decision) never starts the
cooldown, so a later `continue` is not cooled down by a parked terminal
state.

The respawn arm's action line names its outcome honestly: `respawned` /
`respawn_deduped` arm the deferred seal; a dispatcher rejection throws
`usageError` and lands as `respawn_failed` (the spec was refused, not
the report); an exit-0 contract violation is `respawn_unparseable` (no
report body) or `respawn_invalid_payload` (parsed body, `enqueued` not
boolean) — the dispatcher's report shape is the suspect, never the
spec; `budget_lane` / `budget_global` are the hourly caps;
`respawn_skipped_occupied` / `respawn_skipped_no_alias` /
`respawn_skipped_bad_path` are the skip arms. Outcome strings dedupe
per lane (`lastRespawnResult`) so a persistent failure logs once and a
changed failure mode still surfaces.

The stall signal itself is the monitor's `findStalled` admission contract,
deliberately narrower than `settle` — detection, never acceptance. A queue
row is STALLED only when every admission gate passes: in scope
(`--fleet`/`--match`), state `running`/`launching`, runId matching the
dispatcher's `gq<hex16>` contract (a malformed runId is named DEAD by
`diagnose`, never whipped — the watch keys its state tables by runId),
`resultPath` resolving beneath the repo root, and a parseable object
receipt on disk. The receipt check stops there on purpose: prompt/config
drift is MORE reason to inspect a lane, never a reason to skip it. The
remaining receipt legs are anomaly flags, not gates: a receipt whose
`taskKey`/`runId` does not match the row surfaces flagged
`receiptMismatch` (a foreign receipt — the row's own evidence is absent
or clobbered — with `decision` nulled because its fields are untrusted),
and a bound `reportSha256` that no longer matches the report bytes
surfaces flagged `reportDrift` (`mismatch`, or `unreadable` when the
report cannot be read — the digest is only computed for non-foreign
receipts). Neither flag stalls a row by itself: a drifted receipt on a
lane still writing its transcript stays invisible until the lane itself
stalls — the flags ride the stall signal, they do not replace it.
Liveness is the transcript mtime under `.ufo/sessions/<runId>/` (the
watchdog's shared lstat-based `newestMtime`, `.jsonl`-filtered — a
symlinked session entry cannot mask a stall), not the row state: an
iterate lane legitimately continuing in-session also has a receipt on
disk while running. A scan fault surfaces the row flagged `scanError` and
the watch never whips blind; a future-dated transcript mtime is
unprovable liveness and surfaces flagged `futureMtime` as idle-unknown
(`idleMinutes: null`), never as fresh; otherwise the row stalls when idle
≥ `--stale-after-min` (default 10 minutes, must be a finite number > 0).
The watch then walks each stalled row in order: malformed runId → noted
invalid, `scanError` → `whip_skipped_scan_error` every tick (never whip
blind), `receiptMismatch` → `whip_skipped_foreign_receipt` deduped once
per reason, `reportDrift` → the kind-selected drift steer
(`driftWhipText`, exported for the owned probe suite alongside
`whipSkipReason`): `unreadable` → `WHIP_DRIFT_UNREADABLE` (restore a
readable report at the result path first — the lane owns that path, and
the generic re-mint is unfulfillable there because create-receipt throws
`unreadable_input` on a missing report — then re-mint, then complete);
every other kind (`mismatch` today, any future kind) → `WHIP_DRIFT`
(re-mint the receipt against the CURRENT report bytes, then
`ufo-sighting complete`) — the safer default when bytes exist to hash.
Either arm bypasses the decision gate because a dead-ended row can never
settle on stale evidence — a terminal decision needs the same re-mint —
and its action line carries the kind (`whip_drift:<kind> ok|failed`).
Only then the decision gate: `decision === "continue"` whips (`whipSkipReason`:
`stop`/`blocked`/`budget_halt` → `terminal_*`, anything else →
`no_continue`), each skip logged once per reason without starting the
cooldown. Only a fired whip starts the per-lane cooldown, so a parked
terminal state never cools down a later `continue`; a failed steer still
earns the cooldown and its child fault rides the action line
(`whip failed … — <fault>`), so a dead pane is diagnosable instead of a
bare failure. The monitor's STALLED display carries the same anomalies —
`foreign-receipt` / `drift:<kind>` after the title, `future-mtime` or
`scan:<err>` in place of a fabricated idle count.

A third L0-owned surface heals the substrate the lanes stand on, not lane
state: `scripts/ufo-night-watchdog.sh` (hub row `night-watchdog`,
`restart=always` + `persist=true` where the hub supervises it — the
`setsid` detached arm covers a dead or absent supervisor, which is the
observed nc5 launch shape; flock self-singleton on
`.ufo/night-watchdog.lock`). On a 60s tick it probes the wall tmux server
(`tmux list-sessions` under `timeout -k`); on absence it recreates the wall
via `ufo-sighting reconcile` + `open`. On wedge it clears a dead-holder
`operation.lock` but never kills a wedged-but-alive tmux server. It reaps
hung tmux clients (>40 non-server processes); enforces dispatcher and watch
singletons (keep-oldest, anchored `^node scripts/…` patterns — lane argv
embeds script names in prompt text, so a bare `pgrep -f` counts lanes as
daemons); respawns absent daemons detached, kills wedged daemons (dispatcher
pending >15min, watch state >6min), and repends blocked fleet rows older
than 240s through `scripts/ufo-watchdog-repend.mjs` — the refusal-aware
helper extracted from this duty (nc5-swarm r07) so the repend decision is
unit-testable without the daemon's flock/pkill/setsid duties. The cap is 3
successful repends per continuously blocked row key (attempt state is
pruned when the row leaves blocked state;
`.ufo/night-watchdog-repends.json`): a refused or failed repend never
consumes an attempt, and a proven-stable refusal class
(`mission_stale_registered`) on an unchanged row signature is suppressed
inside a 900s quiet floor — any row or manifest change re-enables the
attempt immediately, and unchanged rows still retry at least once per
floor. Its
repend arm overlaps the monitor's repend duty deliberately: the watchdog
covers the case where the watch itself is dead. Same ownership rule — L0
surface only; sibling lanes never edit it.

The same L0 surface serves a display-evidence projection that is strictly
observational — never a classifier, controller, or acceptance path. Three
modules carry it. `scripts/ufo-mission-lifecycle.mjs`
(`projectMissionLifecycle`) projects a wall-manifest row and/or queue task
row into the five-phase vocabulary `queued | working | suspended |
completed | failed` (`ufo-mission-lifecycle-v1`): a live wall status
(`starting`/`running`) supersedes stale queue suspension and maps to
`queued`/`working`; queue `paused`/`blocked` maps to `suspended` with the
blocker's `code`/`failureClass` as `suspendedReason`; queue terminal
states win over a `stopped` wall (a closed wall alone is registration
completion, never proof of successful work); crossed runId/sessionId/
missionId identities and live-vs-terminal contradictions fail closed as
invalid input. `resumed` records an observed successful resume dispatch
(`lastDispatch.command === "resume"` with exit 0 or `recoveredExisting`),
never an attempt count; `resumeHint` is advisory only. There is no
terminal-outcome override — an exit or signal is not proof of success or
cancellation. `scripts/ufo-mission-activity.mjs`
(`projectMissionActivity`, `ufo-mission-activity-v1`) attaches bounded
display text: `sanitizeDisplayText` strips C0/C1 controls, ANSI/OSC
sequences, and bidi controls, and neutralizes tmux format tokens
(`#{`, `#[`, `#(`, `#P`, remaining `#` → `♯`) so caller text is safe for
pane-option placement; activity is bounded at 240 code points, the
composed `label` (`phase` + `resumed` + suspended-reason + activity) at
280 — code points, never UTF-16 units or terminal cells. Terminal phases
render the mission `finalNote`; suspended falls back to the reason then
the bare phase. The label dedupes the appended activity against the
phase, `resumed`, the suspended reason, AND the reason's own 240-cp
truncation — the activity channel's bound means a reason longer than
240 cp reaches `buildLabel` already truncated, so deduping against the
untruncated reason alone would append a visible duplicated head fragment
for reasons in the 240–280 window (nc5-swarm r26).
(`reconcileObservation`, `ufo-mission-observation-v1`) is the single
reconciled snapshot the dispatcher computes per task/mission pair on every
reconcile pass and persists to `.ufo/sighting/observations.json`
(`persistObservations` — `activity`/`label` redacted, tmp-file + rename,
unchanged-content skip via a byte-exact serialized cache; a projection
failure emits `observation_project_failed` and never blocks
reconciliation). For `working`/`queued` phases the live activity is the
route currently serving the seat, with precedence split by phase because
the two fields attest different things: `working` prefers
`lastDispatch.route` — the launcher's attested serving route for the
running era (the dispatcher writes `outcome.activeRoute` on every
accepted launch, while `task.route` stays the configured chain head a
fallback hop leaves behind) — falling back to `task.route`; `queued`
keeps the configured `task.route` authoritative over a `lastDispatch`
record that may be stale from a prior attempt; non-string entries are
skipped for the next candidate. Suspended/terminal phases already carry
the reason or final note.
`ufo-sighting` status reads the sidecar through
`loadObservations` — fail-open (absent or empty → empty Map; symlink,
oversized, or unparseable → a Map tagged `unavailable` so status can
distinguish unreadable evidence from none recorded; rows serialized over
8,192 UTF-16 code units,
identity-mismatched or out-of-vocabulary `phase` rows dropped) — with
`statusPhase` (raw wall status → phase) as
the fallback for missions with no persisted row. The statusline hook does
NOT read the sidecar: it spawns `ufo-sighting status` (`--lite` when the
30s full-refresh stamp is fresh — lite skips the operation lock and the
two tmux spawns of the display refresh) through `node`, never the host's
own `execPath` (the omp ELF would re-enter the host, not Node), under a
3s SIGKILL timeout and a 1 MiB stdout cap. Sessions share the result
through `.ufo/statusline-cache.json` (a hit younger than the 5s poll
interval is served; expired, future-dated, corrupt, or symlinked cache
files are misses; writes are per-writer `pid+time+rand` tmp + rename and
refuse a symlinked or non-regular target) serialized by
`statusline-cache.lock` — a `wx` token file whose stale holder
(mtime older than the spawn timeout + 500ms) is stolen by atomic
rename-aside so exactly one stealer wins, and whose release refuses a
FIFO/device path before reading the token. An envelope gate
(`isStatusEnvelope`: object with `levels` + `phaseCounts` objects and a
string `hatch` — exactly what status full/lite always carry) guards both
format and cache write: drifted producer output publishes `CLOSED` and is
never cached, so a `{}` can never render fabricated zero-fleet text for
every session behind the cache (nc5-tooling r15). All three modules also
run as standalone inspection CLIs sharing `readBoundedJsonInput`
(O_NOFOLLOW + O_NONBLOCK open, fstat-pinned 1 MiB bound, mid-read-grow
detection, bounded chunked stdin with EAGAIN retry); their output is
display evidence only — the wall and dispatcher still own every lifecycle
mutation, and no observation row drives routing or acceptance.

The paragraphs below follow one convention: when a sibling frontier
consolidates a duplicated primitive family into the canonical leaf, the
normative layer names it — one paragraph per family, appended in landing
order. Each paragraph names the primitives and their callers, the
contracts callers keep, the consolidating commit, and the dispatcher
parity source where one exists. Codification waits for the consolidating
commit to land: staged-but-uncommitted consolidation is not named here,
so this layer never describes code that does not exist. A dated
CHANGELOG entry and regenerated mirrors ride every codification — the
tracked mirror set is every `skillTargets` copy in
`scripts/sync-ufo-contracts.mjs` except the two gitignored `.devin/`
projections, and `.omp/skills/ufo` is tracked: the sync gate checks the
working tree, so a regeneration left unstaged is gate-invisible and the
commit must stage the whole set. The
dispatcher's own copies stay its own — importing it remains forbidden —
and they are the parity source the leaf mirrors, not a second contract.

The fleet's durability primitives share one canonical leaf,
`scripts/ufo-mission-result.mjs` (sibling `5048f4ed` collapsed the
private copies) — the adopting scripts import it there
rather than carrying a private copy (the pre-consolidation per-file
copies drifted silently; one implementation keeps the contract
single-sourced — `ufo-state-retention.mjs` still keeps private
`readBoundedFile`/`writeFileAtomic` bodies, `omp-global-config.mjs`,
`the-tick-config.mjs`, and `collect-omp-native-handoff-lib/base.mjs`
their private `readBoundedFile` bodies, and the
dispatcher keeps its own by the import ban below). `readBoundedFd`
fstat-pins the descriptor, pre-fails a regular file already over the
bound (`too_large`), allocates stat-size + 1 slack so a mid-read grow
consumes the slack byte and fails `changed`, retries EAGAIN only on
non-regular fds (an inherited O_NONBLOCK stdin is a drained pipe, not a
dead one), and post-read fstats so a file that changed size mid-read
fails `changed` — including the empty-at-fstat case. `readBoundedFile`
opens `O_NOFOLLOW|O_NONBLOCK` (a symlink propagates ELOOP for the caller
to map; a FIFO fails `not_regular` instead of hanging) and delegates to
`readBoundedFd`. `readBoundedStdin` is fd 0 through the same loop with
raw read faults wrapped as `read_error`. `writeFileAtomic` publishes via
a random `pid+UUID` O_EXCL tmp at 0o600 (a predictable tmp name is a
symlink-squat target on operator-controlled destinations), fsyncs before
rename, fsyncs the directory after, and unlinks the tmp on failure; it
never mkdirs the parent. Every CLI caller passes its own `fail(message,
kind)` so typed error contracts survive byte-identically (the lock-owner
`readBody` seam reads on the leaf default) — kinds are
`too_large` | `not_regular` | `changed` | `read_error`. The mission-*
modules' `readBoundedJsonInput` above is a thin adapter over these
primitives, not a second implementation. The private `readBoundedFile`
copies carry the same `O_NOFOLLOW|O_NONBLOCK` pair (nc5-tooling r15 closed
the last two — a planted FIFO at a config/authority path otherwise blocked
the synchronous open before the `isFile` refusal could run) with one
exception: `ufo-state-retention.mjs`'s private opens stay `O_NOFOLLOW`-only
(the residual FIFO-wedge class is flagged to tooling, not reconciled here).

The same leaf hosts the fleet's shared lock protocols (sibling
`836d9dcb` collapsed the private copies). `withDirLock` is the
mkdir-claimed directory mutex — dispatcher/monitor queue-lock parity:
the holder binds its claim with an `owner.json` (pid + token,
O_EXCL/O_NOFOLLOW, 0o600, fsync'd before any contender can read it); a
contender breaks a held lock only when the owner pid is dead or the
owner record is unreadable once the dir passes a 30s freshness grace
(a future-dated mtime proves nothing and still attempts the break);
the break is fenced — the held dir is quarantined by rename and a
seized owner whose token differs is renamed back, so only a
proven-string token match deletes; release removes the dir only while
`owner.json` still carries the holder's token; acquisition gives up
after 30s; a symlink or non-directory at the lock path fails the
acquire. Callers keep their own token, messages, and owner reader —
the monitor keeps `assertQueueParent` and its `l0-` token, the wave
keeps the registry's parent creation and its typed `invalid_registry`
owner reads. `acquireSingletonLock` is the ticket-serialized singleton
claim shared by `ufo-l0-watch` and `ufo-stale-watchdog`: a
`<lock>.takeover` ticket serializes contenders, the owner record is an
inode-bound hardlink pair carrying pid + starttime + bootId (a torn
pid body recovers through the link), owner state classifies
`dead`/`stale`/`live`/`foreign_live` (identity-observed staleness,
legacy module match as fallback), a `foreign_live` owner is quarantined
`.bad.*` rather than deleted, and the claim is bounded at 8 attempts.
`pidIsAlive` and the proc-identity helpers (`readProcText`,
`readBootId`, `readPidStarttime`, `procIdentity`,
`legacyOwnerMatchesModule`) are deduped here from five byte-identical
copies (`ufo-sighting.mjs` still keeps its own
`pidIsAlive`/`readBootId`/`readPidStarttime` bodies and
`ufo-state-retention.mjs` its own `pidIsAlive` — and
`fleet-ledger-rotate.mjs`/`run-omp-native-trial.mjs` keep private probes
— outside that collapse).
The dispatcher's queue lock and `ufo-sighting`'s
`operation.lock` keep their own bodies — the dispatcher copy is the
parity source `withDirLock` mirrors, not a second contract. The sighting
copy's quarantine arm diverges deliberately on the unreadable-owner edge:
when the seized lock's `owner.json` cannot be read there is no token to
compare, so the quarantine is renamed back rather than deleted — deleting
could destroy a contender's LIVE lock — and a restore that fails with
`EEXIST`/`ENOTEMPTY` proves a contender's fresh `mkdir` won, making the
quarantine's deletion safe.

The same leaf hosts the fleet's log and state-publish primitives
(sibling `8f098cc8` collapsed the private copies). `appendRotatingLog`
is the bounded append-only log called by `ufo-stale-watchdog`'s
telemetry path and by the leaf's `appendStampedLog`, which serves the
watch's `log` and the monitor's `appendLog`: the open carries
`O_NOFOLLOW` (a planted symlink at the fixed log path is refused),
`O_NONBLOCK` (a FIFO fails instead of hanging the caller), `O_APPEND`
(each regular-file write stays atomic), and mode 0o600 (evidence stays
owner-only). Once the open file reaches `maxBytes` the live segment is
renamed to `<path>.1` — one segment is the whole generation set, so the
loss bound is one generation by design; rename(2) is an atomic replace,
so a planted link at the segment path is unlinked without its target
being written. A failed rename keeps the bound soft — the caller's
`rotateFailedLine` is appended to the still-open old fd and the payload
follows it; a successful rename closes the old fd (it still names the
renamed inode), reopens the live path, and writes the caller's
`rotatedLine` inline — never through the function again, so rotation
cannot re-enter itself. `writeFileAtomicIfChanged` is the quiet-tick
publish shared by the watch's `writeState` and the watchdog's
`saveState`: a bounded compare-read plus `Buffer.equals` proves the
file already carries exactly this body and skips the
tmp+rename+fsync+dir-fsync an unchanged state file used to pay every
poll; a corrupted file parses to a different normalized body so
repair-on-load still lands, an external edit differs so
last-writer-wins still overwrites, and an absent or unreadable file
falls through to `writeFileAtomic`. The compare is `Buffer.equals`,
never a decoded-string compare — decoding would alias invalid-UTF-8
file bytes onto U+FFFD and skip a needed repair. Callers keep their own
telemetry bodies and rotation-line text — the watchdog's stamped
telemetry and its rotated/rotate-failed lines stay caller-owned, while
the watch's `log` and the monitor's `appendLog` take the shared stamped
composition (`appendStampedLog`, the sixth paragraph below).

The same leaf hosts the fleet's path-containment and credential gates
(sibling `b0173d15` collapsed the private copies — the drift class was
already realized: the stale watchdog's `redact` lacked the AWS
AKIA/ASIA line the dispatcher canonical carries). `beneath` is the
S-04 containment check shared by the wave planner, collect, and the
monitor — the L0 watch reaches it through the leaf's `containedJoin`:
it realpath-anchors the root (a fresh root
that realpathSync cannot resolve falls back to `resolve(root)` only on
ENOENT), rejects any candidate whose relative path escapes (`..`,
absolute), and walks every resolved component refusing symlinks — an
ENOENT component mid-walk is skipped, not failed. `CREDENTIAL_SHAPE`
and `redact` are the S-06 pair shared by the monitor (the stale
watchdog adopts `redact` alone): the shape matches
key=value credential keys (including `cookie`/`set-cookie`), bearer
and basic blobs, provider key prefixes (`sk-`/`xai-`/`rk-`/`ak-`,
`ghp_`/`gho_`/`ghu_`/`ghs_`/`ghr_`, `github_pat_`), AWS access-key ids
(AKIA long-term, ASIA temporary), JWTs, and PEM private-key blocks;
`redact` rewrites each class to a typed placeholder — `[REDACTED_PEM]`,
`[REDACTED_JWT]`, `[REDACTED_KEY]`, and `[REDACTED]` for bearer/basic/
key=value blobs.
`optionValue` is now a parity leaf with no consumers — collect, its
last importer, moved to `parseDeclaredArgv` one round after the wave
CLI (sibling `a9e89555`, nc3-swarm r57): a duplicate flag and a
missing or `--`-leading value are usage errors routed through the
caller's own typed `fail()`, and that convention survives as the
parity source each `parseDeclaredArgv` adopter restates per call
site. The leaf stays exported but unimported (the dispatcher's,
fake-omp's, `ufo-state-retention.mjs`'s, and `ufo-sighting-lib/argv.mjs`'s
private same-name helpers are unrelated copies with
different signatures, not leaf consumers). The dispatcher's own copies of `beneath`,
`CREDENTIAL_SHAPE`, and `redact` stay its own — its module-load side
effects are why the copies existed, and importing it remains
forbidden; the dispatcher copies are the parity source the leaf
mirrors, not a second contract (the dispatcher's `redact` carries a
quoted-value arm the leaf's does not — the leaf mirrors the unquoted
shape).

The same leaf hosts the fleet's queue-row trust-boundary primitives
(sibling `d0dd958a` collapsed the private copies — monitor `absPath` /
watch `queueRowPath`, watch `statSignature` / the monitor's inline memo
key, the `gq<16hex>` row-id check, the bounded queue read + shape
validation, and the dispatch-snapshot prompt layout had each been
re-derived per consumer). `MAX_QUEUE_BYTES` is the shared 4 MiB bound,
parity with the dispatcher's constant: its acceptance path reads report
and receipt bytes under the same bound, so an oversized artifact fails
closed instead of OOMing a consumer pass — and could never be accepted
anyway. `ALLOW_EXTERNAL_TOOLS` is the S-04 escape flag bound once at
module load, dispatcher parity on the same env var; production stays
default-deny. `isQueueRunId` enforces the dispatcher-minted
`gq<16 hex>` row-id contract (enforced at queue write): anything else
is corruption, not a live lane — and a state-table hazard, since a
`__proto__`/`constructor` runId makes `lanes[id] ??=` resolve to
Object.prototype; the strict pattern makes the inherited-name probe
redundant. `containedJoin` joins a queue-row path field under the root
through the shared `beneath` walk plus the escape flag and returns null
— never throws — so one bad row degrades to a skipped finding instead
of killing the whole pass. `statSignature` is the lstat-based artifact
signature backing the monitor's digest memo and the watch's hole
verdict: lstat rather than stat because `beneath` already refuses
symlinked components and under the escape flag a link's own identity
must still invalidate; any rewrite bumps mtimeNs/ctimeNs/size/ino so a
changed artifact always misses and re-validates fresh — the same trust
boundary the dispatcher's `archiveDirPartsMemo` declares; null means
absent or unreadable, which callers treat exactly like an existsSync
gate. `readQueueFile` is the bounded queue read plus parsed-shape
validation: the dispatcher always writes `tasks` as an array of row
objects, so a truthy non-array or non-object element is corruption —
the shape fault routes through the caller's `fail()` (`optionValue`
convention: each caller keeps its own typed error class) while a JSON
SyntaxError propagates for the caller to name. `dispatchSnapshotPromptPath`
is the snapshot layout `.ufo/sessions/<runId>/dispatch-snapshot-<attempt>/prompt.md`
returned as a RELATIVE path — the caller gates it through
`containedJoin` like every other row path field — or null when the
row's attempt counter is not a positive integer. The wave planner and
collect adopt the shared `ALLOW_EXTERNAL_TOOLS` for their own gates;
the stale watchdog's `isSafeRunId` stays deliberately broader (its
`RUN_ID_PATTERN` accepts sighting-shaped ids plus the inherited-name
probe) and keeps its own body. The dispatcher's copies — the
`MAX_QUEUE_BYTES` constant, `QUEUE_RUN_ID_PATTERN`, and the snapshot
layout built in `dispatchQueuedTask` — stay its own: importing it
remains
forbidden, and they are the parity source the leaf mirrors, not a
second contract.

The same leaf hosts the fleet's wipe-recovery and stamped action-log
primitives (sibling `f9d67284` collapsed the private copies — three
mkdir-retry bodies and two stamped-log compositions across the monitor
and the watch). `writeWithMkdirRetry` is the ENOENT-mkdir retry for
fixed-path writes: a mid-run `.ufo` wipe used to convert a passing heal
into a non-zero exit at its last step (the monitor_failed cluster
during the documented wipe recovery). One retry after recreating the
parent dir; every non-ENOENT fault propagates — or, under `swallow`, is
dropped entirely. `appendStampedLog` composes the
stamped action-log append shared by the monitor's `appendLog` and the
watch's `log`: each line is whitespace-collapsed at the boundary (a
crafted queue-row value can never inject a forged log line),
ISO-stamped, joined, and appended through `appendRotatingLog` with the
shared one-generation rotation lines, under the `writeWithMkdirRetry`
recovery. `swallow` selects the doctrine: the monitor propagates (a
failed heal log is a real fault, not a daemon tick to survive) while
the watch swallows log faults (an unwritable log must never kill the
daemon) yet propagates state-write faults to the tick-level catch,
which logs `tick_error` and keeps cadence — the same best-effort
outcome through the loop guard rather than the write. The stale
watchdog keeps its own `appendRotatingLog` telemetry path — it has no
stamped multi-line action log to consolidate — and the shell night
watchdog's `say` stays a printf append outside the leaf.

The same leaf hosts the fleet's bounded artifact digest (sibling
`f3a078b2` collapsed the private copies — the watch's verbatim
`createHash` body and the monitor's inline digest line). `sha256File`
is `createHash("sha256")` over `readBoundedFile(path, maximum, label)`:
artifact bytes are read under the same bound the dispatcher's
acceptance path applies, so an oversized artifact fails closed at
digest time instead of OOMing the pass — and would be rejected at
acceptance anyway. The monitor keeps its `statSignature`-memoized
wrapper (aliased import): one row's prompt/config/report is digested by
diagnose, repair, rebind, settle and findStalled inside a single pass,
the memo key is `maximum:signature`, a null signature leaves the read
unmemoized, and failures are never memoized — an unreadable artifact
raises on every call, preserving per-row fault isolation. The watch
calls the primitive directly, and the respawn/settle report digest
binds the receipt to the report bytes on disk. Bound and label
are caller arguments, not leaf constants, so the per-call-site bounds
stay visible rather than buried: the monitor digests source prompts
under `MAX_PROMPT_BYTES` (dispatcher parity on the prompt read) while
config and report digests run under `MAX_QUEUE_BYTES` on both daemons;
the snapshot-prompt bound is unified at `MAX_QUEUE_BYTES` inside
`snapshotPromptSha256` (the snapshot-prompt paragraph below). The
dispatcher's own digest compositions — `digest(readBoundedFile(...))`
inline at the acceptance
path and the snapshot-membership walk — stay its own: importing it
remains forbidden, and they are the parity source the leaf mirrors, not
a second contract.

The same leaf hosts the fleet's direct-entry guard (sibling `02897376`
collapsed the private copies — eight verbatim watchdog-guard bodies
across the monitor, the L0 watch, the three mission-* projection CLIs,
the stale watchdog, swarm-collect, and the wave planner; the leaf also
guards its own CLI). `isMainModule(moduleUrl)` answers whether the
process is a direct invocation of the calling module: `process.execArgv`
carrying `-e`/`-p`/`--eval`/`--print` is never a direct invocation —
`node -e 'import(...)' <module-path>` puts the imported path in argv[1]
too, so without the screen an import ran the whole CLI (queue scans,
transcript reads, and whatever mutation the importer's argv happened to
carry) — a missing `argv[1]` is not a direct invocation, and the
comparison realpaths BOTH sides: `realpathSync(argv[1])` against
`realpathSync(fileURLToPath(moduleUrl))`, with any realpath fault
fail-closed to false (a library importer's synthetic argv must not
crash on the guard). The two-sided realpath is the drift class the lift
realized and fixed: the pre-consolidation copies realpathed only
argv[1], so under `--preserve-symlinks` — where `import.meta.url` stays
the symlink path while argv[1] resolves — an intentional symlinked
launch silently refused to run. Callers keep their own entry bodies:
each CLI binds `const isMain = isMainModule(import.meta.url)` at module
(importing it remains forbidden); `ufo-sighting.mjs:4704`,
`sync-global-routing.mjs:377-379`, `fleet-ledger-rotate.mjs:1324`, and
`ufo-state-retention.mjs:77` compare without realpathing argv[1] at all
(a symlinked launch exits 0 having done nothing);
`run-omp-native-trial.mjs:4293`, `the-tick-ping.mjs:716`,
`ufo-ground-handler.mjs:779`, and `charter-scribe/sync.mjs:808`
realpath only argv[1] (the same `--preserve-symlinks` refusal class the
leaf fixed); `prepare-ephemeral-l1.mjs:939` realpaths argv[1] against a
load-time `fileURLToPath`'d MODULE_PATH (`prepare-ephemeral-l1.mjs:31`) — equivalent to the leaf
under default module resolution, minus the execArgv screen (under
`--preserve-symlinks` it shares the refusal class: MODULE_PATH is not
`realpathSync`'d).
The same leaf hosts the fleet's snapshot-prompt digest (sibling
`da2b38d2` collapsed the private copies — verbatim bodies in the L0
monitor and the L0 watch). `snapshotPromptSha256(root, runId, attempt,
digest = sha256File)` digests `dispatch-snapshot-<attempt>/prompt.md` —
the snapshot prompt bytes the lane actually received (skill lines plus
the injected binding overlay), which a receipt may bind instead of the
drifting source file. The queue-row runId is gated through
`containedJoin` like every other row path field — a `..` or non-string
runId yields null, never an out-of-root read — and any digest fault
returns null rather than throwing out of the settle pass. The bound is
`MAX_QUEUE_BYTES`, the dispatcher's own snapshot bound — the realized
drift class the lift fixed: the monitor's private copy digested under
`MAX_PROMPT_BYTES`, which would have false-nulled the fallback on a
>512 KiB snapshot the dispatcher accepts. The optional `digest`
parameter keeps per-pass memoization caller-owned: the monitor passes
its `statSignature`-memoized `sha256File` wrapper, the watch calls the
primitive directly. The dispatcher's own snapshot digest —
`dispatchSnapshotPromptSha256` (`fleet-dispatcher.mjs` private helper), a
presence-based SET over every `dispatch-snapshot-*` directory under the
run's session dir (superseded renames and prior attempts included) —
stays its own: importing it remains forbidden, and it is the parity
source the leaf mirrors, not a second contract. The dispatcher accepts a
receipt prompt digest matching any preserved `dispatch-snapshot-*` prompt,
not only the row's current attempt. The leaf's snapshot-path
builder `dispatchSnapshotPromptPath` is module-private (sibling
`f74b7fae` unexported it): the leaf's public surface stays the digest
primitive alone — callers resolve paths through their own row context,
never through a shared path builder.

The same leaf hosts the fleet's plain-object predicate (sibling
`1ebc7323` collapsed the private copies — four verbatim bodies across
`ufo-mission-activity`, the stale watchdog, swarm-collect, and the wave
planner, plus a dozen inline expansions across the monitor, the L0
watch, `ufo-mission-lifecycle`, `ufo-mission-observation`, and the
leaf's own queue-shape and JSON-input checks). `isPlainObject(value)`
is the non-throwing shape half of the leaf's `plainObject` guard:
`value !== null && typeof value === "object" && !Array.isArray(value)`.
The predicate inspects no prototype — a class instance or a
null-prototype object passes — so it answers "is this a record-shaped
value", never "is this a literal `{}`"; callers needing the stricter
contract keep their own check. The collapsed spellings were
semantically identical but textually divergent — `x === null ||
typeof x !== "object" || Array.isArray(x)` beside `!x || typeof x !==
"object" || Array.isArray(x)` beside `x !== null && typeof x ===
"object" && !Array.isArray(x)` — the drift class the lift fixed: a
future semantic fix to the boundary check would have had to find and
edit sixteen spellings, and the falsy-first forms read as if they
rejected `0`/`""`/`false` where the null-first forms read as if they
rejected only `null`. The dispatcher's private copy
(`fleet-dispatcher.mjs` `isPlainObject`) stays its own — the leaf's parity
source per the convention above. The non-adopting spellings stay their own and the divergence
is now visible per call site: `ufo-state-retention.mjs:350` keeps a
verbatim private copy (the script imports nothing from the leaf);
`prepare-ephemeral-l1.mjs:56` keeps a STRICTER contract — its
`Object.getPrototypeOf` check rejects class instances and null-prototype
objects that the leaf accepts;
and the inline expansions outside the lift's adopt scope —
`collect-omp-native-handoff.mjs` + `collect-omp-native-handoff-lib/`
(36 pure-predicate sites across the module family — entry 5, base 1,
events 1, evidence 7, policy 22, screening 0; a site is a condition
that IS the predicate, not one containing it — and the family adds a
fourth spelling the collapsed set did not carry: `x && typeof x ===
"object" && !Array.isArray(x)`, falsy-rejecting but semantically
identical), `run-omp-native-trial.mjs`,
`probe-ufo-route-health.mjs`, `project-devin-subagents.mjs`,
`local-helper.mjs`, `omp-native-shutdown.mjs`, `omp-role-work.mjs`,
`fleet-dispatcher.test.mjs` — remain unconsolidated, not wrong.

The same leaf hosts the fleet's either-binding receipt validation
(sibling `5e6dd1bc` collapsed the private copies — one verbatim 9-line
block in each L0 daemon: the monitor's `settle` admission and the
watch's hole verdict). `validateTaskReceiptEitherBinding(parsed,
expected, snapshotDigest)` encodes the acceptance contract both daemons
carried: a receipt may bind the SOURCE prompt digest (the queue row's
`promptSha256`) or the dispatch-snapshot digest (the prompt the lane
actually received — the dispatcher's `dispatch_snapshot`
bindingSource). The source binding is tried first; on a
`receipt_mismatch` naming `promptSha256` the snapshot digest is
resolved and the receipt retried against
it — but only when the row resolves one: a null snapshot digest
rethrows the source-binding error, so a missing snapshot never masks
the real mismatch. `snapshotDigest` is a caller-supplied thunk, not a
leaf-resolved path: the monitor passes its `snapshotPromptDigest(task)`
wrapper, the watch the same, keeping row-context resolution
caller-owned like the leaf's other injected dependencies. The
dispatcher stays the parity source — importing it remains forbidden —
and its own check is set-membership over every `dispatch-snapshot-*`
directory under the run's session dir (superseded renames and prior
attempts included): the daemons' single current-attempt fallback is
the stricter subset this helper encodes, so a receipt the dispatcher
would accept on a superseded attempt still fails the daemons — the
set-vs-single divergence the snapshot-digest paragraph named, now
visible as a typed helper boundary rather than two hand-rolled
try/catch ladders.

The same leaf hosts the fleet's declared-argv walk (sibling `f74b7fae`
collapsed the private copies — the monitor's and the L0 watch's
per-daemon loops, each closing the same silent-degradation class:
unknown arguments, value options missing their value, a declared flag
where a value belongs, and duplicate value options).
`parseDeclaredArgv(args, flagNames, valueNames)` walks the declared
surface once and returns `{ flags, values, faults }`: a declared flag
is recorded and consumes nothing; a declared value option faults
`duplicate <name>` on seen-ever re-appearance (the watch's stricter
arm — `--x a --x` reports duplicate, not requires-a-value), faults
`<name> requires a value` when the next argument is absent or itself
declared (a swallowed flag is never a value), consumes a present value
so it is never re-walked as unknown, and keeps the first valid value;
anything else faults `unsupported argument: <arg>`. The caller owns
the refusal — both daemons append their own value-domain checks to
`faults` and emit one typed usage error before any queue read, lock,
or mutation. The lift realized two drift classes: the watch's old
`option()` helper was `argv.indexOf`-based and returned the raw next
argument unvalidated — a declared flag could surface as a value on a
fault-free path the walk had not closed — and the monitor's copy
emitted fewer faults on `--x --x a` (requires-a-value only, where the
leaf reports duplicate AND requires-a-value; the bound value is
identical). The dispatcher's `assertArguments` checks declared value
options for missing or flag-shaped values and throws on the first fault;
it does not walk or reject unknown arguments by itself. This private check
stays its own — importing it remains forbidden. The wave CLI adopted the
leaf walk one round later (sibling `78e6c13e`) for its `record` and
`plan`/`run` spec surfaces, with a stricter bound-value arm at each call site.
`ufo-swarm-collect.mjs` adopted the walk the round after that (sibling
`a9e89555`, nc3-swarm r57) — a fourth adopter carrying the same
`--`-leading-value arm plus a second stricter arm the leaf did not
have: a duplicate `--emit-xml` is refused at the precedence the
private walk kept (after the value-option faults, before the required
checks), while the leaf records a declared flag idempotently and
dedupes it silently. The adoption retired the last `optionValue`
importer. Both stricter arms are now leaf primitives themselves
(sibling `eb37076b`, nc3-swarm r67): `rejectFlagLikeValues(parsed,
valueNames)` unshifts `requires a value` onto a bound value that leads
with `--` — the `optionValue`-parity arm the wave (`ufo-swarm-wave.mjs:1569` record,
`ufo-swarm-wave.mjs:1748` plan/run) and collect (`ufo-swarm-collect.mjs:676`) each restated — and
`hasDuplicateArg(args, name)` is the indexOf/lastIndexOf predicate a
CLI calls when it refuses a flag the walk dedupes silently (collect's
`--emit-xml` at `ufo-swarm-collect.mjs:683`, the wave's `--emit-tasks` at `ufo-swarm-wave.mjs:1767`). The
doctrine is unchanged — the leaf still consumes undeclared
`--`-leading tokens as values and still dedupes declared flags — but
the two refusal shapes now live in one place instead of three.
The non-adopting argv surfaces stay their own and the divergence is
now visible per call site: `prepare-ephemeral-l1.mjs:884`,
`the-tick-ping.mjs:549`, `probe-ufo-route-health.mjs:102-148`, and
`ufo-sighting-lib/argv.mjs:22-35` throw or fail on first fault;
`collect-omp-native-handoff.mjs:118-141` and `fake-omp.mjs:69-80` write
their own usage text; `ufo-mission-activity.mjs:158-183` and
`ufo-stale-watchdog.mjs:971-972` fault unsupported arguments through
their own typed paths — different refusal shapes, not the
collect-then-refuse
walk the leaf codifies. Every census pin in this section cites
COMMITTED bytes (HEAD), never the working tree: sibling WIP shifts
lines without drifting a claim, and a pin verified against uncommitted
bytes is wrong the moment it is written — the `the-tick-ping.mjs`
pin above drifted exactly that way (minted at `the-tick-ping.mjs:549` against WIP;
an intermediate HEAD carried the throw at `the-tick-ping.mjs:541`; current HEAD
carries it at `the-tick-ping.mjs:559` inside the `take` helper spanning `the-tick-ping.mjs:549-560`).
Pin spelling follows one rule: `file.ext:NNN` names its target and is
the required form when the cited file is not the nearest named file in
the sentence; a bare `:NNN` is a relative pin bound to the nearest
preceding `file.ext` mention in the same paragraph — drift-prone
because a re-anchor that updates the named pin can silently leave the
bare one pointing at the old line (the r03 audit found 14 such pins a
`file:NNN`-only census missed). Prefer `file.ext:NNN` whenever the pin
stands alone or the paragraph names more than one file.

The same leaf hosts the fleet's malformed-element row filter (sibling
`eb723399` collapsed the private copies — one hand-rolled `filter` in
each L0 daemon: the watch's `malformedReportMembers` walk over the
monitor report's row arrays and the stale watchdog's
`malformedMissionElements` walk over `status.missions`).
`plainObjectRows(value, onMalformed)` keeps the well-formed
`isPlainObject` members and names each skipped element to the caller's
callback by index — a `null` or a string member used to `TypeError` on
`row.title`/`m.status` and kill the whole duty, so the filter closes
that silent-death class while the surviving rows still reach their
duties. The caller owns the malformed descriptor format (watch:
`member[i]`; watchdog: `missions[i]:<type>`), so emitted telemetry stays
byte-identical to the private walks. The watchdog's `jsonTypeName`
helper is its own private precision fix, not a leaf export: the three
`=== null ? "null" : Array.isArray ? "array" : typeof` spellings named
the same descriptor and the state-member arm silently lacked the null
arm, so a null member reported `"object"` — one helper now reports
the correct `"null"` descriptor. The dispatcher's private `sightingStatus`
element check rejects the whole status on ANY malformed row
(`status.missions.every((row) => isPlainObject(row))`), whereas the leaf
filter skips malformed members and keeps the well-formed ones. The
dispatcher manifest validation also rejects null mission rows.
`receiptCoreFields` is a module-private dedup inside the leaf (the mint
and admission paths used to repeat the seven-field binding block verbatim);
it is not an export and not a fleet primitive.

The dispatcher carries the same private-dedup class (sibling `82d08c49`,
nc3-dissection r17): `beneath(root, candidate, reasonOut)` collapsed
hand-rolled containment checks into one fail-closed primitive: it anchors
the root with realpath, resolves the candidate lexically, rejects symlink
components, and uses stat-keyed memoization (dev:ino:mtimeNs:ctimeNs)
to re-probe a swapped parent. Callers use it at ledger, executable-path,
classifier-fixture, configured-queue, root/state scope, stored-path and
queue-path gates. `clearLatched(kind)` clears the telemetry latch
at recovery edges so a recovered sibling reader/rotator retires its own
fault.
Both are module-private: not exports, not fleet primitives, and
importing them remains forbidden.

The collect bridge carries the same private-dedup class (siblings
`068fa666`, `c0c373b8`): `optionalBoundedString` (`ufo-swarm-collect.mjs:213`)
collapsed five hand-rolled bounded-string checks — wave item, results
item/result/stopReason, registry item — each call site keeping its own
code, label, and byte cap so emitted messages stay byte-identical;
`soleEvidence` (`ufo-swarm-collect.mjs:554`) collapsed the two
distinct-non-null conflict walks (agent ids, item text) into one
helper whose `conflicting_member` semantics are the join contract
stay internal); `OPERATOR_PATH_ERRNOS` (`ufo-mission-result.mjs:879`) names the errno set
an operator can fix by retyping a path flag (ENOENT/ENOTDIR/ELOOP/
EACCES/EPERM/EISDIR map to the caller's typed code; resource faults
typed fail); `resolveAgentId` (`ufo-swarm-collect.mjs:529`) collapses the
absent-or-resolvable agent-id checks (absent → null, unresolvable →
typed fail); `requireArray` (`ufo-swarm-collect.mjs:542`) collapses the member-list
`!Array.isArray → fail(code, "<label> must be an array")` checks —
`registry.members` accepts object-or-array (a deliberately different
surface) and stays inline. All are module-private except the hoisted
`OPERATOR_PATH_ERRNOS` (an export of `ufo-mission-result.mjs:879`,
imported at `ufo-swarm-collect.mjs:52`): not fleet primitives, and
importing the rest remains forbidden — the parity source for any future
adopter is the join contract, not the helpers.

The same leaf hosts the fleet's idle-wait and JSON-emit primitives
(sibling `232f0cef`, nc3-swarm r64). `spinWait(ms)` is the single
`Atomics.wait` on a fresh zeroed `SharedArrayBuffer` cell that every
poller spelled inline — the leaf's own `readBoundedFd` (1 ms),
`acquireSingletonLock` (2 ms), and `withDirLock` (caller-scaled
`waitMs`) loops plus the L0 watch's `INTERVAL_MS` tick and the stale
watchdog's `POLL_MS` tick, five adoptions of one spelling; each caller
keeps its own cadence, so the primitive carries no timing policy.
`emitJson(value)` is the `JSON.stringify(value, null, 2)` + trailing
newline stdout write — four sites inside the leaf's `main()` plus the
wave CLI's registry-record and plan/run outputs, six adoptions; the
leaf's pre-computed-string and XML emit branches stay their own
different shapes. `rethrowInputError` is a module-private dedup inside
the leaf (not an export, not a fleet primitive): both `main()` read
sites spelled the same errno doctrine — a `MissionResultError` passes
through, an errno-coded fs fault keeps `unreadable_input`, and an
uncoded throw is `internal`, never an operator-facing code. The same
commit collapsed `validateTaskReceipt`'s six hand-rolled expected-bag
checks into one cross-check table — a supplied expectation must equal
the receipt's bound field, else `receipt_mismatch` naming that field's
doctrine label (`expected task` for taskKey/runId/sessionId/
promptSha256, `stored config digest`, `result file`) — one doctrine
per bound field, unchanged semantics.

The same leaf hosts the fleet's residue primitives (sibling `d3998f39`).
`readBoundedJson(path, maximum, label, fail)` composes
`JSON.parse(readBoundedFile(…).toString("utf8"))` for bounded JSON
artifact reads —
eleven call sites: the monitor's four receipt reads (parent, prior,
settle, and scan), the watch's three, the wave's policy and lock-owner
reads, and the leaf's own `readQueueFile` plus `withDirLock`'s `readOwner`
default. A JSON SyntaxError propagates for the caller to name; `fail`
keeps the caller's typed-error contract (the `readBoundedFile`
convention). `collapseWhitespace(value)` is the
`String(x).replace(/\s+/gu, " ")` one-line collapse — seven call sites:
the leaf's `appendStampedLog` stamp, the monitor's `field()` and
repend-fault clip (`ufo-l0-monitor.mjs:360`/`ufo-l0-monitor.mjs:842`), the watch's
`noteInvalidRunId` pair (`ufo-l0-watch.mjs:309`/`ufo-l0-watch.mjs:313`) and `childFault` (`ufo-l0-watch.mjs:544`), and activity's `sanitizeDisplayText`
(`ufo-mission-activity.mjs:67`); callers keep their own slice bounds at the call site.
`emitErrorJson(payload)` is the `process.stderr.write(JSON.stringify(
payload) + "\n")` typed-boundary emit — eighteen call sites across nine
files (monitor 4, watch 2, activity 1, lifecycle 1, observation 1, the
leaf's own `main()` catch, watchdog 1, collect 3, wave 4); the payload
shape (schema, code, message, optional details) stays the caller's.
`TERMINAL_QUEUE_STATES` is the shared `{completed, failed}` set —
dispatcher parity made structural (the dispatcher's private copy at
`fleet-dispatcher.mjs:138` stays its own, importing it remains
forbidden): the monitor binds it as `TERMINAL` (`ufo-l0-monitor.mjs:133`), the watch
imports it directly (`ufo-l0-watch.mjs:58` — the
`TERMINAL_QUEUE_STATES_LOCAL` alias was removed nc4-swarm r01);
`ufo-state-retention.mjs:126` keeps a verbatim private copy (the script
imports nothing from the leaf).
`MAX_EVIDENCE_LOG_BYTES` is the shared 1 MiB evidence-log cap —
monitor `ufo-l0-monitor.mjs:855`, watch `ufo-l0-watch.mjs:451`, watchdog `ufo-stale-watchdog.mjs:130`, each aliased
`MAX_LOG_BYTES`; the watchdog's `MAX_STATE_BYTES` is a different class
and stays local. `expectedReceiptBag(task, reportSha256)` is the
six-field expected bag the monitor's settle (`ufo-l0-monitor.mjs:1038`) and the watch's
hole verdict (`ufo-l0-watch.mjs:819`) rebuilt inline — `promptSha256`/`configSha256`
ride the bag (omitted-as-undefined when the row carries none); the
either-binding's `snapshotDigest` callback is the second arm for a
rebound prompt, not a substitute for the source binding.
`nonStringFields(obj, fields)` is the present-non-string field walk the
wave's registry loader ran twice (`ufo-swarm-wave.mjs:513` document fields, `ufo-swarm-wave.mjs:534` member
fields) — a declared-but-mistyped field is corruption named by the
caller's typed error. The non-adopting spellings stay their own and the
divergence is documented at each site: collect's `readJsonInput` keeps
its `enoentAsNull`/errno doctrine, the wave's `loadRegistry` keeps its
own `invalid_registry` parse arm, the watchdog's `readBoundedFile` keeps its utf8-string return and EINVAL/EFBIG codes, the watch's
`readState` lane-field loop treats null as corruption too (a different
predicate, `ufo-l0-watch.mjs:407`), the watch's `writeSync(1, …)`
refused payload and the watchdog's `writeSync(2, …)` telemetry fallback
are not the CLI envelope, and `ufo-ground-handler.mjs:347` carries a
same-name `readBoundedJson` with a response-object signature — an
unrelated private copy, not a leaf consumer. `buildRegistryDoc`
(`ufo-swarm-wave.mjs:617`) is a module-private dedup inside the wave
(`mainRecord` plus the registry rewrite at `ufo-swarm-wave.mjs:1477`/`ufo-swarm-wave.mjs:1714`): not an
export, not a fleet primitive. Sibling `2ef45bed` (nc3-swarm r68) added
two more: `stalledIdleText(row, suffix)` is the leaf's stalled-row idle
field — the monitor's text report (`ufo-l0-monitor.mjs:1571`, suffix
`" idle"`) and the watch's whip action line (`ufo-l0-watch.mjs:1018`,
suffix `""`) rendered the same three-arm doctrine (a scanError shows the
fault, a future-dated transcript mtime is unprovable liveness named
`future-mtime`, an absent transcript is `no-transcript`, and only a
provable age renders as minutes); the watch never sees a scanError row
but the arm stays so the helper is total over the row shape.
`rejectDuplicate(entries, onDuplicate)` is a module-private dedup inside
the wave (`ufo-swarm-wave.mjs:319`; expanded-prompt `ufo-swarm-wave.mjs:989`, resume-id
`ufo-swarm-wave.mjs:996`, `--assignments` handle `ufo-swarm-wave.mjs:1598` checks) — the first-duplicate-wins
scan that names the typed refusal on the FIRST colliding pair so later
duplicates never mask it; not an export, not a fleet primitive, and the
wave's `usedNames` Set stays inline (no carried tag). Sibling `3854da5c`
(nc3-swarm r69) added four more wave-private primitives:
`reportInstruction(reportDir, name)` (`ufo-swarm-wave.mjs:193`) is the
verbatim per-lane report line the composition sites (resume message
`ufo-swarm-wave.mjs:1110`, spawn prompt `ufo-swarm-wave.mjs:1135`, compact prompt `ufo-swarm-wave.mjs:1157`) rendered inline — one renderer so the
paths can never drift on the path join or wording;
`checkComposedText(text, label, cause)` (`ufo-swarm-wave.mjs:218`) is the composition tail —
a fully-composed lane text is byte-bounded then envelope-checked in that
order, `cause` carrying the site-specific bound phrase so emitted
messages stay byte-identical to the inline arms they replace (resume
`ufo-swarm-wave.mjs:1118`, spawn `ufo-swarm-wave.mjs:1148`, compact `ufo-swarm-wave.mjs:1160`); `memberEntries` (`ufo-swarm-wave.mjs:1061`) mints each member's
registry row beside its task in the same pass (`ufo-swarm-wave.mjs:1103` resume, `ufo-swarm-wave.mjs:1128`
spawn — the judgment binding persists with the member), so the registry
key can never diverge from the dispatch name and the `lane.name`
write-back is gone (`members: Object.fromEntries(memberEntries)` `ufo-swarm-wave.mjs:1262`);
and the `atRest` agentId→holders index (`ufo-swarm-wave.mjs:1614`) replaces the
per-assignment O(M) rescan of `doc.members` with one O(M) build, each
holder list preserving the original member-order scan's first-conflict
naming exactly. All four are module-private: not exports, not fleet
primitives. Sibling `eb147b51` (nc3-swarm r70) added five more
module-private dedups: `planSwarmWave`'s lane classify is one pass — the
`file(lane)` closure pushes each validated lane into `lanes` and its
`spawns`/`resumes` bucket together, where a `lanes.map` plus two filters
ran three traversals for one pass's work; `planToDispatchPayload` splits
`plan.tasks` in the same single pass — two independent `if` arms, not
else-if, so an entry carrying both `agent` and `resume` (never minted by
`planSwarmWave`, but the payload builder is an exported boundary) lands
in BOTH lists exactly as the two-filter version placed it; the monitor's
`siblingsByReceipt` index (`ufo-l0-monitor.mjs:645`) resolves each
sibling's receipt path once on first need — the `prior_evidence_drift`
arm rebinds every non-terminal sibling bound to the same parent receipt,
and a queue-wide rescan per repair re-walked every sibling's
`containedJoin`; the watch's `canonicalScopesOverlap`
(`ufo-l0-watch.mjs:204`) takes already-canonical scope lists so the
tick's hole detector canonicalizes each held row once per tick
(`occupied.push(canonicalScopes(...))` `ufo-l0-watch.mjs:1166`/`ufo-l0-watch.mjs:1307`) instead of once per
candidate per row; and the watch's `successorByResultPath` index
(`ufo-l0-watch.mjs:1144`) resolves a sealed lane's successor row by `resultPath` once on
first need (first-wins on a duplicate `resultPath`, `find` parity)
instead of a `queue.tasks.find` per sealed lane. All five dedups are
module-internal — not leaf primitives; `canonicalScopesOverlap` and
`holeCandidates` are exported watch test seams (the r29 suite
de-mirroring), so two of the five ride exported helpers.
The dispatcher's
own copies — the
`TERMINAL_QUEUE_STATES` constant and the expected-bag cross-check in
its acceptance path — stay its own: importing it remains forbidden, and
they are the parity source the leaf mirrors, not a second contract.

The sighting surface's dispatch-attestation internals stay its own
(sibling `5289d1a6` codified them; sibling `7fba1db0` split the entry
under the 256 KiB contract-file ceiling into
`scripts/ufo-sighting-lib/{base,argv,observe,surface}.mjs`, the entry
indirect substrate launches — the factored `shellLaunches`/
`appearsToLaunch` pair (`ufo-sighting-lib/argv.mjs:139-204`) takes the
target detector plus its shell predicate and unwraps `env` indirection
to depth 3 per detector invocation — a detected `bash -c` string is
checked through the shell predicate starting a fresh detector — so a
wrapped launch cannot pass as a generic argv mission.
`INDIRECT_OMP_DISPATCH` (`ufo-sighting-lib/argv.mjs:467`) mirrors
`INDIRECT_OPENCODE_DISPATCH`: a wrapped `omp` launch would skip the
`parseOmpArgv`/`attestedOmpSession` apparatus (exact-resume attestation,
headless rejection), so it fails rather than degrading. The codifying
commit also bounded `runTmux` at 30s (`TMUX_ERROR` on timeout — a wedged
server can no longer hang a verb) and bound `isIdlePane` to the live
pane cmdline (a foreign process respawned into an ex-idle pane keeps the
`__idle` start command but is no longer idle).

### 8.2 L0 fleet dispatch protocol (NC2 standard)

NC2/`nightcall` is the standard shape of every fleet dispatch, not one
mission's private format. The dispatcher's enqueue default is the canonical
overlay `config/mission-nightcall.yml` with `missionFormat.defaultIterateRounds`
iteration (a ceiling, not a completion target; an honest terminal receipt
still ends the chain) under `sighting.dispatch.missionFormat`. The judged
OMP native topology (§4.2) stays a separate, judged shape; this section
governs unjudged fleet missions.

```
fn dispatch_fleet(fleet):
    map = wwkd_map(fleet)            // data walk, dynamic axes, stop conditions
    require(disjoint_mutation_scopes(map.l1s))
    batch_enqueue(map.frontiers)     // independent self-iterating L1s,
                                     // requestedRunners: 1, iterate: defaultIterateRounds
    // each L1 then fields sequential 16-100 L2 waves, up to 100 members total
```

1. **One L1 per mission; at most 32 live L1s globally**
   (`sighting.dispatch.maxConcurrentL1`). No mission mints a second
   orchestrator, and no wrap-up seat edits a sibling scope: cross-scope
   findings go to L0 or the verify report. L0 is the sole operator↔mission
   interaction and monitor surface — it steers and monitors, never judges
   inside a mission.
2. **Batch frontier after the map.** Every mission is one fresh L1 whose
   prompt begins `/skill:ufo`. L0 maps the whole fleet first, then
   batch-enqueues the independent self-iterating L1 frontiers — crates,
   tooling, tests, docs, packages, evidence, verify — each with
   `requestedRunners: 1` and `defaultIterateRounds` iteration. Verify runs as a concurrent
   read-only frontier, and later iterate/integration receipts may add
   dependencies.
3. **Global routing only.** Every L1 — fleet mission or native-trial Main —
   selects a bare alias that resolves in the fd-bound global OMP config;
   `missionFormat.l1Alias` supplies only the `m_daybreak` default. The observed
   NC2 split uses `m_swe` for crates/tests and `m_daybreak` for
   tooling/docs/packages/evidence/verify; an LSP-integration Nightcall uses
   `m_kimi_devin_high`. These are examples, not a project allowlist. Every L2
   seat resolves role routing and typed cascades only through the global OMP
   alias table (§6). Per-project and per-mission concrete model declarations
   are prohibited; a mission spec selects an alias, never a concrete route.
4. **Independent finite bounds.** `task.maxConcurrency: 0` everywhere — the
   OMP host adds no secondary cap. UFO policy owns the bounds: at most 100
   atomized L2 members per L1, delivered as sequential waves of 16–100 (§4.3;
   wave N+1 launches only as wave N settles), under the configured global
   runner ceiling.
5. **Standard lane families.** crates, tooling, tests, docs, packages,
   evidence, verify. The reference graph is the observed NC2 fleet:
   independent source frontiers for crates, tooling, tests, docs, and
   packages; an evidence lane that reads every scope; and a concurrent
   read-only verify frontier. The exact subset follows the disjoint work
   decomposition, never padding. The verify lane is read-only integration
   unless it is explicitly given an ownership scope; dependencies beyond that
   arrive through later iterate/integration receipts.
6. **Prompt and mechanics contract.** Leading `/skill:ufo` with
   `/skill:godspeed` as the second line (the dispatcher mints both —
   `fleet-dispatcher.mjs` writes `/skill:ufo\n/skill:godspeed` into the
   snapshot prompt), the exact authored
   directive bytes, explicit owned paths, non-goals, and acceptance criteria,
   one report and receipt per round, exactly one terminal `| godspeed`. Every
   fresh L2 task text begins `/skill:godspeed` — the invocation, never bare
   shorthand. The L1 runs on the OMP-native `task`/Hub transport, executes its
   own work, self-iterates and self-improves, discovers axes dynamically per
   round, atomizes real work, and dispatches sequential 16–100 batch/swarm
   waves up to 100 members total. Contract freeze (§4) and same-identity
   reroute (§6) are unchanged.
   Minted prompts additionally carry a dispatch binding (task/run/session
   ids, result+receipt paths, prompt/config SHA-256) and require receipt
   schema `ufo-task-receipt-v1` (exact keys; unknown keys rejected; validated
   by `validateTaskReceipt`). `promptSha256` is read verbatim from the
   dispatch snapshot sidecar
   `.ufo/sessions/<runId>/dispatch-snapshot-<attempt>/prompt.md.sha256` — the
   digest of the exact prompt received, never re-hashed by the lane;
   `configSha256` is copied verbatim; `reportSha256` is computed after the
   last report write — `create-receipt` accepts an optional `reportPath`
   input key (stripped before schema validation, never a receipt key) that
   hashes the report file's raw bytes at mint and fills `reportSha256`,
   refusing `""`/`"-"`/`--*` as `invalid_type` and a disagreeing declared
   digest as `receipt_mismatch` — closing the hand-computed stale-digest
   hole the dispatcher only rejects at settle. `create-receipt --out
   <path>` publishes the minted receipt atomically (tmp+fsync+rename+
   dir-fsync, stdout silent) so a crash mid-mint can never leave the
   truncated file a shell `> receipt.json` redirect produces; `--out`
   refuses `-`, empty, and `--`-leading paths like any non-path value.
   `validate-receipt` is shape-only BY DEFAULT: bare exit 0 means
   schema-valid JSON, never fleet acceptance — acceptance is the
   dispatcher's expected-bag cross-check binding
   taskKey/runId/sessionId/promptSha256/configSha256/reportSha256 to the
   task that produced it. Two opt-in local gates tighten it without
   changing that boundary: `--iterate` requires `iteration.decision`
   (fails one-shot receipts closed), and repeatable `--expected
   key=value` asserts equality against one of the six acceptance fields
   (malformed, unknown, or duplicate keys are usage refusals, exit 64) —
   a passing `--expected` proves local equality only, never that the
   dispatcher accepted the receipt against its own task record.
   Iterate tasks require `iteration.decision` ∈
   {continue, stop, blocked, budget_halt} (missing fails closed; one-shot
   tasks omit `iteration`). Optional `iteration` fields: `reason` (free-form
   stop cause ≤1 KiB — a `stop` declaring saturation names saturation
   there), `nativeVerdict` (must reference a real canonical verdict digest —
   never fabricate one), and `blockedAudit` (`{transportFailures,
   workFailures}` nonnegative integers plus optional `detail` ≤1 KiB,
   riding the queue outcome as machineable blocked-chain evidence — absent
   means absent, never a fabricated zero).

The dispatcher's queue read is a full integrity pass, not a parse
(`fleet-dispatcher.mjs:4704-4813`): `validateQueue` requires the queue
schema plus a nonnegative safe-integer `revision` strictly below
`MAX_SAFE_INTEGER` (a stored max row makes every subsequent write throw
and wedges the queue read-only), runs `validateQueueTask` per row, then
enforces uniqueness across task keys, runIds, sessionIds, and
resultPaths (two live rows sharing a resultPath share one receipt path —
whichever settles second overwrites the first's evidence), and rejects
dependency edges that self-reference, dangle, or cycle — including a
chain member waiting on its own resolved root, which is a self-edge
through `afterChains`. Archive-backed completed keys remain durable
after capacity relief, so a `dependsOn`/`afterChains` edge to one is a
satisfied leaf, not an invalid reference (`:4753-4774`). Malformed-row
attribution is typed (`:398-413`): `taskIndex` always, `queueRevision`
when the stored revision is a safe integer, and `taskKey` only when the
stored key already matches the minted shape — a malformed key never
reaches telemetry. A failed read is typed `QUEUE_INVALID`
(`:4823-4851`), surfaced as `queue_invalid` on once/daemon/fatal
(`:9615-9626`) rather than a generic `dispatcher_cycle_error`; malformed
input never mutates the queue.

The fleet lifecycle ledger (`.ufo/fleet-ledger.jsonl`,
`UFO_FLEET_LEDGER_PATH` override gated through `beneath(UFO_STATE, …)`,
schema `ufo-process-lifecycle-v1`) is appended by the dispatcher under the
ledger lock (`appendLifecycleEvents` dedupe+append) and rotated at
`MAX_LEDGER_BYTES`/`MAX_LEDGER_SEGMENTS`. Its read and rotate paths are
optional sibling modules the dispatcher dynamically imports at boot:
`fleet-ledger-read.mjs` is the preferred streaming reader — newest-wins
dedupe during the pass, per-segment coverage (bytesRead vs stat size,
malformed line/segment classes, `reused_event_ids`, `tornTail`), a
pre-dedupe `processIndex` so duplicate spawn/terminal detection survives
dedupe, and no total-size correctness cap (bounded chunks and a 4 MiB
per-line bound make size safe) — where the inline reader spent a 32 MiB
byte budget and silently skipped rotated segments, turning already-appended
events into fresh `ledger_event_drift`. Its return is a superset of the
inline shape; the dispatcher normalizes both, and a sibling that throws or
returns an incompatible shape degrades to the inline reader with typed
`ledger_*_module_error` telemetry — a bad module can never crash the
cycle. `fleet-ledger-rotate.mjs` is the same optional-sibling class for
rotation, invoked `prelocked` under the ledger lock the dispatcher already
holds. `UFO_FLEET_DISABLE_LEDGER_MODULES=1` forces the inline paths (ops
escape hatch and deterministic fallback test hook). Outside the
dispatcher, `ufo-state-retention.mjs` statically imports
`loadLifecycleLedger` for its fail-closed `readLedgerActivity` — a
malformed or unreadable ledger is `ledger_incomplete`/`ledger_unreadable`,
never read as terminal. Both siblings are standalone drop-ins importing no
sibling; their deliberate helper mirrors of each other carry a same-change
port rule, not a leaf import.

Generated-mirror sync is a single post-settlement step owned by L0: canonical
source owners settle first, then mirrors regenerate once.

---

## 9. Cross-substrate contract sync

There is one implementation, not seven adapted loops.

```
fn sync_contracts(canonical):
    parallel_for mirror in declared_skill_mirrors:
        require(mirror.skill_tree == canonical.skill_tree)
    parallel_for mirror in declared_agent_mirrors:
        require(mirror.agent_cards == canonical.agent_cards)
    parallel_for target in [omp, kimi, codex, cursor, opencode, grok, devin]:
        require(target.wrapper.delegates_to == "ufo-cli")   // doctrinal: asserted by each entrypoint, not mechanically synced
        require(target.wrapper.passes_substrate == target.name)  // doctrinal
    require(no_missing_drifted_or_extra_mirror_files)
    return ContractSyncReport
```

`scripts/sync-ufo-contracts.mjs` is the mechanical authority for the declared
skill and agent mirror targets; `--check` rejects missing, drifted, or extra
files under every declared target.
`--check` also gates the `.omp/config.yml` projection, charterlist scope
tags, the bundled runtime config, the bundled asset mirrors (godspeed
filter/velocity/SHA256SUMS and the wwkd skill copies inside
`crates/ufo-core-runtime/bundled`), the godspeed directive mirrors, package
scope tags and the rejection of stray `packages/*/ufo-skill-scope.json`
files outside the expected set, deps closure, skills sums, constants
uniqueness, docs dates, the L1 overlay, the tick machine, the
sighting-surface digest, and seat-route equivalence — its authority exceeds
skill and agent mirrors alone.

The `.cursor/` tree straddles that authority boundary. Of its twelve
tracked files, ten are managed: six ride the declared `project-cursor`
skill target (`.cursor/skills/ufo/**`), three are dependency mirrors
(`.cursor/ssot/godspeed-core/directive.md`,
`.cursor/skills/wwkd/{SKILL.md,SHA256SUMS}` — the package root of the
`project-cursor` target is `.cursor` itself), and one rides the godspeed
directive channel (`.cursor/skills/godspeed/directive.md`). Two are
unmanaged: `.cursor/skills/godspeed/SKILL.md` — an unmanaged copy of
`skills/godspeed/SKILL.md`, whose source is SHA256SUMS-pinned but sits
outside `canonicalSources`, so the copy drifts invisibly to `--check`
(drifted at nc5 r06: it predates the canonical `## Envelope marker`
section) —
and `.cursor/rules/godspeed-always.mdc`, a cursor-native always-apply
rule with no canonical counterpart. A lane reading this tree as fully
managed (or fully unmanaged) misjudges both halves; register the copy in
the mirror map or delete it — the decision is mirror-map-owned, not
guidance-owned.

Contract sync proves shape parity. It does not prove an authenticated host CLI
ran. Behavioral evidence comes from invoking each target's local `self-iter`
command separately.

---

## 10. Local ship

```
fn ship_local():   // contract shape, not a wired pipeline — `ufo local-ship`
                   // is a separate atomic-apply verb; the aggregate flow is
                   // scripts/gates.sh plus per-substrate `ufo self-iter`
    require(sync_contracts().ok)
    require(build_canonical_runtime())   // doctrine: cargo build is the
                                       // charter Phase0 "build" stage; no
                                       // ship-time build step exists
    for target in supported_substrates:  // sequential, one --substrate each —
                                       // no all-seven parallel invoke exists
        report = invoke_local_self_iter_surface(target)
        require(report.runtime == "crates/ufo-core-runtime")
        require(report.substrate == target)
        require(report.operatorGuidanceThemes == exact_three_themes)
    emit_local_artifacts()
```

No runtime path commits, pushes, publishes, deploys, or infers credentials.

Local ship is transactional: the admitted candidate applies against its
pinned baseline snapshot (the hash the judge admitted — an admitted
candidate applied to a different tree is a mismatch, not a ship) under a
mission-scoped writer lease with fencing epochs (`.ufo/writer-lease.json`;
a stale-epoch write is rejected, and of two supervisors advancing one
mission exactly one lease wins), through a crash-recoverable ownership
journal (`.ufo/apply-journal/`): per-operation records with before/
candidate digests and the preimage bytes; recovery rolls back ONLY owned
pending operations, and a file whose bytes match neither digest is a
pre-existing user edit — it is never a rollback casualty. Raw transcripts
are preserved beside normalized evidence with a canonicalizer version and
raw/derived digests plus a redaction map (`evidence_originals`); no hash
of a derived copy stands in for its original, and tampering with either
layer is independently detectable. Self-modification is promotion: the
running contract validates a candidate contract for a successor boundary
(the §8 membrane sign-off is the promotion permission); the candidate
never edits the live gates and never approves itself.

---

## 11. Definition of done

The map holds when a local command reaches a verified result through one
runtime and one judge; Phase 0 rejects drift; a route failure reroutes the same
logical lane and cache without a replacement identity; every substrate surface
preserves the three themes; budget and blocked outcomes remain non-success;
and the loop can stop itself at honest saturation.

For OMP native execution, done additionally requires the exact native
depth-0/1/2 topology (Main, depth-1 planner/proposal/distiller seats, and the
executor-owned depth-2 labrat), full-prompt integrity, concurrent-wave timing,
per-tier artifact and model provenance, and a digest-bound Rust
`judge-handoff` verdict. A fixture run is never substituted for that proof.

Self-driving is demonstrated by two contiguous native rounds on one bounded
task. Round 1: WWKD plan → native dispatch → evidence → an accepted change.
Round 2: a NEW WWKD plan that reads the changed baseline, prior rejects, and
prior failures → new native dispatch → a verdict linked to round 1's. Both
rounds carry genuine native traces with distinct real transcript ids; the
successor is bound to its predecessor's contract, accepted artifacts, axes,
unfinished work, and relevant lane history. A fixture, a merely scheduled
fleet successor, or a re-run of round 1's plan is never a substitute (T02).

The receipt is `.ufo/receipts/<runId>/round-chain.json` — per round an entry
`{round, plan_digest, handoff_digest, verdict_digest, baseline_before,
baseline_after, predecessor}` where `predecessor` is the prior round's entry.
The scaffolding and its digest fields land with PC-A; the two-round proof
itself is the pack's capstone gate (P9).

Runtime identity is fixed. Host command shape is adaptable.
