# Pertemuan 2: TCP/IP Vulnerabilities
| Nama                            | NRP        |
| ------------------------------- | ---------- |
| Fadlillah Cantika Sari Hermawan | 5027231042 |

## Objectives
1. Menjelaskan struktur header IPv4 dan IPv6
2. Menjelaskan bagaimana kerentanan IP dapat dimanfaatkan untuk serangan jaringan
3. Menjelaskan bagaimana kerentanan TCP dan UDP dapat dimanfaatkan untuk serangan jaringan

## Struktur Header IPv4
Header pada protokol IPv4 terdiri atas sejumlah field penting yang menyimpan informasi kendali dan alamat. Setiap field memiliki peran khusus dalam memastikan paket dapat dikirimkan dengan benar.
1. Version
Menunjukkan versi protokol. Untuk IPv4 nilainya adalah 4 (0100 dalam biner).
2. Internet Header Length (IHL)
Menyatakan panjang header dalam satuan 32-bit word. Nilai minimum adalah 20 byte, tetapi bisa lebih panjang jika terdapat field Options.
3. Differentiated Services (DS) / DiffServ
- Field 8-bit untuk mekanisme Quality of Service (QoS).
- 6 bit pertama disebut DSCP (Differentiated Services Code Point).
- 2 bit terakhir disebut ECN (Explicit Congestion Notification).
4. Total Length
Menunjukkan ukuran total paket (header + data). Ukuran maksimal adalah 65.535 byte.
5. Identification, Flags, dan Fragment Offset
Digunakan ketika paket perlu dipecah (fragmentasi) karena jalur jaringan tidak mendukung ukuran besar.
- Identification membantu mengelompokkan fragmen.
- Flags memberi tanda apakah paket masih bisa difragmentasi.
- Fragment Offset menunjukkan posisi fragmen dalam paket asli.
6. Time To Live (TTL)
Field 8-bit untuk membatasi umur paket. Nilainya dikurangi satu setiap kali melewati router. Jika bernilai nol, paket dibuang, dan sumber akan menerima pesan ICMP Time Exceeded.
7. Protocol
Field 8-bit yang menunjukkan protokol lapisan di atasnya, misalnya TCP, UDP, atau ICMP.
8.Header Checksum
Digunakan untuk mendeteksi error pada header. Jika terjadi kesalahan, paket akan dibuang.
9. Source Address
Alamat IPv4 sumber berukuran 32-bit.
10. Destination Address
Alamat IPv4 tujuan berukuran 32-bit.
11. Options dan Padding
Field opsional untuk kebutuhan khusus. Padding digunakan agar ukuran header selalu kelipatan 32 bit.
