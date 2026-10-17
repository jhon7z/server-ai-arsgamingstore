# Desain: ARS AI — "LLM Uncensored Tercepat untuk AI Developer"

- **Tanggal**: 2026-10-17
- **Status**: DRAFT v0.4 — DD supplier selesai (izin jual-ulang ✓); siap **direview owner** untuk approval
- **Repo**: `jhon7z/server-ai-arsgamingstore` (GitHub) → deploy **Cloudflare Workers + Pages**
- **Owner**: ARSGAMINGSTORE (IG/WA/Telegram) · **Builder**: agent OpenCode

---

## 1. Latar & alasan (kenapa ini dibangun)

ARSGAMINGSTORE sudah punya mesin dagang yang jalan: akun PB, topup MLBB/PUBGM/Genshin, channel IG/WA/Telegram, pembayaran QRIS/e-wallet, dan pembeli repeat yang percaya.

Permintaan datang sendiri: pembeli mulai nanya **"ada LLM Uncensored Tercepat untuk AI Developer ga bg jun?"**. Artinya demand-nya sudah ada sebelum barangnya ada — posisi paling enak buat mulai.

Tujuan utamanya uang: jual akses LLM uncensored dengan format yang familiar buat pembeli ARS (paket kecil, harga rupiah, proses cepat), ambil margin dari selisih harga wholesale → retail. Efek sampingnya bagus: jadi pintu masuk lini produk AI lain di store (chat access, tools, bundle topup) dan memperkuat citra ARS sebagai "toko yang selalu bisa nyediain apa yang diminta".

## 2. Apa yang dibangun (v1)

Satu platform "ARS AI":

1. **Gateway API** (Cloudflare Worker, OpenAI-compatible): `POST /v1/chat/completions` (streaming + tool calling), `GET /v1/models`. Auth per API key, kuota token, rate limit, logging pemakaian.
2. **Web** (Cloudflare Pages): landing + pricing (IDR), docs Bahasa Indonesia (quickstart curl/Python/JS + panduan tool populer), **playground** (coba model pakai trial), dashboard pembeli (sisa kuota, pemakaian, key, riwayat order).
3. **Panel admin** (internal): order masuk, konfirmasi bayar manual, auto-issue key, revoke, monitor pemakaian & saldo upstream.
4. **Alur beli gaya topup**: pilih paket → bayar (QRIS/e-wallet yang sudah dipakai ARS) → konfirmasi → key tampil otomatis + dikirim via WA/Telegram/email.
5. Semua jalan di **Cloudflare** (Workers, Pages, D1, KV) + source di **GitHub**. Tanpa VPS, tanpa server nganggur.

## 3. Goals / Non-goals / Anti-goals

**Goals**
- G1: pembeli ARS & developer Indonesia bisa beli akses uncensored < 5 menit, tanpa ngerti crypto/English.
- G2: margin kotor positif per transaksi sejak hari pertama (target awal 40–60%).
- G3: bangun **bertahap & santai** — milestone utama = "versi yang bisa di-publish"; opening ke publik keputusan owner (tanpa target tanggal keras).
- G4: nol ops server; biaya tetap ± $0–5/bulan di awal.

**Non-goals (v1)**: bikin model sendiri; GPU sendiri; aplikasi chat selesai; langganan bulanan; multi-bahasa; SLA formal.

**Anti-goals**: jangan janji yang tak terukur ("tercepat" wajib ada angka/label tier yang bisa dibuktiin); jangan bocorin identitas upstream (master key & nama provider = server-side only); jangan layani konten ilegal (AUP + blocklist minimal); jangan single point of failure di satu upstream (selalu ada plan B).

## 4. Constraint & keputusan owner

- **Deploy**: Cloudflare Workers & Pages; source di GitHub `jhon7z/server-ai-arsgamingstore`.
- **Domain**: `arsgaming.web.id` (aktif di Cloudflare) → web di `ai.arsgaming.web.id`, gateway di `api.arsgaming.web.id`.
- **Bentuk usaha**: reseller akses LLM uncensored (beli wholesale, jual retail) — bukan training model sendiri (di awal).
- **Target awal**: pembeli existing ARS + developer Indonesia.
- **Harga**: rupiah, paket kecil-kecil gaya topup game.
- **Brand**: **ARS AI** (sub-brand ARS) — tagline utama: *"Uncensored LLM tercepat untuk AI Developer"*.
- **Konten**: diizinkan (termasuk dewasa yang legal) dengan gate umur + "gunakan dengan bijak"; ilegal dilarang keras (lihat §9).
- **Timing**: santai — "training web" bareng, tiap step dijelasin; opening setelah versi publishable dianggap layak oleh owner.

## 5. Produk & harga (DEFAULT USULAN — angka final = owner)

Unit: **token** (input + output dihitung). Buat gambaran: 1 balasan chat medium ≈ 500–1.000 token (in+out), jadi 1 juta token ≈ ratusan balasan.

**Tier & model** (nama publik pakai alias kita `ars-fast` / `ars-flagship`; mapping upstream disimpan server-side):

| Tier | Model upstream (internal) | Catatan |
|---|---|---|
| Fast | GLM 5.3 Flash Uncensored (NanoGPT), gemma-4-26B-A4B (Featherless) | janji "tercepat" — kasus utama agent/chat |
| Flagship | Dolphin 72B, Llama 3.3 70B abliterated (Unfil) | kualitas lebih tinggi |
| (M2) Fiction | Mistral Small 3.2 abliterated / model RP | buat bot karakter/roleplay |
| (M2) Bahasa | Qwen/Gemma — model global yang jago Bahasa Indonesia | ditandai di docs biar gampang dipilih |

**Paket (default usulan):**

| Paket | Kuota token | Harga | Estimasi cost | Margin kotor |
|---|---|---|---|---|
| Trial (gratis, sekali/akun) | 50.000 | Rp 0 | ± Rp 500 | hook |
| Fast Kecil | 500.000 | Rp 9.000 | ± Rp 4.100 | ± 55% |
| Fast Standar | 1.000.000 | Rp 15.000 | ± Rp 8.250 | ± 45% |
| Fast Gede | 3.000.000 | Rp 39.000 | ± Rp 24.750 | ± 37% |
| Flagship Kecil | 500.000 | Rp 12.000 | ± Rp 5.400 | ± 55% |
| Flagship Standar | 1.000.000 | Rp 21.000 | ± Rp 10.700 | ± 49% |
| Flagship Gede | 3.000.000 | Rp 55.000 | ± Rp 32.200 | ± 41% |

Asumsi: FX Rp 16.500/$, campuran input:output 1:1, harga upstream per 2026-10-17. Kuota habis → beli lagi (repeat natural). M2: langganan bulanan + bundle "topup game + token bonus".

**Aturan kuota (keputusan builder):** tiap pembelian = satu *bucket* kuota yang terikat tier-nya (kuota Fast hanya bisa dipakai di model Fast; Flagship di Flagship). Bucket se-tier bisa menumpuk (sisa dijumlahkan). Kuota **tidak expired** — sisa kuota yang tak terpakai = margin ekstra (breakage); kalau owner mau expiry, tinggal bilang.

## 6. Supply (hulu) & due diligence

**Semua model = open-weight global** (Llama, Mistral, Qwen, Gemma, GLM) yang disajikan lewat provider global (NanoGPT, Unfil, Featherless, dll) — bisa diakses dari mana saja termasuk Indonesia, via API OpenAI-compatible. LLM "resmi Indonesia" (Sahabat-AI dkk) tidak dipakai: kebanyakan di-fine-tune dari base global yang sama tapi sudah *aligned* (bukan bahan uncensored) dan tidak ada jalur wholesale buat reseller. Bonus: model global yang kita pakai (Qwen, Gemma) sudah kuat Bahasa Indonesia.

**Hasil due diligence (2026-10-17 — dicek langsung ke ToS/site masing-masing; kutipan & bukti lengkap di `docs/research/2026-10-17-supplier-dd.md`):**

| Provider | Izin jual-ulang | Logging prompt | OpenAI-compat | Bayar |
|---|---|---|---|---|
| **NanoGPT** | ✅ **EKSPLISIT** di pay-as-you-go ("Reselling access to our Services as part of your own service offerings"); subscription TIDAK boleh untuk resale; ada **Partner Program** resmi | Default tidak menyimpan prompt; tidak training (log opt-in 1–30 hari) | ✅ terverifikasi: SSE + tools | Kartu dari $1; crypto dari $0.10 |
| **Featherless** | ✅ hanya plan **Scale/business** ("including inference resale"); plan Chat dilarang | Tidak log chat/prompt/completion | ✅ OpenAI-compat; tools native hanya Kimi-K2 & Qwen 3; ⚠️ streaming belum terdokumentasi | Kartu (Stripe); $50+/bulan |
| **NSFW AI API** | ⚠️ commercial ✅; resale tidak dibahas → minta izin tertulis | Tidak untuk training; klaim no-log tidak eksplisit | ✅ lengkap (SSE + tools + 100k ctx) | **Crypto only** $20–500 (USDT/USDC); bonus +5/10/15% |
| **Unfil AI** | ⚠️ business use implied; resale tidak published → kontak support; situs belum kelar (docs "coming soon") | Tidak disimpan setelah diproses; tidak training | ⚠️ tidak bisa diverifikasi | Kartu/wallet/crypto; min tidak dipublish |
| **abliteration.ai** | ⚠️ ToS tidak menyebut resale → kontak; zero-retention paling kuat | ZDR default; telemetry saja | ✅ (tanpa `response_format`) | Stripe; plan $20/50/200 + prepaid |

**Harga model (kandidat):** NanoGPT — GLM 5.3 Flash Uncensored $0.20/$0.80, Qwen 3.8 27B Uncensored $1/$3, Abliterated Large V2 $3/$5. Unfil — Dolphin 72B $0.6/$0.7, Llama 70B abliterated $1.1/$1.2, Hermes 405B $1.2/$1.2. NSFW AI API — $0.25/$1.00 (1 model). Featherless — flat (gemma-4-26B-A4B dll).

**Keputusan supply (revisi):**
- **Fast tier → NanoGPT pay-as-you-go** — jalur paling aman: izin resale eksplisit, streaming + tools terbukti, topup crypto murah. **Link integrasi: `https://api.nano-gpt.com/api/v1`** (OpenAI-compatible; docs `docs.nano-gpt.com` — diverifikasi 2026-10-17). **Partner Program** mereka (white-label: NanoGPT urus billing di belakang) dievaluasi di M0 sebagai opsi percepatan.
- **Flagship tier → kandidat NanoGPT dulu** (Abliterated Large V2 / Qwen 3.8 27B Uncensored); provider lain masuk setelah izin tertulis.
- **Aksi lanjutan (builder):** (1) email partner@nano-gpt.com + support: scope resale & Partner Program; (2) minta izin resale tertulis dari Unfil / NSFW AI API / abliteration.ai bila mau dipakai; (3) konfirmasi Featherless: padanan plan "Scale" saat ini + dukungan streaming; (4) arsipkan semua bukti di `docs/research/`.

**Fallback** kalau izin provider tersendat: (a) supplier lain dengan izin eksplisit; (b) sewa GPU + vLLM host model abliterated sendiri (M3 dipercepat).

Funding wholesale: kartu (NanoGPT dari $1) atau crypto (NanoGPT dari $0.10; NSFW AI API USDT/USDC $20–500). Currency risk: harga kita rupiah, biaya dolar → buffer di margin + review harga berkala.

## 7. Arsitektur

```
Pembeli ──► Web (CF Pages): landing · pricing · docs · playground · dashboard
               │ REST
               ▼
        Gateway (CF Worker, OpenAI-compatible)
        auth key → cek kuota (D1) → rate limit (KV) → model map → proxy streaming
               │
               ▼
        Upstream uncensored (NanoGPT / Unfil / …)  ← saldo wholesale

Admin ──► /admin (Pages, dilindungi): order → konfirmasi bayar → issue key; monitor
Data   ──► D1: users, api_keys, orders, products, usage_events, upstream_models, settings
           KV: rate limit · Secrets: master key upstream (TIDAK masuk repo)
Cron   ──► rollup pemakaian harian, alarm saldo upstream tipis, expire order
Deploy ──► GitHub → Actions: wrangler deploy (Worker) · Pages via integrasi git
```

Detail kunci:
- **Alias model publik** (`ars-fast`, `ars-flagship`, dst) → mapping ke upstream di D1. Ganti provider tanpa ubah docs/harga.
- **Key**: format `ars-xxxx`, disimpan hashed (SHA-256 + prefix lookup); full key tampil sekali + di halaman order.
- **Identitas pembeli (keputusan builder)**: M0 tanpa akun — order via WA, admin terbitkan key. M1: login dashboard pakai *magic link* email; No WA opsional disimpan buat delivery. Trial 1× per email+No WA (dijaga sistem; kebocoran trial ditoleransi karena biayanya kecil).
- **Playground** dilindungi key (trial atau berbayar) + rate limit per IP.
- **Streaming SSE passthrough** (wajib — ini inti UX); error upstream di-map ke JSON rapi.
- **Usage log per request**: key_id, model, token in/out, latency, status, ts — async (`waitUntil`) biar tidak nambah latency.
- **Rate limit** per key (RPM) di KV; budget hard-stop di cek kuota.
- **Admin manual confirm**: state machine order (created → paid → issued → expired/refunded), idempotent, audit-logged.
- **CF limits** (verifikasi saat build): Workers free ± 100k req/hari; paid $5 utk 10jt req; D1 free 5 GB. Cukup untuk fase awal.

## 8. Pembayaran & fulfillment

- **v1 — manual-confirm** (persis alur toko sekarang): order dari web/WA → instruksi bayar QRIS/e-wallet → admin klik "Lunas" → key otomatis di-generate, tampil & terkirim. Tanpa integrasi payment gateway dulu.
- **v2 (M1+)**: webhook gateway QRIS otomatis; opsi crypto (USDT) buat segmen internasional.
- Edge cases: order hangus 24 jam; refund manual (sebelum key dipakai banyak); kebijakan salah kirim.

## 9. Legal & AUP

- **Posisi konten (DIPUTUSKAN owner)**: diizinkan, termasuk dewasa yang legal, dengan gate umur + pesan "gunakan dengan bijak"; **ilegal dilarang keras** — pelanggaran = revoke tanpa refund. Gate umur diset **18+** di dokumen/site (standar global & lebih aman buat payment; owner awalnya bilang 17+ — bisa diganti kapan saja).
- **AUP publik**: larangan konten ilegal (mengacu hukum Indonesia & umum). "Uncensored" = model open-weight tanpa lapisan filter vendor — bukan izin bebas.
- **Terms + Privacy**: data minimal (email/No WA opsional); log pemakaian disimpan X hari (default usulan 30–90, owner putuskan).
- **Enforcement reaktif**: laporan abuse + monitoring metadata + revoke/ban — **isi prompt tidak disimpan** secara default.
- Risk note: jual akses API legal; risiko utama ada di konten user + kebijakan pembayaran.

## 10. Roadmap (santai, step-by-step)

- **M0 — "Fondasi & Training"**: setup repo + project Cloudflare; halaman pertama dipublish (biar ada kemenangan cepat & lu bisa lihat prosesnya); gateway dasar (auth/quota/streaming/1–2 model); admin panel minimal. Mode belajar: tiap step dijelasin, lu bisa tanya & ikut ngecek.
- **M1 — "Versi Publishable"**: web penuh (landing/docs/playground/dashboard), order otomatis + auto-issue + delivery WA/TG/email, polish "secanggih mungkin" (gaya ARS). → **opening = keputusan owner** setelah ini (jualan ke pembeli lama bisa lebih awal kalau owner mau).
- **M2 — "Growth"**: langganan bulanan, bundle topup game + token bonus, referral/komunitas, konten SEO ID ("LLM uncensored murah", "API uncensored Indonesia"), panduan integrasi tool populer.
- **M3 — "Infra Sendiri"**: GPU sewa + vLLM (model abliterated sendiri) → margin naik, klaim "tercepat" makin tajam, ketergantungan upstream turun.

## 11. Metrik

- **Bisnis**: revenue/hari · key aktif · margin kotor % · repeat rate · refund %.
- **Teknis**: uptime gateway · overhead latency kita p95 (< 50 ms target) · error rate · saldo upstream (alarm) · token cost aktual vs asumsi.

## 12. Risiko utama & mitigasi

| Risiko | Dampak | Mitigasi |
|---|---|---|
| ToS upstream melarang jual-ulang | Bisnis mati | DD pra-launch; multi-upstream; fallback self-host |
| Upstream deprecated / naik harga | Margin tergerus | alias mapping gampang ganti; buffer harga; review bulanan |
| Abuse konten ilegal oleh user | Legal & payment | AUP, blocklist minimal, monitoring, ban tegas |
| Kebocoran master key | Fatal | secrets-only; rotasi berkala; audit log |
| CF limits kena | Downtime | monitor; upgrade $5 saat perlu; desain cache-friendly |
| Kompetitor undercut | Margin | fokus pengalaman lokal (Bahasa, support cepat, bundling ARS) |

## 13. Keputusan yang diambil builder (buat dicek owner)

- Gateway **custom di Workers + D1** (LiteLLM tidak bisa jalan di Workers — tidak dipakai).
- **Supply utama = NanoGPT pay-as-you-go** — izin resale eksplisit di ToS (subscription bukan untuk resale); Partner Program mereka dievaluasi di M0.
- **v1 manual-confirm** (tanpa integrasi payment gateway dulu; nyusul di M1).
- **Alias model publik**; identitas upstream internal saja.
- Log pemakaian disimpan (default 30–90 hari; owner bisa ubah) — metadata saja, isi prompt tidak disimpan.
- Klaim "tercepat" selalu dengan label tier/angka yang bisa dibuktiin.
- Identitas: M0 tanpa akun; M1 magic link email (WA OTP = nanti).
- **Kuota per-tier bucket, tanpa expiry.**
- Scope M1: delivery outbound + deep link saja — bot WA inbound (order otomatis penuh) di luar scope v1. Email sender butuh domain final; TG bot opsional kalau owner sudah punya.
- Nama produk **"ARS AI"** (bukan "ARS AI Developer" — kata "Developer" jadi bagian tagline biar brand tetap pendek & lentur).
- Subdomain: **`ai.arsgaming.web.id`** (web) + **`api.arsgaming.web.id`** (gateway) — domain final, sudah aktif di Cloudflare.
- Gate umur dibakukan **18+** (dari owner "17+").

## 14. Open questions (buat owner)

1. **Metode bayar wholesale**: buat topup saldo provider nanti, lu punya opsi apa — kartu internasional (Visa/MC), crypto (USDT), atau lainnya?
2. **Lama simpan log pemakaian** (usulan default 30–90 hari; metadata saja).
3. **Nama brand**: default **ARS AI** (rekomendasi builder); opsi **ARS AI DEV** kalau lu mau — tinggal pilih.

**Sudah selesai:** Domain ✓ (`ai.arsgaming.web.id` + `api.arsgaming.web.id`). DD provider ✓ (NanoGPT paygo — izin resale eksplisit; aksi lanjutan: izin tertulis provider backup + konfirmasi Featherless, tidak blocking).

## 15. Left to builder

Skema D1 lengkap + migrations; implementasi Worker & halaman; desain UI (gaya ARS); copywriting; test plan (streaming, quota, revoke, load dasar); setup project Cloudflare & GitHub Actions; panduan integrasi; hardening; **due diligence izin jual-ulang provider (dengan bukti)**.
