## Ai : Gemini Ai


## Prompt: 

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

Fault Tolerance (Kode Mata Kuliah: FIF25002T, 3 SKS, Prodi Informatika, Fakultas Teknologi Informasi UTDI).

---

### B. Tujuan Pembelajaran Utama

* Memahami dan mampu menjelaskan alasan perlunya *fault tolerance* pada sistem terdistribusi dan terdesentralisasi.


* Memahami dan mampu menjelaskan pengertian dari *fault tolerance* serta *fault tolerant systems*.


* Memahami dan mampu menjelaskan berbagai jenis *fault* serta klasifikasinya berdasarkan sumbernya.


* Memahami berbagai *design patterns* untuk mencapai *fault tolerance* serta dapat mengaplikasikannya menggunakan Python.


* Memahami bagaimana berbagai bahasa pemrograman serta peranti pengembangan mengimplementasikan *fault tolerance*.


---

### C. Poin-Poin Penting & Konsep Inti

**1. Konsep Dasar dan Arti Penting *Fault Tolerance***

* **Definisi:** *Fault tolerance* adalah kemampuan suatu sistem untuk tetap mempertahankan operasional secara tepat meskipun terjadi kegagalan atau kesalahan pada satu maupun beberapa komponennya.


* **Urgensi:** Sangat krusial bagi sistem dengan tingkat ketersediaan tinggi (*high availability*), *mission-critical*, maupun *life-critical system*. Pada sistem terdistribusi dan terdesentralisasi yang memiliki banyak komponen dan koneksi jaringan, semakin kritikal sebuah aplikasi maka semakin tinggi tuntutan agar layanan terus berfungsi dengan baik meskipun terjadi gangguan.



**2. Jenis-Jenis *Fault* dan Klasifikasinya**

* **Empat Jenis *Fault* Berdasarkan Perilaku:**
* *Transient Fault*: Kegagalan yang bersifat sementara, misalnya akibat sambaran petir.


* *Intermittent Fault*: Kegagalan yang muncul dan hilang secara berulang, misalnya akibat panas berlebih (*overheat*) pada perangkat keras.


* *Permanent Fault*: Kegagalan yang bersifat tetap dan tidak pulih dengan sendirinya.


* *Byzantine Fault*: Kegagalan di mana komponen memberikan hasil yang acak, tidak konsisten, atau bertindak menyimpang (diilustrasikan dengan analogi *traitor* atau pengkhianat dalam jaringan).


* **Tiga Klasifikasi *Fault* Berdasarkan Sumber:**
* *Hardware Faults*: Gangguan perangkat keras seperti *disk crash* dan *power failure*.


* *Software Faults*: Gangguan perangkat lunak seperti *bugs*, *memory leak*, dan *race condition*.


* *Communication Faults*: Gangguan komunikasi jaringan seperti *packet loss* dan *network partition*.

**3. Lima Teknik Utama dan Pola Desain (*Design Patterns*) *Fault Tolerance***

* **Redundansi dan Replikasi:** Menyediakan lebih dari satu sumber daya dengan mereplikasinya ke berbagai *node* guna menghilangkan titik tunggal kegagalan (*single point of failure*).


* **Load Balancing:** Menskalakan aplikasi menjadi beberapa *instance* proses aktif dan mendistribusikan beban menggunakan *load balancer* seperti HAProxy atau Nginx.


* **Checkpointing and Rollback Recovery:** *Checkpointing* menyimpan status sistem secara berkala ke media penyimpanan, sedangkan *rollback recovery* mengembalikan sistem ke titik *checkpoint* terakhir saat terjadi kegagalan agar pemulihan tidak dimulai dari awal serta meminimalkan kehilangan data dan waktu pemrosesan.


* **Heartbeat and Failure Detection:** Komponen saling mengirimkan sinyal periodik (*heartbeat*) sebagai tanda masih aktif; apabila pemantau tidak menerima sinyal dalam batas waktu tertentu, komponen tersebut dinyatakan gagal dan tidak responsif (dapat dikombinasikan dengan pustaka pengulangan koneksi seperti `tenacity` di Python).


* **Circuit Breaker (Tahapan State Machine Step-by-Step):**
1. **Status *Closed*:** Permintaan ke layanan eksternal diizinkan mengalir seperti biasa sambil terus dipantau tingkat kegagalannya.


2. **Transisi ke *Open*:** Jika jumlah kegagalan mencapai ambang batas tertentu (misalnya `fail_max=4` pada pustaka Python `pybreaker`), pemutus sirkuit terbuka dan langsung memblokir permintaan berikutnya demi mencegah kegagalan berantai serta memberi waktu layanan untuk pulih.


3. **Transisi ke *Half-Open*:** Setelah melewati batas waktu tunggu (`reset_timeout`), sirkuit masuk ke status *half-open* dan mengizinkan sejumlah kecil permintaan pengujian untuk memeriksa apakah layanan sudah pulih.


4. **Evaluasi Pemulihan:** Jika permintaan pengujian berhasil, sirkuit kembali ke status *closed*; jika masih gagal, sirkuit kembali ke status *open*.


* **Consensus and Coordination:** *Consensus* adalah proses beberapa *node* menyepakati satu nilai, status, atau urutan operasi meski ada kegagalan/penundaan jaringan (contoh: algoritma Raft), sedangkan *coordination* adalah praktik mengelola interaksi antar *node* agar bekerja sama secara konsisten.


**4. *Actor Model* dan Implementasi pada Bahasa Pemrograman**

* **Actor Model untuk Supervisi Proses:** Setiap unit komputasi (*actor*) memiliki kotak surat (*mailbox*) masing-masing untuk berkomunikasi melalui pesan dan diatur dalam hierarki pengawasan (*top-level supervisor* dan *supervisor*). *Supervisor* memantau status hidup (*check if alive*) dari *actor* di bawahnya dan melakukan tindakan pemulihan seperti *restart* jika ada *actor* yang gagal.


* **Dukungan Bahasa dan Pustaka:**
* *Dukungan Bawaan (Built-in)*: Erlang dan Elixir memiliki dukungan bawaan untuk *actor model* serta pola *Supervisor-Worker*, sedangkan Pony dirancang khusus untuk *Actor model*.


* *Pustaka Pihak Ketiga (3rd Party)*: Python menggunakan Xoscar, `tenacity`, dan `pybreaker`; Java menggunakan Apache Pekko (untuk *actor model* dan *Supervisor-Worker*) serta Resilience4j.


---

## D. Contoh Sederhana di Kehidupan Sehari-hari

* **Pemilihan *Leader* Database (*Database Leader Election*):** Di dalam klaster database yang punya banyak salinan, algoritma konsensus seperti Raft dipakai untuk memilih satu server utama (*leader*) yang bertugas menangani semua proses penulisan data (*write*).


* **Update File di *Cloud Storage*:** Waktu kamu mengedit atau menyimpan ulang file di layanan seperti Google Drive, sistemnya memakai mekanisme konsensus supaya perubahan itu disetujui (*commit*) oleh mayoritas server dulu sebelum dianggap sah dan disalin ke semua server lain.


* **Aset Kripto dan *Blockchain*:** Jaringan *blockchain* mengandalkan konsensus terdistribusi untuk mengecek dan mengesahkan setiap transaksi tanpa perlu campur tangan satu bos atau otoritas pusat.


* **Sekring Listrik Rumah (*Circuit Breaker*):** Cara kerjanya persis seperti sekring listrik di rumah yang langsung memutus arus saat ada korsleting biar barang elektronik lain tidak ikut terbakar. Di arsitektur *microservices*, pola *circuit breaker* langsung memblokir permintaan ke layanan yang sedang *error* sampai layanan itu pulih kembali.


---

## E. Daftar Istilah Penting

* **Fault Tolerance:** Kemampuan sistem untuk tetap berjalan normal dan akurat walaupun ada satu atau beberapa komponen di dalamnya yang rusak atau gagal.


* **Byzantine Fault:** Jenis gangguan saat suatu komponen sistem bertingkah aneh dan mengeluarkan hasil yang acak atau berbeda-beda ke tiap penerima.


* **Checkpointing:** Kebiasaan sistem menyimpan kondisi (*state*) terbarunya secara berkala ke penyimpanan permanen, supaya nanti gampang dipulihkan kalau sewaktu-waktu terjadi gangguan.


* **Heartbeat:** Sinyal rutin yang dikirim antar komponen di dalam sistem sebagai tanda kalau komponen pengirim masih hidup dan aktif bekerja.


* **Circuit Breaker:** Pola desain pada *microservices* dengan tiga status (*closed*, *open*, dan *half-open*) yang tugasnya menahan sementara aliran permintaan ke layanan yang bermasalah agar tidak merembet jadi kegagalan berantai.


* **Consensus:** Proses saat beberapa *node* berunding untuk menyepakati satu nilai, status, atau urutan proses yang sama, meskipun kondisi jaringan sedang terganggu atau telat.

---

### F. Soal Latihan beserta Kunci Jawaban & Pembahasannya

**1. Sebuah server mengalami gangguan koneksi yang muncul dan hilang secara berulang setiap kali suhu ruangan meningkat dan menyebabkan perangkat keras *overheat*. Termasuk ke dalam jenis *fault* apakah kejadian tersebut?**

* **Kunci Jawaban:** *Intermittent Fault*.


* **Pembahasan:** Modul mendefinisikan *intermittent fault* sebagai jenis kegagalan yang muncul dan hilang secara berulang, dengan contoh spesifik berupa *overheat* pada perangkat keras, berbeda dengan *transient fault* yang terjadi sekali sementara (misalnya akibat petir) maupun *permanent fault* yang bersifat permanen.



**2. Sebuah layanan pemantau dalam klaster mikroservis menggunakan pola *Circuit Breaker* dengan konfigurasi `fail_max = 4` dan `reset_timeout = 20`. Apa yang terjadi pada status *circuit breaker* tepat setelah 4 permintaan berturut-turut mengalami kegagalan, dan apa tujuannya?**

* **Kunci Jawaban:** Status *circuit breaker* berubah dari *closed* menjadi *open*, yang bertujuan menolak permintaan berikutnya secara langsung untuk mencegah kegagalan berantai serta memberi waktu bagi layanan yang bermasalah untuk pulih.


* **Pembahasan:** Saat dalam status *closed*, *circuit breaker* memantau jumlah kegagalan. Begitu ambang batas kegagalan (`fail_max = 4`) tercapai, sirkuit berpindah ke status *open* dan memblokir panggilan selama durasi `reset_timeout` (20 detik) sebelum mencoba masuk ke status *half-open*.


**3. Dalam arsitektur *Actor Model*, bagaimana mekanisme penanganan kegagalan dilakukan ketika salah satu *worker actor* mengalami *crash* saat memproses pesan di *mailbox*-nya?**

* **Kunci Jawaban:** *Supervisor actor* yang membawahi *worker actor* tersebut akan mendeteksi status kegagalan dan melakukan tindakan pemulihan berupa *restart* terhadap *actor* yang gagal.


* **Pembahasan:** *Actor Model* menyusun proses secara hierarkis dengan *top-level supervisor* dan *supervisor* di bawahnya yang secara aktif memeriksa status hidup (*check if alive*) dari setiap *actor* dan me-*restart* komponen yang bermasalah.


**4. Sebutkan tiga klasifikasi *fault* berdasarkan sumbernya beserta masing-masing dua contoh yang tercantum dalam modul!**

* **Kunci Jawaban:**
1. *Hardware Faults*: *disk crash* dan *power failure*.


2. *Software Faults*: *bugs*, *memory leak*, dan *race condition*.


3. *Communication Faults*: *packet loss* dan *network partition*.

* **Pembahasan:** Sumber kegagalan dalam sistem informasi terdistribusi dikelompokkan menjadi tiga lapisan utama tersebut agar perancang sistem dapat menentukan teknik mitigasi yang sesuai, seperti replikasi penyimpanan untuk *hardware fault* atau *retry* dan konsensus untuk *communication fault*.


## Yang diedit :

## D. Contoh Sederhana di Kehidupan Sehari-hari

* **Pemilihan *Leader* Database (*Database Leader Election*):** Di dalam klaster database yang punya banyak salinan, algoritma konsensus seperti Raft dipakai untuk memilih satu server utama (*leader*) yang bertugas menangani semua proses penulisan data (*write*).


* **Update File di *Cloud Storage*:** Waktu kamu mengedit atau menyimpan ulang file di layanan seperti Google Drive, sistemnya memakai mekanisme konsensus supaya perubahan itu disetujui (*commit*) oleh mayoritas server dulu sebelum dianggap sah dan disalin ke semua server lain.


* **Aset Kripto dan *Blockchain*:** Jaringan *blockchain* mengandalkan konsensus terdistribusi untuk mengecek dan mengesahkan setiap transaksi tanpa perlu campur tangan satu bos atau otoritas pusat.


* **Sekring Listrik Rumah (*Circuit Breaker*):** Cara kerjanya persis seperti sekring listrik di rumah yang langsung memutus arus saat ada korsleting biar barang elektronik lain tidak ikut terbakar. Di arsitektur *microservices*, pola *circuit breaker* langsung memblokir permintaan ke layanan yang sedang *error* sampai layanan itu pulih kembali.


---

## E. Daftar Istilah Penting

* **Fault Tolerance:** Kemampuan sistem untuk tetap berjalan normal dan akurat walaupun ada satu atau beberapa komponen di dalamnya yang rusak atau gagal.


* **Byzantine Fault:** Jenis gangguan saat suatu komponen sistem bertingkah aneh dan mengeluarkan hasil yang acak atau berbeda-beda ke tiap penerima.


* **Checkpointing:** Kebiasaan sistem menyimpan kondisi (*state*) terbarunya secara berkala ke penyimpanan permanen, supaya nanti gampang dipulihkan kalau sewaktu-waktu terjadi gangguan.


* **Heartbeat:** Sinyal rutin yang dikirim antar komponen di dalam sistem sebagai tanda kalau komponen pengirim masih hidup dan aktif bekerja.


* **Circuit Breaker:** Pola desain pada *microservices* dengan tiga status (*closed*, *open*, dan *half-open*) yang tugasnya menahan sementara aliran permintaan ke layanan yang bermasalah agar tidak merembet jadi kegagalan berantai.


* **Consensus:** Proses saat beberapa *node* berunding untuk menyepakati satu nilai, status, atau urutan proses yang sama, meskipun kondisi jaringan sedang terganggu atau telat.

