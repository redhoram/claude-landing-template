# _landing-template

> 🇬🇧 [English version](./README.md)

Template framework untuk **landing page & aplikasi sederhana** — berat di desain & konten, ringan di logika. Saudara dari `_pipeline-template` (yang buat app CRUD kompleks), tapi dioptimalkan untuk kerja visual yang iteratif.

## Filosofi: loop visual, bukan pipeline batch

Desain itu iteratif & visual (lihat → ubah → lihat lagi). Maksain pipeline batch lima-tahap di sini malah mematikan loop itu. Jadi framework ini punya **dua mode**:

- **0→1 — `/craft [halaman/section]`**: spin-up draft kuat dari nol lewat 3 subagent (designer → builder → qa). Buat dapetin fondasi cepat.
- **1→bagus — interaktif / `/polish [target]`**: poles di main session pakai live preview. Di sinilah desain jadi tajam.

Pipeline batch cocok buat CRUD; poles visual butuh mata di layar.

## Beda dari `_pipeline-template`

| | `_pipeline-template` (CRUD kompleks) | `_landing-template` (landing & app sederhana) |
|---|---|---|
| Mode | Batch, doc-driven, fire-and-forget | Loop visual + interaktif |
| Agent | planner → designer → coder → tester → reviewer | designer → builder → qa |
| Gate akhir | Reviewer (SHIP/BLOCK, fokus keamanan) | QA (punch-list, fokus UI/UX) |
| Command | `/ship` | `/craft` (0→1) + `/polish` (1→bagus) |
| Verifikasi | build/lint/test + skenario | live preview: render, responsif, console |

## Isi

- `CLAUDE.md` — jantungnya: brand/design system + prinsip desain + anggaran kualitas + mode kerja. **Isi placeholder-nya dulu.**
- `.claude/agents/` — `designer`, `builder`, `qa`
- `.claude/commands/` — `craft`, `polish`
- `.claude/skills/` — `premium-design` (skill kualitas desain bawaan: palette, tipografi, motion, adaptasi konteks)
- `.craft/` — workspace handoff (`design.md`, `build-notes.md`, `qa-report.md`)

## Bikin project baru

1. Copy `_landing-template` → rename folder
2. Isi `CLAUDE.md` — terutama section **Brand & Design System** (ini yang bikin output konsisten & tajam)
3. Scaffold stack (default Vite + React + TS + Tailwind v4 + lucide-react)
4. `git init`

## Standar

Yang bikin output beda dari generator instan: **berani di desain, disiplin di kode.** Detail di prinsip & anggaran kualitas dalam `CLAUDE.md`.
