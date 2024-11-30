# Ujian Akhir Semester - Komunikasi dan Jaringan Komputer  

**Semester Gasal Tahun Ajaran 2024/2025**  

**PROGRAM PASCASARJANA TEKNIK INFORMATIKA & KOMPUTER**  

**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA**  

*Kampus PENS Jl. Raya ITS Keputih Sukolilo Surabaya 60111*  

**Mata Kuliah:** Komunikasi dan Jaringan Komputer  
**Dosen:** Ferry Astika Saputra  
**Kelas:** S2 IT A  
**Sifat:** Buku Terbuka  
**Waktu/Jam:** 13:00-17:00 (4 jam)  
**Hari / Tgl:** Senin, 2 Desember 2024  


## Pertanyaan (berdasarkan file trace tcp-ethereal-trace-1)  

**Petunjuk:** Jawaban berikut berdasarkan file trace `tcp-ethereal-trace-1` yang terdapat di `http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip`  

**Jawab pertanyaan berikut untuk segmen TCP:**  

1. **Alamat IP dan Nomor Port TCP yang digunakan oleh komputer klien (sumber) untuk mentransfer file ke gaia.cs.umass.edu? (10%)**  

    *Jawaban:* Komputer klien (sumber) menggunakan alamat IP **192.168.1.102** dan nomor port TCP **1161** untuk mentransfer file ke gaia.cs.umass.edu.  Komputer tujuan, gaia.cs.umass.edu, memiliki alamat IP **128.119.245.12** dan menggunakan port TCP **80**.  
    
    ![desc for picture ](./assets/answare1.png)

2. **Apa yang digunakan gaia.cs.umass.edu sebagai alamat IP dan nomor port untuk menerima file? (Lampirkan tangkapan layar tampilan Wireshark Anda) (10%)**  

   *Jawaban:* [Masukkan jawaban di sini]  
   *Tangkapan Layar:* [Masukkan gambar tangkapan layar di sini]  


3. **Berapakah nomor urut segmen TCP SYN yang digunakan untuk memulai koneksi TCP antara komputer klien dan gaia.cs.umass.edu? Apa yang ada di segmen tersebut yang mengidentifikasi segmen sebagai segmen SYN? (Lampirkan tangkapan layar tampilan Wireshark Anda) (10%)**  

   *Jawaban:* [Masukkan jawaban di sini]  
   *Tangkapan Layar:* [Masukkan gambar tangkapan layar di sini]  


4. **Berapakah nomor urut segmen SYNACK yang dikirim oleh gaia.cs.umass.edu ke komputer klien sebagai balasan terhadap SYN? Berapakah nilai bidang ACKnowledgement di segmen SYNACK? Bagaimana gaia.cs.umass.edu menentukan nilai tersebut? Apa yang ada di segmen tersebut yang mengidentifikasi segmen sebagai segmen SYNACK? (Lampirkan tangkapan layar tampilan Wireshark Anda) (10%)**  

   *Jawaban:* [Masukkan jawaban di sini]  
   *Tangkapan Layar:* [Masukkan gambar tangkapan layar di sini]  


5. **Berapakah nomor urut segmen TCP yang berisi perintah HTTP POST? Perhatikan bahwa untuk menemukan perintah POST, Anda perlu menggali ke dalam bidang konten paket di bagian bawah jendela Wireshark, mencari segmen dengan "POST" di dalam bidang DATANYA. (Lampirkan tangkapan layar tampilan Wireshark Anda) (15%)**  

   *Jawaban:* [Masukkan jawaban di sini]  
   *Tangkapan Layar:* [Masukkan gambar tangkapan layar di sini]  


6. **Anggap segmen TCP yang berisi HTTP POST sebagai segmen pertama dalam koneksi TCP. Berapakah nomor urut dari enam segmen koneksi TCP pertama (termasuk segmen HTTP POST)? Pada waktu berapakah setiap segmen dikirim? Kapan ACK untuk setiap segmen diterima? Dengan mempertimbangkan perbedaan antara waktu setiap segmen TCP dikirim dan waktu pengakuannya diterima, berapakah nilai RTT untuk masing-masing dari enam segmen tersebut? Berapakah nilai EstimatedRTT (lihat halaman 237 di buku teks) setelah penerimaan setiap ACK? Asumsikan bahwa nilai EstimatedRTT sama dengan RTT yang diukur untuk segmen pertama, dan kemudian dihitung menggunakan persamaan EstimatedRTT pada halaman 237 untuk semua segmen berikutnya. (30%)**  

   *Jawaban:* [Masukkan jawaban di sini, termasuk tabel dengan informasi waktu dan perhitungan RTT dan EstimatedRTT]  


7. **Berapakah panjang masing-masing dari enam segmen TCP pertama? (Lampirkan tangkapan layar tampilan Wireshark Anda) (15%)**  

   *Jawaban:* [Masukkan jawaban di sini]  
   *Tangkapan Layar:* [Masukkan gambar tangkapan layar di sini]