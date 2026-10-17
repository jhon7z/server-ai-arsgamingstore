# Recon Harga Sumber GLM 5.3 Flash — Jalur Termurah untuk Reseller

- **Tanggal**: 2026-10-17 (semua harga dicek live)
- **Konteks**: kompetitor jual Rp 5.000–7.000/M ⇒ landed cost harus ≤ $0.182 @Rp5k / ≤ $0.255 @Rp7k supaya margin ≥40% (kurs dokumen 16.500; spot hari ini ~18.015).
- **1:1 mix** = (input + output) / 2.

## Tabel utama (base `z-ai/glm-5.3-flash`, urut termurah)

| Provider | Model / ID | In $/M | Out $/M | 1:1 $/M | Catatan |
|---|---|---|---|---|---|
| OpenRouter batch | `z-ai/glm-5.3-flash:batch` | $0.05 | $0.18 | **$0.115** | Async/batch, bukan realtime. OR ToS larang resale. |
| Bitdeer AI ⚠ | GLM-5.3-Flash | $0.07* | $0.25* | $0.16* | *Dari Artificial Analysis; halaman harga mereka JS-only — belum terverifikasi langsung. |
| OrcaRouter ⚠ | `z-ai/glm-5.3-flash` | $0.07–0.075 | $0.25 | ~$0.16 | Blog mereka sebut $0.07/$0.25 (cache $0.017). ToS/SLA belum direview. **Org yang sama menerbitkan bobot uncensored.** |
| DeepInfra | `zai-org/GLM-5.3-Flash` | $0.075 (**50% off**, list $0.15) | $0.25 (list $0.50) | **$0.1625** | 1M ctx, fp4, zero-retention, tools+JSON, multimodal. Promo aktif. ToS: resale hanya "under a Service Order" (kontak sales). |
| OpenRouter – StreamLake | sama | $0.075 | $0.25 | $0.1625 | OR +5.5% fee + larangan resale. |
| OpenRouter – Decart | sama | $0.0825 | $0.275 | $0.1788 | idem. |
| OpenRouter – Novita | sama | $0.084 | $0.28 | $0.182 | idem; Novita langsung list $0.15/$0.50. |
| OpenRouter – GMICloud | sama | $0.09 | $0.30 | $0.195 | idem. |
| Z.ai China / BigModel ⚠ | GLM-5.3-Flash | ¥0.80 ≈ $0.119 (promo ¥0.40 ≈ $0.060) | ¥2.80 ≈ $0.418 (promo ¥1.40 ≈ $0.209) | $0.269 (promo $0.134) | Platform China, perlu verifikasi +86; halaman geo-gated. |
| SiliconFlow | `zai-org/GLM-5.3-Flash` | ¥0.80 ≈ $0.119 | ¥2.80 ≈ $0.418 | $0.269 | Platform China/RMB. |
| Gonka broker | `zai-org/GLM-5.3-Flash` | $0.20 | $0.20 flat | $0.20 | DePIN via broker, 400K ctx, free tier ~1.2M tok/bln. |
| NanoGPT | `z-ai/glm-5.3-flash` | $0.10 | $0.30 | $0.20 | Base model; badge "Unavailable" hari ini ⚠; cache read $0.025. |
| Requesty – Melious | `glm-5.3-flash` | $0.12 | $0.46 | $0.29 | +5% fee. |
| Z.ai intl (first-party) | GLM-5.3-Flash | $0.15 | $0.50 | $0.325 | Harga list resmi; cached $0.03. |
| Fireworks | `glm-5p3-flash` | $0.15 | $0.50 | $0.325 | Model page langsung. |
| Together AI | `zai-org/GLM-5.3-Flash` | $0.15 | $0.50 | $0.325 | Serverless + dedicated. |
| Novita direct | `zai-org/glm-5.3-flash` | $0.15 | $0.50 | $0.325 | fp8, 1M ctx, tools. |

## Varian uncensored / abliterated

| Provider | Model / ID | In $/M | Out $/M | 1:1 | Catatan |
|---|---|---|---|---|---|
| NanoGPT | `z-ai/glm-5.3-flash-uncensored` | $0.20 | $0.80 | **$0.50** | = finetune abliterated NVFP4 dari OrcaRouter; tools/structured output. "Unavailable" ⚠. |
| NanoGPT | `z-ai/glm-5.3-flash-apex-abliterated` | $0.15 | $0.50 | $0.325 | Varian abliterated; "Unavailable" ⚠. |
| Routeway | `glm-5.3-flash-uncensored` | $0.35 | $1.40 | $0.875 | 262K ctx. |
| Abliteration.ai | `abliterated-model-large-v2` | $3.00 | $5.00 | $4.00 | GLM-5.3 abliterated (bukan Flash). Tidak viable di harga jalanan. |

## Featherless & Chutes
- **Featherless**: GLM-5.3-Flash ada (FP8, 256K), tapi pricing table menyatakan **"Reselling access: No"** di Chat ($25/bln) & Developer ($50/bln credits). Cuma **Business (custom contract)** yang "Negotiable". *Revisi dari DD awal.*
- **Chutes**: GLM-5.3-Flash tidak ditemukan di katalog per-token. Subscriptions Plus/Pro $10/$20 — bukan jalur resale.

## Plan langganan / flat-rate (🡒 ToS flag)
| Plan | Harga | Catatan |
|---|---|---|
| NanoGPT Pro | $12/bln | 60M input tokens/minggu; metering output tidak jelas; ketentuan resale tidak terverifikasi — pertanyaan kepatuhan. |
| Z.ai Coding Plan | $18/$80/$168 | Dirancang khusus coding tools — resale = pelanggaran ToS. |
| Featherless Chat/Dev | $25/$50 | Eksplisit no-resale. |
| Abliteration.ai | $20/$50/$200 | Per-token $3/$5 — tidak viable. |

## Kesimpulan ToS (untuk resale API mentah)
- **OpenRouter**: eksplisit melarang "reselling API access to Models" ❌
- **DeepInfra**: resale hanya dengan Service Order (kontak sales) ⚠
- **Featherless**: No di Chat/Dev; Business nego ⚠
- **NanoGPT**: predominant eksplisit izin (paygo) ✅
- **Self-host**: satu-satunya jalur bebas-ToS (bobot base MIT; bobot abliterated NVFP4 dipublikasikan OrcaRouter; ekonomi belum dimodelkan).

## Shortlist jalur komersial resale
1. **DeepInfra promo $0.075/$0.25 ($0.1625 @1:1)** — termurah terverifikasi realtime; GM 46%/62% @Rp5k/7k. Wajib nego hak resale (Service Order); promo berakhir → list $0.15/$0.50 jadi negatif @Rp5k.
2. **OrcaRouter $0.07–0.075/$0.25 (~$0.16)** — ekonomi sama, single-hop; juga vendor bobot uncensored. Verifikasi ToS & kapasitas.
3. **Bitdeer AI $0.07/$0.25 (⚠ unverified)** — kandidat termurah; enterprise-oriented (SOC2/ISO). Verifikasi harga & reseller terms.
4. **Novita promo endpoint $0.084/$0.28 (~$0.182)** — ≈40%/57% GM; nego promo langsung, bukan lewat OR.
5. **Z.ai China / SiliconFlow (~$0.269)** — hanya cocok kalau input-heavy/cache-heavy atau promo 50% ($0.134). Perlu akun China.
6. **Realita uncensored**: NanoGPT $0.20/$0.80 satu-satunya paid uncensored API yang ketemu; @1:1 butuh ≥Rp ~8.250/M untuk GM 40% → tidak bisa samain Rp 5–7k/M. Jalur struktural paling murah = **self-host bobot abliterated open** (M3).

## Item belum terverifikasi (eksplisit)
- Harga per-token Bitdeer (JS-only; sumber AI Analysis).
- Rate per-model GLM-5.3-Flash di Featherless (JS).
- Teks ToS NanoGPT + metering output subscription; badge "Unavailable" di halaman GLM 5.3 (mungkin transien).
- ToS Chutes; ketiadaan GLM-5.3-Flash = "tidak ditemukan", bukan pernyataan resmi.
- Harga open.bigmodel.cn (geo-gated; second-hand).
- Rute upstream asli kompetitor (ArxPays) — tidak diketahui.

## Metode & FX
- Semua sumber di-fetch 2026-10-17: Z.ai docs, DeepInfra, Together, Fireworks, Novita, SiliconFlow, Featherless, NanoGPT, Chutes, OrcaRouter, Routeway, Abliteration.ai, Gonka broker, OpenRouter endpoints API.
- CNY 6.698/USD; **IDR spot ~18.015/USD** (er-api). @spot: Rp5.000/M = $0.278 ⇒ hanya jalur ≤~$0.167 (kelas promo DeepInfra/OrcaRouter) yang tetap ≥40% GM di harga lantai jalanan; jalur $0.18 drop ke ~36%.
- Prompt caching (cache $0.015–0.03 di tier $0.15) = lever utama menahan GM ≥40% kalau mentok harga list.
- Fee OpenRouter: 5.5% kartu / 5% crypto; BYOK gratis s/d $25k/bln lalu 5%.
