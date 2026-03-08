# LAPORAN PRAKTIKUM JARINGAN KOMPUTER - MODUL 2
## Pengenalan Tools

---

### Identitas Praktikan
| Item | Keterangan |
|------|------------|
| **Nama** | Restu Fadilah Al Fatah |
| **NIM** | 103072400081 |
| **Kelas** | IF-04-01 |

---

## 1. Capaian Pembelajaran

Berdasarkan modul praktikum Jaringan Komputer Semester Genap 2025/2026, setelah mengikuti praktikum ini mahasiswa diharapkan dapat:

1. Melakukan proses instalasi serta konfigurasi awal pada aplikasi Wireshark.
2. Menggunakan Wireshark untuk melakukan proses penangkapan (capture) paket data yang melewati jaringan.
3. Mengidentifikasi dan menganalisis struktur paket data berdasarkan lapisan protokol yang digunakan dalam jaringan.
---

## 2. Landasan Teori

### 2.1 Packet Sniffer

Wireshark merupakan salah satu aplikasi yang menerapkan konsep **Packet Sniffer**, yaitu perangkat lunak yang digunakan untuk memantau dan merekam proses pertukaran pesan antar entitas protokol dalam jaringan komputer..

| Komponen | Deskripsi |
|----------|-----------|
| **Sifat Kerja** | Bersifat pasif, yaitu hanya melakukan pengamatan terhadap lalu lintas jaringan tanpa mengirim ataupun mengubah paket |
| **Fungsi Utama** | Menangkap (sniffing) paket data yang dikirim maupun diterima oleh komputer dalam jaringan |

### 2.2 Struktur Packet Sniffer

| No | Komponen | Fungsi |
|----|----------|--------|
| 1 | Command Menu | Menyediakan berbagai menu utama seperti File, Capture, Analyze, Help, dan menu lainnya. |
| 2 | Packet Listing Window | Menampilkan daftar paket yang berhasil ditangkap dalam bentuk ringkasan satu baris untuk setiap paket |
| 3 | Packet Header Details Window |Menyajikan informasi detail mengenai struktur protokol dari paket yang dipilih |
| 4 | Packet Contents Window | Menampilkan isi frame paket dalam format heksadesimal dan ASCII |
| 5 | Display Filter Field | Kolom yang digunakan untuk menyaring paket berdasarkan protokol atau parameter tertentu |

---

## 3. LANGKAH KERJA

### 3.1 Tahapan Praktikum

| Tahap | Aktivitas | Keterangan |
|-------|-----------|------------|
| **Persiapan** | Pastikan koneksi internet aktif, buka browser, jalankan Wireshark | Verifikasi interface jaringan terdeteksi |
| **Start Capture** | Capture > Interfaces > Pilih interface aktif > Start | Pilih Wi-Fi atau Ethernet yang sedang digunakan |
| **Generasi Traffic** | Akses URL: `http://gaia.cs.umass.edu/wireshark-labs/INTRO-wireshark-file1.html` | Tunggu hingga halaman web selesai dimuat |
| **Stop Capture** | Klik tombol Stop (kotak merah) pada toolbar Wireshark | Proses capture selesai, paket tersimpan di memori |
| **Filter Paket** | Ketik `http` pada Display Filter Field, tekan Enter | Hanya paket HTTP yang ditampilkan |
| **Analisis Paket** | Pilih paket HTTP GET, ekspansi detail HTTP, minimalkan protokol lain | Fokus pada field metode, host, user-agent |
| **Selesai** | Tutup aplikasi Wireshark | Praktikum selesai |

### 3.2 URL Target Praktikum

| Parameter | Nilai |
|-----------|-------|
| **URL** | `http://gaia.cs.umass.edu/wireshark-labs/INTRO-wireshark-file1.html` |
| **Protokol** | HTTP (Port 80) |
| **Server** | gaia.cs.umass.edu |
| **Jenis Request** | GET |

---

## 4. HASIL DAN PEMBAHASAN

### 4.1 Dokumentasi Tampilan Wireshark

| No | Deskripsi | Gambar |
|----|-----------|--------|
| 1 | Tampilan awal Wireshark (Welcome Screen) | ![Tampilan Awal](../week2/assets/images/Tampilan%20awal.png) |
| 2 | Jendela pemilihan interface capture | ![Pilih Interface](../week2/assets/images/Menu%20pilihan%20awal.png) |
| 3 | Daftar paket hasil capture (Packet List) | ![Packet List](../week2/assets/images/Daftar%20paket%20hasil%20capture%20(Packet%20List).png) |
| 4 | Hasil filter paket dengan ekspresi `http` | ![Filter HTTP](../week2/assets/images/Hasil%20filter%20paket%20dengan%20ekspresi%20http.png) |
| 5 | Detail paket HTTP GET (Packet Details) | ![HTTP Detail](../week2/assets/images/Detail%20paket%20HTTP%20GET%20(Packet%20Details).png) |
| 6 | Konten paket dalam format Hex & ASCII | ![Packet Bytes](../week2/assets/images/Konten%20paket%20dalam%20format%20Hex%20&%20ASCII.png) |

---

## 5. KESIMPULAN

| No | Poin Kesimpulan | Penjelasan |1
|----|----------------|------------|
| 1 | Instalasi Wireshark | Wireshark berhasil diinstal dan berjalan stabil pada sistem operasi yang digunakan |
| 2 | Fungsi Packet Sniffer | Wireshark mampu menangkap paket secara pasif tanpa mengganggu lalu lintas jaringan |
| 3 | Antarmuka Pengguna | Lima komponen utama Wireshark terintegrasi dengan baik untuk memudahkan analisis berlapis |
| 4 | Display Filter | Fitur filter sangat efektif untuk mengisolasi paket spesifik dari ribuan paket yang tertangkap |

---