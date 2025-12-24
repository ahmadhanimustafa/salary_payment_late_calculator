# Cara Menggunakan Tracker Pembayaran & Denda Gaji

1. **Buka aplikasi**
   - Buka `index.html` langsung di browser modern, atau jalankan server statis: `python -m http.server 8000` lalu buka `http://localhost:8000`.

2. **Tambah kewajiban gaji**
   - Isi **Total gaji bulan ini (Rp)**.
   - Isi **Tanggal jatuh tempo gaji (tanggal gajian setiap bulan)**.
   - Isi **Hitung denda sampai tanggal** (tanggal referensi; jika masih ada sisa gaji, perhitungan akan otomatis memakai hari ini).
   - (Opsional) Isi **Estimasi bunga per bulan** untuk bunga setelah 30 hari.
   - Klik **Simpan jadwal**.

3. **Catat pembayaran**
   - Di kartu jadwal, gunakan formulir **Catat pembayaran**.
   - Pilih tanggal bayar, nilai (rupiah atau persentase dari gaji), lalu klik **Tambah pembayaran**.
   - Pembayaran persentase otomatis dikonversi ke rupiah dan dibatasi ke sisa gaji.
   - Anda bisa menghapus pembayaran yang salah via tombol **Hapus** di tabel pembayaran.

4. **Kelola rencana pembayaran (planned)**
   - Tambahkan rencana di bagian **Jadwal pembayaran (rencana)** (tanggal, nilai, mode rupiah/persen).
   - Klik **Tambah rencana bayar** untuk menyimpan ke `localStorage`.
   - Gunakan **Tandai sudah dibayar** untuk memindahkan rencana menjadi pembayaran aktual.
   - Gunakan **Hapus** untuk membuang rencana tanpa mencatat pembayaran.

5. **Lihat hasil perhitungan**
   - Kartu jadwal menampilkan total gaji, sudah dibayar, sisa gaji, total denda (termasuk bunga), dan total kewajiban.
   - Catatan denda menampilkan denda dasar sebelum/after batas 50% dan bunga setelah 30 hari.

6. **Ekspor & reset**
   - Klik **Export data (JSON)** untuk mengunduh seluruh jadwal beserta pembayaran/rencana dari `localStorage`.
   - Klik **Bersihkan semua data** untuk menghapus semua penyimpanan lokal dan memulai ulang.

## Catatan logika denda
- Hari 4–8: 5% per hari dari sisa gaji belum dibayar.
- Hari 9 dan seterusnya: +1% per hari; total denda dasar dibatasi 50% dari gaji.
- Lewat 30 hari: bunga harian = (bunga per bulan / 30) × sisa gaji, dihitung di luar batas 50%.
- Jika outstanding masih ada, perhitungan otomatis memakai tanggal hari ini meski tanggal referensi lampau.
