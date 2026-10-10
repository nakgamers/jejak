# JEJAK — AI Teman Mendaki 🏔️

Submission untuk **Hacktoberfest Open-Source AI Challenge Week 1: Touch Grass** (10–11 Okt 2026).

Asisten pendakian berbahasa Indonesia bertenaga **model open-weight
(`openai/gpt-oss-20b`)** via Groq. Pengguna menjawab profil pendakiannya →
model mencocokkan dengan **18 gunung Indonesia dari dataset kurasi**
(tidak mengarang!) → keluar rekomendasi + itinerary + packing list
+ peringatan keselamatan.

## Cara jalanin

1. Buka `index.html` di browser (atau serve: `python3 -m http.server`).
2. Bikin API key **gratis** di `console.groq.com` → API Keys (2 menit,
   tanpa kartu kredit).
3. Klik **KONFIGURASI MODEL**, tempel key-nya (tersimpan hanya di
   localStorage browser-mu).
4. Isi profil pendakian → **Minta Rekomendasi**.

Model default: `openai/gpt-oss-20b` (open-weight, Apache 2.0) — cepat
(~1000 tok/detik) dan gratis di tier Groq. Bisa diganti ke model
open-weight lain dari kolom pengaturan.

> Catatan: versi awal memakai Hugging Face Inference Providers, tapi malam
> sebelum deadline ketahuan layanannya butuh kredit berbayar. Karena modelnya
> open-weight, pindahnya semudah ganti endpoint — cerita ini malah jadi
> bagian "why open matters" di postingan submission.

## Deploy ke Render (Best Use of Render)

Repo ini 100% static — deploy sebagai **Static Site** di Render:

1. Push repo ini ke GitHub.
2. Render Dashboard → New → Static Site → pilih repo.
3. Build Command: kosongkan. Publish Directory: `.` (atau `/`).
4. Deploy. Selesai — dapat URL `https://jejak-xxxx.onrender.com`.

Klaim kredit $50 Hacktoberfest di hacktoberfest.com/my → Billing di Render.

## Struktur

- `index.html` — seluruh aplikasi (UI + dataset 18 gunung + pemanggil model)
- `dev-post-draft.md` — draft postingan submission DEV

## Kenapa open?

- Model **open-weight** (gpt-oss-20b): bisa diganti ke model lain, bisa di-self-host
  (Ollama/llama.cpp) tanpa tergantung satu vendor — cocok untuk dipakai di basecamp
  tanpa sinyal kalau nanti di-bundle offline.
- Dataset kurasi lokal: rekomendasi di-grounding ke data nyata, bukan halusinasi model.
- Token milik pengguna sendiri: tidak ada server perantara yang menyimpan data.
