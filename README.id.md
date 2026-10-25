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

Template framework untuk **landing page & aplikasi sederhana**: berat di desain & konten, ringan di logika. Saudara dari [`_pipeline-template`](https://github.com/redhoram/claude-pipeline-template) (yang buat app CRUD kompleks), tapi dioptimalkan untuk kerja visual yang iteratif.

### Filosofi: loop visual, bukan pipeline batch

Desain itu iteratif & visual (lihat → ubah → lihat lagi). Maksain pipeline batch lima-tahap di sini malah mematikan loop itu. Jadi framework ini punya **dua mode**:

- **0→1 lewat `/craft [halaman/section]`**: spin-up draft kuat dari nol lewat 4 subagent (writer → designer → builder → qa). Copy dulu: writer menetapkan hierarki pesan + headline/CTA persis, baru designer menata layoutnya. Buat dapetin fondasi cepat.
- **1→bagus, interaktif atau `/polish [target]`**: poles di main session pakai live preview. Di sinilah desain jadi tajam.

Pipeline batch cocok buat CRUD; poles visual butuh mata di layar.

- **QA ngeliat, bukan cuma grep**: setelah cek statis, QA menyajikan build produksi, ngambil screenshot headless di 375, 768, dan 1280px (bagian atas lipatan dan halaman penuh), lalu menilainya sendiri. Temuan visual severity 3 ke atas berarti NEEDS WORK. Hover, animasi, dan console tetap dicek langsung di main session.
- **Copy jujur sesuai sumber**: writer cuma ngambil klaim, angka, testimoni, dan logo dari section `Content sources` di `CLAUDE.md`; selebihnya ditandai ilustratif. Klise AI bahasa Indonesia juga disaring, dan skill `humanizer` bawaan dijalankan ke copy.
- **Jejak audit dan commit**: tiap `/craft` mindahin file `.craft/` lama ke arsip, bukan ngehapus, dan saat PASS nawarin commit file yang dibangun, di-stage per path. Nggak pernah push tanpa konfirmasimu.
- **Model override**: model tiap agent bisa diganti per project di `CLAUDE.md`, tanpa ngedit file agent.

### Beda dari `_pipeline-template`

| | `_pipeline-template` (CRUD kompleks) | `_landing-template` (landing & app sederhana) |
|---|---|---|
| Mode | Batch, doc-driven, fire-and-forget | Loop visual + interaktif |
| Agent | planner → designer → coder → tester → reviewer | writer → designer → builder → qa |
| Gate akhir | Reviewer (SHIP/BLOCK, fokus keamanan) | QA (punch-list, fokus UI/UX) |
| Command | `/ship` (fitur baru) + `/fix` (revisi) | `/craft` (0→1) + `/polish` (1→bagus) |
| Verifikasi | build/lint/test + skenario + screenshot | screenshot QA + live preview: render, responsif, console |

### Isi

- `CLAUDE.md`: jantungnya, berisi brand/design system + prinsip desain + anggaran kualitas + mode kerja. **Isi placeholder-nya dulu.**
- `.claude/agents/`: `writer`, `designer`, `builder`, `qa`
- `.claude/commands/`: `craft`, `polish`
- `.claude/skills/`: 10 skill bawaan yang ditegakkan para agent (matriks di bawah)
- `.craft/`: workspace handoff (`copy.md`, `design.md`, `build-notes.md`, `qa-report.md`, `shots/`), dengan run lama di `.craft/archive/`

### Matriks skill

Tiap agent cuma baca skill milik tahapnya: didokumentasikan di sini biar pemetaannya bisa diaudit:

| Skill | Dipakai oleh | Menegakkan |
|---|---|---|
| `conversion-copy` | writer | Formula headline + tes spesifisitas, pilihan arc PAS-vs-AIDA, hierarki bukti jujur, penanganan objection, aturan CTA/microcopy dan bahasa |
| `seo-content-strategist` | writer + qa | SEO diputusin saat nulis: hierarki heading sebagai struktur konten, penempatan keyword, title/meta sebagai ad copy, pilihan JSON-LD, alt text; dicatat di SEO notes copy.md; QA verifikasi build-nya cocok |
| `humanizer` | writer | Membuang pola tulisan AI dari copy yang sudah jadi: kontras yang dibuat-buat, kalimat penutup dramatis, triad paksaan, klaim yang digelembungkan, label tebal, kata pengisi |
| `premium-design` | designer | Disiplin palet, metrik tipografi, motion yang disengaja, intensitas marketing-vs-product |
| `ux-research` | designer + qa | Landasan user + JTBD, 3-5 prinsip psikologi bernama per surface, checklist usability, state interaksi dan microcopy (pending, loading, gagal, fokus, target sentuh), garis keras anti dark-pattern; diagnostik 10 pertanyaan (severity 0-4) dibagi antara screenshot QA dan taste loop langsung |
| `web-quality` | builder | Pola write-time pencapai angka budget: preload LCP, dimensi anti-CLS, feedback INP, disiplin bundle, idiom Tailwind v4; adaptasi dari [web-quality-skills](https://github.com/addyosmani/web-quality-skills) tim Google Chrome (MIT) |
| `antislop` | designer + builder + qa | Filter inti hasil adaptasi anti-slop: uji tujuan untuk tiap teknik visual, 38 aturan dalam tiga tingkat, Design Read dengan dial ENERGY/RHYTHM/MOTION, dan laporan Delivery Gate beserta buktinya |
| `antislop-ui` | designer + builder + qa | Pola UI khas AI lengkap dengan ciri, alasan, dan perbaikannya: gradien default, glassmorphism di mana-mana, bento grid, terminal palsu, badge di atas headline, statistik karangan, tombol mati |
| `antislop-layoutmobile` | builder + qa | Tata letak yang menyesuaikan dari ponsel ke desktop: breakpoint, skala fluid, grid yang menumpuk, overflow, target sentuh, navigasi mobile |
| `antislop-human` | builder + qa | Kontras yang dihitung dengan `contrast-check.py`, keyboard dan fokus, umpan balik yang hanya mengandalkan warna, state UI, zoom |

### Prasyarat

- [Claude Code](https://claude.com/claude-code) ter-install: `/craft` dan `/polish` itu **slash command Claude Code**, diketik di dalam sesi Claude Code di folder project (bukan script npm).
- Node.js 18+ dan npm (stack default berbasis Vite).
- Browser berbasis Chromium (Chrome, Edge, atau Chromium) supaya QA bisa ngambil screenshot headless. Kalau nggak ada, QA balik ke checklist untuk main session.

### Bikin project baru

1. Copy `_landing-template` → rename folder
2. Isi `CLAUDE.md`: terutama section **Brand & Design System** (ini yang bikin output konsisten & tajam) dan **Content sources** (apa yang boleh diklaim writer)
3. Scaffold stack (default Vite + React + TS + Tailwind v4 + lucide-react), atau skip aja: `/craft` auto-scaffold kalau `package.json` belum ada
4. `git init`
5. Buka Claude Code di folder itu → jalankan `/craft [halaman/section]`

### Standar

Yang bikin output beda dari generator instan: **berani di desain, disiplin di kode.** Detail di prinsip & anggaran kualitas dalam `CLAUDE.md`.

Dan **gagal keras, bukan diam-diam**: copy spec dan design spec bawa flag status READY/BLOCKED, builder bilang BLOCKED daripada muter-muter di build yang rusak, dan QA nggak pernah klaim cek visual yang nggak dia lakukan: dia menilai screenshot-nya sendiri, nulis "not checked" kalau nggak ada browser, dan nyerahin hover, animasi, dan console ke main session dengan mata di live preview.

### Kredit

**Author**
- Redho Ramadhani: [linkedin.com/in/redhoramadhanihamid](https://id.linkedin.com/in/redhoramadhanihamid) · [github.com/redhoram](https://github.com/redhoram)

**Skill bawaan hasil adaptasi**
- `antislop` dan skill pendampingnya: diadaptasi dari [anti-slop](https://github.com/miqdadbadjuber/anti-slop) v3.2.23 karya miqdadbadjuber, Lisensi MIT (`.claude/skills/antislop/LICENSE`). Perubahan: tanpa wizard instalasi dan pertanyaan mode, mode tetap per agent, toggle tema hanya kalau diminta, dan tanpa karakter em dash atau emoji.
- `humanizer` v3.1.0 karya Siqi Chen, Lisensi MIT (`.claude/skills/humanizer/LICENSE`), disertakan tanpa perubahan; contoh di dalamnya tetap memuat dash dan emoji yang justru diajarkan untuk dibuang.

Dibangun dengan [Claude Code](https://claude.com/claude-code).
