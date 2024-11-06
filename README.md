# UJIAN TENGAH SEMESTER - JARINGAN KOMPUTER LANJUT (CIE722)

**Nama:** Nadia Recilia Dahmi  
**NIM:** 20220801041  
**Mata Kuliah:** Jaringan Komputer Lanjut (CIE722)  
**Dosen Pengampu:** Jefry Sunupurwa Asri, S.Kom., M.Kom.  
**Fakultas/Prodi:** Ilmu Komputer/Teknik Informatika
___
## ESSAY! 

**1. Jelaskan menurut Anda apa itu Routing Static?**

**Jawab:** 

Routing Static termasuk metode routing di mana jalur yang dilalui oleh data ditentukan oleh admin jaringan. Jalur yang dimaksud ini tetap dan tidak berubah kecuali admin jaringan itu sendiri yang memperbarui. 

Pada *Routing Static*, admin menambahkan rute baru ke *Routes* dengan parameter tertentu. Berikut adalah langkah-langkah dasar untuk menambah rute baru:

1. **Destination Address**: Masukkan IP tujuan, misalnya `192.168.2.0/24`.
2. **Gateway**: Masukkan IP Gateway yang akan dilalui untuk mencapai tujuan, misalnya `192.168.1.1`.
3. Klik **OK** untuk menyimpan konfigurasi.
___

**2. Jelaskan menurut Anda apa itu Routing Dynamic?**  

**Jawab:**

Routing Dynamic secara otomatis mencari dan memilih jalur untuk mengirim data. Routing ini menggunakan protokol seperti RIP yang memungkinkan router berkomunikasi satu sama lain dan lebih efisien untuk jaringan yang besar dan sering mengalami perubahan.

#### Langkah-langkah Konfigurasi Routing Dynamic

**Pada Router 1:**

1. **Tambahkan IP Address:**
   - Pada Ether 1: `192.168.1.1/24`
   - Pada Ether 2: `10.10.1.1/30`

2. **Konfigurasi RIP:**
   - Tambahkan *new RIP Interface* pada Ether 2, atur `Receive v1-2` dan `Send v2`, lalu klik **apply**.
   - Tambahkan *RIP Network* dengan Address: `10.10.10.0/30`, lalu **apply**.
   - Tambahkan *new Interface* pada Ether 1, atur `Receive v1-2` dan `Send v2`, lalu **apply**.
   - Tambahkan *RIP Network* dengan Address: `192.168.1.0/24`, lalu **apply**.
   - Buka *Route List* pada RIP.

3. **Sambungkan ke PC Lainnya**

4. **Atur DHCP Server:**
   - Buka *DHCP Setup* pada Ether 1.

5. Jalankan perintah `ipconfig` di PC.

6. Uji koneksi dengan **ping** ke PC lain:
   - `ping 10.10.10.2`
   - `ping 192.168.2.254`

7. Jalankan perintah **ping** di *Terminal Winbox* untuk:
   - `ping 10.10.10.2`
   - `ping 192.168.2.254`
   - `ping 192.168.2.1`

**Pada Router 2:**

1. **Tambahkan IP Address:**
   - Pada Ether 2: `10.10.10.2/30`
   - Pada Ether 1: `192.168.2.1`

2. **Konfigurasi RIP:**
   - Tambahkan *new RIP Interface* pada Ether 1, atur `Receive v1-2` dan `Send v2`, lalu **apply**.
   - Tambahkan *new Interface* pada Ether 2, atur `Receive v1-2` dan `Send v2`, lalu **apply**.
   - Tambahkan *RIP Network* dengan Address: `10.10.10.0/30`, lalu **apply**.
   - Tambahkan *RIP Network* dengan Address: `192.168.2.0/24`, lalu **apply**.

3. **Sambungkan ke PC Lainnya**

4. **Atur DHCP Server:**
   - Pilih *DHCP Setup* pada Ether 1.

5. Jalankan perintah `ipconfig` di PC.

6. Uji koneksi dengan **ping** ke PC lain:
   - `ping 10.10.10.2`
   - `ping 192.168.2.254`

7. Jalankan perintah **ping** di *Terminal Winbox* untuk:
   - `ping 10.10.10.2`
   - `ping 192.168.2.254`
   - `ping 192.168.2.1`
___
**3. Jelaskan menurut Anda apa itu Firewall?**

**Jawab:**

Firewall merupakan sistem keamanan yang dirancang menjaga gerbang antara komputer dan internet, menyaring dan memblokir data atau akses yang tidak sah, dan hanya mengizinkan data aman yang masuk.

___
**4. Jelaskan menurut Anda apa itu NAT?**

**Jawab:**

NAT merupakan cara agar beberapa perangkat dalam jaringan lokal bisa berbagi satu alamat IP publik saat mengakses internet. 

Untuk mengonfigurasi NAT di firewall, berikut langkah-langkahnya:

1. Buka pengaturan NAT di firewall.
2. Di bagian **NAT General**, tentukan jenis NAT yang digunakan.
3. Di bagian **NAT Action**, pilih aksi yang diinginkan untuk menerjemahkan alamat IP.

Dengan konfigurasi NAT, perangkat dalam jaringan lokal dapat berkomunikasi dengan internet menggunakan satu alamat IP publik.

___
## **CASED** 
## ANALISIS TOPOLOGI 

Analisis dari topologi ini membahas cara ISP berperan sebagai pengganti IP publik dalam menghubungkan tiga lokasi berbeda yang masing-masing memiliki satu perangkat Mikrotik. Jaringan dikonfigurasi menggunakan tunnel untuk memastikan komunikasi aman antar-lokasi melalui jaringan internet dari ISP.

Langkah pertama adalah mengatur konfigurasi dasar pada tiap perangkat Mikrotik di lokasi kampus KJ, kampus CR, dan kampus HI. Setiap Mikrotik diberikan IP lokal untuk jaringan internal serta IP publik dari ISP untuk akses internet. DHCP Server diaktifkan pada tiap perangkat Mikrotik agar perangkat dalam jaringan lokal dapat menerima IP secara otomatis, dan NAT juga diaktifkan agar perangkat tersebut dapat mengakses internet melalui IP publik.

Kemudian, tunnel diatur di setiap Mikrotik dan diarahkan melalui ISP. Sebagai contoh, Mikrotik di lokasi kampus KJ membuat tunnel ke ISP, dan hal yang sama diterapkan di lokasi kampus CR dan kampus HI. Hal ini memungkinkan data untuk mengalir secara langsung antara lokasi-lokasi tersebut, karena titik akhir tunnel terhubung ke IP publik ISP.

Setiap Mikrotik juga dikonfigurasi dengan routing statis untuk memastikan lalu lintas dapat mengalir ke lokasi lain. Dengan demikian, perangkat di lokasi kampus KJ, kampus CR, dan kampus HI bisa saling berkomunikasi. Dalam hal ini, ISP menyediakan IP publik, sedangkan tunnel dan enkripsi menjaga agar komunikasi antar-lokasi tetap efisien dan aman.



