## Ai : Gemin Ai

## Prompt :

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

## Rangkuman Materi 02

### A. Judul Materi

Proses dan Komunikasi Antar Proses pada Sistem Terdistribusi (Kode Mata Kuliah: FIF25002T, 3 SKS, Prodi Informatika, Fakultas Teknologi Informasi UTDI).

---

### B. Tujuan Pembelajaran Utama

* Mampu menjelaskan konsep proses pada sistem terdistribusi.


* Mampu menjelaskan berbagai jenis komunikasi antar proses atau *Inter-Process Communication* (IPC).


* Mampu menganalisis isu sinkronisasi, reliabilitas, dan keamanan pada sistem terdistribusi.


* Mampu mengaitkan konsep ke contoh nyata seperti *microservices*, *cloud*, maupun *distributed messaging*.

---

### C. Poin-Poin Penting & Konsep Inti

**1. Konsep Proses dan Manajemen Proses**

* **Proses vs Program:** Program merupakan kumpulan instruksi pasif yang tersimpan di *disk*, sedangkan proses adalah program yang diinstansiasi ke dalam RAM untuk dieksekusi oleh CPU melalui penjadwal sistem operasi (*scheduler*) dengan mekanisme *context switch* dan *preemption*.


* **Tiga Aktivitas Manajemen Proses:**
1. *Process Creation* (Pembuatan Proses): Sistem operasi menerima permintaan pembuatan proses, mengalokasikan sumber daya (memori, *file*), dan menginisialisasi lingkungan eksekusi seperti *Process Control Block* (PCB), register, serta *stack* hingga proses siap dijalankan (*ready to run*).


2. *Process Migration* (Migrasi Proses): Sistem operasi memindahkan proses yang sedang berjalan atau siap berjalan dari satu CPU atau *node* ke *node* lain untuk menyeimbangkan beban (*load balancing*), meningkatkan performa, atau menangani kegagalan.


3. *Process Monitoring* (Pemantauan Proses): Sistem operasi melacak status proses, penggunaan sumber daya (CPU dan memori), serta performa untuk memastikan eksekusi berjalan semestinya dan mengambil tindakan korektif bila perlu.

**2. Sistem Terdistribusi dan Model Komunikasi**

* **Definisi:** Sistem terdistribusi adalah sekumpulan komputer atau *node* independen yang menjalankan proses masing-masing dan bekerja sama dalam satu koordinasi sebagai satu kesatuan logis melalui jaringan.


* **Tujuan Komunikasi Antar Node:** Pertukaran data, koordinasi (sinkronisasi, konsistensi data, manajemen transaksi), keandalan (*reliability* saat salah satu *node* gagal), dan skalabilitas dinamis.


* **Jenis Komunikasi & Model Pesan:**
* Komunikasi *Request-Response* (permintaan layanan/data dan balasan) serta *Publish-Subscribe* (mengirim *event* dan menerima notifikasi).


* Komunikasi langsung menggunakan *socket* (misalnya antarmuka *loopback* `127.0.0.1` pada port tertentu), komunikasi tidak langsung menggunakan *mailboxes* atau *message queues* (seperti perintah `write` di Linux), serta pola *Pub/Sub* melalui perantara *Topic*.


* **Sinkron vs Asinkron:** Pada komunikasi sinkron (*Synchronous*), klien mengirim permintaan lalu berhenti menunggu hingga server memberikan respons; sedangkan pada komunikasi asinkron (*Asynchronous*), klien mengirim permintaan lalu langsung melanjutkan pekerjaan lain sebelum mengambil respons.

**3. Inter-Process Communication (IPC) pada Sistem Terdistribusi**

* Karena proses berada di berbagai *node* yang terpisah secara fisik dan tidak memiliki akses memori bersama, mekanisme *Shared Memory* tidak cocok digunakan untuk sistem terdistribusi.


* Tiga mekanisme IPC yang relevan untuk sistem terdistribusi meliputi:
* **Message Passing:** Pertukaran pesan langsung antar proses melalui tautan komunikasi menggunakan primitif `send` dan `receive`. Standar yang digunakan adalah MPI (*Message Passing Interface*, versi terakhir sampai Oktober 2026 adalah versi 5.0) dengan implementasi seperti `openMPI` atau `mpi4py` di Python.


* **Remote Procedure Call (RPC):** Memungkinkan klien memanggil prosedur atau fungsi di server jarak jauh seolah-olah pemanggilan lokal menggunakan perantara *Stub* di sisi klien dan server. Contoh penerapannya adalah gRPC yang menggunakan *Proto Request* dan *Proto Response* lintas bahasa pemrograman.


* **Message-Oriented Middleware (MOM):** Infrastruktur perantara (*messaging provider*) yang memfasilitasi transfer unit informasi mandiri (*message*) antar aplikasi secara asinkron. Standar dan protokol MOM meliputi XATMI, AMQP (*enterprise apps*), HLA IEEE 1516, MQTT (*resource-constrained devices*), DDS, dan XMPP.

**4. Masalah Komunikasi, Protokol, dan Tantangan Sistem**

* **Empat Masalah Utama Komunikasi Antar Proses:**
1. *Reliability*: Menjamin pesan terkirim lengkap dan berurutan meski terjadi kehilangan paket atau *crash* (Solusi: *acknowledgement*, transmisi ulang, protokol TCP).


2. *Ordering*: Menjamin pesan diproses dalam urutan logis (Solusi: *Pipes FIFO*, *message queues*, *shared memory*, *sockets/message passing*, dan RPC).


3. *Security*: Enkripsi dan autentikasi.


4. *Performance*: Pengelolaan latensi dan *bandwidth*.

* **Protokol Komunikasi:** Protokol dasar meliputi TCP, UDP, dan HTTP; protokol utama di atas HTTP meliputi gRPC, GraphQL, dan REST. Modul juga membandingkan arsitektur HTTP/2 (HTTPS + TLS di atas TCP) dengan HTTP/3 (HTTPS + QUIC di atas UDP).


* **Tantangan & Solusi Tambahan:** *Message loss* diatasi dengan *retransmission* dan *acknowledgement*; *deadlock* diatasi dengan *timeout* dan *detection algorithm*; *data inconsistency* diatasi dengan *consensus protocol* (Raft, Paxos); serta *security* diatasi dengan SSL/TLS dan OAuth2.


* **Isu Terkini (*Current Issues*):** *Edge and Fog Computing*, *observability and tracing* (*telemetry*), serta *container orchestration* (Kubernetes, Docker Swarm).

**5. Sinkronisasi Waktu, Logical Clock, dan Koordinasi Proses**

* **Sinkronisasi Clock:** Setiap *node* memiliki jam lokal yang rentan mengalami deviasi akibat latensi jaringan dan pergeseran perangkat keras. Sinkronisasi eksternal menggunakan *atomic clock* (menghasilkan TAI), GPS, dan UTC, lalu diselaraskan menggunakan protokol NTP (*Network Time Protocol*) atau PTP (*Precision Time Protocol*, yang lebih presisi daripada NTP).


* **Tahapan Algoritma Lamport Logical Clock (Step-by-Step):**
1. Inisialisasi: Setiap *node* atau layanan memulai dengan nilai *logical clock* `0`.

2. Kejadian Internal: Setiap kali terjadi suatu kejadian (*event*), *node* menambahkan angka `1` pada *logical clock* lokalnya.

3. Pengiriman Pesan: Saat mengirim pesan ke *node* lain, pengirim menyertakan nilai *logical clock* miliknya saat itu.

4. Penerimaan Pesan: Saat menerima pesan, penerima membandingkan nilai *logical clock* lokalnya dengan nilai yang dibawa oleh pesan, memilih angka terbesar di antara keduanya, lalu menambahkan angka `1` sebagai nilai *logical clock* terbarunya.

* **Pengembangan setelah Scalar Clock Lamport:** Vector clocks (1988), Plausible clocks (1999), Chain Clocks (2005), Interval Tree Clocks (2008), dan Blum Clocks (2019).

* **Koordinasi Proses:** Mekanisme untuk menyelaraskan kerja proses independen pada sumber daya bersama tanpa konflik seperti *deadlock* atau *race condition*, menggunakan perangkat seperti Apache ZooKeeper, etcd, Consul, ClickHouse Keeper, Oxia, dan KRaft.

---

## D. Contoh Sederhana di Kehidupan Sehari-hari

* **Contoh Nyata dari Modul:**
* **Aplikasi Ojek Online (Gojek/Grab):** Saat kita memesan ojek, tampilan aplikasi di HP sebenarnya berkomunikasi dengan banyak layanan terpisah di balik layar—mulai dari pencari *driver*, pelacak posisi (*location tracing*), sampai penghitung tarif perjalanan.
* **Aplikasi Chat (WhatsApp):** Memakai jalur komunikasi *point-to-point* untuk mengirim pesan maupun *video call* di atas jaringan infrastruktur yang tersebar.
* **Game Online Multipemain (*Multiplayer Games*):** Butuh pertukaran data antar pemain (*node*) secara *real-time* supaya posisi dan kondisi permainan di layar semua pemain selalu sinkron.


* **Perumpamaan Komunikasi Sinkron vs Asinkron:**
* **Sinkron:** Anggap saja seperti sedang menelepon. Begitu kamu bertanya, kamu harus tetap memegang telepon menunggu lawan bicara menjawab sebelum bisa lanjut mengerjakan hal lain.
* **Asinkron:** Mirip seperti mengirim pesan singkat atau menaruh surat di kotak pos (*mailbox*). Setelah pesan terkirim, kamu bisa langsung ditinggal mengerjakan urusan lain, lalu baru membaca balasannya nanti saat pesan balasan masuk.



---

## E. Daftar Istilah Penting

* **Sistem Terdistribusi:** Sekumpulan komputer atau *node* yang berdiri sendiri-sendiri, tetapi saling terkoordinasi sehingga dari luar terlihat seperti satu sistem yang utuh.
* **Inter-Process Communication (IPC):** Cara antar proses saling bertukar data dan berkomunikasi, baik di dalam satu komputer yang sama maupun lintas *node* di jaringan terdistribusi.
* **Stub:** Bagian perantara di sisi klien dan server pada arsitektur RPC yang tugasnya membungkus data parameter pemanggilan fungsi beserta hasil eksekusinya agar bisa dikirim lewat jaringan.
* **Message-Oriented Middleware (MOM):** Jalur perantara yang memungkinkan aplikasi saling berkirim paket pesan secara asinkron tanpa harus terhubung langsung secara bersamaan.
* **Lamport Logical Clock:** Teknik mengurutkan kejadian di sistem terdistribusi memakai angka penghitung logis (*scalar clock*), jadi tidak perlu bergantung pada jam fisik masing-masing komputer.
* **Koordinasi Proses:** Pengaturan komunikasi, sinkronisasi, dan giliran akses sumber daya bersama antar proses agar tidak tabrakan (*race condition*) atau saling mengunci (*deadlock*).

---

## F. Soal Latihan dan Pembahasan

**1. Kenapa metode *Shared Memory* kurang cocok dijadikan cara komunikasi (IPC) utama di sistem terdistribusi?**

* **Jawaban:** Karena proses-proses dalam sistem terdistribusi berjalan di komputer atau *node* yang terpisah secara fisik, sehingga tidak bisa mengakses ruang memori yang sama secara langsung.
* **Pembahasan:** Konsep *shared memory* menuntut dua proses untuk membaca dan menulis di area memori fisik yang sama dalam satu sistem operasi. Di sistem terdistribusi yang komputernya terpisah-pisah, komunikasi wajib lewat jaringan menggunakan *Message Passing*, RPC, atau *Middleware*.

**2. Sebuah transaksi dicatat di *Sales Service*, diteruskan ke *Product Service*, lalu masuk ke *Invoice Service*. Jika awalnya nilai *Lamport Logical Clock* di semua layanan adalah `0`, berapa nilai *logical clock* di *Invoice Service* tepat setelah pesan diterima dan faktur dibuat?**


* **Jawaban:** `3`.
* **Pembahasan:**
* *Sales Service* mencatat transaksi (`0 + 1 = 1`), lalu mengirim pesan dengan angka `1` ke *Product Service*.
* *Product Service* membandingkan angka lokalnya (`0`) dengan pesan masuk (`1`), ambil yang paling besar (`1`), lalu tambah `1` menjadi `2`, kemudian kirim pesan bernilai `2` ke *Invoice Service*.
* *Invoice Service* membandingkan angka lokalnya (`0`) dengan pesan masuk (`2`), ambil yang paling besar (`2`), lalu tambah `1` sehingga nilainya menjadi `3` saat faktur selesai dibuat.



**3. Perangkat Internet of Things (IoT) biasanya punya kapasitas komputasi dan jaringan yang terbatas. Protokol standar MOM mana yang paling pas dipakai berdasarkan materi modul?**

* **Jawaban:** MQTT (*MQ Telemetry Transport*).
* **Pembahasan:** Pada pembahasan protokol MOM di modul, MQTT memang dirancang khusus untuk perangkat dengan sumber daya terbatas (*resource-constrained devices*), berbeda dengan AMQP yang lebih banyak dipakai untuk kebutuhan aplikasi skala *enterprise*.

**4. Apa tantangan utama di sistem terdistribusi yang berkaitan dengan perbedaan data antar *node*, dan bagaimana cara mengatasinya menurut modul?**

* **Jawaban:** Tantangannya disebut *Data inconsistency*, dan solusinya memakai protokol konsensus (*consensus protocol*) seperti Raft atau Paxos.
* **Pembahasan:** Saat banyak *node* saling bertukar dan mengubah data secara bersamaan, jeda waktu atau gangguan jaringan bisa membuat isi data di tiap *node* jadi tidak sama. Protokol konsensus membantu memastikan semua *node* sepakat pada satu kondisi data yang seragam.

Yang saya edit :

## D. Contoh Sederhana di Kehidupan Sehari-hari

* **Contoh Nyata dari Modul:**
* **Aplikasi Ojek Online (Gojek/Grab):** Saat kita memesan ojek, tampilan aplikasi di HP sebenarnya berkomunikasi dengan banyak layanan terpisah di balik layar—mulai dari pencari *driver*, pelacak posisi (*location tracing*), sampai penghitung tarif perjalanan.
* **Aplikasi Chat (WhatsApp):** Memakai jalur komunikasi *point-to-point* untuk mengirim pesan maupun *video call* di atas jaringan infrastruktur yang tersebar.
* **Game Online Multipemain (*Multiplayer Games*):** Butuh pertukaran data antar pemain (*node*) secara *real-time* supaya posisi dan kondisi permainan di layar semua pemain selalu sinkron.


* **Perumpamaan Komunikasi Sinkron vs Asinkron:**
* **Sinkron:** Anggap saja seperti sedang menelepon. Begitu kamu bertanya, kamu harus tetap memegang telepon menunggu lawan bicara menjawab sebelum bisa lanjut mengerjakan hal lain.
* **Asinkron:** Mirip seperti mengirim pesan singkat atau menaruh surat di kotak pos (*mailbox*). Setelah pesan terkirim, kamu bisa langsung ditinggal mengerjakan urusan lain, lalu baru membaca balasannya nanti saat pesan balasan masuk.

---

## E. Daftar Istilah Penting

* **Sistem Terdistribusi:** Sekumpulan komputer atau *node* yang berdiri sendiri-sendiri, tetapi saling terkoordinasi sehingga dari luar terlihat seperti satu sistem yang utuh.
* **Inter-Process Communication (IPC):** Cara antar proses saling bertukar data dan berkomunikasi, baik di dalam satu komputer yang sama maupun lintas *node* di jaringan terdistribusi.
* **Stub:** Bagian perantara di sisi klien dan server pada arsitektur RPC yang tugasnya membungkus data parameter pemanggilan fungsi beserta hasil eksekusinya agar bisa dikirim lewat jaringan.
* **Message-Oriented Middleware (MOM):** Jalur perantara yang memungkinkan aplikasi saling berkirim paket pesan secara asinkron tanpa harus terhubung langsung secara bersamaan.
* **Lamport Logical Clock:** Teknik mengurutkan kejadian di sistem terdistribusi memakai angka penghitung logis (*scalar clock*), jadi tidak perlu bergantung pada jam fisik masing-masing komputer.
* **Koordinasi Proses:** Pengaturan komunikasi, sinkronisasi, dan giliran akses sumber daya bersama antar proses agar tidak tabrakan (*race condition*) atau saling mengunci (*deadlock*).

---

## F. Soal Latihan dan Pembahasan

**1. Kenapa metode *Shared Memory* kurang cocok dijadikan cara komunikasi (IPC) utama di sistem terdistribusi?**

* **Jawaban:** Karena proses-proses dalam sistem terdistribusi berjalan di komputer atau *node* yang terpisah secara fisik, sehingga tidak bisa mengakses ruang memori yang sama secara langsung.
* **Pembahasan:** Konsep *shared memory* menuntut dua proses untuk membaca dan menulis di area memori fisik yang sama dalam satu sistem operasi. Di sistem terdistribusi yang komputernya terpisah-pisah, komunikasi wajib lewat jaringan menggunakan *Message Passing*, RPC, atau *Middleware*.

**2. Sebuah transaksi dicatat di *Sales Service*, diteruskan ke *Product Service*, lalu masuk ke *Invoice Service*. Jika awalnya nilai *Lamport Logical Clock* di semua layanan adalah `0`, berapa nilai *logical clock* di *Invoice Service* tepat setelah pesan diterima dan faktur dibuat?**

* **Jawaban:** `3`.
* **Pembahasan:**
* *Sales Service* mencatat transaksi (`0 + 1 = 1`), lalu mengirim pesan dengan angka `1` ke *Product Service*.
* *Product Service* membandingkan angka lokalnya (`0`) dengan pesan masuk (`1`), ambil yang paling besar (`1`), lalu tambah `1` menjadi `2`, kemudian kirim pesan bernilai `2` ke *Invoice Service*.
* *Invoice Service* membandingkan angka lokalnya (`0`) dengan pesan masuk (`2`), ambil yang paling besar (`2`), lalu tambah `1` sehingga nilainya menjadi `3` saat faktur selesai dibuat.



**3. Perangkat Internet of Things (IoT) biasanya punya kapasitas komputasi dan jaringan yang terbatas. Protokol standar MOM mana yang paling pas dipakai berdasarkan materi modul?**

* **Jawaban:** MQTT (*MQ Telemetry Transport*).
* **Pembahasan:** Pada pembahasan protokol MOM di modul, MQTT memang dirancang khusus untuk perangkat dengan sumber daya terbatas (*resource-constrained devices*), berbeda dengan AMQP yang lebih banyak dipakai untuk kebutuhan aplikasi skala *enterprise*.

**4. Apa tantangan utama di sistem terdistribusi yang berkaitan dengan perbedaan data antar *node*, dan bagaimana cara mengatasinya menurut modul?**

* **Jawaban:** Tantangannya disebut *Data inconsistency*, dan solusinya memakai protokol konsensus (*consensus protocol*) seperti Raft atau Paxos.
* **Pembahasan:** Saat banyak *node* saling bertukar dan mengubah data secara bersamaan, jeda waktu atau gangguan jaringan bisa membuat isi data di tiap *node* jadi tidak sama. Protokol konsensus membantu memastikan semua *node* sepakat pada satu kondisi data yang seragam.