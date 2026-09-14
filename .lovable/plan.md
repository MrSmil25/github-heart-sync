# Rebuild Landing dan Login My Room

## Ringkasan
Membangun ulang hanya halaman `/` dan `/login` sebagai React + TypeScript, mengikuti tampilan dan gerak dari file referensi. Alur Supabase, pendaftaran dengan kode undangan, lupa password, dashboard, dan seluruh halaman setelah login tetap dipertahankan.

## Yang akan dibangun
- Landing layar penuh dengan header My Room, teks utama sesuai referensi, aura, vignette, ambient canvas, dua objek 3D berputar, drag/spin, partikel transisi, tombol jeda, CTA “Masuk ke ruang”, dan footer.
- Objek pertama memakai identitas visual My Room yang tersedia; objek kedua memakai simbol “M” netral agar mudah diganti nanti.
- `/login` memakai latar animasi yang sama dan menampilkan kartu login sebagai lapisan di atasnya, termasuk tombol kembali.
- Form login tetap memanggil `supabase.auth.signInWithPassword({ email, password })`, menampilkan kegagalan di area status, lalu menuju `/dashboard` setelah berhasil.
- “Lupa password?” menjadi tautan ke `/forgot-password`; “Daftar” menjadi tautan ke `/register`, sehingga alur kode undangan yang sudah ada tidak berubah.
- Mode gelap mengikuti referensi. Mode terang memakai latar putih, aura biru muda, teks navy, kartu putih, dan aksen biru My Room.
- Toggle matahari/bulan diletakkan di kanan atas dekat tombol jeda. Pilihan disimpan dengan key `my-room-theme`; bila belum ada pilihan, nilai awal mengikuti preferensi perangkat.

## Batas perubahan
- Mengubah hanya presentasi dan perilaku halaman My Room yang dipakai oleh `/` dan `/login`, beserta mesin canvas/WebGL khusus kedua halaman tersebut.
- Tidak mengubah halaman register, lupa password, reset password, dashboard, sidebar, struktur data, atau aturan autentikasi.
- Tidak menggunakan HTML mentah atau `dangerouslySetInnerHTML`; struktur halaman dibuat sebagai JSX semantik.

## Detail teknis
- Pecah struktur layar, header/toggle, kartu login, canvas, dan fallback menjadi komponen React kecil.
- Pertahankan teknik renderer WebGL, ambient canvas, drag inertia, pause/resume, dan particle transition dari referensi; sesuaikan warna renderer dengan tema aktif.
- Semua loop, fetch model, listener, observer, pointer capture, dan konteks WebGL dibersihkan saat unmount agar aman ketika berpindah Landing → Login → Landing.
- Gunakan aset logo My Room yang sudah ada di proyek dan pertahankan fallback visual jika WebGL tidak tersedia.
- Tambahkan metadata Inter melalui head route, bukan impor URL di CSS.

## Verifikasi
- Uji desktop dan mobile untuk dark/light, panjang teks, posisi kartu, dan tidak adanya sidebar.
- Uji drag, spin, partikel, jeda/lanjut animasi, penyimpanan tema, serta preferensi awal perangkat.
- Uji `/` → `/login` → kembali → `/` berulang tanpa freeze.
- Uji tautan `/register` dan `/forgot-password`, kegagalan login di area status, serta login sukses menuju dashboard.
- Pastikan hasil kompilasi bersih dan tidak ada error runtime/console baru.
