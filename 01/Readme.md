Ai : Gemini AI

prompt : 

Berdasarkan teks materi modul di atas (atau dari dokumen/file yang saya lampirkan), bertindaklah sebagai seorang tutor/pengajar profesional yang ahli dalam menyederhanakan materi kompleks menjadi mudah dipahami. 

Buatlah ringkasan komprehensif dari materi tersebut dengan format output berikut:
A. Judul Materi
B. Tujuan Pembelajaran Utama (3-5 poin)
C. Poin-Poin Penting & Konsep Inti (Gunakan bullet points/poin singkat)
D. Analogi atau Contoh Sederhana dalam Kehidupan Sehari-hari
E. Daftar Istilah Penting beserta Definisi Singkatnya
F. 3-5 Soal Latihan beserta Kunci Jawaban & Pembahasannya untuk menguji pemahaman

Aturan tambahan:
- Fokus hanya pada informasi yang ada di dalam modul tersebut.
- Gunakan bahasa Indonesia yang baku, lugas, dan komunikatif.
- Jangan mengurangi fakta atau detail penting dari aslinya.
- Jika ada rumus atau tahapan/prosedur, buat dalam bentuk langkah demi langkah (step-by-step).

## Rangkuman Materi 01:

### A. Judul Materi

Pengenalan Sistem Terdistribusi dan Terdesentralisasi (Kode Mata Kuliah: FIF25002T, 3 SKS, Prodi Informatika, Fakultas Teknologi Informasi UTDI).

---

### B. Tujuan Pembelajaran Utama

* Mampu menjelaskan konsep sistem terdistribusi.


* Mampu menjelaskan konsep sistem terdesentralisasi.


* Mampu menjelaskan perbedaan antara sistem terdistribusi dengan sistem terdesentralisasi.


* Mampu menyebutkan berbagai contoh penerapan nyata dari sistem terdistribusi dan terdesentralisasi.


* Mampu menyebutkan berbagai tantangan dan tren terbaru di dunia sistem terdistribusi dan terdesentralisasi.



---

### C. Poin-Poin Penting & Konsep Inti

**1. Arti Penting dan Pengertian Dasar**

* **Arti Penting:** Pertumbuhan data serta jumlah pengguna yang sangat besar menuntut layanan modern untuk memiliki skalabilitas, sifat *fault-tolerant*, performa tinggi, serta ketersediaan layanan 24/7. Tanpa kedua sistem ini, platform seperti Google, Netflix, maupun *Blockchain* tidak akan terwujud.


* **Sistem Terdistribusi:** Sekumpulan komputer independen yang berkomunikasi melalui jaringan dan tampak bagi penggunanya sebagai satu sistem tunggal yang koheren (*a collection of independent computers that appears to its users as a single coherent system* — Andrew S. Tanenbaum dan Marteen van Steen, 2007).


* **Lima Karakteristik Utama Sistem Terdistribusi:** Transparansi lokasi (serta akses, replikasi, dan kegagalan), skalabilitas, *fault tolerance*, kinerja tinggi, dan heterogenitas.


* **Sistem Terdesentralisasi:** Berbeda dengan sistem tersentralisasi yang bertumpu pada 1 titik kontrol, sistem terdesentralisasi menerapkan distribusi kontrol tanpa titik tunggal kegagalan (*single point of failure*) di mana keputusan diambil secara kolektif melalui mekanisme konsensus.


* **Perbedaan Inti:** Sistem terdistribusi berfokus pada **pembagian beban kerja** (contoh: Google File System, MinIO Object Storage yang kini di-*fork* ke Silo), sedangkan sistem terdesentralisasi berfokus pada **pembagian kontrol** (contoh: *Blockchain*).



**2. Arsitektur Sistem Dasar & Studi Kasus**

* **Tiga Arsitektur Dasar:**
* *Client-Server*: Banyak *client* terhubung melalui internet ke *server* penyedia layanan.


* *Peer-to-Peer (P2P)*: Setiap *node* terhubung langsung secara setara tanpa server pusat (contoh: BitTorrent dan jaringan mata uang kripto seperti Bitcoin, Ethereum, Ripple, Uniswap, Cardano, Doge, Chainlink, Litecoin, Theta).


* *Hybrid*: Kombinasi antara koneksi *client-server* dengan *peer-to-peer* melalui *supernodes* (contoh: Signal, WhatsApp, Telegram).




* **Studi Kasus Sistem Terdistribusi:** Google File System / HDFS (penyimpanan data besar), Apache Kafka dan Apache Pulsar (*messaging* & *streaming*), layanan *streaming* video (Netflix, Twitch, YouTube), serta media sosial (Instagram, Threads, Facebook, TikTok).


* **Studi Kasus Sistem Terdesentralisasi:** *Blockchain* (Bitcoin, Ethereum, Algorand, Sui, Near, Aptos), DNS (*Domain Name System*), dan BitTorrent.



**3. Teorema CAP dan Konsistensi Data**

* **Teorema CAP (Brewer's Theorem, tahun 2000):** Pada penyimpanan data terdistribusi, tidak mungkin mendapatkan *Consistency* (C) dan *Availability* (A) secara bersamaan karena partisi jaringan (*Partition Tolerance* / P) pasti terjadi.


* *Consistency (C)*: Setiap operasi baca mengembalikan hasil penulisan terbaru atau pesan *error*.


* *Availability (A)*: Setiap permintaan ke *node* yang tidak gagal akan menerima respons non-*error* meskipun datanya bukan versi terbaru.


* *Partition Tolerance (P)*: Sistem tetap beroperasi meskipun komunikasi antar *node* terputus atau terfragmentasi.




* **Kompromi Saat Terjadi Partisi (Step-by-Step Pemilihan):**
1. Jika perancang memilih **AP (*Availability + Partition Tolerance*)**, sistem tetap melayani seluruh permintaan data meskipun berisiko data tidak sinkron atau mengorbankan konsistensi (contoh: MongoDB).


2. Jika perancang memilih **CP (*Consistency + Partition Tolerance*)**, sistem menolak permintaan baca maupun tulis selama partisi berlangsung demi menjamin data tetap konsisten atau mengorbankan ketersediaan (contoh: Apache Cassandra).




* **Tingkat Konsistensi Data:** *Strong Consistency* (hasil selalu sama di semua *node*, wajib untuk perbankan) dan *Eventual Consistency* (data akan konsisten setelah beberapa waktu, memadai untuk media sosial).



**4. Tantangan dan Tren Masa Depan**

* **Tantangan Utama:** *Latency* (lama waktu pemrosesan) dan *throughput* (jumlah data yang diproses per satuan waktu), keamanan siber (serangan DDoS dan *Sybil attack*), kompleksitas manajemen *node*, serta tata kelola (*governance*) pada sistem terdesentralisasi.


* **Tren Masa Depan:** Teknologi *Cloud-native* (Kubernetes, Docker), *Edge & Fog Computing*, Web3 & DeFi, serta *Federated Data - Learning* (kecerdasan buatan terdistribusi).



---

D. Contoh Penerapan di Kehidupan Sehari-hari

* **Layanan Perbankan (*Strong Consistency*):** Sistem transaksi bank wajib memakai *strong consistency* supaya saldo rekeningmu selalu tercatat persis sama dan *up-to-date*, mau dicek lewat mesin ATM mana pun atau lewat aplikasi *mobile banking*.


* **Media Sosial (*Eventual Consistency*):** Aplikasi seperti Instagram, Facebook, atau TikTok cukup memakai *eventual consistency*. Jadi kalau unggahan baru atau jumlah *like* muncul agak telat beberapa detik di layar pengguna lain, layanannya tetap aman dan tidak jadi masalah.


* **Aplikasi Belanja Online (*E-Commerce*):** Waktu kamu membuka aplikasi belanja lewat HP atau *browser*, setiap permintaanmu masuk dulu lewat *API Gateway* menggunakan REST API, lalu bebannya dibagi ke layanan yang terpisah-pisah—seperti bagian akun (*Account Service*), stok barang (*Inventory Service*), dan pengiriman (*Shipping Service*) yang masing-masing punya database sendiri. Meski di balik layar terpisah, kamu tetap merasakannya sebagai satu aplikasi belanja yang utuh.



---

E. Daftar Istilah Penting

* Skalabilitas: Seberapa sanggup sebuah sistem atau jaringan menampung lonjakan pengguna dan beban kerja yang makin besar tanpa bikin performanya melambat.


* Sistem Fault-Tolerant: Sistem yang tetap bisa berjalan normal walau ada sebagian komponen *hardware* atau *software* di dalamnya yang mendadak rusak atau *error*.


* Sistem Terdistribusi: Kumpulan komputer yang berdiri sendiri-sendiri tapi saling terhubung lewat jaringan untuk membagi beban kerja. Dari sisi pengguna, semuanya terasa seperti satu sistem tunggal yang utuh.


* Sistem Terdesentralisasi: Sistem yang menyebar kendali atau otoritasnya ke banyak *node* sekaligus lewat kesepakatan bersama (konsensus), jadi tidak bergantung pada satu pusat kendali yang rawan lumpuh (*single point of failure*).


* Latency & Throughput: *Latency* mengukur seberapa lama waktu yang dibutuhkan untuk memproses satu permintaan, sedangkan *throughput* mengukur seberapa banyak data atau pekerjaan yang sanggup diselesaikan dalam satu waktu.


* Sybil Attack: Serangan siber di jaringan *peer-to-peer* atau *blockchain* saat pelaku membuat ribuan akun atau identitas palsu sekaligus untuk memanipulasi suara dan mendominasi jaringan.



---

### F. Soal Latihan beserta Kunci Jawaban & Pembahasannya

**1. Jelaskan perbedaan mendasar antara sistem terdistribusi dengan sistem terdesentralisasi beserta masing-masing satu contoh penerapannya!**

* **Kunci Jawaban:** Sistem terdistribusi berfokus pada pembagian beban kerja (contoh: Google File System atau MinIO/Silo), sedangkan sistem terdesentralisasi berfokus pada pembagian kontrol tanpa otoritas pusat tunggal (contoh: *Blockchain*, DNS, atau BitTorrent).


* **Pembahasan:** Berdasarkan diagram jaringan Paul Baran (1964) dan ringkasan materi, kedua konsep ini saling berkaitan tetapi berbeda fokus utamanya: distribusi memecah pemrosesan/penyimpanan ke banyak mesin agar efisien, sementara desentralisasi menghilangkan *single point of failure* dalam pengambilan keputusan.



**2. Sebuah platform *e-commerce* global mengalami gangguan kabel laut sehingga koneksi jaringan antar pusat data terputus (*network partition*). Jika perancang sistem memilih konfigurasi CP (*Consistency + Partition Tolerance*) berdasarkan Teorema CAP, apa yang terjadi ketika pelanggan mencoba melakukan transaksi?**

* **Kunci Jawaban:** Sistem akan menolak permintaan baca maupun tulis dari pelanggan selama partisi berlangsung untuk memastikan data tetap konsisten, sehingga mengorbankan aspek *Availability*.


* **Pembahasan:** Dalam Teorema CAP oleh Eric Brewer, ketika terjadi partisi jaringan, perancang hanya dapat memilih antara AP (tetap melayani permintaan dengan risiko data tidak sinkron) atau CP (menolak permintaan demi menjaga konsistensi data antar *node*).



**3. Dalam sebuah jaringan *blockchain* publik, seorang penyerang membuat ribuan *node* dan akun palsu sekaligus guna memanipulasi hasil pemungutan suara konsensus dan merusak integritas jaringan. Jenis serangan keamanan apakah yang sedang terjadi?**

* **Kunci Jawaban:** *Sybil Attack*.


* **Pembahasan:** *Sybil attack* merupakan serangan yang menyasar sistem terdesentralisasi (seperti P2P atau *blockchain*) dengan cara menciptakan banyak identitas atau *node* palsu secara bersamaan untuk mendominasi pengaruh dan suara di dalam jaringan.



**4. Mengapa aplikasi perbankan dan aplikasi media sosial memiliki kebutuhan model konsistensi data yang berbeda?**

* **Kunci Jawaban:** Aplikasi perbankan membutuhkan *Strong Consistency* agar saldo dan transaksi selalu akurat serta seragam di semua *node*, sedangkan media sosial cukup menggunakan *Eventual Consistency* di mana pembaruan data akan sinkron secara bertahap seiring waktu.


* **Pembahasan:** Kesalahan atau keterlambatan sinkronisasi saldo pada sistem perbankan dapat menimbulkan kerugian finansial fatal, sementara pada media sosial keterlambatan sinkronisasi unggahan atau komentar dalam hitungan detik masih dapat ditoleransi demi kecepatan akses.


Yang saya edit :

## D. Contoh Penerapan di Kehidupan Sehari-hari

* **Layanan Perbankan (*Strong Consistency*):** Sistem transaksi bank wajib memakai *strong consistency* supaya saldo rekeningmu selalu tercatat persis sama dan *up-to-date*, mau dicek lewat mesin ATM mana pun atau lewat aplikasi *mobile banking*.


* **Media Sosial (*Eventual Consistency*):** Aplikasi seperti Instagram, Facebook, atau TikTok cukup memakai *eventual consistency*. Jadi kalau unggahan baru atau jumlah *like* muncul agak telat beberapa detik di layar pengguna lain, layanannya tetap aman dan tidak jadi masalah.


* **Aplikasi Belanja Online (*E-Commerce*):** Waktu kamu membuka aplikasi belanja lewat HP atau *browser*, setiap permintaanmu masuk dulu lewat *API Gateway* menggunakan REST API, lalu bebannya dibagi ke layanan yang terpisah-pisah—seperti bagian akun (*Account Service*), stok barang (*Inventory Service*), dan pengiriman (*Shipping Service*) yang masing-masing punya database sendiri. Meski di balik layar terpisah, kamu tetap merasakannya sebagai satu aplikasi belanja yang utuh.

## E. Daftar Istilah Penting

**Skalabilitas:** Seberapa sanggup sebuah sistem atau jaringan menampung lonjakan pengguna dan beban kerja yang makin besar tanpa bikin performanya melambat.


**Sistem Fault-Tolerant:** Sistem yang tetap bisa berjalan normal walau ada sebagian komponen *hardware* atau *software* di dalamnya yang mendadak rusak atau *error*.


**Sistem Terdistribusi:** Kumpulan komputer yang berdiri sendiri-sendiri tapi saling terhubung lewat jaringan untuk membagi beban kerja. Dari sisi pengguna, semuanya terasa seperti satu sistem tunggal yang utuh.


**Sistem Terdesentralisasi:** Sistem yang menyebar kendali atau otoritasnya ke banyak *node* sekaligus lewat kesepakatan bersama (konsensus), jadi tidak bergantung pada satu pusat kendali yang rawan lumpuh (*single point of failure*).


**Latency & Throughput:** *Latency* mengukur seberapa lama waktu yang dibutuhkan untuk memproses satu permintaan, sedangkan *throughput* mengukur seberapa banyak data atau pekerjaan yang sanggup diselesaikan dalam satu waktu.


**Sybil Attack:** Serangan siber di jaringan *peer-to-peer* atau *blockchain* saat pelaku membuat ribuan akun atau identitas palsu sekaligus untuk memanipulasi suara dan mendominasi jaringan.
