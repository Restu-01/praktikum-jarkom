# LAPORAN PRAKTIKUM JARINGAN KOMPUTER - MODUL 5
## UDP

### Identitas Mahasiswa
**Nama:** Restu Fadilah Al Fatah
**NIM:** 103072400081  
**Kelas:** IF - 04 - 01

---

# BAB 1. PENDAHULUAN

## 1.1 Latar Belakang

User Datagram Protocol (UDP) adalah protokol pada lapisan transport yang mengirimkan data tanpa membangun koneksi terlebih dahulu. Karena memiliki header yang sederhana, UDP mampu mengirimkan data dengan lebih cepat sehingga sering digunakan pada layanan seperti DNS, VoIP, video streaming, dan game online. Pada praktikum ini dilakukan analisis paket UDP menggunakan Wireshark untuk mengamati struktur header serta proses komunikasi request dan response yang terjadi dalam jaringan.


## 1.2 Tujuan Praktikum

1. Memahami struktur header pada protokol UDP.
2. Mengidentifikasi field-field yang terdapat pada header UDP.
3. Menganalisis paket UDP menggunakan Wireshark.
4. Memahami hubungan antara paket request dan response pada komunikasi UDP.

---

# BAB 2. DASAR TEORI

## 2.1 User Datagram Protocol (UDP)

UDP (User Datagram Protocol) merupakan protokol transport yang bersifat connectionless. Berbeda dengan TCP, UDP tidak melakukan proses pembentukan koneksi sebelum mengirimkan data sehingga memiliki overhead yang lebih kecil.

Karakteristik UDP:

- Connectionless.
- Tidak menjamin pengiriman data.
- Tidak melakukan retransmisi paket yang hilang.
- Header berukuran kecil (8 byte).
- Cocok digunakan untuk aplikasi real-time.

## 2.2 Struktur Header UDP

Header UDP terdiri dari empat field utama:

| Field | Ukuran |
|---|---|
| Source Port | 2 Byte |
| Destination Port | 2 Byte |
| Length | 2 Byte |
| Checksum | 2 Byte |

Total ukuran header UDP adalah 8 byte.

## 2.3 Wireshark

Wireshark merupakan aplikasi network protocol analyzer yang digunakan untuk menangkap dan menganalisis paket data yang melewati jaringan komputer.

---

# BAB 3. METODOLOGI PRAKTIKUM

## 3.1 Perangkat yang Digunakan

- Laptop/Komputer
- Sistem Operasi Windows
- Wireshark
- Koneksi Internet

## 3.2 Langkah Percobaan

1. Membuka aplikasi Wireshark.
2. Memilih interface jaringan yang aktif.
3. Menjalankan proses packet capture.
4. Membuka Command Prompt (CMD).
5. Menjalankan perintah berikut:

\`\`\`bash
nslookup www.google.com
\`\`\`

6. Menghentikan proses capture.
7. Memasukkan filter:

\`\`\`
udp
\`\`\`

8. Memilih salah satu paket UDP yang muncul.
9. Mengamati detail header UDP.

---

# BAB 4. HASIL DAN PEMBAHASAN

## 4.1 Hasil Capture Paket UDP

Setelah proses packet capture dilakukan, Wireshark berhasil menangkap paket UDP yang berasal dari proses DNS Query menuju domain \`www.google.com\`. Filter \`udp\` digunakan untuk menampilkan seluruh paket UDP yang tertangkap selama proses capture berlangsung.

### Gambar 4.1 Hasil Capture Paket UDP

![Hasil Capture UDP](../week5/assets/week5.png)

---

## 4.2 Analisis Header UDP

Berdasarkan hasil pengamatan pada Wireshark, diperoleh informasi sebagai berikut:

| Field | Nilai |
|---|---|
| Source Port | 65518 |
| Destination Port | 53 |
| Length | 40 |
| Checksum | 0x352b |
| UDP Payload | 32 Byte |

## 4.3 Jawaban Pertanyaan Praktikum

### 1. Berapa banyak field yang terdapat pada header UDP? Sebutkan nama-namanya.

Berdasarkan hasil pengamatan, terdapat 4 field pada header UDP, yaitu:

1. Source Port
2. Destination Port
3. Length
4. Checksum

---

### 2. Berapa panjang masing-masing field yang terdapat pada header UDP?

| Field | Panjang |
|---|---|
| Source Port | 2 Byte |
| Destination Port | 2 Byte |
| Length | 2 Byte |
| Checksum | 2 Byte |

Total ukuran header UDP adalah:

\`\`\`
2 + 2 + 2 + 2 = 8 Byte
\`\`\`

---

### 3. Nilai yang tertera pada field Length menyatakan nilai apa?

Field Length menunjukkan total ukuran segmen UDP yang terdiri dari header UDP dan payload UDP.

Berdasarkan hasil capture:

\`\`\`
Length = 40 Byte
\`\`\`

Karena ukuran header UDP adalah 8 byte, maka:

\`\`\`
Payload = Length - Header UDP
Payload = 40 - 8
Payload = 32 Byte
\`\`\`

Hasil tersebut sesuai dengan informasi yang ditampilkan oleh Wireshark yaitu UDP payload sebesar 32 byte.

---

### 4. Berapa jumlah maksimum byte yang dapat disertakan dalam payload UDP?

Field Length memiliki ukuran 16 bit sehingga nilai maksimum yang dapat direpresentasikan adalah:

\`\`\`
65535 Byte
\`\`\`

Karena header UDP berukuran 8 byte, maka:

\`\`\`
65535 - 8 = 65527 Byte
\`\`\`

Jadi jumlah maksimum payload UDP adalah **65527 byte**.

---

### 5. Berapa nomor port terbesar yang dapat menjadi port sumber?

Field Source Port memiliki ukuran 16 bit sehingga nilai maksimum yang dapat direpresentasikan adalah:

\`\`\`
65535
\`\`\`

Jadi nomor port terbesar yang dapat digunakan sebagai Source Port adalah **65535**.

---

### 6. Berapa nomor protokol UDP?

Pada header IP terlihat informasi:

\`\`\`
Next Header: UDP (17)
\`\`\`

Sehingga:

| Format | Nilai |
|---|---|
| Desimal | 17 |
| Heksadesimal | 0x11 |

---

### 7. Jelaskan hubungan antara nomor port pada kedua paket tersebut!

Pada komunikasi DNS menggunakan UDP, paket request dikirim dari client menuju server DNS menggunakan Source Port acak dan Destination Port 53. Ketika server mengirimkan balasan, nomor port tersebut akan bertukar posisi.

Contoh:

**Paket Request**

\`\`\`
Source Port      = 65518
Destination Port = 53
\`\`\`

**Paket Response**

\`\`\`
Source Port      = 53
Destination Port = 65518
\`\`\`

Dengan demikian, Source Port pada request akan menjadi Destination Port pada response, sedangkan Destination Port pada request akan menjadi Source Port pada response.

---

# BAB 5. KESIMPULAN

Berdasarkan praktikum yang telah dilakukan, dapat disimpulkan bahwa UDP merupakan protokol transport yang bersifat connectionless dan memiliki ukuran header yang kecil yaitu 8 byte. Header UDP terdiri dari empat field utama yaitu Source Port, Destination Port, Length, dan Checksum. Pada hasil capture Wireshark diperoleh paket DNS Query menuju domain \`www.google.com\` dengan Source Port 65518, Destination Port 53, Length 40 byte, dan payload sebesar 32 byte. Analisis ini menunjukkan bagaimana UDP digunakan dalam proses komunikasi DNS pada jaringan komputer.

---

# DAFTAR PUSTAKA

1. Kurose, J. F., & Ross, K. W. *Computer Networking: A Top-Down Approach*.
2. RFC 768 - User Datagram Protocol (UDP).
3. Wireshark Foundation. *Wireshark User Guide*.