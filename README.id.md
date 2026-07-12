<p align="center">
  <img src="https://img.shields.io/badge/Claude%20Code-Template-D97757?logo=anthropic&logoColor=white" alt="Claude Code Template">
  <img src="https://img.shields.io/badge/Visual-Loop-informational" alt="Visual Loop">
  <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License">
</p>

<p align="center">
  <a href="README.md">English</a> | <a href="README.id.md">Bahasa Indonesia</a>
</p>

---

# _landing-template

Template framework untuk **landing page & aplikasi sederhana** — berat di desain & konten, ringan di logika. Saudara dari [`_pipeline-template`](https://github.com/redhoram/claude-pipeline-template) (yang buat app CRUD kompleks), tapi dioptimalkan untuk kerja visual yang iteratif.

### Filosofi: loop visual, bukan pipeline batch

Desain itu iteratif & visual (lihat → ubah → lihat lagi). Maksain pipeline batch lima-tahap di sini malah mematikan loop itu. Jadi framework ini punya **dua mode**:

- **0→1 — `/craft [halaman/section]`**: spin-up draft kuat dari nol lewat 4 subagent (writer → designer → builder → qa). Copy dulu: writer menetapkan hierarki pesan + headline/CTA persis, baru designer menata layoutnya. Buat dapetin fondasi cepat.
- **1→bagus — interaktif / `/polish [target]`**: poles di main session pakai live preview. Di sinilah desain jadi tajam.

Pipeline batch cocok buat CRUD; poles visual butuh mata di layar.

### Beda dari `_pipeline-template`

| | `_pipeline-template` (CRUD kompleks) | `_landing-template` (landing & app sederhana) |
|---|---|---|
| Mode | Batch, doc-driven, fire-and-forget | Loop visual + interaktif |
| Agent | planner → designer → coder → tester → reviewer | writer → designer → builder → qa |
| Gate akhir | Reviewer (SHIP/BLOCK, fokus keamanan) | QA (punch-list, fokus UI/UX) |
| Command | `/ship` | `/craft` (0→1) + `/polish` (1→bagus) |
| Verifikasi | build/lint/test + skenario | live preview: render, responsif, console |

### Isi

- `CLAUDE.md` — jantungnya: brand/design system + prinsip desain + anggaran kualitas + mode kerja. **Isi placeholder-nya dulu.**
- `.claude/agents/` — `writer`, `designer`, `builder`, `qa`
- `.claude/commands/` — `craft`, `polish`
- `.claude/skills/` — 4 skill bawaan yang ditegakkan para agent (matriks di bawah)
- `.craft/` — workspace handoff (`copy.md`, `design.md`, `build-notes.md`, `qa-report.md`)

### Matriks skill

Tiap agent cuma baca skill milik tahapnya — didokumentasikan di sini biar pemetaannya bisa diaudit:

| Skill | Dipakai oleh | Menegakkan |
|---|---|---|
| `conversion-copy` | writer | Formula headline + tes spesifisitas, pilihan arc PAS-vs-AIDA, hierarki bukti jujur, penanganan objection, aturan CTA/microcopy dan bahasa |
| `premium-design` | designer | Disiplin palet, metrik tipografi, motion yang disengaja, intensitas marketing-vs-product |
| `ux-research` | designer + qa | Landasan user + JTBD, 3-5 prinsip psikologi bernama per surface, checklist usability, garis keras anti dark-pattern; diagnostik 10 pertanyaan (severity 0-4) jalan di visual taste loop |
| `web-quality` | builder | Pola write-time pencapai angka budget: preload LCP, dimensi anti-CLS, feedback INP, disiplin bundle, idiom Tailwind v4 — adaptasi dari [web-quality-skills](https://github.com/addyosmani/web-quality-skills) tim Google Chrome (MIT) |

### Prasyarat

- [Claude Code](https://claude.com/claude-code) ter-install — `/craft` dan `/polish` itu **slash command Claude Code**, diketik di dalam sesi Claude Code di folder project (bukan script npm).
- Node.js 18+ dan npm (stack default berbasis Vite).

### Bikin project baru

1. Copy `_landing-template` → rename folder
2. Isi `CLAUDE.md` — terutama section **Brand & Design System** (ini yang bikin output konsisten & tajam)
3. Scaffold stack (default Vite + React + TS + Tailwind v4 + lucide-react) — atau skip aja: `/craft` auto-scaffold kalau `package.json` belum ada
4. `git init`
5. Buka Claude Code di folder itu → jalankan `/craft [halaman/section]`

### Standar

Yang bikin output beda dari generator instan: **berani di desain, disiplin di kode.** Detail di prinsip & anggaran kualitas dalam `CLAUDE.md`.

Dan **gagal keras, bukan diam-diam**: copy spec dan design spec bawa flag status READY/BLOCKED, builder bilang BLOCKED daripada muter-muter di build yang rusak, dan QA nggak pernah klaim cek visual yang nggak bisa dia lakukan headless — penilaian visual terjadi di main session, dengan mata di live preview.

### Kredit

**Author**
- Redho Ramadhani — [linkedin.com/in/redhoramadhanihamid](https://id.linkedin.com/in/redhoramadhanihamid) · [github.com/redhoram](https://github.com/redhoram)

Dibangun dengan [Claude Code](https://claude.com/claude-code).
