# Workspaces

Each subdirectory is one **long-horizon workflow** organized with the ICM operating model
(`docs/systems/icm-operating-model.md`). A workspace is a copyable, stage-structured unit where each
stage loads only the context it needs.

## Start a new workspace

```
cp -r workspaces/_template-icm workspaces/<your-workflow>
```

Then fill `identity.md` (L0) and `routing.md` (L1) once, write a tight `CONTEXT.md` per stage (L2),
put rules in `_config/` + `references/` (L3), and write run output to each stage's `output/` (L4).

## Layers (quick reference)

- L0 identity → `identity.md`
- L1 routing → `routing.md`
- L2 stage contract → `stages/NN-name/CONTEXT.md`
- L3 reference / factory → `_config/`, `references/`
- L4 working artifacts / product → `stages/NN-name/output/`

## Added on top of ICM (non-optional)

- `evals/` — per-stage acceptance checks (gate before advancing).
- `evidence/` · `claims/` · `decisions/` — keep epistemic categories separate.
- `provenance.md` — append-only log of externally retrieved content (treat as untrusted).
