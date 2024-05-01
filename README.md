# 1

1. **Unary Streaming**
   - **Karakteristik:** Client mengirimkan satu paket data kecil ke server.
   - **Kegunaan:** Metode ini efektif untuk autentikasi, otorisasi, dan pengiriman formulir.

2. **Server Streaming**
   - **Karakteristik:** Server mengirimkan serangkaian data besar kepada client.
   - **Kegunaan:** Cocok untuk distribusi informasi yang membutuhkan pembaruan kontinu seperti harga saham atau berita terkini.

3. **Bidirectional Streaming**
   - **Karakteristik:** Data ditransmisikan dua arah antara client dan server.
   - **Kegunaan:** Ideal untuk aplikasi yang memerlukan kolaborasi intensif seperti editing bersama, permainan real-time, atau layanan chatbot.
# 2
GRPC memerlukan validasi autentikasi dan autorisasi yang berulang untuk setiap segmen data yang dikirim, berbeda dengan REST yang hanya memerlukan satu kali validasi per permintaan. Selain itu, dalam GRPC, setiap segmen data, baik dari server maupun klien, harus dienkripsi secara individual untuk memastikan keamanan. Hal ini berarti bahwa GRPC membutuhkan validasi berulang untuk autentikasi, autorisasi, dan enkripsi dalam satu aliran permintaan data, sedangkan REST hanya memerlukan satu kali validasi karena koneksi diputus setelah mendapatkan respons. Oleh karena itu, dari segi pertimbangan keamanan terkait autentikasi, otorisasi, dan enkripsi, GRPC dianggap lebih unggul karena melakukan enkripsi secara otomatis dan berulang, berbeda dengan REST yang dilakukan secara manual.GRPC memerlukan validasi autentikasi dan autorisasi yang berulang untuk setiap segmen data yang dikirim, berbeda dengan REST yang hanya memerlukan satu kali validasi per permintaan. Selain itu, dalam GRPC, setiap segmen data, baik dari server maupun klien, harus dienkripsi secara individual untuk memastikan keamanan. Hal ini berarti bahwa GRPC membutuhkan validasi berulang untuk autentikasi, autorisasi, dan enkripsi dalam satu aliran permintaan data, sedangkan REST hanya memerlukan satu kali validasi karena koneksi diputus setelah mendapatkan respons. Oleh karena itu, dari segi pertimbangan keamanan terkait autentikasi, otorisasi, dan enkripsi, GRPC dianggap lebih unggul karena melakukan enkripsi secara otomatis dan berulang, berbeda dengan REST yang dilakukan secara manual.

# 3
Dalam pengembangan aplikasi chat yang menggunakan Rust gRPC, berbagai kendala dapat muncul ketika mengimplementasikan streaming dua arah. Isu-isu ini meliputi kurangnya sinkronisasi yang akurat antara pengirim dan penerima, kemungkinan terjadinya deadlock saat kedua ujung saluran menunggu satu sama lain, serta risiko terjadinya overflow buffer jika pesan tidak segera diproses. Selain itu, penting untuk memiliki mekanisme pemulihan kesalahan yang efektif untuk mengatasi koneksi yang tidak stabil dan memastikan bahwa aspek konkurensi dan keamanan seperti enkripsi dan otentikasi pengguna ditangani dengan baik.

# 4
Penggunaan `tokio_stream::wrappers::ReceiverStream` dalam layanan Rust gRPC menawarkan keuntungan berikut:
- **Fleksibilitas:** Mendukung berbagai jenis penerima, termasuk channel dan future.
- **Integrasi yang Mudah:** Memudahkan integrasi dengan komponen lain dalam ekosistem Tokio.

Namun, pendekatan ini juga menyajikan beberapa tantangan:
- **Kompleksitas yang Meningkat:** Ada penambahan kompleksitas, khususnya bagi pengembang yang belum terbiasa dengan pemrograman asinkron dan konsep-konsep Tokio.
- **Overhead Potensial:** Terdapat overhead kecil yang mungkin terjadi akibat penggunaan pola asinkron ini.

# 5
Dengan struktur yang tepat, Rust gRPC mendukung peningkatan kemudahan pemeliharaan dan perluasan. Hal ini terjadi karena penggunaan protokol .proto dan integrasi dengan antarmuka yang mengizinkan pembuatan kelas di Rust, yang memudahkan penambahan fitur baru dan modifikasi kode secara umum.

# 6
Untuk menangani logika pemrosesan pembayaran yang lebih kompleks dalam implementasi MyPaymentService, beberapa langkah tambahan yang mungkin diperlukan mencakup:

- Validasi dan penanganan kesalahan yang cermat
- Otentikasi dan otorisasi pengguna
- Integrasi dengan gateway pembayaran eksternal
- Manajemen status transaksi
- Skalabilitas
- Penegakan aturan bisnis
- Notifikasi acara
- Rekonsiliasi transaksi
- Pengujian yang cermat

Atau bahkan dalam beberapa kasus, bisa saja kita ubah pattern dari networking yang digunakan yang awalnya unary menjadi server streaming.

Dengan langkah-langkah ini, logika pemrosesan pembayaran dapat ditingkatkan untuk menangani skenario yang lebih kompleks dengan efektif.

# 7
Dengan menggunakan gRPC, pengguna tidak perlu lagi memikirkan cara mengakses modul melalui protokol komunikasi HTTP. gRPC mengotomatisasi proses pemanggilan metode yang diinginkan melalui definisi yang disetujui dalam file proto. Ini memudahkan klien untuk memanggil fungsi dari server, menyederhanakan konektivitas dan operasi antar berbagai teknologi, platform, dan sistem yang tersebar.

# 8
HTTP/2 memungkinkan banyak permintaan dan respons untuk dilakukan melalui satu koneksi, yang memberi keunggulan dibandingkan HTTP/1.1. Namun, ini bisa menyebabkan biaya overhead yang lebih besar dalam hal kinerja dan penggunaan memori, terutama ketika mengirim data dalam jumlah kecil. Meski begitu, HTTP/2 lebih efektif untuk pengiriman data dalam volume besar. Dalam penggunaan REST API, HTTP/2 lebih sesuai karena mendukung fitur seperti multiplexing, kompresi header, server push, dan prioritas aliran. Ini juga lebih banyak didukung di infrastruktur web. Sementara itu, WebSocket lebih ideal untuk komunikasi real-time.

# 9
Model REST API umumnya mengikuti pola permintaan dan tanggapan yang satu arah, di mana klien mengirim permintaan dan server memberikan tanggapan. Sebaliknya, gRPC menawarkan kemampuan streaming bidireksional, yang memungkinkan komunikasi dua arah antara klien dan server secara langsung dan real-time. Dari segi responsivitas dan komunikasi real-time, gRPC memberikan kinerja yang lebih unggul dengan kemampuannya untuk mengirim dan menerima data secara asinkron, sedangkan REST API memerlukan permintaan dari klien sebelum bisa memberikan tanggapan.

# 10
gRPC menggunakan Protocol Buffers yang menyediakan efisiensi, keandalan, dan keamanan yang tinggi dalam pertukaran data antar layanan, berbeda dengan REST API yang menggunakan JSON yang lebih fleksibel namun kurang efisien dan kurang ketat dalam struktur datanya. Meskipun gRPC mungkin memerlukan waktu lebih lama untuk dipelajari, ia menawarkan kinerja yang lebih tinggi dan menjamin konsistensi dalam pertukaran data.

Untuk aplikasi yang membutuhkan kecepatan dan keamanan tinggi, gRPC bisa menjadi pilihan yang tepat. Namun, jika keflexibilitasan dalam struktur data dan kemudahan belajar lebih diutamakan, REST API dengan JSON bisa menjadi pilihan yang baik.






