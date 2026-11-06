## Decision Log - Minggu 1

- **Permasalahan / Kebutuhan Konfigurasi:**
  Membangun dan menyiapakan lingkungan kerja dasar praktikum Administrasi Sistem Linux menggunakan mesin virtual Ubuntu Server 24.04 LTS di VirtualBox. Kebutuhan utamanya adalah memastikan VM dapat diakses secara remote dari host (laptop) via SSH, mengonfigurasi skema penyimpanan LVM dengan ruang bebas (VFree 7-8 GB), serta menghubungkan autentikasi Git/GitHub dari dalam VM menggunakan SSH Key.

- **Keputusan Teknis yang Diambil:**
  - **Jaringan (NAT + Port Forwarding):** Memilih port forwarding (Host 127.0.0.1:2222 -> Guest:22) agar sesi SSH dapat dilakukan langsung dari terminal laptop tanpa perlu GUI VirtualBox, sekaligus menjaga kestabilan koneksi meskipun laptop berpindah-pindah jaringan Wi-Fi.
  - **Skema Partisi LVM:** Mengubah ukuran `ubuntu-lv` menjadi 10 GiB saat instalasi agar menyisakan ruang bebas (*VFree*) sebesar ~7-8 GiB pada `ubuntu-vg` sebagai persiapan alokasi volume pada materi praktikum selanjutnya.
  - **Autentikasi SSH Key ed25519:** Membuat kunci SSH khusus (`ed25519`) untuk GitHub agar proses `git push` aman dan tidak lagi membutuhkan autentikasi password interaktif.
  - **Monitoring Layanan:** Berdasarkan pengecekan `sudo ss -tulpn`, ditemukan layanan OpenSSH yang sedang *listening* pada port 22 untuk menerima koneksi remote.

- **Evaluasi Kritis Generative AI:**
  - *Prompt yang digunakan:* "Jelaskan fungsi dari perintah `sudo ss -tulpn` pada Linux dan bagaimana cara membaca keluarannya."
  - *Hasil evaluasi:* Membantu. AI memberikan penjelasan yang akurat bahwa `ss` digunakan untuk melihat socket jaringan (`-t` untuk TCP, `-u` untuk UDP, `-l` untuk listening, `-p` untuk menampilkan PID/proses, dan `-n` untuk menampilkan nomor port secara numerik). Penjelasan ini sangat relevan dan sesuai dengan keluaran terminal di Ubuntu Server.

