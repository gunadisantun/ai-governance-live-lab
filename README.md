# AI Governance Live Lab

Aplikasi HTML untuk fasilitator pelatihan AI Governance. Dibuat oleh Santun Gunadi.

## Modul MVP
- Live Polling: opini peserta tentang penggunaan GenAI.
- AI Governance Quiz: satu jawaban benar, skor 100.
- Decision Game: keputusan implementasi AI credit scoring.
- Crisis Room: respons insiden GenAI dan data nasabah.
- QR code dan kode ruang 6 angka.
- Presenter Dashboard dan Participant Mode.
- Grafik respons, leaderboard, ekspor CSV.

Semua kasus dan pertanyaan bersifat sintetis. Hindari memasukkan data nasabah, data internal organisasi, atau informasi rahasia.

## Status
- Database Supabase telah disiapkan pada project ref bxfmocbpeqsepltixbce.
- Skema memiliki 5 tabel dengan Row Level Security aktif.
- Aplikasi statis berada di \`index.html\`.
- Aplikasi **belum dideploy** ke website publik.
- Pengujian sintaks JavaScript lulus, namun perlu uji end-to-end di browser dengan dua perangkat.

## Publikasikan online (Cloudflare Pages)
1. Hubungkan akun GitHub ke Cloudflare Pages.
2. Pilih repository \`gunadisantun/ai-governance-live-lab\`.
3. Pilih situs static HTML. Tidak perlu perintah build, dan output directory adalah \`/\` (root).
4. Deploy dan catat URL \`https://...pages.dev\`.
5. Di Supabase dashboard, pilih project yang ada, buka Authentication > Providers lalu aktifkan **Anonymous Sign-Ins** untuk peserta yang tidak login.
6. Pastikan Email Auth tersedia untuk presenter. Pada Authentication > URL Configuration, set **Site URL** ke URL hasil deployment dan masukkan URL ke redirect allowlist bila perlu.
7. Di aplikasi, pilih Presenter Mode > Daftar presenter. Verifikasi email bila diperlukan, lalu login.
8. Buat Sesi Baru dan minta peserta scan QR / masukkan kode.
9. Tes empat aktivitas menggunakan HP di jaringan internet yang berbeda.

## Kebijakan keamanan
- Hanya \`sb_publishable_...\` key yang boleh ada di HTML; jangan taruh service-role atau secret key.
- Semua tabel menggunakan RLS. Partisipasi dan pengiriman jawaban terjadi melalui RPC yang memeriksa identitas dan status sesi.
- Skor quiz dihitung di database; kunci jawaban disimpan pada tabel khusus yang hanya bisa dibaca presenter.
- Nama peserta sebaiknya berupa nama samaran. CSV hanya diekspor presenter.
- Sebelum dipakai untuk acara besar, aktifkan CAPTCHA/rate limiting untuk anonymous signup, batasi siapa yang boleh membuat akun presenter, atur retensi dan penghapusan data sesi, serta lakukan load test.
- Gunakan hosting dengan HTTPS. Jadikan GitHub repository private jika ingin membatasi keterlihatan kode; kode situs publik tetap dapat dilihat dari browser.

## Catatan keamanan Supabase
Supabase Security Advisor dapat memberikan peringatan karena RPC \`public.lab_join\` dan \`public.lab_submit\` berstatus SECURITY DEFINER. Kedua fungsi ini memang membutuhkan hak terbatas untuk mencatat keanggotaan/jawaban secara terkontrol. Fungsinya memeriksa auth.uid(), status sesi, dan keanggotaan; akses RPC untuk role anon telah dicabut. Tinjau lagi keamanan fungsi sebelum penggunaan produksi.

## Pemeliharaan
Pertanyaan awal ada pada konstanta \`demo\` di \`index.html\`. Setelah perubahan, commit kembali ke GitHub. Setiap sesi baru akan menggunakan pertanyaan terbaru, sedangkan sesi lama menyimpan salinannya sendiri.

## Kontak / penulis
Santun Gunadi
