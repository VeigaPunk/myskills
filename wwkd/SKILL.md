---
name: wwkd
description: >
  What Would Karpathy Do — the planning posture of the ufo L1. Not a standalone
  skill: wwkd is the axes-mapping layer the L1 loads to turn a task into a
  dynamic axis set, group axes into milestones, and hand both to the L1
  dispatcher for L2 seat assignment. Pairs with the godspeed directive: the
  L1 orchestrates under the wwkd map, L2 agents execute under the directive
  with unbounded capability and no rigidly assigned goal. Activate on "/wwkd",
  "plan this", "map the axes", "break this down", or whenever ufo loads its
  planner stance. Under ufo, run-logic §5 is normative: this file is the
  enrichment, and any drift resolves in §5's favor (I9).
---

# WWKD — Axes-Mapping Posture (ufo L1)

WWKD maps a task onto **axes**, groups axes into **milestones**, and hands the
map to the L1 dispatcher. It does not execute the plan, does not own agents,
and does not stand alone outside the ufo structure. Under ufo it is
**idempotent**: loading it never changes ufo behavior beyond the plan it
helps write — it is enrichment, never a gate (I9; run-logic §5 wins on drift).

The output of WWKD is not "a plan you follow." It is the round's **axis set +
milestone map** — the bounded problem the L1 orchestrates this turn.

---

## The pair: wwkd × godspeed

- **wwkd bounds the L1.** The axes map keeps multi-axis optimization
  tractable: the L1 is given a turn to orchestrate, not a chaotic,
  impossible problem. Exploration happens inside the map, not instead of it.
- **godspeed frees the L2.** Each dispatched L2 assignment carries exactly one
  `directive.md` prefix — the quintessential form for unbounded capability
  expression. No rigid goal is attributed to an L2; the axis improvement is
  the direction, the directive is the posture.
- **The trilogy is L1/judge-only.** `filter.md` and `velocity.md` are loaded
  only by the judge seat. L2s never see them; neither does any other role.

---

## The mapping pipeline

### 1. Data walk (always first)
Inspect the thing itself — inputs, outputs, telemetry, local diff — before
naming anything. A map drawn from the spec instead of the data plans against
a fiction.

### 2. Name the axes (dynamic, per task)
Axes are **minted for the task at hand**: never fixed, never a standing
taxonomy, **never attached to an agent**. Every declared axis names its
measurement (`Axis.measurement`, declared with the round's axis set):

- `executable` — measured by the runtime in bounded scratch copies of
  baseline and candidate trees; computed direction-aware delta, advisory
  seat scores never override a computed regression.
- `subjective` — improvement admitted only through the recorded symmetric
  argument (for and against, role-appropriate evidence); one-sided claims
  are clamped to baseline and flagged.
- `evidence` — computed by the judge from typed handoff evidence; native
  path only, rejected at admission elsewhere.

**Unmeasurable axes are not axes.** An axis without a measurement declaration
fails plan admission — the verification-gate stance applied to the axis set
itself. A check that fails to run measures UNKNOWN: never regression cover,
never a phantom gain; UNKNOWN on a material axis blocks admission as
`INSUFFICIENT_EVIDENCE`.

### 3. Group axes into milestones
Axes that co-move land in the same milestone. Order by **least disruption** —
each milestone remains runnable in isolation, each move Pareto-checkable on
its own:

1. **Skeleton** — one end-to-end shape before capacity.
2. **Overfit one case** — prove exactly one concrete path, bit-for-bit.
3. **Generalize** — widen one axis at a time; a broken earlier gate blocks widening.
4. **Polish** — last, only after correctness is proven across the range.

### 4. Hand to the L1 dispatcher
The L1 assigns milestones and axis groups to L2 seats from the round's
context — the axes themselves belong to no agent. Each dispatched assignment
gets exactly one directive prefix and one terminal marker. The L1 orchestrates
**and** executes (I2); it never blocks waiting on lanes, never spawns a second
L1 (I1).

### 5. Assimilate and remap
The L1 collects results, the judge computes measurements per axis, and the
next turn's WWKD plan re-declares the axis set: **stable within a round, free
to evolve between rounds, never frozen at Phase 0.** Every judged round
writes one WWKD plan before specialists are dispatched.

---

## L2 roster (reference seats)

The L1 dispatches from the authored roster (e.g. `ufo-fsd-alpha/.omp/agents/`).
Seats are capabilities, not axis owners:

| Seat | Charge |
|---|---|
| planner | Mandatory planner seat each judged round — data walk, skeleton, one-case overfit, then generalize |
| executor | Scoped implementation with behavioral evidence |
| reviewer | Surgical correctness review of a bounded change |
| critic | Adversarial approach review against the round's declared axes and invariants |
| sentinel | Adversarial security review of a bounded change |
| scout | Read-only codebase research for a bounded unknown |
| connector | Cross-axis pattern finder — mandatory in every proposal wave (native) and every PROPOSE phase after Round 0 (fleet) |
| distiller | Deduplicate complete proposals before Pareto judgment |
| labrat | Bounded empirical probe for one falsifiable hypothesis |
| mutation-tester | Mutate-run-revert probe for missing behavioral coverage |
| revenger | Reverse-engineer undocumented local behavior and original intent |
| scribe | Evidence and gate reporter; never a shipping authority |
| simplifier | YAGNI deletion that preserves verified behavior |

---

## Refusals

This posture refuses to produce:

- **Fixed axis taxonomies** — axes are minted per task, per round.
- **Agent-attached axes** — seats are assigned by the L1; axes belong to the round.
- **Rigid goals for L2s** — direction yes, attributed goal no; the directive is the form.
- **Unmeasurable axes** — no measurement declaration, no axis.
- **Standalone planning** — outside ufo there is no dispatcher to hand the map to.

---

## Conceptual frame (operator)

> "Frontier shows itself by ceasing to move."

> "Pareto-optimal iteration at velocity, with no rigidly defined goal."

> "Quality cannot be defined, but it can be recognized."
