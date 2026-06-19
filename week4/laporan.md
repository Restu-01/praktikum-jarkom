# Laporan Praktikum Jaringan Komputer - Modul 4
## Domain Name System (DNS)

> **Semester Genap 2025/2026 | Fakultas Informatika | Universitas Telkom**

---

### Identitas Praktikan

| Keterangan | Informasi |
|------------|-----------|
| **Nama Lengkap** | Restu Fadilah Al Fatah |
| **NIM** | 103072400081 |
| **Kelas** | IF-04-01 |

---

## 1. Capaian Pembelajaran

| No | Tujuan | Penjelasan Sederhana |
|----|--------|---------------------|
| 1 | Memahami konsep DNS | Mengerti bagaimana nama website diubah jadi angka IP |
| 2 | Menggunakan nslookup | Bisa pakai perintah `nslookup` untuk cek DNS |
| 3 | Mengenal jenis record DNS | Tahu bedanya A, NS, MX, CNAME, dan fungsinya |
| 4 | Memahami hierarki DNS | Mengerti alur dari DNS lokal → root → TLD → server asli |
| 5 | Mengelola cache DNS | Bisa lihat dan hapus cache DNS pakai `ipconfig` |

---

## 2. Dasar Teori (Versi Simpel)

### 2.1 Apa Itu DNS?

Domain Name System (DNS) merupakan singkatan dari Domain Name System, yaitu sistem yang berfungsi untuk menerjemahkan nama domain menjadi alamat IP yang dapat dikenali oleh perangkat komputer. Sebagai contoh, ketika pengguna mengetikkan google.com pada browser, DNS akan mengubah nama tersebut menjadi alamat IP seperti 142.250.185.46 agar perangkat dapat terhubung ke server tujuan. DNS dapat dianalogikan sebagai buku telepon yang membantu mencocokkan nama dengan nomor yang sesuai. Tanpa adanya DNS, pengguna harus mengingat dan memasukkan alamat IP setiap situs web secara langsung, sehingga proses akses internet menjadi lebih sulit dan tidak praktis.

### 2.3 Jenis-Jenis Record DNS

|Jenis-jenis record DNS memiliki fungsi yang berbeda sesuai dengan kebutuhan pengelolaan dan proses pencarian informasi domain. Berikut penjelasannya:

**A Record (Address Record)**
Digunakan untuk menghubungkan nama domain dengan alamat IPv4. Record ini merupakan jenis record yang paling umum digunakan dalam proses akses website.

**AAAA Record**
Berfungsi untuk memetakan nama domain ke alamat IPv6. Fungsinya sama seperti A Record, tetapi menggunakan format alamat IP generasi terbaru.

**NS Record (Name Server Record)**
Menunjukkan server DNS yang berwenang atau bertanggung jawab dalam mengelola informasi suatu domain. Record ini membantu proses pencarian informasi domain pada sistem DNS.

**MX Record (Mail Exchange Record)**
Digunakan untuk menentukan server email yang menerima dan mengelola pesan elektronik untuk suatu domain. Record ini sangat penting dalam layanan surat elektronik (email).

**CNAME Record (Canonical Name Record)**
Berfungsi sebagai alias yang mengarahkan suatu nama domain ke domain lain. Dengan record ini, beberapa nama domain dapat mengarah ke tujuan yang sama tanpa perlu menggunakan alamat IP secara langsung.

**PTR Record (Pointer Record)**
Digunakan untuk melakukan reverse DNS lookup, yaitu menerjemahkan alamat IP kembali menjadi nama domain. Record ini sering dimanfaatkan untuk keperluan verifikasi dan keamanan jaringan.

---

## 3. Langkah Kerja 

### 3.1 Ringkasan Semua Percobaan

Praktikum ini terdiri dari beberapa percobaan yang bertujuan untuk memahami cara kerja DNS serta menganalisis proses resolusi nama domain menjadi alamat IP. Setiap percobaan dilakukan menggunakan perintah nslookup, ipconfig, dan aplikasi Wireshark untuk mengamati berbagai informasi yang berkaitan dengan DNS. Adapun rincian percobaan yang dilakukan adalah sebagai berikut:

**Percobaan 1 – Query A Record**
Menggunakan perintah nslookup www.mit.edu untuk mengetahui alamat IP yang terkait dengan domain tersebut melalui pencarian A Record.

**Percobaan 2 – Query NS Record**
Menggunakan perintah nslookup -type=NS www.mit.edu untuk melihat server DNS otoritatif yang bertanggung jawab terhadap domain tersebut.

**Percobaan 3 – Query ke DNS Server Tertentu**
Menggunakan perintah nslookup www.aiit.or.kr 8.8.8.8 untuk melakukan resolusi domain menggunakan Google Public DNS dan membandingkan hasilnya dengan DNS lokal.

**Percobaan 4 – Query Domain di Asia**
Menggunakan perintah nslookup www.nus.edu.sg untuk mengetahui alamat IP dari server web National University of Singapore dan mengamati hasil resolusi DNS pada domain yang berada di wilayah Asia.

**Percobaan 5 – Query NS Domain Eropa**
Menggunakan perintah nslookup -type=NS www.ox.ac.uk untuk mengidentifikasi name server yang mengelola domain University of Oxford.

**Percobaan 6 – Query MX Record**
Menggunakan perintah nslookup -type=MX yahoo.com 8.8.8.8 untuk mengetahui server email yang digunakan oleh domain Yahoo beserta prioritasnya.

**Percobaan 7 – Pemeriksaan Konfigurasi Jaringan**
Menggunakan perintah ipconfig /all untuk melihat informasi konfigurasi jaringan seperti alamat IP, DNS server, subnet mask, gateway, dan informasi adapter jaringan.

**Percobaan 8 – Melihat Cache DNS**
Menggunakan perintah ipconfig /displaydns untuk menampilkan daftar cache DNS yang tersimpan pada komputer, termasuk domain yang pernah diakses sebelumnya.

**Percobaan 9 – Analisis DNS Menggunakan Wireshark Tanpa nslookup**
Melakukan akses ke situs www.ietf.org sambil melakukan packet capture menggunakan Wireshark untuk mengamati proses DNS Query dan DNS Response yang terjadi secara otomatis.

**Percobaan 10 – Analisis nslookup Menggunakan Wireshark
Menjalankan perintah nslookup www.mit.edu sambil merekam lalu lintas jaringan menggunakan Wireshark untuk melihat detail paket DNS yang dikirim dan diterima selama proses resolusi domain.

---

## 📸 4. Hasil dan Pembahasan

### 4.1 Query A Record (Domain → IP)

> **Gambar 1**: Hasil `nslookup www.mit.edu`  
> ![Query A](../week4/assets/dns_a_record.png)

| Informasi | Nilai |
|-----------|-------|
| Domain yang dicek | `www.mit.edu` |
| Hasil IP | `23.15.150.186` |
| DNS Server yang dipakai | DNS lokal (dari `ipconfig`) |
| Status jawaban | Non-authoritative (dari cache) |


---

### 4.2 Query NS Record (Siapa Server Resminya?)

> **Gambar 2**: Hasil `nslookup -type=NS www.mit.edu`  
> ![Query NS](../week4/assets/dns_ns_record.png)

| Informasi | Nilai |
|-----------|-------|
| Domain | `www.mit.edu` |
| Jenis Query | NS (Name Server) |
| Hasil | Daftar server DNS resmi MIT |
| Contoh | `dscb.akamaiedge.net` |

---

### 4.3 Query ke DNS Server Tertentu

> **Gambar 3**: Hasil `nslookup www.aiit.or.kr 8.8.8.8`  
> ![Query DNS](../week4/assets/dns_compare.png)

| Parameter | Nilai |
|-----------|-------|
| Domain | `www.aiit.or.kr` |
| DNS Server yang dipakai | `8.8.8.8` (Google Public DNS) |
| Hasil IP | `172.67.152.120`, `104.21.74.8` |

---

### 4.4 Query Alamat IP Server Web di Asia

> **Gambar 4**: Hasil `nslookup www.nus.edu.sg`  
> ![Query DNS](../week4/assets/dns_nus.png)

| Domain | Lokasi | Hasil IP | Keterangan |
|--------|--------|----------|------------|
| `www.nus.edu.sg` | Singapura 🇸🇬 | `45.60.35.225` | National University of Singapore |

**Analisis:**

* Perintah `nslookup www.nus.edu.sg` digunakan untuk mengetahui alamat IP dari domain tersebut.
* Domain **[www.nus.edu.sg](http://www.nus.edu.sg)** merupakan server web milik National University of Singapore (NUS) di Asia.
* Hasil query menampilkan satu atau lebih alamat IP yang terasosiasi dengan domain tersebut.
* Alamat IP inilah yang digunakan oleh client untuk mengakses server web tujuan.
* Query ini menunjukkan proses dasar resolusi DNS dari nama domain menjadi alamat IP.

---

### 4.5 Query DNS Otoritatif (NS Record)

> **Gambar 5**: Hasil `nslookup -type=NS www.ox.ac.uk`  
> ![Query DNS](../week4/assets/dns_ns.png)

**Analisis:**

* Perintah `nslookup -type=NS www.ox.ac.uk` digunakan untuk mengetahui server DNS otoritatif dari domain tersebut.
* Hasil query menampilkan daftar **Name Server (NS)** yang bertanggung jawab atas domain **[www.ox.ac.uk](http://www.ox.ac.uk)**.
* Server DNS otoritatif adalah server yang memiliki informasi resmi terkait domain tersebut.
* Informasi ini penting untuk memahami bagaimana DNS mendistribusikan tanggung jawab pengelolaan domain.
* Domain tersebut merupakan milik University of Oxford di Eropa.

---

### 4.6 Query MX Record (Server Email)

> **Gambar 6**: Hasil `nslookup -type=MX yahoo.com 8.8.8.8`  
> ![Query MX](../week4/assets/dns_mx_yahoo.png)

| Mail Server | Fungsi |
|-------------|--------|
| `mta7.am0.yahoodns.net` | Prioritas tertinggi |
| `mta6.am0.yahoodns.net` | Cadangan |
| `mta5.am0.yahoodns.net` | Cadangan lagi |

**Penjelasan Priority:**
- Angka kecil = prioritas lebih tinggi
- Email dikirim ke server priority 1 dulu
- Kalau gagal, coba priority 5, lalu 10, dst.

---

### 4.7 Perintah ipconfig (Cek & Kelola Jaringan)

#### 4.7.1 `ipconfig /all` — Lihat Semua Info Jaringan

> **Gambar 7**: Hasil `ipconfig /all`  
> ![Ipconfig All](../week4/assets/ipconfig_all.png)

| Informasi | Contoh Nilai | Kegunaan |
|-----------|-------------|----------|
| IPv4 Address | `192.168.1.100` | Alamat laptop di jaringan lokal |
| Subnet Mask | `255.255.255.0` | Menentukan rentang jaringan |
| Default Gateway | `192.168.1.1` | Alamat router / modem |
| DNS Servers | `192.168.1.1`, `8.8.8.8` | Server yang dipakai untuk resolusi DNS |
| Physical Address | `AA:BB:CC:DD:EE:FF` | MAC Address adapter jaringan |

#### 4.7.2 `ipconfig /displaydns` — Lihat Cache DNS

> **Gambar 8**: Hasil `ipconfig /displaydns`  
> ![Display DNS](../week4/assets/ipconfig_displaydns.png)

| Field | Arti |
|-------|------|
| Record Name | Nama domain yang di-cache |
| Record Type | Jenis record (A, AAAA, CNAME, dll) |
| Time To Live | Berapa detik lagi cache ini kadaluarsa |
| Data Length | Ukuran data record |
| Section | Bagian pesan DNS (Answer, Authority, Additional) |

---

### 4.8 Analisis DNS via Wireshark (Tanpa nslookup)

> **Gambar 10-11**: Capture DNS saat akses `www.ietf.org`  
> ![Wireshark DNS](../week5/assets/wireshark_dns.png)
> ![Wireshark DNS Response](../week4/assets/wireshark_dns_response.png)

#### 4.8.1 Pertanyaan & Jawaban Analisis

| No | Pertanyaan | Jawaban |
|----|-----------|---------|
| 1 | Pakai UDP atau TCP? | **UDP** (lebih cepat untuk query kecil) |
| 2 | Port sumber & tujuan? | Sumber: ephemeral (misal 56839), Tujuan: **53** (DNS) |
| 3 | IP tujuan query = DNS lokal? | ✅ Ya, sama dengan yang muncul di `ipconfig` |
| 4 | Jenis query? | **A** (IPv4) dan **AAAA** (IPv6) |
| 5 | Apakah query punya jawaban? | ❌ Tidak, query hanya pertanyaan |
| 6 | Isi jawaban response? | IPv4: `104.16.45.99`, `104.16.44.99` + IPv6 addresses |
| 7 | IP di response cocok dengan TCP SYN? | ✅ Ya, browser langsung konek ke IP tersebut |
| 8 | Perlu query DNS tiap gambar? | ❌ Tidak, karena ada cache DNS (TTL) |

### 4.9 Analisis DNS via Wireshark + nslookup

> **Gambar 12-13**: Capture `nslookup www.mit.edu`  
> ![Wireshark DNS nslookup](../week4/assets/wireshark_dns_nslookup.png)
> ![Wireshark DNS Response nslookup](../week4/assets/wireshark_dns_response_nslookup.png)

#### 4.9.1 Port Tujuan dan Sumber

| Jenis Paket  | Port Sumber | Port Tujuan |
| ------------ | ----------- | ----------- |
| DNS Query    | 56839       | 53          |
| DNS Response | 53          | 56839       |

* Port **53** digunakan oleh DNS server
* Port **56839** adalah *ephemeral port* dari client

---

#### 4.9.2 Alamat IP tujuan DNS

* IP tujuan DNS Query: **10.159.118.217**
* IP tersebut merupakan **DNS server lokal** (jika sesuai dengan hasil `ipconfig`)

---

#### 4.9.3 Jenis Query dan Kandungan Jawaban

* Tipe query: **A (IPv4 Address)**
* Jumlah pertanyaan: 1
* **Tidak terdapat jawaban pada query (Answer RRs = 0)**

Hal ini karena query hanya berisi permintaan, sedangkan jawaban terdapat pada response.

---

#### 4.9.4 Isi Jawaban DNS Response

| No | Type | Name | Data / IP | TTL |
|----|------|------|-----------|-----|
| 1 | CNAME | `www.mit.edu` | `www.mit.edu.edgekey.net` | 1495s |
| 2 | CNAME | `www.mit.edu.edgekey.net` | `e9566.dscb.akamaiedge.net` | 295s |
| 3 | A | `e9566.dscb.akamaiedge.net` | `23.217.163.122` | 20s |

---

### 4.10 Tracing DNS dengan Wireshark - Query ke DNS Server Spesifik

> **Gambar 14-15**: Capture DNS saat akses `www.aiit.or.kr`    
> ![Wireshark DNS ](../week4/assets/dns_req.png)
> ![Wireshark DNS Response](../week4/assets/dns_res.png)

#### 4.10.1 Alamat IP Tujuam DNS Query

* IP tujuan: **8.8.8.8**
* DNS lokal (berdasarkan konfigurasi): **10.159.118.217**

Query dikirim ke **Google Public DNS (8.8.8.8)**, bukan DNS lokal.

* Kemungkinan terjadi resolusi awal untuk server **bitsy.mit.edu**
* Atau sistem menggunakan DNS publik sebagai resolver utama

---

#### 4.10.2 Jenis Query DNS

* Tipe: **A (IPv4 Address)**
* Jumlah pertanyaan: 1
* **Tidak mengandung jawaban (Answer RRs = 0)**

Query hanya berisi permintaan, sedangkan jawaban terdapat pada response.

---

#### 4.10.3 Isi Jawaban DNS Response

Jumlah jawaban: **2 record (A)**

| No | Domain                                  | IP Address         | TTL       |
| -- | --------------------------------------- | ------------------ | --------- |
| 1  | [www.aiit.or.kr](http://www.aiit.or.kr) | **172.67.152.120** | 300 detik |
| 2  | [www.aiit.or.kr](http://www.aiit.or.kr) | **104.21.74.8**    | 300 detik |

**Analisis:**

* Domain memiliki **lebih dari satu IP** → load balancing
* IP termasuk dalam jaringan Cloudflare (CDN)
* TTL: 300 detik (5 menit) → cache relatif singkat
* Response bersifat **non-authoritative** (dari cache DNS)
* Response time ±292 ms (lebih lambat dibanding DNS lokal)

---

#### 4.10.4 Karakteristik Tambahan

* Menggunakan protokol **UDP port 53**
* Terdapat query tambahan tipe **AAAA (IPv6)**
* Mendukung **dual-stack network (IPv4 & IPv6)**

---

## 5. Kesimpulan

| No | Poin Kesimpulan | Penjelasan Simpel |
|----|----------------|-------------------|
| 1 | DNS itu penting | Tanpa DNS, kita harus hafal angka IP tiap website |
| 2 | nslookup itu berguna | Tool simpel buat cek "IP dari domain X apa?" |
| 3 | DNS punya banyak jenis record | A untuk IP, NS untuk server resmi, MX untuk email, dll |
| 4 | DNS bekerja bertingkat | Dari cache → DNS lokal → root → TLD → server asli |
| 5 | DNS pakai UDP port 53 | Lebih cepat daripada TCP untuk query kecil |
| 6 | Satu domain bisa punya banyak IP | Untuk load balancing dan backup (redundancy) |
| 7 | CDN bikin DNS lebih kompleks | Domain bisa redirect ke server edge terdekat |
| 8 | Cache DNS menghemat waktu | Hasil query disimpan sementara (TTL) agar tidak tanya ulang |
| 9 | DNS publik vs lokal ada trade-off | Lokal cepat, publik stabil — pilih sesuai kebutuhan |
| 10 | Wireshark bantu "lihat" DNS | Bisa intip paket query/response secara real-time |

---