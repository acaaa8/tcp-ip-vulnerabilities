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

## Struktur Header IPv6
IPv6 didesain lebih sederhana dan efisien dibanding IPv4. Banyak field yang dianggap tidak penting dihapus untuk mempercepat pemrosesan paket oleh router. Field-field utama dalam IPv6 antara lain:
1. Version
Nilai biner 0110 untuk menunjukkan bahwa paket adalah IPv6.
2. Traffic Class
Field 8-bit, setara dengan Differentiated Services pada IPv4, digunakan untuk QoS dan prioritas paket.
3. Flow Label
Field 20-bit untuk mengidentifikasi aliran paket yang sama. Semua paket dengan label ini akan diperlakukan sama oleh router, berguna untuk aplikasi real-time seperti VoIP atau streaming.
4. Payload Length
Field 16-bit yang menyatakan panjang data (payload) dalam paket IPv6.
5. Next Header
Setara dengan field Protocol pada IPv4. Digunakan untuk menunjukkan protokol lapisan transport berikutnya (TCP, UDP, ICMPv6, dll).
6. Hop Limit
Menggantikan TTL pada IPv4. Nilainya berkurang setiap kali melewati router, dan jika nol maka paket dibuang.
7. Source Address
Alamat IPv6 sumber berukuran 128-bit.
8. Destination Address
Alamat IPv6 tujuan berukuran 128-bit.

## Perbedaan Utama IPv4 dan IPv6
Perbedaan paling menonjol antara keduanya adalah ukuran dan kompleksitas header. IPv4 memiliki banyak field tambahan seperti fragmentasi, checksum, dan opsi, yang meskipun fleksibel tetapi membuat pemrosesan lebih lambat. Pada IPv6, field yang jarang dipakai dihapus atau dipindahkan ke extension header. Dengan demikian, header IPv6 menjadi lebih sederhana dan router dapat memproses paket dengan lebih cepat dan efisien. Selain itu, panjang alamat meningkat dari 32 bit pada IPv4 menjadi 128 bit pada IPv6, sehingga mendukung jumlah perangkat yang jauh lebih besar.

## Kerentanan IP
- ICMP Attacks: Digunakan untuk reconnaissance (mengumpulkan informasi jaringan), scanning untuk mendeteksi host aktif, Denial of Service (DoS/DDoS) untuk membanjiri target, redirect untuk mengubah jalur trafik, serta router discovery untuk menemukan jalur jaringan.
- Amplification & Reflection: Contohnya Smurf Attack, di mana penyerang memanfaatkan broadcast ICMP untuk membanjiri target dengan lalu lintas yang diperbesar.
- IP Spoofing: Teknik menyembunyikan identitas dengan memalsukan alamat IP, sehingga bisa menyamar sebagai pengguna sah dan menghindari deteksi.
- MAC Spoofing: Menyamar di jaringan lokal dengan memalsukan alamat MAC, memungkinkan akses ke jaringan internal atau melewati kontrol keamanan berbasis MAC.
- Man-in-the-Middle & Session Hijacking: Penyerang menyusup ke komunikasi sah antara dua pihak untuk memantau, mencuri, atau memodifikasi data, termasuk mengambil alih sesi pengguna.

## Kerentanan TCP dan UDP
A. TCP (Transmission Control Protocol)

Header segmen mencakup: Source/Destination Port, Sequence Number, Acknowledgment Number, Window Size, dan Checksum.
Kerentanannya antara lain:
- SYN Flood: Menyebabkan server kehabisan sumber daya dengan membuka banyak koneksi palsu.
- TCP Reset Attack: Memaksa koneksi TCP sah untuk terputus.
- Session Hijacking: Mengambil alih sesi TCP yang sah dengan memanfaatkan nomor urut paket.

  
B. UDP (User Datagram Protocol)

Header datagram mencakup: Source/Destination Port, Length, dan Checksum.
Karakteristik: connectionless, overhead rendah, tidak menyediakan reliabilitas bawaan, sehingga lebih cepat tapi rentan.
Kerentanannya antara lain:
- UDP Flood Attack: Membanjiri target dengan datagram UDP palsu.
- Data mudah disadap atau diubah karena UDP tidak memiliki mekanisme validasi dan konfirmasi pengiriman bawaan.
