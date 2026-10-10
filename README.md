# letriv v2

**LETRIV** — AI-assisted diagnostic writing platform untuk evaluasi menulis Bahasa Arab.

> Trace. Revise. Improve.

## Dokumentasi

| Kategori | Link |
|----------|------|
| **Indeks lengkap** | [docs/README.md](docs/README.md) |
| MVP Plan | [docs/mvp/MVP.md](docs/mvp/MVP.md) |
| Backlog | [docs/mvp/BACKLOG.md](docs/mvp/BACKLOG.md) |
| Core Loop | [docs/mvp/CORE_LOOP.md](docs/mvp/CORE_LOOP.md) |
| Role Flows | [docs/mvp/ROLE_FLOWS.md](docs/mvp/ROLE_FLOWS.md) |
| Setup Dev | [docs/operations/SETUP.md](docs/operations/SETUP.md) |
| Arsitektur | [docs/technical/ARCHITECTURE.md](docs/technical/ARCHITECTURE.md) |
| PRD | [PRD_LETRIV_v2.docx](PRD_LETRIV_v2.docx) |

## Modul Sistem

- **Writing Workspace** — input, pra-pemrosesan, revisi berversi
- **OCR Review** — transkripsi dan verifikasi manusia
- **Diagnostic Map** — diagnosis span-level, dashboard, ekspor
- **Annotation Studio** — moderasi dosen, anotasi pakar
- **Admin Console** — RBAC, taksonomi, audit log

## Quick Start

```bash
pnpm install
pnpm db:start && pnpm db:reset
pnpm dev          # web → localhost:3000
pnpm dev:nlp      # nlp → localhost:8000
```

Lihat [docs/operations/SETUP.md](docs/operations/SETUP.md) untuk panduan lengkap.

Layanan diagnosis adalah microservice FastAPI (`pnpm dev:nlp`, `apps/nlp-service`) — rules 0.4.0 + CAMeL Tools Beta (opsional). Bukan placeholder string di web.

## Status

🟢 **MVP core loop selesai** — Examine → Trace → Verify → Revise & Export

| Area | Status |
|------|--------|
| Foundation + Auth + Admin | ✅ |
| Writing Workspace + OCR (E-01–E-05) | ✅ |
| Diagnosis + Diagnostic Map (T-01–T-08) | ✅ |
| Annotation Studio (V-01–V-05, V-08) | ✅ |
| Revisi + Ekspor (R-01–R-03, X-01–X-02) | ✅ |
| Hardening + QA checklist | ✅ |

## Korpus dummy (pre uji lapangan)

12 teks Arab contoh tersedia tanpa perlu uji lapangan dulu:

- **UI:** `/workspace/samples` atau pemilih di **Tulis Baru**
- **Kode:** `apps/web/src/lib/fixtures/arabic-samples.ts`
- **Indeks:** `tests/fixtures/arabic-samples.json`

Sampel D01–D12 mencakup morfologi, sintaksis, leksikal, campuran, dan edge case relatif bersih.

```bash
pnpm test          # shared-types + arabic-utils + taxonomy
pnpm test:nlp      # pytest detectors (rules 0.4.0 + CAMeL jika terpasang)
pnpm eval:gold:all # pilot + open gold eval
pnpm import:field-transcripts:force  # UNISSA Task4 → batch assignment + NLP
pnpm test:e2e      # Playwright core loop (butuh web :3000)
pnpm smoke         # build + health checks (butuh dev server untuk health)
```

Checklist uji manual: [docs/mvp/QA_CHECKLIST.md](docs/mvp/QA_CHECKLIST.md)

---

LETRIV adalah merek milik PT Grafisio Indotama.
