
**1. Jelaskan secara singkat tujuan penggunaan klausa JOIN pada basis data relasional dan apa kelemahannya jika digunakan pada tabel dengan jutaan baris data!**

* **Jawab:**
Klausa JOIN bertujuan untuk menyatukan data dari beberapa tabel yang saling terhubung melalui kolom kunci yang sama. Kendalanya, jika kueri ini dipaksakan pada tabel yang berisi jutaan data, performa sistem akan drastis menurun dan menjadi sangat lambat. Hal ini terjadi karena mesin basis data harus bekerja ekstra keras untuk mencocokkan jutaan baris data secara langsung.

---

**2. Apa yang dimaksud dengan redundansi data, dan mengapa dalam konsep "Denormalisasi" redundansi ini sengaja diciptakan?**

* **Jawab:**
Redundansi data adalah situasi di mana data yang sama disimpan berulang kali di beberapa tempat atau tabel yang berbeda. Meskipun dalam normalisasi hal ini dihindari, dalam teknik "Denormalisasi" duplikasi data ini justru sengaja diterapkan demi meningkatkan kecepatan pembacaan data, sehingga aplikasi tidak perlu lagi memproses operasi JOIN yang panjang dan rumit setiap kali menampilkan informasi.

---

**3. Berikan satu contoh konkret bagaimana sebuah atribut turunan dapat menghindari penggunaan fungsi agregasi (seperti SUM) dalam query!**

* **Jawab:**
Sebagai contoh konkretnya, ketimbang harus selalu menggunakan fungsi SUM(total_harga) melalui operasi JOIN dari tabel transaksi setiap kali ingin memuat data belanja pelanggan, kita bisa menerapkan atribut turunan berupa kolom fisik baru (misalnya kolom total_belanja) langsung di dalam tabel master pelanggan. Dengan begitu, nilai totalnya sudah siap saji dan bisa langsung dipanggil tanpa perlu melakukan kalkulasi ulang yang berat.

---
