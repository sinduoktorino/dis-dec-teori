## AI : Gemini AI


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

## Materi yang dirangkum
### A. Judul Materi

04: Konsistensi dan Replikasi pada Sistem Terdistribusi (Kode Mata Kuliah: FIF25002T, 3 SKS, Prodi Informatika, Fakultas Teknologi Informasi UTDI).

---

### B. Tujuan Pembelajaran Utama

* Memahami dan mampu menjelaskan konsep konsistensi dalam sistem terdistribusi.


* Mampu menjelaskan berbagai model konsistensi.


* Mampu menjelaskan konsep replikasi data.


* Mengetahui dan mampu menjelaskan berbagai protokol dan strategi replikasi.


* Mampu melakukan analisis studi kasus replikasi pada sistem nyata yang banyak digunakan di industri (seperti PostgreSQL 18 dan Apache Ignite 3).



---

### C. Poin-Poin Penting & Konsep Inti

**1. Konsep Dasar Konsistensi dan Teorema CAP**

* **Definisi Konsistensi:** Menjamin bahwa semua *node* dalam sistem terdistribusi memiliki data yang sama atau tampak sama pada waktu tertentu meskipun salinan data tersebar di banyak lokasi dan diubah secara bersamaan oleh proses berbeda.


* **Pentingnya Konsistensi:** Mencegah pengguna melihat versi data yang berbeda atau tidak mutakhir (*up-to-date*) bergantung pada server tempat data dibaca.


* **Teorema CAP:** Dalam kondisi jaringan nyata yang rentan mengalami pemutusan koneksi (*partition*), sebuah sistem tidak mungkin memenuhi ketiga aspek secara ideal sekaligus (*Consistency*, *Availability*, *Partition Tolerance*).


* *Consistency (C)*: Semua *node* memiliki data yang sama dan konsisten.


* *Availability (A)*: Data tetap tersedia untuk diakses kapan pun pengguna membutuhkannya.


* *Partition Tolerance (P)*: Sistem tetap beroperasi meskipun terjadi kegagalan atau putusnya koneksi antar komponen jaringan.


* Sistem harus memilih kompromi ketika partisi terjadi, yakni **AP** (tetap melayani transaksi meski data sementara tidak sinkron) atau **CP** (menolak transaksi sementara demi menjaga konsistensi data).



**2. Spektrum Model Konsistensi (Dari Kuat ke Lemah)**

* **Linearizability:** Varian terkuat dari *strong consistency*; setiap operasi tampak dieksekusi secara atomik dan langsung dalam urutan global *real-time* yang sama bagi semua *node* (seperti satu *node* tunggal), digunakan pada `etcd`, ZooKeeper, dan Google Spanner.


* **Strong Consistency:** Setelah data diperbarui (*write*), setiap pembacaan (*read*) berikutnya di seluruh *node* pasti langsung mendapatkan nilai terbaru, umumnya memakai protokol *Two-Phase Commit* atau Paxos.


* **Sequential Consistency:** Semua operasi tampak dieksekusi dalam urutan penulisan yang sama bagi semua *node*, meskipun tidak harus secara *real-time*.


* **Causal Consistency:** Operasi yang memiliki hubungan sebab-akibat wajib dijaga urutannya di semua *node*, sedangkan operasi yang independen boleh terlihat dalam urutan berbeda.


* **Read-Your-Writes Consistency:** Setelah pengguna menulis data, pembacaan berikutnya oleh pengguna itu sendiri dijamin melihat hasil tulisannya, meski pengguna lain belum tentu langsung melihatnya.


* **Monotonic Read Consistency:** Jika pengguna membaca data berulang kali, sistem menjamin ia tidak akan pernah melihat versi data yang lebih lama daripada versi yang sudah pernah dilihatnya sebelumnya.


* **Eventual Consistency (BASE):** Tidak menjamin kesamaan data seketika, tetapi seluruh replika akan menjadi konsisten setelah jangka waktu tertentu apabila tidak ada pembaruan baru. Menggunakan prinsip **BASE** (*Basically Available*, *Soft-state*, *Eventual consistency*), diterapkan pada Amazon DynamoDB dan Apache Cassandra.



**3. Trade-Off Latensi dan Konsistensi**

* Terdapat hubungan berbanding lurus antara tingkat konsistensi dan latensi: semakin tinggi konsistensi ($\text{Konsistensi}\uparrow$), semakin besar waktu respons atau latensi yang ditanggung pengguna ($\text{Latensi}\uparrow$) karena sistem menunggu sinkronisasi lintas jaringan. Sebaliknya, konsistensi lemah menghasilkan latensi rendah ($\text{Konsistensi}\downarrow \rightarrow \text{Latensi}\downarrow$).



**4. Pengertian, Jenis, dan Strategi Replikasi Data**

* **Pengertian & Tujuan:** Proses membuat dan memelihara salinan data yang sama di beberapa server untuk meningkatkan ketersediaan (*availability*), kinerja baca (*performance*), reliabilitas, dan skalabilitas beban baca (*read load*).


* **Jenis Replikasi:**
* *Master-Slave (Primary-Secondary)*: Satu *master* menangani penulisan (*write*), sedangkan *slave* hanya menangani pembacaan (*read*) (contoh: PostgreSQL *streaming replication*).


* *Multi-Master (Peer-to-Peer)*: Semua *node* dapat melakukan operasi baca dan tulis (contoh: PostgreSQL *logical replication*, Apache Cassandra, MongoDB, Apache Ignite).


* *Synchronous vs Asynchronous Replication*: Replikasi sinkron menunggu seluruh *node* selesai menulis sebelum transaksi tuntas (contoh: Google Spanner), sedangkan asinkron menyelesaikan transaksi di *master* terlebih dahulu baru mengirim pembaruan ke replika (contoh: MySQL *async mode*, DynamoDB).


* **Strategi Sinkronisasi Replika:**
* *Berdasarkan Waktu*: *Synchronous* (menunggu semua replika *commit*), *Semi-synchronous* (menunggu minimal satu replika menerima data, seperti pada MySQL), dan *Asynchronous* (tanpa menunggu replika).


* *Berdasarkan Arah*: *Master-slave*, *master-master* (peran dan sumber daya setara), serta *master-master asymmetric* (peran dan sumber daya berbeda).


* *Berdasarkan Cara*: *Pull-based* (replika memeriksa pembaruan secara periodik ke *source*), *Push-based* (*source* aktif mengirim pembaruan memakai CDC / *Change Data Capture* melalui WebSockets atau SSE), dan *Hybrid*.


* *Berdasarkan Penanganan Konflik*:
* **LWW (*Last Write Wins*):** Memilih pembaruan dengan *timestamp* terbaru dan mengabaikan lainnya.


* **Vector Clock:** Pengurutan kejadian berbasis vektor logis.


* **CRDT (*Conflict-free Replicated Data Type*):** Struktur data lokal di tiap *node* yang digabung secara deterministik tanpa konflik (contoh: Yjs pada editor kolaboratif seperti Google Docs).


* **OT (*Operational Transformation*):** Mentransformasikan indeks atau parameter operasi yang masuk berdasarkan riwayat perubahan lokal agar hasil akhir dokumen di setiap *node* identik.


**5. Protokol Replikasi (Tahapan & Rumus)**

* **Primary-based (Master-Slave):** Satu pusat tulis-baca, sisanya hanya baca.


* **Quorum-based:** Operasi tulis ($W$) dan baca ($R$) pada klaster berjumlah $N$ *node* dinyatakan sah apabila memenuhi syarat rumus $W + R > N$.


* *Langkah Kerja Quorum ($N=3, W=2, R=2$)*: (1) Klien mengirim perintah tulis secara paralel ke seluruh *node*; (2) Setelah minimal $W=2$ *node* membalas konfirmasi (ACK), penulisan dianggap berhasil meski 1 *node* terlambat; (3) Saat membaca, klien meminta data dari minimal $R=2$ *node* sehingga irisan pembacaan pasti mencakup minimal satu *node* yang menyimpan versi data terbaru.


* **State Machine Replication:** (1) Klien mengirim perintah ke *leader*; (2) *Leader* memberi nomor urutan, mencatat ke log, dan meneruskan ke seluruh replika; (3) Setelah menerima konfirmasi dari replika, perintah dinyatakan *commit*; (4) Seluruh replika mengeksekusi perintah dalam urutan log yang persis sama; (5) *Leader* mengembalikan hasil ke klien.


* **Gossip Protocol:** (1) Sebuah *node* mendeteksi pembaruan data atau status tetangga; (2) Setiap detik, *node* tersebut memilih 1–3 *peer* secara acak dan membagikan status terbarunya; (3) *Peer* penerima memperbarui status lokalnya lalu meneruskannya kembali ke *peer* acak lainnya hingga seluruh klaster memperoleh informasi yang sama (contoh: Apache Cassandra).


* **Chain Replication:** *Node* disusun berantai dari *head* hingga *tail*; klien mengirim operasi tulis (*write*) ke *head* yang meneruskannya secara berurutan ke *node* berikutnya hingga *tail* mengirimkan balasan konfirmasi (*ack*) kembali, sedangkan klien melakukan operasi baca (*read*) langsung dari *tail*.


---

## D. Contoh Sederhana di Kehidupan Sehari-hari

* **Transfer Uang Antar Rekening Bank:** Misalnya seorang nasabah mentransfer dana dari rekening A (yang datanya disimpan di Server 1) ke rekening B (di Server 2). Kalau Server 1 sudah memotong saldo rekening A tapi Server 2 belum sempat menambahkan saldonya ke rekening B, nasabah jelas belum bisa memakai uang itu karena kondisi sistemnya belum sinkron.
* **Toko Online Lintas Wilayah Saat Jaringan Putus:** Anggap saja Server A melayani pembeli di Indonesia Barat dan Server B melayani Indonesia Timur. Kalau sewaktu-waktu kabel jaringan antar pulau terputus (*partition*), sistem toko online harus ambil keputusan: tetap membiarkan pembeli checkout walau ada risiko jumlah stok selisih sementara (**AP**), atau menutup transaksi dulu sampai jaringan pulih supaya hitungan stok tetap akurat (**CP**).
* **Media Sosial dan Aplikasi Chat:**
* *Causal Consistency*: Komentar atau tombol reaksi pada sebuah postingan tidak boleh muncul duluan sebelum postingan utamanya tampil.
* *Read-Your-Writes*: Pesan WhatsApp yang baru saja kamu kirim langsung terlihat di layar HP-mu sendiri, walaupun orang yang dikirimi belum membacanya.
* *Monotonic Read*: Lini masa (*timeline*) media sosial tidak mundur menampilkan postingan-postingan lama setelah halamannya kamu muat ulang (*refresh*).



---

## E. Daftar Istilah Penting

* **Teorema CAP:** Prinsip yang menyatakan bahwa sistem terdistribusi tidak bisa menjamin *Consistency*, *Availability*, dan *Partition Tolerance* secara bersamaan begitu terjadi gangguan partisi jaringan.
* **Linearizability:** Tingkatan konsistensi paling ketat yang menjamin setiap operasi berjalan utuh dan langsung terlihat dalam urutan waktu *real-time* yang sama di seluruh sistem.
* **BASE:** Singkatan dari *Basically Available*, *Soft-state*, dan *Eventual consistency*, yaitu pendekatan perancangan sistem yang lebih mengutamakan ketersediaan layanan dan respons cepat ketimbang data yang langsung seragam seketika.
* **Replikasi Data:** Proses menggandakan dan merawat salinan data yang persis sama di beberapa *node* terpisah supaya sistem lebih andal, cepat diakses, dan selalu tersedia.
* **CRDT (*Conflict-free Replicated Data Type*):** Tipe struktur data yang dirancang khusus agar perubahan data dari berbagai *node* yang terpisah bisa digabungkan otomatis tanpa memicu bentrok.
* **Change Data Capture (CDC):** Mekanisme pada metode sinkronisasi *push-based* yang bertugas mendeteksi perubahan data di basis data utama (*source*) untuk langsung diteruskan ke salinan replikanya.

---

## F. Soal Latihan dan Pembahasan

**1. Sebuah klaster basis data terdistribusi punya $N = 5$ *node*. Kalau administrator menetapkan batas minimal konfirmasi penulisan $W = 3$, berapa jumlah minimal *node* pembacaan ($R$) supaya sistem tetap menjamin data terbaru terbaca pada protokol *Quorum-based*?**

* **Jawaban:** $R = 3$ *node*.
* **Pembahasan:** Aturan protokol *Quorum-based* mensyaratkan $W + R > N$. Dengan nilai $N = 5$ dan $W = 3$, perhitungannya menjadi $3 + R > 5 \Rightarrow R > 2$. Jadi, angka bulat terkecil yang memenuhi syarat adalah $R = 3$.

**2. Pada skenario edit dokumen bareng memakai *Operational Transformation* (OT), teks awalnya adalah `"abc"`. Pengguna A menyisipkan huruf `'x'` di indeks `0` (teksnya berubah jadi `"xabc"`), sementara di detik yang sama Pengguna B menghapus huruf `'c'` di indeks `2` (teksnya menjadi `"ab"`). Bagaimana cara OT membereskan konflik ini di layar Pengguna A supaya hasil teks akhir keduanya sama?**

* **Jawaban:** Perintah hapus dari Pengguna B diubah di sisi Pengguna A dari "hapus indeks 2" menjadi "hapus indeks 3", sehingga hasil teks akhirnya sama-sama `"xab"`.
* **Pembahasan:** Karena Pengguna A baru saja menyisipkan satu karakter di posisi paling depan (indeks `0`), otomatis posisi seluruh huruf aslinya bergeser satu langkah ke kanan. Kalau perintah dari Pengguna B langsung dijalankan mentah-mentah di indeks `2`, yang terhapus malah huruf `'b'` (`"xac"`). Makanya, indeks target harus digeser ke indeks `3` supaya huruf `'c'` yang terhapus dan menghasilkan `"xab"`.

**3. Ada dua pusat data yang berlokasi di Jakarta dan Yogyakarta. Sistemnya diatur supaya setiap kali ada perubahan data di Jakarta, sistem harus menunggu sampai salinannya sama persis di Yogyakarta sebelum mengirim konfirmasi sukses ke pengguna. Model konsistensi apa yang dipakai dan bagaimana dampaknya ke latensi?**

* **Jawaban:** Model *Strong Consistency* dengan dampak latensi yang tinggi (respons terasa lebih lambat).
* **Pembahasan:** Di model *Strong Consistency*, sistem wajib memastikan semua *node* menyimpan data yang identik sebelum membalas permintaan pengguna. Proses pengiriman data lewat jaringan untuk menyamakan isi kedua pusat data ini menambah waktu tunggu, yang akhirnya bikin latensi meningkat.

**4. Pada sistem *Chain Replication* yang berurutan dari *node* `head -> A -> B -> C -> tail`, ke *node* mana klien mengirim permintaan tulis (*write*) dan dari *node* mana klien membaca data (*read*)?**

* **Jawaban:** Permintaan tulis (*write*) dikirim ke *node* `head`, sedangkan pembacaan (*read*) diambil dari *node* `tail`.
* **Pembahasan:** Sesuai alur kerja *Chain Replication*, semua perintah *write* masuk lewat pintu depan yaitu `head` lalu diteruskan secara berantai sampai ke ujung di `tail`, sementara klien membaca data yang sudah sah terkonfirmasi langsung dari `tail`.

## Yang saya edit :

## D. Contoh Sederhana di Kehidupan Sehari-hari

* **Transfer Uang Antar Rekening Bank:** Misalnya seorang nasabah mentransfer dana dari rekening A (yang datanya disimpan di Server 1) ke rekening B (di Server 2). Kalau Server 1 sudah memotong saldo rekening A tapi Server 2 belum sempat menambahkan saldonya ke rekening B, nasabah jelas belum bisa memakai uang itu karena kondisi sistemnya belum sinkron.
* **Toko Online Lintas Wilayah Saat Jaringan Putus:** Anggap saja Server A melayani pembeli di Indonesia Barat dan Server B melayani Indonesia Timur. Kalau sewaktu-waktu kabel jaringan antar pulau terputus (*partition*), sistem toko online harus ambil keputusan: tetap membiarkan pembeli checkout walau ada risiko jumlah stok selisih sementara (**AP**), atau menutup transaksi dulu sampai jaringan pulih supaya hitungan stok tetap akurat (**CP**).
* **Media Sosial dan Aplikasi Chat:**
* *Causal Consistency*: Komentar atau tombol reaksi pada sebuah postingan tidak boleh muncul duluan sebelum postingan utamanya tampil.
* *Read-Your-Writes*: Pesan WhatsApp yang baru saja kamu kirim langsung terlihat di layar HP-mu sendiri, walaupun orang yang dikirimi belum membacanya.
* *Monotonic Read*: Lini masa (*timeline*) media sosial tidak mundur menampilkan postingan-postingan lama setelah halamannya kamu muat ulang (*refresh*).



---

## E. Daftar Istilah Penting

* **Teorema CAP:** Prinsip yang menyatakan bahwa sistem terdistribusi tidak bisa menjamin *Consistency*, *Availability*, dan *Partition Tolerance* secara bersamaan begitu terjadi gangguan partisi jaringan.
* **Linearizability:** Tingkatan konsistensi paling ketat yang menjamin setiap operasi berjalan utuh dan langsung terlihat dalam urutan waktu *real-time* yang sama di seluruh sistem.
* **BASE:** Singkatan dari *Basically Available*, *Soft-state*, dan *Eventual consistency*, yaitu pendekatan perancangan sistem yang lebih mengutamakan ketersediaan layanan dan respons cepat ketimbang data yang langsung seragam seketika.
* **Replikasi Data:** Proses menggandakan dan merawat salinan data yang persis sama di beberapa *node* terpisah supaya sistem lebih andal, cepat diakses, dan selalu tersedia.
* **CRDT (*Conflict-free Replicated Data Type*):** Tipe struktur data yang dirancang khusus agar perubahan data dari berbagai *node* yang terpisah bisa digabungkan otomatis tanpa memicu bentrok.
* **Change Data Capture (CDC):** Mekanisme pada metode sinkronisasi *push-based* yang bertugas mendeteksi perubahan data di basis data utama (*source*) untuk langsung diteruskan ke salinan replikanya.

---

## F. Soal Latihan dan Pembahasan

**1. Sebuah klaster basis data terdistribusi punya $N = 5$ *node*. Kalau administrator menetapkan batas minimal konfirmasi penulisan $W = 3$, berapa jumlah minimal *node* pembacaan ($R$) supaya sistem tetap menjamin data terbaru terbaca pada protokol *Quorum-based*?**

* **Jawaban:** $R = 3$ *node*.
* **Pembahasan:** Aturan protokol *Quorum-based* mensyaratkan $W + R > N$. Dengan nilai $N = 5$ dan $W = 3$, perhitungannya menjadi $3 + R > 5 \Rightarrow R > 2$. Jadi, angka bulat terkecil yang memenuhi syarat adalah $R = 3$.

**2. Pada skenario edit dokumen bareng memakai *Operational Transformation* (OT), teks awalnya adalah `"abc"`. Pengguna A menyisipkan huruf `'x'` di indeks `0` (teksnya berubah jadi `"xabc"`), sementara di detik yang sama Pengguna B menghapus huruf `'c'` di indeks `2` (teksnya menjadi `"ab"`). Bagaimana cara OT membereskan konflik ini di layar Pengguna A supaya hasil teks akhir keduanya sama?**

* **Jawaban:** Perintah hapus dari Pengguna B diubah di sisi Pengguna A dari "hapus indeks 2" menjadi "hapus indeks 3", sehingga hasil teks akhirnya sama-sama `"xab"`.
* **Pembahasan:** Karena Pengguna A baru saja menyisipkan satu karakter di posisi paling depan (indeks `0`), otomatis posisi seluruh huruf aslinya bergeser satu langkah ke kanan. Kalau perintah dari Pengguna B langsung dijalankan mentah-mentah di indeks `2`, yang terhapus malah huruf `'b'` (`"xac"`). Makanya, indeks target harus digeser ke indeks `3` supaya huruf `'c'` yang terhapus dan menghasilkan `"xab"`.

**3. Ada dua pusat data yang berlokasi di Jakarta dan Yogyakarta. Sistemnya diatur supaya setiap kali ada perubahan data di Jakarta, sistem harus menunggu sampai salinannya sama persis di Yogyakarta sebelum mengirim konfirmasi sukses ke pengguna. Model konsistensi apa yang dipakai dan bagaimana dampaknya ke latensi?**

* **Jawaban:** Model *Strong Consistency* dengan dampak latensi yang tinggi (respons terasa lebih lambat).
* **Pembahasan:** Di model *Strong Consistency*, sistem wajib memastikan semua *node* menyimpan data yang identik sebelum membalas permintaan pengguna. Proses pengiriman data lewat jaringan untuk menyamakan isi kedua pusat data ini menambah waktu tunggu, yang akhirnya bikin latensi meningkat.

**4. Pada sistem *Chain Replication* yang berurutan dari *node* `head -> A -> B -> C -> tail`, ke *node* mana klien mengirim permintaan tulis (*write*) dan dari *node* mana klien membaca data (*read*)?**

* **Jawaban:** Permintaan tulis (*write*) dikirim ke *node* `head`, sedangkan pembacaan (*read*) diambil dari *node* `tail`.
* **Pembahasan:** Sesuai alur kerja *Chain Replication*, semua perintah *write* masuk lewat pintu depan yaitu `head` lalu diteruskan secara berantai sampai ke ujung di `tail`, sementara klien membaca data yang sudah sah terkonfirmasi langsung dari `tail`.