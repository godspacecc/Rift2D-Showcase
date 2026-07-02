# Rift2D Roadmap

[English](ROADMAP_EN.md) | [中文](ROADMAP.md)

---

## Current Status

v0.1.0 core systems foundation released. Offline combat, Survivor mode, wilderness maps, story performance, and realtime multiplayer are advancing in parallel, with playable prototypes in some areas.

---

## Directions & Progress

### 1. Architecture responsibility governance

- **Goal**: Reduce the global state bucket and implicit process dependencies so offline dungeons, realtime dungeons, and Survivor mode can keep extending on clear data ownership.
- **Path**: Split apart `GameStateModel`'s global-phase, dungeon, and settlement state → funnel entering-dungeon, extraction, settlement, and return-to-lobby flows into explicit Commands/Systems → have scene construction use explicit context.
- **Progress**: Partially done. Dungeon and settlement state have a split direction; still need to migrate references, funnel the flows, and split offline vs realtime dungeon scene-build context.

### 2. Offline combat & offline dungeons

- **Goal**: Provide a stable underlying combat foundation for normal offline dungeons, Survivor mode, and future combat gameplay.
- **Path**: Complete the offline combat base loop and entity-projectile pipeline → presentation-sync incrementality, general combat performance baseline, core turret general capabilities → unify offline dungeon win/loss and settlement.
- **Progress**: Partially done. Offline combat entry and base rules exist; entity-projectile sync, spawning, removal, and same-frame hit protection, plus presentation-sync incrementality and the general performance baseline, are still pending.

### 3. Survivor mode

- **Goal**: Take Survivor mode from basically playable to a standalone mode with pacing, builds, and replay goals.
- **Path**: Stabilize the mode base and performance/capacity → tune target time, XP curve, dedicated waves, and Boss pacing → expand weapon builds, out-of-run records, and long-term progression.
- **Progress**: Partially done. Base mode, XP, and upgrade choices have a prototype; target-time config, early upgrade feedback, dedicated waves, Boss pacing, settlement summary, and out-of-run progression are still pending.

### 4. Map editor & wilderness maps

- **Goal**: Upgrade maps from editable grid data into wilderness maps that support exploration, resources, enemies, risk/reward, and extraction-route judgment.
- **Path**: Map data, runtime base, wilderness terrain generation, and editor regionalized production are done → regional gameplay distribution logic and gameplay health (done) → presentation polish, final art, and performance optimization.
- **Progress**: First three phases done. Regional gameplay distribution logic landed: biome gameplay semantics, stable generation of resource / enemy / hazard points, risk-reward scoring and health evaluation, and an editor gameplay preview, all covered by EditMode tests; gameplay points are logic-only and not written to the document. Next up: presentation polish, final art, performance work, and wiring the values into Survivor / loot / monster configs.

### 5. Story performance system

- **Goal**: Expand story from static NPC dialogue into a configurable, verifiable, incrementally enhancable performance pipeline.
- **Path**: Complete story data sources and a lightweight `StoryPerform` player → non-blocking playback, Dialogue steps, character turn/move, and basic camera work → quest/area triggers, VFX/SFX, and complex cutscenes.
- **Progress**: Partially done. Dialogue system and base player are wired in; the Luban source pipeline, non-blocking playback, Dialogue steps, and real character performance are still pending.

### 6. Realtime multiplayer

- **Goal**: Improve multiplayer code maintainability and fix realtime movement stutter and remote-player jitter.
- **Path**: Tidy up Net/Handler business entry points → diagnose movement sync quality → add snapshot buffer interpolation for remote players → local prediction and server reconciliation if needed → keep splitting up the protocol-handling structure.
- **Progress**: Partially done. Base multiplayer structure and naming direction exist; movement-sync diagnosis, remote interpolation, and local prediction are still pending.

---

## Near-term priorities

1. **Offline combat entity-projectile loop** — shared foundation for Survivor and normal offline combat presentation.
2. **Survivor target time, XP curve, and dedicated waves** — fastest path to better current playability.
3. **Map gameplay distribution presentation hookup** — regional gameplay distribution logic (resource / enemy / hazard points + risk-reward health) is done; next, wire the logic points into final resource, monster, and loot configs.
4. **GameStateModel responsibility consolidation** — reduce global-state coupling when extending future gameplay.
5. **Realtime multiplayer movement-sync diagnosis and remote interpolation** — quantify the problem first, then pick a presentation strategy.

---

## Milestones

| Version | Content | Status |
|---------|---------|--------|
| v0.1.0 | Core systems foundation | ✅ Released |
| v0.2.0 | Combat & Dungeon | In progress |
| v0.3.0 | Progression system | Planned |
| v1.0.0 | Full release | Planned |

---

*Roadmap updated as development progresses.*
