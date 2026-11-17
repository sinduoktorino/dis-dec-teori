## Ai : Gemini AI

## Prompt yang saya gunakan :

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

## Rangkuman Materi :

### A. Judul Materi

03: Sinkronisasi dan Koordinasi pada Sistem Terdistribusi (Kode Mata Kuliah: FIF25002T, 3 SKS, Prodi Informatika, Fakultas Teknologi Informasi UTDI).

---

### B. Tujuan Pembelajaran Utama

* Memahami dan mampu menjelaskan alasan perlunya sinkronisasi untuk koordinasi beserta berbagai tantangannya pada sistem terdistribusi.


* Memahami dan mampu menjelaskan sinkronisasi waktu fisik beserta algoritma dan protokolnya.


* Memahami dan mampu menjelaskan sinkronisasi waktu logis beserta algoritma terkait.


* Memahami dan mampu menjelaskan masalah *mutual exclusion* beserta berbagai algoritma penyelesaiannya.


* Memahami dan mampu menjelaskan masalah pemilihan koordinator (*coordinator election*), pemecahannya, serta studi kasus nyatanya di industri.

---

### C. Poin-Poin Penting & Konsep Inti

**1. Konsep Dasar Sinkronisasi dan Pentingnya dalam Sistem Terdistribusi**

* **Definisi:** Sinkronisasi adalah koordinasi proses, data, dan sumber daya di berbagai *node* dalam jaringan untuk menjaga konsistensi data, mengelola proses konkuren, mencegah konflik data (*data race*), dan memastikan perilaku sistem yang koheren serta andal.


* **Perbedaan *Data Race* vs *Race Condition*:**
* *Data Race*: Terjadi di level rendah (*low-level* akses memori fisik) ketika minimal 2 *thread* mengakses lokasi memori yang sama secara bersamaan, minimal 1 akses adalah operasi *write*, dan tidak ada sinkronisasi (*mutex/lock*), yang berdampak pada korupsi memori atau *undefined behavior*.


* *Race Condition*: Terjadi di level tinggi (*high-level* logika aplikasi) ketika kebenaran hasil bergantung pada urutan dan waktu eksekusi instruksi yang tidak terprediksi, yang berdampak pada kesalahan logika bisnis seperti saldo minus (*double spending*). Solusinya adalah desain ulang alur kontrol seperti *Atomic Check-and-Act* atau *Database Transaction Lock*.


* **Alasan Pentingnya Sinkronisasi:** Menjaga integritas data, sinkronisasi *state* antar *node*, koordinasi *tasks*, pengelolaan sumber daya, menjaga *state* untuk mekanisme pemulihan (*recovery*), efisiensi utilisasi (mencegah operasi redundan), *load balancing*, mencegah *deadlock*, dan mendukung skalabilitas operasi.


* **Tantangan Sinkronisasi:** Latensi jaringan dan partisi (*network latency and partitioning*), skalabilitas, sistem toleran kesalahan (*fault-tolerant system*), kontrol konkurensi (*concurrency control*), konsistensi data (*data consistency*), dan sinkronisasi waktu.



**2. Sinkronisasi Waktu Fisik**

* **Tujuan:** Menyelaraskan *real-time clock* pada sistem terdistribusi dengan standar umum demi akurasi korelasi log, penjadwalan *event*, dan konsistensi sistem.


* **Standar Waktu:**
* GMT (*Greenwich Mean Time*): Sudah tidak digunakan.


* UTC (*Universal Coordinated Time*): Standar internasional yang didefinisikan oleh ITU sejak 1963/1967, berbasis pada TAI (*International Atomic Time* / *Temps Atomique International*).


* LTC (*Coordinated Lunar Time*): Masih dalam tahap pengembangan.


* **Sumber dan Alur Sinkronisasi Perangkat Keras:** *Master atomic clock* di darat (seperti di *U.S. Naval Observatory* dan *Schriever Space Force Base*) menyinkronkan *atomic clock* pada satelit (31 satelit GPS di orbit MEO, misi DSAC NASA, dan ACES di ISS). Sinyal waktu GPS ditangkap oleh *GPS Dongle* (misalnya U-Blox G-7020 melalui `/dev/ttyACM0` dan layanan `gpsd`), diteruskan melalui *shared memory* (RAM) ke server NTP/PTP, lalu menyinkronkan *client*.


* **Protokol Waktu:**
* **NTP (*Network Time Protocol* - RFC 5905):** Dikembangkan oleh David L. Mills dkk. (1985), diimplementasikan antara lain melalui perangkat lunak `chrony` (`chronyd` dan `chronyc`), memberikan akurasi dalam hitungan milidetik di internet dan puluhan mikrodetik di LAN.


* **PTP (*Precision Time Protocol* - IEEE 1588):** Standar IEEE (versi 1588-2002, 1588-2008/PTPv2, 1588-2019, serta adaptasi IEEE 802.1AS/gPTP) yang diimplementasikan di Linux melalui `linuxptp` (`ptp4l` dan `phc2sys`). PTP mensyaratkan kartu jaringan (NIC) yang mendukung *hardware timestamping*.



**3. Sinkronisasi Waktu Logis dan *Vector Clocks***

* **Konsep:** Menetapkan urutan sebab-akibat kejadian (*causal order of events*) berdasarkan prinsip transitivitas (jika $A \rightarrow B$ dan $B \rightarrow C$, maka $A \rightarrow C$) tanpa terikat waktu fisik.


* **Tahapan Algoritma *Vector Clocks* (Step-by-Step untuk 3 Proses: A, B, C):**
1. **Inisialisasi:** Setiap proses memulai dengan vektor bernilai nol sesuai jumlah proses, yaitu A `[0, 0, 0]`, B `[0, 0, 0]`, dan C `[0, 0, 0]` (indeks 0 untuk A, indeks 1 untuk B, indeks 2 untuk C).


2. **Kejadian Internal (*Internal Event*):** Setiap kali suatu proses melakukan aksi internal, tambahkan `1` pada indeks miliknya sendiri (contoh: A melakukan aksi internal menjadi `[1, 0, 0]`).


3. **Pengiriman Pesan (*Send Message*):** Sebelum mengirim pesan, pengirim menambahkan `1` pada indeksnya sendiri lalu menyertakan vektor tersebut dalam pesan (contoh: A menjadi `[2, 0, 0]` lalu mengirim ke B).


4. **Penerimaan Pesan (*Receive Message*):** Penerima membandingkan setiap elemen vektor yang diterima dengan vektor lokalnya untuk mengambil nilai maksimum per elemen (*element-wise max*), lalu menambahkan `1` pada indeks miliknya sendiri jika disertai kejadian reaksi (contoh: B menerima `[2, 0, 0]`, memperbarui posisinya menjadi `[2, 0, 0]`, lalu saat mengirim ke C menaikkan indeksnya menjadi `[2, 1, 0]`).


5. **Aturan Perbandingan Urutan:** Kejadian pada vektor $X$ terjadi sebelum $Y$ jika seluruh elemen pada $X \le Y$ dan minimal ada satu elemen yang lebih kecil; jika tidak memenuhi syarat tersebut, kedua kejadian bersifat *concurrent* (independen).



**4. Tantangan *Mutual Exclusion* (Mutex)**

* **Tujuan:** Memastikan hanya satu proses atau *thread* yang mengakses bagian kode sumber daya bersama (*Critical Section* / CS) pada satu waktu.


* **Empat Prinsip Mutex:** *Mutual Exclusion* (maksimal 1 proses di CS), *Progress* (CS bebas dapat segera diakses), *Bounded Waiting* (tidak ada proses menunggu selamanya), dan *Fairness* (permintaan dilayani secara adil).


* **Tiga Pendekatan Solusi:**
1. **Centralized Algorithm:** Satu *node* bertindak sebagai koordinator pengatur izin masuk/keluar CS. Kelebihan: sederhana dan biaya rendah; Kekurangan: *single point of failure* dan potensi *bottleneck*.


2. **Ricart-Agrawala:** Terdistribusi penuh tanpa koordinator; proses menyiarkan permintaan berstempel waktu ke semua *node* dan masuk CS setelah semua membalas OK. Membutuhkan $2 \times (N - 1)$ pesan per entri CS. Kelebihan: *fault tolerant*; Kekurangan: *overhead* pesan tinggi.


3. **Token-Based Algorithm:** Sebuah token unik beredar antar proses; hanya pemegang token yang boleh masuk CS. Kelebihan: hanya membutuhkan 1 pesan per entri CS; Kekurangan: deteksi kehilangan token sulit dan butuh mekanisme pemulihan.


**5. Pemilihan Koordinator (*Coordinator Election*)**

* **Tujuan:** Memilih satu pemimpin (*leader*) secara otomatis saat koordinator sebelumnya gagal atau *node* baru bergabung untuk mengelola sumber daya bersama, menyinkronkan operasi, dan membuat keputusan global.


* **Algoritma & Implementasi:** Menggunakan *Bully Algorithm*, *Ring Algorithm*, atau protokol berbasis konsensus seperti Raft dan Paxos. Contoh di industri: Apache ZooKeeper menggunakan Zab (*ZooKeeper Atomic Broadcast*, mirip Paxos) dan Kubernetes menggunakan Raft (melalui `etcd`).

---

## D. Contoh Sederhana di Kehidupan Sehari-hari

* **Stok Barang di Toko Online (*Race Condition*):** Bayangkan ada 10 unit Produk X yang tersisa. Pembeli A dan Pembeli B mengecek stok di detik yang persis sama, jadi keduanya sama-sama melihat angka 10. Saat keduanya langsung beli 1 unit berbarengan, sistem sama-sama menghitung sisa stok $10 - 1 = 9$. Akibatnya, padahal ada 2 barang yang sudah terjual, stok di sistem malah tercatat sisa 9, bukan 8.
* **Tarik Tunai Saldo Bank (*Race Condition*):** Misalnya saldo rekeningmu berisi $\$100$. Tiba-tiba ada dua transaksi penarikan sebesar $\$80$ yang masuk di waktu bersamaan. Karena kedua transaksi lolos pengecekan saldo ($\ge \$80$) sebelum nilai saldonya sempat diperbarui, keduanya sama-sama memotong saldo awal dan bikin saldo akhirmu malah jadi minus (-$60).
* **Game Online Multipemain & Keranjang Belanja Web:** Di game online, posisi karakter, sisa darah (*health*), dan isi tas pemain terus disinkronkan ke layar semua pemain supaya tampilannya seragam. Hal yang mirip juga terjadi di aplikasi web saat isi keranjang belanjamu disinkronkan antara *browser* dan *database*, jadi barang belanjaanmu tetap sama waktu kamu buka akun lewat perangkat lain.

---

## E. Daftar Istilah Penting

* **Data Race:** Situasi ketika dua *thread* atau lebih mengakses lokasi memori yang sama di waktu bersamaan tanpa penguncian (*lock*), dan setidaknya ada satu yang melakukan proses tulis (*write*), sehingga bikin datanya rusak.
* **Race Condition:** Masalah pada alur logika program saat hasil akhirnya sangat bergantung pada urutan dan waktu eksekusi perintah yang tidak bisa ditebak.
* **Deadlock:** Kondisi saat proses-proses saling menunggu satu sama lain secara melingkar—misalnya Proses 1 menunggu sumber daya R3 yang dipakai Proses 2, sementara Proses 2 menunggu R2 yang dipegang Proses 1—akhirnya tidak ada satu pun yang bisa jalan lagi.
* **UTC (*Universal Coordinated Time*):** Standar waktu internasional yang mengacu pada *International Atomic Time* (TAI) untuk menyamakan jam fisik di seluruh dunia.
* **Critical Section (CS):** Potongan kode program yang mengakses sumber daya bersama (seperti *printer*, berkas, atau *database*) dan cuma boleh dijalankan oleh satu proses saja dalam satu waktu.
* **Vector Clocks:** Struktur penanda waktu logis berupa susunan angka dinamis yang menyimpan hitungan setiap proses di sistem terdistribusi, gunanya untuk melacak urutan sebab-akibat maupun kejadian yang berjalan bersamaan (*concurrency*).

---

## F. Soal Latihan dan Pembahasan

**1. Dalam sistem terdistribusi yang berisi 3 proses (A, B, dan C) dengan kondisi awal `[0, 0, 0]`, proses A melakukan 1 kejadian internal lalu mengirim pesan ke B. Proses B menerima pesan itu dan langsung meneruskannya ke C. Proses C lalu menerima pesan tersebut sebagai kejadian internal. Berapa nilai *Vector Clock* akhir di proses C?**

* **Jawaban:** `[2, 1, 1]`.
* **Pembahasan:**
* Awalnya A melakukan kejadian internal sehingga nilainya naik menjadi `[1, 0, 0]`, lalu indeksnya dinaikkan lagi sebelum mengirim pesan ke B menjadi `[2, 0, 0]`.
* B menerima `[2, 0, 0]`, membandingkannya dengan nilai lokal `[0, 0, 0]` dan mengambil angka terbesar tiap elemen menjadi `[2, 0, 0]`. Sebelum mengirim ke C, B menaikkan indeksnya sendiri (indeks ke-1) sehingga pesan yang dikirim bernilai `[2, 1, 0]`.
* C menerima `[2, 1, 0]`, mengambil nilai maksimum per elemen dengan `[0, 0, 0]` menjadi `[2, 1, 0]`, lalu menambah `1` di indeksnya sendiri (indeks ke-2) karena ada kejadian internal penerimaan pesan, sehingga hasil akhirnya `[2, 1, 1]`.



**2. Jika diketahui *Vector Clock* kejadian di proses A adalah `[2, 0, 0]` dan di proses C adalah `[2, 1, 2]`, bagaimana hubungan urutan waktu di antara kedua kejadian itu?**

* **Jawaban:** Kejadian di A terjadi lebih dulu (*happens before*) dibanding kejadian di C.
* **Pembahasan:** Menurut aturan *Vector Clocks*, kejadian A terjadi sebelum C karena semua angka pada vektor A (`2, 0, 0`) nilainya lebih kecil atau sama dengan angka yang posisinya sejajar pada vektor C (`2, 1, 2`), ditambah ada minimal satu elemen yang nilainya benar-benar lebih kecil (di indeks ke-1: $0 < 1$ dan indeks ke-2: $0 < 2$).

**3. Sebuah klaster sistem terdistribusi punya $N = 6$ *node* dan memakai algoritma *Ricart-Agrawala* untuk mengatur *mutual exclusion*. Berapa total pesan yang dibutuhkan setiap kali ada satu proses yang mau masuk ke *Critical Section*?**

* **Jawaban:** `10` pesan.
* **Pembahasan:** Algoritma *Ricart-Agrawala* membutuhkan $2 \times (N - 1)$ pesan tiap kali sebuah proses ingin masuk ke *Critical Section* (terdiri dari $N - 1$ pesan permintaan izin dan minimal $N - 1$ pesan balasan OK). Karena jumlahnya $N = 6$, perhitungannya menjadi $2 \times (6 - 1) = 10$ pesan.

**4. Seorang administrator jaringan ingin memakai *Precision Time Protocol* (PTP) lewat `linuxptp` di antarmuka `eth0`, tapi gagal mendapat akurasi perangkat keras karena hasil perintah `ethtool -T eth0` memunculkan tulisan `PTP Hardware Clock: none`. Kira-kira apa penyebabnya menurut modul?**

* **Jawaban:** Kartu jaringan (NIC) pada server tersebut belum mendukung fitur *hardware timestamping*.
* **Pembahasan:** Supaya PTP bisa jalan dengan presisi tinggi, kartu jaringan (NIC) wajib punya dukungan *hardware timestamping* secara fisik. Kalau hasil pengecekan `ethtool -T` memunculkan keterangan `none` pada bagian *PTP Hardware Clock* maupun *Hardware Transmit/Receive Timestamp Modes*, artinya perangkat kerasnya memang tidak memenuhi syarat untuk sinkronisasi PTP berbasis *hardware*.

## Yang saya edit :

## D. Contoh Sederhana di Kehidupan Sehari-hari

* **Stok Barang di Toko Online (*Race Condition*):** Bayangkan ada 10 unit Produk X yang tersisa. Pembeli A dan Pembeli B mengecek stok di detik yang persis sama, jadi keduanya sama-sama melihat angka 10. Saat keduanya langsung beli 1 unit berbarengan, sistem sama-sama menghitung sisa stok $10 - 1 = 9$. Akibatnya, padahal ada 2 barang yang sudah terjual, stok di sistem malah tercatat sisa 9, bukan 8.
* **Tarik Tunai Saldo Bank (*Race Condition*):** Misalnya saldo rekeningmu berisi $\$100$. Tiba-tiba ada dua transaksi penarikan sebesar $\$80$ yang masuk di waktu bersamaan. Karena kedua transaksi lolos pengecekan saldo ($\ge \$80$) sebelum nilai saldonya sempat diperbarui, keduanya sama-sama memotong saldo awal dan bikin saldo akhirmu malah jadi minus (-$60).
* **Game Online Multipemain & Keranjang Belanja Web:** Di game online, posisi karakter, sisa darah (*health*), dan isi tas pemain terus disinkronkan ke layar semua pemain supaya tampilannya seragam. Hal yang mirip juga terjadi di aplikasi web saat isi keranjang belanjamu disinkronkan antara *browser* dan *database*, jadi barang belanjaanmu tetap sama waktu kamu buka akun lewat perangkat lain.

---

## E. Daftar Istilah Penting

* **Data Race:** Situasi ketika dua *thread* atau lebih mengakses lokasi memori yang sama di waktu bersamaan tanpa penguncian (*lock*), dan setidaknya ada satu yang melakukan proses tulis (*write*), sehingga bikin datanya rusak.
* **Race Condition:** Masalah pada alur logika program saat hasil akhirnya sangat bergantung pada urutan dan waktu eksekusi perintah yang tidak bisa ditebak.
* **Deadlock:** Kondisi saat proses-proses saling menunggu satu sama lain secara melingkar—misalnya Proses 1 menunggu sumber daya R3 yang dipakai Proses 2, sementara Proses 2 menunggu R2 yang dipegang Proses 1—akhirnya tidak ada satu pun yang bisa jalan lagi.
* **UTC (*Universal Coordinated Time*):** Standar waktu internasional yang mengacu pada *International Atomic Time* (TAI) untuk menyamakan jam fisik di seluruh dunia.
* **Critical Section (CS):** Potongan kode program yang mengakses sumber daya bersama (seperti *printer*, berkas, atau *database*) dan cuma boleh dijalankan oleh satu proses saja dalam satu waktu.
* **Vector Clocks:** Struktur penanda waktu logis berupa susunan angka dinamis yang menyimpan hitungan setiap proses di sistem terdistribusi, gunanya untuk melacak urutan sebab-akibat maupun kejadian yang berjalan bersamaan (*concurrency*).

---

## F. Soal Latihan dan Pembahasan

**1. Dalam sistem terdistribusi yang berisi 3 proses (A, B, dan C) dengan kondisi awal `[0, 0, 0]`, proses A melakukan 1 kejadian internal lalu mengirim pesan ke B. Proses B menerima pesan itu dan langsung meneruskannya ke C. Proses C lalu menerima pesan tersebut sebagai kejadian internal. Berapa nilai *Vector Clock* akhir di proses C?**

* **Jawaban:** `[2, 1, 1]`.
* **Pembahasan:**
* Awalnya A melakukan kejadian internal sehingga nilainya naik menjadi `[1, 0, 0]`, lalu indeksnya dinaikkan lagi sebelum mengirim pesan ke B menjadi `[2, 0, 0]`.
* B menerima `[2, 0, 0]`, membandingkannya dengan nilai lokal `[0, 0, 0]` dan mengambil angka terbesar tiap elemen menjadi `[2, 0, 0]`. Sebelum mengirim ke C, B menaikkan indeksnya sendiri (indeks ke-1) sehingga pesan yang dikirim bernilai `[2, 1, 0]`.
* C menerima `[2, 1, 0]`, mengambil nilai maksimum per elemen dengan `[0, 0, 0]` menjadi `[2, 1, 0]`, lalu menambah `1` di indeksnya sendiri (indeks ke-2) karena ada kejadian internal penerimaan pesan, sehingga hasil akhirnya `[2, 1, 1]`.



**2. Jika diketahui *Vector Clock* kejadian di proses A adalah `[2, 0, 0]` dan di proses C adalah `[2, 1, 2]`, bagaimana hubungan urutan waktu di antara kedua kejadian itu?**

* **Jawaban:** Kejadian di A terjadi lebih dulu (*happens before*) dibanding kejadian di C.
* **Pembahasan:** Menurut aturan *Vector Clocks*, kejadian A terjadi sebelum C karena semua angka pada vektor A (`2, 0, 0`) nilainya lebih kecil atau sama dengan angka yang posisinya sejajar pada vektor C (`2, 1, 2`), ditambah ada minimal satu elemen yang nilainya benar-benar lebih kecil (di indeks ke-1: $0 < 1$ dan indeks ke-2: $0 < 2$).

**3. Sebuah klaster sistem terdistribusi punya $N = 6$ *node* dan memakai algoritma *Ricart-Agrawala* untuk mengatur *mutual exclusion*. Berapa total pesan yang dibutuhkan setiap kali ada satu proses yang mau masuk ke *Critical Section*?**

* **Jawaban:** `10` pesan.
* **Pembahasan:** Algoritma *Ricart-Agrawala* membutuhkan $2 \times (N - 1)$ pesan tiap kali sebuah proses ingin masuk ke *Critical Section* (terdiri dari $N - 1$ pesan permintaan izin dan minimal $N - 1$ pesan balasan OK). Karena jumlahnya $N = 6$, perhitungannya menjadi $2 \times (6 - 1) = 10$ pesan.

**4. Seorang administrator jaringan ingin memakai *Precision Time Protocol* (PTP) lewat `linuxptp` di antarmuka `eth0`, tapi gagal mendapat akurasi perangkat keras karena hasil perintah `ethtool -T eth0` memunculkan tulisan `PTP Hardware Clock: none`. Kira-kira apa penyebabnya menurut modul?**

* **Jawaban:** Kartu jaringan (NIC) pada server tersebut belum mendukung fitur *hardware timestamping*.
* **Pembahasan:** Supaya PTP bisa jalan dengan presisi tinggi, kartu jaringan (NIC) wajib punya dukungan *hardware timestamping* secara fisik. Kalau hasil pengecekan `ethtool -T` memunculkan keterangan `none` pada bagian *PTP Hardware Clock* maupun *Hardware Transmit/Receive Timestamp Modes*, artinya perangkat kerasnya memang tidak memenuhi syarat untuk sinkronisasi PTP berbasis *hardware*.