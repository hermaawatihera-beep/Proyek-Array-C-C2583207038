# Sistem Monitoring Stok dan Penjualan Kantin Kampus

## Identitas

| Keterangan   | Isi                                   |
|--------------|---------------------------------------|
| Nama Lengkap | [ISI NAMA LENGKAP]                    |
| NIM          | [ISI NIM]                             |
| Kelas        | [PTI3A / PTI3B]                       |
| Mata Kuliah  | Algoritma dan Pemrograman Lanjutan    |
| Dosen        | Taofik Muhammad, M.Kom                |
| Nama Proyek  | Sistem Monitoring Stok dan Penjualan Kantin Kampus |

## Deskripsi Singkat

Aplikasi console berbahasa C untuk membantu pengelola kantin kampus mencatat produk, memantau stok, memproses transaksi penjualan, serta melihat laporan penjualan. Seluruh data disimpan di dalam array selama program berjalan (tanpa database atau file eksternal). Kapasitas maksimal 50 produk dengan 6 produk sebagai data awal (Nasi Goreng, Mie Ayam, Es Teh Manis, Gorengan, Air Mineral, dan Kopi Susu).

## Daftar Fitur

1. Lihat Daftar Produk (nama, harga, stok)
2. Tambah Produk
3. Ubah Produk (harga dan stok)
4. Transaksi Penjualan (beberapa jenis produk dalam satu transaksi)
5. Tambah Stok
6. Cari Produk berdasarkan nama
7. Urutkan Produk (harga termurah dan jumlah terjual terbanyak)
8. Laporan Penjualan (jumlah terjual per produk, total unit, total pendapatan, produk terlaris)
9. Cek Stok Menipis (stok < 5)
0. Keluar

Validasi input: pilihan menu tidak tersedia, nomor produk tidak ditemukan, jumlah beli nol/negatif, harga/stok negatif, jumlah beli melebihi stok, dan kapasitas array penuh.

## Penjelasan Penggunaan Array

Data disimpan dalam array dengan indeks yang saling berkaitan (indeks yang sama = produk yang sama).

| Array | Tipe | Fungsi |
|-------|------|--------|
| `[NAMA_ARRAY_NAMA]` | array karakter 2 dimensi | Menyimpan nama produk |
| `[NAMA_ARRAY_HARGA]` | array 1 dimensi | Menyimpan harga produk |
| `[NAMA_ARRAY_STOK]` | array 1 dimensi | Menyimpan stok produk |
| `[NAMA_ARRAY_TERJUAL]` | array 1 dimensi | Menyimpan jumlah terjual |
| `[VARIABEL_JUMLAH]` | integer | Jumlah data produk aktif |

Contoh deklarasi (sesuaikan dengan kode Anda):

```c
#define MAKS_PRODUK 50
#define PANJANG_NAMA [ISI]

char   [array_nama][MAKS_PRODUK][PANJANG_NAMA];
[tipe] [array_harga][MAKS_PRODUK];
int    [array_stok][MAKS_PRODUK];
int    [array_terjual][MAKS_PRODUK];
int    [jumlah_produk];
```

**Cara kerja singkat:**
- Produk baru ditambahkan pada indeks `[jumlah_produk]`, lalu `[jumlah_produk]` bertambah satu.
- Penambahan ditolak jika `[jumlah_produk]` sudah mencapai 50.
- Pencarian: [JELASKAN ALGORITMA ANDA, misalnya sequential search]. Pencarian tidak membedakan huruf besar/kecil dan mencocokkan sebagian nama (mencari "kopi" menemukan "Kopi Susu").
- Pengurutan: [JELASKAN ALGORITMA ANDA, misalnya bubble sort] pada array harga dan jumlah terjual, dengan semua array ikut ditukar agar data tetap sinkron. Nomor produk asli tetap ditampilkan pada hasil urutan.

## Cara Kompilasi dan Menjalankan

Prasyarat: compiler GCC.

```bash
gcc main.c -o kantin
```

Menjalankan di Linux/Mac:

```bash
./kantin
```

Menjalankan di Windows:

```bash
kantin.exe
```

## Pengujian

Data awal: 6 produk.

| No | Nama Produk  | Harga | Stok |
|----|--------------|-------|------|
| 1  | Nasi Goreng  | 12000 | 20   |
| 2  | Mie Ayam     | 10000 | 15   |
| 3  | Es Teh Manis | 4000  | 30   |
| 4  | Gorengan     | 2000  | 40   |
| 5  | Air Mineral  | 3000  | 4    |
| 6  | Kopi Susu    | 8000  | 12   |

### Skenario 1: Tambah Produk
- **Input/Tindakan:** Menu 2, masukkan produk baru: Ayam geprek, harga 8000, stok awal 40. Lalu buka menu 1.
- **Hasil yang diharapkan:** Produk muncul dalam daftar.
- **Keterangan:** Program menampilkan pesan `Produk "Ayam geprek" berhasil ditambahkan.` Pada daftar produk, Ayam geprek muncul sebagai nomor 7 dengan harga 8000 dan stok 40.

![Skenario 1](screenshots/01-tambah-produk.png)

### Skenario 2: Transaksi
- **Input/Tindakan:** Menu 4, beli beberapa produk: Mie Ayam x 4, Air Mineral x 2, Ayam geprek x 3. Akhiri input dengan nomor produk 0, lalu konfirmasi `y`.
- **Hasil yang diharapkan:** Subtotal dan total benar.
- **Keterangan:** Hitungan manual: Mie Ayam 4 x 10000 = 40000; Air Mineral 2 x 3000 = 6000; Ayam geprek 3 x 8000 = 24000. Total = 40000 + 6000 + 24000 = 70000. Rincian transaksi di program menampilkan total pembayaran 70000, sama dengan hitungan manual.

![Skenario 2](screenshots/02-transaksi.png)

### Skenario 3: Pembaruan Stok
- **Input/Tindakan:** Selesaikan transaksi pada skenario 2, lalu buka menu 1.
- **Hasil yang diharapkan:** Stok dan jumlah terjual berubah.
- **Keterangan:** Stok Mie Ayam 15 -> 11, Air Mineral 4 -> 2, Ayam geprek 40 -> 37. Jumlah terjual masing-masing bertambah 4, 2, dan 3 (terlihat pada laporan penjualan). Stok produk lain tidak berubah.

![Skenario 3 - sebelum](screenshots/03a-stok-sebelum.png)
![Skenario 3 - sesudah](screenshots/03b-stok-sesudah.png)

### Skenario 4: Stok Tidak Cukup
- **Input/Tindakan:** Menu 4, beli melebihi stok: Es Teh Manis (stok 30) x 31. Lalu masukkan 0 untuk selesai.
- **Hasil yang diharapkan:** Transaksi ditolak; stok tetap.
- **Keterangan:** Program menampilkan `[!] Stok Es Teh Manis tidak cukup (tersedia 30, sudah dipilih 0).` Karena tidak ada produk yang berhasil dipilih, transaksi dibatalkan. Laporan penjualan sesudahnya tidak berubah (total unit terjual tetap 9 dan pendapatan tetap 70000), sehingga stok tidak terpengaruh.

![Skenario 4 - penolakan](screenshots/04a-stok-tidak-cukup.png)
![Skenario 4 - stok tetap](screenshots/04b-stok-tetap.png)

### Skenario 5: Laporan
- **Input/Tindakan:** Menu 8.
- **Hasil yang diharapkan:** Unit, pendapatan, dan produk terlaris benar.
- **Keterangan:** Terjual: Mie Ayam 4 unit (40000), Air Mineral 2 unit (6000), Ayam geprek 3 unit (24000), produk lain 0. Total unit = 4 + 2 + 3 = 9. Total pendapatan = 70000. Produk terlaris adalah Mie Ayam (4 unit). Semuanya sesuai dengan hitungan manual.

![Skenario 5](screenshots/05-laporan.png)

### Skenario 6: Pengurutan
- **Input/Tindakan:** Menu 7, urutkan berdasarkan harga termurah (pilihan 1) lalu jumlah terjual terbanyak (pilihan 2).
- **Hasil yang diharapkan:** Harga dari termurah; jumlah terjual dari terbanyak.
- **Keterangan:** Urutan harga: Gorengan 2000, Air Mineral 3000, Es Teh Manis 4000, Kopi Susu 8000, Ayam geprek 8000, Mie Ayam 10000, Nasi Goreng 12000. Urutan jumlah terjual: Mie Ayam 4, Ayam geprek 3, Air Mineral 2, lalu Nasi Goreng, Es Teh Manis, Gorengan, dan Kopi Susu dengan 0 terjual. Produk berharga atau berjumlah terjual sama tetap berurutan sesuai nomor asalnya.

![Skenario 6 - harga](screenshots/06a-urut-harga.png)
![Skenario 6 - terjual](screenshots/06b-urut-terjual.png)

### Skenario 7: Pencarian dan Stok
- **Input/Tindakan:** Menu 6 cari produk: `kopi`. Lalu menu 9 untuk cek stok < 5.
- **Hasil yang diharapkan:** Hasil pencarian dan peringatan stok menipis tepat.
- **Keterangan:** Pencarian `kopi` (huruf kecil) menemukan 1 produk, yaitu Kopi Susu (harga 8000, stok 12). Menu 9 menampilkan satu peringatan: Air Mineral dengan stok 2 (setelah transaksi), satu-satunya produk dengan stok kurang dari 5.

![Skenario 7 - pencarian](screenshots/07a-cari-produk.png)
![Skenario 7 - stok menipis](screenshots/07b-stok-menipis.png)

## Struktur Repository

```
Proyek-Array-C-[NIM]/
├── main.c
├── README.md
└── screenshots/
```
