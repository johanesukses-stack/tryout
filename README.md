# TRYOUT TKA MI HUSNAYAIN SLEMAN

Paket awal dibuat dari `Latihan_TKAD_IPAS_Paket3.docx`. Gambar setiap soal dipotong otomatis dari hasil render dokumen; gambar soal tidak perlu diunggah satu per satu. Roster berasal dari `Data Kelas 6 Ujian online.xlsx` (38 siswa). Jawaban/kunci tidak disimpan pada file publik `data/questions.json`; kunci disimpan di tabel database.

## Isi paket
- `index.html`, `style.css`, `app.js`: aplikasi responsif untuk HP/PC.
- `assets/questions/`: 30 gambar soal hasil ekstraksi/crop otomatis dari dokumen.
- `data/questions.json`: urutan soal dan jenis respons.
- Backend Supabase: disiapkan pada file terpisah `Supabase_Setup_PRIVATE.sql` (diunduh terpisah). File tersebut berisi data peserta, NISN, hash password, dan kunci jawaban. **Jangan unggah file ini ke GitHub. Jalankan langsung di Supabase SQL Editor.**
- `config.js`: tempat mengisi URL project dan public anon/publishable key Supabase.

## A. Buat database/backend Supabase
1. Buat project baru di Supabase.
2. Buka **SQL Editor**. Buka file terpisah `Supabase_Setup_PRIVATE.sql`, salin seluruh isinya, lalu jalankan sekali di SQL Editor. File tersebut memuat schema, kunci jawaban dan data siswa. Jangan unggah file ini ke GitHub.
3. Dari **Project Settings → API**, salin Project URL dan anon/publishable key. Key ini boleh digunakan pada frontend; jangan pernah menaruh `service_role` key di `config.js` atau GitHub.
4. Edit `config.js`:
   - `SUPABASE_URL`: URL project.
   - `SUPABASE_ANON_KEY`: anon/publishable key.
   - WhatsApp guru sudah disetel ke nomor yang diberikan.

## B. Publikasikan di GitHub Pages
1. Buat repositori GitHub. Unggah hanya file aplikasi: `index.html`, `style.css`, `app.js`, `config.js`, folder `assets/`, folder `data/`, dan `README.md`. Jangan unggah `Supabase_Setup_PRIVATE.sql` ke GitHub.
2. Buka **Settings → Pages**, pilih deploy dari branch `main`, folder `/ (root)`, lalu Save.
4. Tunggu alamat Pages muncul. Buka URL tersebut di HP untuk uji tampilan.

## Data login awal
Password pada spreadsheet yang diunggah adalah `husnayain` untuk seluruh siswa. Untuk keamanan, minta siswa menggantinya setelah uji coba atau ubah hash password melalui SQL sebelum ujian resmi. NISN disimpan sebagai teks agar angka nol di depan tidak hilang.

## Cara kerja ujian
- Waktu 90 menit dimulai saat pertama kali siswa menekan tombol masuk ke ujian.
- Setiap siswa hanya memiliki satu record pengerjaan. Setelah dikumpulkan atau waktu habis, login tidak dapat memulai ulang ujian.
- Jawaban disimpan otomatis ke backend setiap kali berubah.
- Tombol Panel Guru meminta PIN `321789`; rekap nilai dan analisis butir dapat diekspor CSV.
- Tombol WhatsApp membuka percakapan ke guru di `082143534304`.
- Layar penuh/browser tidak bisa benar-benar mengunci HP atau mencegah perpindahan aplikasi. Sistem memberi peringatan jika siswa kembali ke tab ujian; waktu tetap berjalan.

## Catatan penting sebelum dipakai resmi
- Jalankan tes lengkap dengan 1 akun percobaan terlebih dahulu: login salah/benar, autosave, refresh, timer, submit, blokir pengerjaan kedua, panel guru, CSV, dan HP.
- Database mengunci satu attempt per NISN. Jika ingin mengulang ujian untuk seluruh siswa, admin harus mereset data attempt secara sengaja di database (tidak tersedia di UI siswa).
- Gambar soal berasal dari dokumen latihan yang diunggah. Gunakan sesuai izin/syarat sumber dokumen; dokumen menyebut soal latihan dan tidak untuk diperjualbelikan.
- Analisis butir saat ini menghitung indeks kesukaran (proporsi benar). Analisis daya pembeda memerlukan pengolahan tambahan.
