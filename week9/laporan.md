# Laporan Praktikum Jaringan Komputer - Modul 9
## Web Server Programming dengan Python Socket

### Identitas Praktikan
**Nama    :** [RESTU FADILAH AL FATAH]
**NIM     :** [103072400081 ]
**Kelas   :** [IF-04-01 ]

---

## 9.1 Tujuan Praktikum
Mahasiswa bisa membuat program web server sederhana berbasis TCP socket 
programming
---

## 9.2 Dasar Teori

Web server adalah aplikasi perangkat lunak yang menangani permintaan HTTP dari klien (biasanya browser web). Dalam modul ini, kita membangun server web sederhana menggunakan Python yang berjalan di atas protokol TCP.

Proses kerja server web sederhana ini adalah:
1. Membuat soket TCP (SOCK_STREAM).
2. Mengikat (bind) soket ke alamat IP dan nomor port tertentu.
3. Mendengarkan (listen) koneksi masuk dari klien.
4. Menerima koneksi (accept) dan membuat soket koneksi baru untuk klien tersebut.
5. Menerima pesan HTTP dari klien.
6. Mengurai (parse) pesan untuk mendapatkan nama file yang diminta.
7. Membaca file dari sistem file lokal.
8. Membuat respons HTTP yang terdiri dari header status (misalnya 200 OK atau 404 Not Found) diikuti oleh isi file.
9. Mengirim respons kembali ke klien melalui soket koneksi.
10. Menutup soket koneksi.

Jika file tidak ditemukan, server harus mengirimkan pesan error HTTP "404 Not Found".

---

## 9.3 Langkah Kerja

**1. Siapkan File HTML**  

**File:** `HelloWorld.html`

```html
<!DOCTYPE html>
<html>
<head>
    <title>Hello World</title>
</head>
<body>
    <h1>Hello World</h1>
    <p>Web server Python berhasil.</p>
</body>
</html>
```

**2. Implementasi Kode Server**
Lengkapi kode skeleton (server.py) yang disediakan dalam modul. Berikut adalah kode lengkap setelah diisi :

```python
#import socket module
from socket import *

import sys # In order to terminate the program

serverSocket = socket(AF_INET, SOCK_STREAM)

#Prepare a sever socket
#Fill in start
serverPort = 6789
serverSocket.bind(('', serverPort))
serverSocket.listen(1)
#Fill in end

while True:
    print('Ready to serve...')
    connectionSocket, addr = serverSocket.accept()

    try:
        message = connectionSocket.recv(1024).decode()
        filename = message.split()[1]

        f = open(filename[1:])
        outputdata = f.read()

        connectionSocket.send("HTTP/1.1 200 OK\r\n\r\n".encode())

        for i in range(0, len(outputdata)):
            connectionSocket.send(outputdata[i].encode())

        connectionSocket.send("\r\n".encode())
        connectionSocket.close()

    except IOError:
        #Send response message for file not found
        connectionSocket.send("HTTP/1.1 404 Not Found\r\n\r\n".encode())
        connectionSocket.send(
            "<html><body><h1>404 Not Found</h1></body></html>".encode()
        )

        #Close client socket
        connectionSocket.close()

serverSocket.close()
sys.exit() #Terminate the program after sending the corresponding data
```
---

## 9.4 Hasil Praktikum

### 9.4.1 Screenshot HTML
[Tampilan HTML](../week9/assets/HTML.png)

### 9.4.1 Screenshot HTML Not Found
[Not Found](../week9/assets/NotFound.png)


## 9.7 Kesimpulan

Berdasarkan praktikum yang telah dilakukan:

1. Berhasil membuat web server sederhana menggunakan Python Socket Programming yang mampu melayani permintaan HTTP dasar.
2. Memahami perbedaan penanganan koneksi TCP pada server (bind, listen, accept) dibandingkan dengan klien.
3. Memahami struktur pesan HTTP Request dan Response, termasuk pentingnya header status code (200 OK dan 404 Not Found).
4. Server dapat membedakan antara file yang ada dan tidak ada, serta memberikan respons yang sesuai kepada klien (browser).

---