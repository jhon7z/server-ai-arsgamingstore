# Due Diligence Supplier — Izin Jual-Ulang API Uncensored

- **Tanggal**: 2026-10-17
- **Untuk**: ARS AI (reseller akses LLM uncensored) — repo `jhon7z/server-ai-arsgamingstore`
- **Metode**: pengecekan langsung ke ToS/terms/pricing/docs masing-masing provider pada 2026-10-17. Kutipan verbatim + link. Item yang tidak bisa diverifikasi ditandai eksplisit (bukan ditebak).

## Ringkasan

| Provider | Izin jual-ulang? | Logging prompt | OpenAI-compat (stream/tools) | Bayar |
|---|---|---|---|---|
| **NanoGPT** | ✅ Eksplisit di pay-as-you-go ("Reselling access to our Services as part of your own service offerings"); ❌ subscription tidak boleh. Ada Partner Program resmi | Off by default ("we do NOT store prompt or conversation content"); no training; opt-in log 1–30 hari | ✅ chat/completions; ✅ SSE `stream:true`; ✅ tools/tool_choice | Kartu dari $1 (Stripe); Nano + crypto lain dari $0.10 |
| **Unfil AI** | ⚠️ Tidak dipublikasikan — perlu kontak support (business use implied; resale eksplisit tidak ada; docs "coming soon") | Tidak disimpan setelah diproses; tidak untuk training (klaim mereka) | ⚠️ "OpenAI SDK drop-in" hanya di halaman comparison; streaming/tools tidak bisa diverifikasi | Kartu, digital wallet, crypto; min topup tidak dipublikasikan |
| **NSFW AI API** | ⚠️ Commercial ✅ eksplisit, tapi resale tidak dibahas — perlu kontak support | Tidak untuk training; tidak ada komitmen eksplisit soal tidak-logging prompt | ✅ chat/completions; ✅ SSE; ✅ tools (termasuk streaming) | **Crypto only** (USDT TRC20 / USDC Base), $20–$500; bonus +5/10/15% |
| **Featherless** | ✅ hanya plan Scale/business ("including inference resale"); ❌ plan Chat/individual dilarang | "does not log chats, prompts, or completions"; no training | ✅ OpenAI-compatible; tools native hanya Kimi-K2 & Qwen 3 family; ⚠️ streaming tidak ada di docs vendor — verifikasi ke support | Kartu (Stripe); Chat $25/bln; Developer $50+; Business invoice |
| **abliteration.ai** | ⚠️ Tidak dipublikasikan — ToS diam soal resale | Zero-retention default; "never stored… never used to train"; telemetry saja | ✅ chat + responses; ✅ SSE; ✅ tools; ⚠️ tanpa `response_format` | Stripe; plan $20/$50/$200 per bulan + prepaid; kredit tidak expired |

## 1. NanoGPT — nano-gpt.com

**a) Commercial use / resale — EKSPLISIT DIIZINKAN (paling jelas dari kelimanya)**
Dari ToS ("Commercial Use Permitted", update 11 Okt 2026):
> "You are explicitly permitted to use NanoGPT as part of your commercial projects and services. This includes: … **Reselling access to our Services as part of your own service offerings** … Using our API or Services as a microservice within your commercial infrastructure"
— https://nano-gpt.com/legal/terms-of-service

Catatan di dokumen yang sama:
> "Subscription plans are intended for personal, non-commercial use only. Using a subscription for commercial purposes, including but not limited to reselling access … is not permitted. If you require commercial access, please use the pay-as-you-go model, which explicitly permits commercial use."

> "NanoGPT permits these commercial uses, including resale, but this permission does not override restrictions imposed by a Model Provider." (ketentuan per-model tetap berlaku)

**b) Data policy**
> "By default, we do NOT store prompt or conversation content on our servers." — https://nano-gpt.com/legal/privacy-policy
> "We do not train on your Input or Output, and we do not sell your Content." (ToS "Data Use Promise")
Ada opt-in log terenkripsi 1–30 hari (off by default). Per-provider pihak ketiga bisa punya kebijakan sendiri; ada ZDR routing settings.

**c) OpenAI compatibility — terverifikasi**
- `POST /api/v1/chat/completions` (OpenAI-compatible), base `https://api.nano-gpt.com/api/v1` — https://docs.nano-gpt.com/
- Streaming SSE terdokumentasi (`stream:true`, `text/event-stream`, `[DONE]`).
- Function calling OpenAI-compatible (tools, tool_choice, parallel_tool_calls; delta events mirror OpenAI).

**d) Funding**: "No deposit fees — start from $0.10 crypto or $1 card" — https://nano-gpt.com/pricing. Metode: Nano, kartu via Stripe, crypto via BTCPay/Nanswap/BoomFi. Volume discount: kontak.

**e) Partner Program — ADA (formal)**
> "The NanoGPT Partner Program lets you add AI — chat, image, video, and audio — inside your own product while NanoGPT runs the models, balances, and billing behind the scenes." (user-funded balances, referal opsional, tier partner) — https://docs.nano-gpt.com/partner/overview · apply: partner@nano-gpt.com

## 2. Unfil AI — unfil.ai

**a) Resale**: tidak dipublikasikan. ToS: lisensi "non-exclusive, non-transferable, revocable… use our Services"; homepage menyasar "SAAS AND SERVICES / CASINO / ADULT / CONTENT FARM" + "advise[s] you to implement your own alignment layer before exposing the model as a service" (implisit, bukan grant eksplisit). → **perlu kontak support untuk izin tertulis**.

**b) Data**: "We do not store your API prompts or responses after processing, and we do not use your API interactions to train our models." — /privacy-policy (log usage 30 hari untuk keamanan).

**c) OpenAI compat**: klaim "Drop-in replacement for OpenAI API" hanya di halaman /comparison. Docs = `/coming-soon` (kosong). **Streaming/tools tidak bisa diverifikasi.** Catatan: situs masih ada placeholder "localhost:3000" — situs belum kelar.

**d) Funding**: kartu/wallet/crypto; min tidak dipublikasikan; diskon volume sampai 40% bila >$10k/bulan.

**e) Partner program**: tidak ada (form kontak punya subjek "Partnership").

## 3. NSFW AI API — nsfwaiapi.com

**a) Commercial**: ✅ eksplisit — FAQ: "Yes. The uncensored model is suitable for both personal and commercial use. As long as the content is lawful and does not involve minors…". **Resale tidak dibahas** → perlu kontak.

**b) Data**: "not used to train models"; usage counter per key disimpan; tidak ada statement eksplisit "prompts tidak di-log". Hard limit: konten seksual dengan minor diblokir/refused.

**c) OpenAI compat — terdokumentasi lengkap**: base `https://api.nsfwaiapi.com/v1`, model ID `uncensored`, OpenAI SDK "work unchanged, SSE streaming, tools/tool_choice (termasuk streaming), JSON mode, 100k context, 300 rpm, 8 concurrent.

**d) Funding — crypto only**: USDT TRON / USDC Base, $20–$500; trial $0.50 (7 hari); bonus +5% (≥$50) / +10% (≥$100) / +15% (≥$200); kredit tidak expired.

**e) Partner program**: tidak ada (form kontak ada subjek "Partnership"). Tidak ada SLA/uptime guarantee.

## 4. Featherless AI — featherless.ai

**a) Resale**: ✅ hanya di plan **Scale/business**:
> "Individual plans are for interactive use or proto-typing… **Scale plans are not subject to said limits and may be used in arbitrary applications, including inference resale.**" — /legal/terms-of-service
Halaman pricing: plan Chat = "Not for reselling, app/API traffic, background automation… Misuse may lead to cancellation without refund." Saat ini plan = Chat / Developer / Pay-As-You-Go / Business — **konfirmasi plan mana yang setara "Scale"** ke sales.

**b) Data**: "Featherless does not log chats, prompts, or completions sent through our API…" — /docs/privacy-and-logging.

**c) OpenAI compat**: base `https://api.featherless.ai/v1`; tools native hanya "moonshotai/Kimi-K2-Instruct" & "Qwen 3 family"; **streaming tidak ada di docs vendor** (lihat LiteLLM docs sebagai indikasi, bukan bukti vendor) → verifikasi.

**d) Funding**: Stripe (kartu); Chat $25/bln; Developer $50+/bln; PAYG credits; Business annual. Tidak ada crypto/bonus.

**e) Partner/reseller program**: tidak ada formal; jalur = Scale/Business plans + volume pricing.

## 5. abliteration.ai

**a) Resale**: ToS tidak menyebut commercial-use atau resale sama sekali → **perlu kontak**. Enterprise: "Custom contracts and compliance review… Volume pricing".

**b) Data — terkuat dari kelimanya**: "Prompts, completions, and images are processed in memory and never stored by default… never used to train or fine-tune any model." Endpoint table: Zero data retention: Yes. Retained: token counts, timestamps, status, billing metadata.

**c) OpenAI compat — terverifikasi**: `/v1/chat/completions`, `/v1/responses`, `/v1/models`, Anthropic Messages; SSE `stream:true`; tools di semua surface; **tanpa `response_format`**.

**d) Funding**: Stripe; plan Developer $20 / Growth $50 / Scale $200 per bulan (termasuk credit + diskon 2.5/5/10%) + prepaid pack (~$20–500, ukuran = dari widget JS — *unverified*); kredit tidak expired; try free tanpa kartu.

**e) Partner program**: tidak dipublikasikan.

## Keterbatasan verifikasi (eksplisit)

- **Unfil AI**: docs belum ada ("coming soon") — OpenAI-compat/streaming/tools tidak bisa diverifikasi dari dokumen vendor.
- **Featherless**: tidak ada halaman docs soal SSE streaming.
- **abliteration.ai/pricing**: ukuran prepaid pack dari rendering cached (widget JS), bukan fetch halaman biasa — anggap belum terverifikasi.
- **nsfwaiapi.com**: FAQ hanya di `<details>`/JSON-LD — diambil dari page source.

## Kesimpulan

**Shortlist berbasis ketentuan tertulis:** **NanoGPT** (izin resale eksplisit + Partner Program) dan **Featherless** (izinkan "inference resale" di plan Scale/business). NSFW AI API & Unfil mengizinkan commercial use tapi kata "resale" harus didapat tertulis dari support sebelum launch; abliteration.ai tidak membahas sama sekali.
