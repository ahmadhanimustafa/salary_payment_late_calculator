# Salary Payment Late Calculator

Single-page tracker to calculate late payment penalties, log partial/complete salary payments, and manage planned installments. Built as a static HTML page (`index.html`) with all logic running in the browser and stored in `localStorage`.

## Quick start

1. Buka `index.html` di browser modern (cukup klik dua kali file atau gunakan server statis seperti `python -m http.server`).
2. Isi form **Tambah kewajiban gaji**:
   - Total gaji bulan ini (Rp)
   - Tanggal gajian bulanan
   - Tanggal referensi hitung denda (otomatis lanjut ke hari ini selama masih ada sisa gaji)
   - (Opsional) bunga bank per bulan setelah >30 hari
3. Simpan jadwal, lalu gunakan kartu yang muncul untuk:
   - Menambah pembayaran (rupiah atau persentase dari gaji)
   - Membuat rencana pembayaran, menandai rencana sebagai dibayar, atau menghapusnya
   - Melihat akumulasi denda, sisa gaji, dan total kewajiban
4. Gunakan tombol **Export data (JSON)** untuk mengunduh seluruh jadwal, pembayaran, dan rencana yang tersimpan di `localStorage`.
5. Gunakan **Bersihkan semua data** untuk menghapus penyimpanan lokal dan memulai ulang.

## Penjelasan denda (ringkas)

- Hari 4–8: 5% per hari atas sisa gaji belum dibayar.
- Hari 9 dan seterusnya: +1% per hari, total denda dasar dibatasi 50% dari gaji.
- Lewat 30 hari: bunga harian = (bunga per bulan / 30) × sisa gaji; bunga di luar batas 50%.
- Denda otomatis berhenti saat outstanding = 0; jika masih ada sisa, kalkulasi memakai tanggal hari ini.
