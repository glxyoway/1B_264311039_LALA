**1.	Lampirkan kedua script SQL kelompok Anda: (1) Query JOIN yang kompleks, dan (2) Script DDL pembentukan kolom/tabel denormalisasi beserta query panggilannya!**

jawab:
```sql
-- Menghitung total tempat/lokasi ramah lingkungan yang didaftarkan oleh setiap mitra
SELECT 
    u.user_id AS id_mitra,
    u.name AS nama_mitra,
    COUNT(l.lokasi_id) AS total_lokasi_terdaftar
FROM users u
JOIN lokasi l ON u.user_id = l.mitra_id
WHERE u.role = 'mitra'
GROUP BY u.user_id, u.name;
```
<br>

```sql
-- A. DDL: Menambahkan kolom atribut turunan (redudan) pada tabel master (users)
ALTER TABLE users 
ADD COLUMN total_lokasi_terdaftar INT DEFAULT 0;

-- B. Mengisi kolom turunan tersebut dengan data hasil agregasi dari tabel lokasi
UPDATE users u
SET total_lokasi_terdaftar = (
    SELECT COUNT(l.lokasi_id)
    FROM lokasi l
    WHERE l.mitra_id = u.user_id
);

-- C. Pembuktian: Query baca kilat (untuk dasbor) tanpa JOIN atau agregasi
SELECT 
    user_id AS id_mitra,
    name AS nama_mitra,
    total_lokasi_terdaftar
FROM users
WHERE role = 'mitra';
```

---

**2. Berdasarkan percobaan kelompok Anda, jelaskan dengan bahasa sendiri kelebihan denormalisasi dalam memangkas penggunaan klausa JOIN pada sistem informasi!**  

jawab:
Kelebihan utama denormalisasi dalam sistem ini terletak pada kemampuannya untuk memangkas waktu eksekusi serta menghindari fungsi agregasi yang berat saat menampilkan data rekapitulasi. Dengan menyimpan atribut hasil kalkulasi secara permanen di dalam tabel master, sistem dapat langsung membaca data tersebut tanpa harus menjalankan operasi JOIN berulang kali, sehingga proses pemuatan data menjadi jauh lebih cepat dan optimal.

---

**3.Jelaskan secara singkat, apa risiko utama terhadap data (contoh: inkonsistensi) yang muncul akibat kelompok Anda menambahkan atribut turunan atau tabel rekapitulasi tersebut?**

jawab:
Risiko paling krusial dari penerapan denormalisasi ini adalah munculnya inkonsistensi data. Hal ini dikarenakan atribut turunan disimpan secara tetap di dalam tabel master, sehingga ketika data sumbernya mengalami perubahan—seperti saat mitra menambah atau menghapus lokasi baru—nilai rekapitulasinya tidak akan otomatis ikut terbarui kecuali dilakukan pembaruan manual atau menggunakan trigger. Dampaknya, informasi yang disajikan pada aplikasi berisiko menjadi tidak sinkron dan tidak sesuai dengan kondisi data aslinya.
