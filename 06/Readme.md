## AI : Gemini AI

## Pormpt : 

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


## Rangkuman Materi 06

### A. Judul Materi

Distributed File System (Kode Mata Kuliah: FIF25002T, 3 SKS, Prodi Informatika, Fakultas Teknologi Informasi UTDI).

---

### B. Tujuan Pembelajaran Utama

* Memahami dan mampu menjelaskan pengertian *file system* (FS), berbagai jenisnya, serta cara kerjanya secara umum.


* Memahami dan mampu menjelaskan pengertian *Distributed File System* (DFS), berbagai jenis DFS, serta cara kerjanya secara umum.


* Mampu melakukan instalasi salah satu DFS (seperti HDFS) guna memahami mekanisme kerjanya secara langsung.


* Mampu memahami dan menjelaskan *cloud storage* serta hubungannya dengan DFS.


* Mampu melakukan instalasi salah satu *object storage* sebagai implementasi *cloud storage*.


---

### C. Poin-Poin Penting & Konsep Inti

**1. Konsep Dasar *File System* (FS) dan Cara Kerjanya**

* **Pengertian FS:** Metode yang digunakan oleh sistem operasi untuk mengelola dan mengatur berkas (*file*) pada media penyimpanan seperti *harddisk*, USB *flashdisk*, maupun SSD.


* **Contoh Berdasarkan Sistem Operasi:**
* Linux: `ext4`, `XFS`, `btrfs`, `ReiserFS`.


* DOS/Windows: `FAT 16`, `FAT 32`, `NTFS`.


* Mac: `APFS` (*Apple File System*).


* **FS vs Hirarki FS:** Hirarki FS adalah pengaturan *files* dan direktori pada suatu sistem operasi (misalnya standar *Filesystem Hierarchy Standard* / FHS 3.0 pada sistem mirip UNIX seperti `/bin`, `/boot`, `/dev`, `/etc`, `/home`, `/lib`, `/usr`, `/var`), sehingga pengguna cukup melihat struktur direktori tanpa mempedulikan tipe *file system* di bawahnya.


* **Alur Kerja Akses FS (Step-by-Step):**
1. Aplikasi di *User Space* (seperti *System Utilities*, *Shell/CLI*, atau *GUI Applications*) mengirimkan permintaan operasi berkas (misalnya `read()` atau `write()`).


2. Permintaan diteruskan melalui *System Call Interface* menuju *Virtual File System* (VFS) di dalam *Kernel Space*.


3. Kernel memanggil *driver* *file system* yang sesuai (misalnya EXT4 atau XFS).


4. *Device drivers* mengakses perangkat keras media penyimpanan fisik (*Disk Storage*).


**2. *Distributed File System* (DFS) dan Perbandingan Arsitektur Penyimpanan**

* **Pengertian DFS:** Sistem abstraksi perangkat lunak yang terkoordinasi dari sekumpulan media penyimpanan di banyak mesin (*node*) yang menutupi heterogenitas, kegagalan, dan konkurensi. Bagi pengguna, kumpulan media penyimpanan tersebut tampak sebagai satu kesatuan penyimpanan tunggal (*Global Namespace*) yang andal dan berkinerja tinggi.


* **Perbedaan DAS, NAS, SAN, dan DFS:**
* *DAS (Direct-Attached Storage)*: Media penyimpanan yang terhubung langsung ke satu komputer/server lokal (seperti partisi `/dev/nvme0n1p2`).


* *NAS (Network-Attached Storage)*: Penyimpanan bersama berbasis *file system* melalui jaringan bersama (*shared network*) dengan manajemen yang lebih mudah.


* *SAN (Storage Area Network)*: Penyimpanan bersama berbasis *block storage* melalui jaringan khusus (*dedicated network* menggunakan *SAN switch*) yang berkecepatan tinggi namun mahal; umumnya dipakai sebagai *backend* basis data besar, penyuntingan audio-video, dan virtualisasi skala besar, serta tidak disarankan sebagai dasar DFS karena DFS lebih mengarah pada penggunaan DAS di setiap *node*.


* **Contoh DFS Umum:** Google File System (GFS), Colossus (pengganti GFS untuk YouTube, Gmail, Google Docs), CephFS, Gluster, HDFS (*Hadoop DFS*), dan Lustre.


**3. Studi Kasus: *Hadoop Distributed File System* (HDFS)**

* **Karakteristik:** Bersifat *open source*, *scalable*, terdistribusi, dan *fault-tolerant* untuk menyimpan *dataset* berukuran besar di atas klaster *commodity hardware* (perangkat keras massal berbiaya murah dan mudah dipertukarkan).


* **Arsitektur & Cara Kerja HDFS (Step-by-Step):**
1. Berkas berukuran besar dipecah menjadi blok-blok (*blocks*), didistribusikan ke berbagai server penyimpanan (*DataNodes* di berbagai *Rack*), dan direplikasi (misalnya 3 replika) demi mencapai *high-availability*.


2. *NameNode* (*Master*) mengelola *metadata* (nama berkas, lokasi blok, jumlah replika) dan mengatur operasi blok (*Block ops*), sedangkan *Resource Manager* mengelola sumber daya klaster.


3. Saat membaca (*Client Read*), klien menghubungi *NameNode* untuk operasi *metadata* guna mengetahui lokasi blok, lalu membaca blok data langsung dari *DataNode* terdekat.


4. Saat menulis (*Client Write*), klien menulis blok data ke *DataNode* pada satu *rack* dan sistem mereplikasikannya ke *DataNode* lain (termasuk lintas *rack*).


* **Persyaratan Instalasi Apache Hadoop 3.5.0:** Menggunakan JDK 17 untuk server (dan JDK 17 atau 21 untuk *client*), `pdsh`, serta layanan `ssh`/`sshd` yang aktif.


**4. *Cloud Storage*, Tipe Penyimpanan, dan Relasinya dengan DFS**

* **Pengertian *Cloud Storage*:** Model penyimpanan data daring yang dikelola secara jarak jauh dalam suatu *pool* logis di atas infrastruktur server milik penyedia *cloud* dan diakses melalui jaringan internet (contoh: Amazon S3, Azure Blob Storage, Google Cloud Storage).


* **Relasi *Cloud Storage* dengan DFS:** *Cloud storage* berfungsi sebagai tempat penyimpanan fisik/objeknya, sedangkan DFS bertindak sebagai lapisan pengorganisasian dan operasi *file system*. Sebagai contoh, HDFS dapat dikonfigurasi melalui berkas `core-site.xml` menggunakan properti `fs.s3a.access.key`, `fs.s3a.secret.key`, dan `fs.s3a.endpoint` untuk mengelola data yang tersimpan di Amazon S3.


* **Tiga Tipe *Cloud Storage*:**
* *Block Storage*: Menggunakan transpor FC atau iSCSI dengan antarmuka *Direct Attached* atau SAN; memiliki latensi rendah dan paling cocok untuk data terstruktur.


* *File Storage*: Menggunakan transpor TCP/IP dengan antarmuka NFS atau SMB; memiliki performa baik untuk berbagi berkas (*file sharing*) dan *global file locking*.


* *Object Storage*: Menggunakan transpor TCP/IP dengan antarmuka HTTP/REST (seperti S3); mudah diskalakan tanpa batas dan dapat diakses lintas LAN maupun WAN.


* **Studi Kasus Perangkat Lunak Penyimpanan *Cloud-Native*:** Ceph (penyimpanan terdistribusi terpadu), CubeFS (penyimpanan data tidak terstruktur yang mendukung antarmuka S3, HDFS, dan POSIX dengan komponen *Master*, *Metadata Subsystem*, *Object Subsystem*, dan *Data Subsystem*), RustFS (pengganti MinIO & S3 berkinerja tinggi tanpa *garbage collection*), PGSTY SILO (*fork* komunitas MinIO yang kompatibel dengan S3 pada port `:9000` dan konsol `:9001`), serta Rook (orkestrator penyimpanan *cloud-native* untuk Kubernetes).

---

### D. Analogi atau Contoh Sederhana dalam Kehidupan Sehari-hari

* **Layanan Ekosistem Google (Colossus):** Saat Anda membuka lampiran di Gmail, menonton video di YouTube, atau menyunting dokumen di Google Docs, seluruh data tersebut disimpan di atas infrastruktur *Distributed File System* bernama Colossus yang menyatukan ribuan server menjadi satu ruang penyimpanan terpadu.


* **Penggabungan Penyimpanan Lintas Lokasi (*Global Namespace*):** Bayangkan Anda memiliki beberapa lemari arsip terpisah di kantor pusat (NAS 1 dan NAS 2), kantor cabang (Linux NFS dan Windows SMB), serta gudang sewaan (*Public Cloud*). DFS bertindak seperti satu katalog resepsionis terpusat (*Global Namespace*) sehingga pegawai cukup mencari nama berkas di satu daftar tanpa perlu tahu di lemari atau gedung mana berkas fisik tersebut berada.

---

## E. Daftar Istilah Penting

* **File System (FS):** Cara sistem operasi mengatur, menyimpan, dan mengelola file di dalam media penyimpanan fisik seperti harddisk atau SSD.


* **Distributed File System (DFS):** Lapisan perangkat lunak yang menyatukan media penyimpanan dari banyak komputer (*node*) di jaringan agar terlihat dan bekerja layaknya satu ruang penyimpanan tunggal yang terkoordinasi, andal, dan tahan gangguan.


* **Commodity Hardware:** Perangkat keras komputer standar yang diproduksi massal, harganya terjangkau, gampang diganti, dan banyak dijual di pasaran untuk menyusun klaster komputasi seperti HDFS.


* **NameNode:** Server pusat (*master*) di arsitektur HDFS yang mengurus semua *metadata* file, mulai dari nama folder, letak blok data, sampai jumlah salinan replikanya.


* **DataNode:** Server pekerja (*slave*) di klaster HDFS yang menyimpan potongan blok data aslinya serta menangani permintaan baca-tulis dari klien maupun proses penyalinan antar *node*.


* **Object Storage:** Model penyimpanan cloud yang diakses lewat jalur HTTP/REST (contohnya Amazon S3), dibuat agar kapasitasnya bisa diperbesar tanpa batas untuk menampung data tidak terstruktur lewat jaringan LAN maupun WAN.


---

## F. Soal Latihan dan Pembahasan

**1. Apa beda mendasar antara *File System* (FS) dengan *Hirarki File System* di suatu sistem operasi?**

* **Jawaban:** *File system* itu metode teknis yang dipakai sistem operasi untuk mengurus file di media penyimpanan (misalnya `ext4` atau `NTFS`), sedangkan *hirarki file system* adalah susunan folder dan file yang langsung dilihat pengguna (seperti `/bin`, `/etc`, `/home` di standar FHS).


* **Pembahasan:** Sehari-hari, pengguna dan aplikasi cukup berurusan dengan susunan folder tanpa perlu pusing memikirkan jenis *file system* apa yang memformat harddisk di baliknya. Semua perbedaan *driver* FS itu sudah dijembatani otomatis oleh *Virtual File System* (VFS) di dalam kernel.


**2. Kenapa *Storage Area Network* (SAN) tidak disarankan sebagai tempat penyimpanan utama saat membangun *Distributed File System* (DFS)?**

* **Jawaban:** Karena SAN menawarkan penyimpanan berbasis blok yang mahal lewat jaringan khusus untuk *backend* database besar atau virtualisasi, sementara DFS sendiri sudah bekerja di level perangkat lunak dan lebih pas memakai penyimpanan lokal (*Direct-Attached Storage* / DAS) di tiap *node*.


* **Pembahasan:** Tujuan utama DFS memang menggabungkan penyimpanan lokal murah (*commodity hardware* / DAS) dari banyak *node* menjadi satu kesatuan yang hemat biaya dan tahan banting. Jadi, memakai SAN yang berbiaya tinggi justru kurang pas secara konsep arsitektur.


**3. Jelaskan tugas masing-masing dari *NameNode* dan *DataNode* di arsitektur *Hadoop Distributed File System* (HDFS)!**

* **Jawaban:** *NameNode* bertugas sebagai *master* yang mencatat *metadata* (nama file, posisi blok, dan jumlah replika), sedangkan *DataNode* bertindak sebagai *slave* yang menyimpan blok data fisiknya sekaligus melayani proses baca, tulis, dan replikasi.


* **Pembahasan:** Waktu klien mau membaca file di HDFS, langkah pertamanya adalah bertanya dulu ke *NameNode* untuk mengecek di mana lokasi blok datanya berada. Setelah tahu posisinya, klien baru mengambil isi datanya langsung dari *DataNode* terkait.


**4. Sebuah instansi butuh layanan *cloud storage* yang kapasitasnya gampang diperbesar tanpa batas dan bisa diakses lewat antarmuka HTTP/REST lintas jaringan WAN. Tipe *cloud storage* mana yang paling tepat dipilih, dan sebutkan dua contoh software *open-source* di modul yang mendukung antarmuka S3?**

* **Jawaban:** Tipe *Object Storage*; contoh perangkat lunak *open-source* dari modul antara lain CubeFS, RustFS, PGSTY SILO, atau Ceph.


* **Pembahasan:** Merujuk pada tabel perbandingan tipe penyimpanan, *Object Storage* memakai jalur TCP/IP dengan antarmuka HTTP/REST (standar S3) dan memang dirancang agar mudah diskalakan tanpa batas lewat LAN maupun WAN—berbeda dengan *Block Storage* (FC/iSCSI) dan *File Storage* (NFS/SMB).


## Yang saya edit:

## E. Daftar Istilah Penting

* **File System (FS):** Cara sistem operasi mengatur, menyimpan, dan mengelola file di dalam media penyimpanan fisik seperti harddisk atau SSD.


* **Distributed File System (DFS):** Lapisan perangkat lunak yang menyatukan media penyimpanan dari banyak komputer (*node*) di jaringan agar terlihat dan bekerja layaknya satu ruang penyimpanan tunggal yang terkoordinasi, andal, dan tahan gangguan.


* **Commodity Hardware:** Perangkat keras komputer standar yang diproduksi massal, harganya terjangkau, gampang diganti, dan banyak dijual di pasaran untuk menyusun klaster komputasi seperti HDFS.


* **NameNode:** Server pusat (*master*) di arsitektur HDFS yang mengurus semua *metadata* file, mulai dari nama folder, letak blok data, sampai jumlah salinan replikanya.


* **DataNode:** Server pekerja (*slave*) di klaster HDFS yang menyimpan potongan blok data aslinya serta menangani permintaan baca-tulis dari klien maupun proses penyalinan antar *node*.


* **Object Storage:** Model penyimpanan cloud yang diakses lewat jalur HTTP/REST (contohnya Amazon S3), dibuat agar kapasitasnya bisa diperbesar tanpa batas untuk menampung data tidak terstruktur lewat jaringan LAN maupun WAN.

---

## F. Soal Latihan dan Pembahasan

**1. Apa beda mendasar antara *File System* (FS) dengan *Hirarki File System* di suatu sistem operasi?**

* **Jawaban:** *File system* itu metode teknis yang dipakai sistem operasi untuk mengurus file di media penyimpanan (misalnya `ext4` atau `NTFS`), sedangkan *hirarki file system* adalah susunan folder dan file yang langsung dilihat pengguna (seperti `/bin`, `/etc`, `/home` di standar FHS).


* **Pembahasan:** Sehari-hari, pengguna dan aplikasi cukup berurusan dengan susunan folder tanpa perlu pusing memikirkan jenis *file system* apa yang memformat harddisk di baliknya. Semua perbedaan *driver* FS itu sudah dijembatani otomatis oleh *Virtual File System* (VFS) di dalam kernel.



**2. Kenapa *Storage Area Network* (SAN) tidak disarankan sebagai tempat penyimpanan utama saat membangun *Distributed File System* (DFS)?**

* **Jawaban:** Karena SAN menawarkan penyimpanan berbasis blok yang mahal lewat jaringan khusus untuk *backend* database besar atau virtualisasi, sementara DFS sendiri sudah bekerja di level perangkat lunak dan lebih pas memakai penyimpanan lokal (*Direct-Attached Storage* / DAS) di tiap *node*.


* **Pembahasan:** Tujuan utama DFS memang menggabungkan penyimpanan lokal murah (*commodity hardware* / DAS) dari banyak *node* menjadi satu kesatuan yang hemat biaya dan tahan banting. Jadi, memakai SAN yang berbiaya tinggi justru kurang pas secara konsep arsitektur.


**3. Jelaskan tugas masing-masing dari *NameNode* dan *DataNode* di arsitektur *Hadoop Distributed File System* (HDFS)!**

* **Jawaban:** *NameNode* bertugas sebagai *master* yang mencatat *metadata* (nama file, posisi blok, dan jumlah replika), sedangkan *DataNode* bertindak sebagai *slave* yang menyimpan blok data fisiknya sekaligus melayani proses baca, tulis, dan replikasi.


* **Pembahasan:** Waktu klien mau membaca file di HDFS, langkah pertamanya adalah bertanya dulu ke *NameNode* untuk mengecek di mana lokasi blok datanya berada. Setelah tahu posisinya, klien baru mengambil isi datanya langsung dari *DataNode* terkait.


**4. Sebuah instansi butuh layanan *cloud storage* yang kapasitasnya gampang diperbesar tanpa batas dan bisa diakses lewat antarmuka HTTP/REST lintas jaringan WAN. Tipe *cloud storage* mana yang paling tepat dipilih, dan sebutkan dua contoh software *open-source* di modul yang mendukung antarmuka S3?**

* **Jawaban:** Tipe *Object Storage*; contoh perangkat lunak *open-source* dari modul antara lain CubeFS, RustFS, PGSTY SILO, atau Ceph.


* **Pembahasan:** Merujuk pada tabel perbandingan tipe penyimpanan, *Object Storage* memakai jalur TCP/IP dengan antarmuka HTTP/REST (standar S3) dan memang dirancang agar mudah diskalakan tanpa batas lewat LAN maupun WAN—berbeda dengan *Block Storage* (FC/iSCSI) dan *File Storage* (NFS/SMB).