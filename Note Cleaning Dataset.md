Note Cleaning Dataset: 

1. Missing values di highlight dengan warna kuning (crtl+G - go to special - blanks)
2. Mengisi missing values di kolom "productname" dan "brand" dengan "UNKNOWN"
3. Mengisi kolom "unitprice" dengan median
4. Hitung nilai MEDIAN kolom "unitprice"
5. masukkan nilai median yg dihasilkan dalam kolom missing di "unitprice"
6. Ambil Value/ nilainya saja dari kolom "Rawweight" 
7. Ambil satuan nilai dari kolom "Rawweight"
8. Strandarisasi satuan pada kolom "weight\_unit" - ada satuan yang masih "aneh" tetapi dibiarkan terlebih dahulu
9. Encoding huruf "aneh-Ã© dll" dalam kolom "brand"
10. Standarisasi kolom "brand" untuk memastikan tulisan sama dg proper dan trim / penulisan nya disamakan
11. Isi kolom "productname" yang kosong dengan "Unknown" \& melakukan standarisari penulisan dengan proper \& trim
12. Menghapus 1 row dari kolom "orderdate" karena nilai kosong. jika mengisi tgl atau lainnya tidak bisa di rata2 dan membuat data tdk akurat. dan hanya 1 row yg kosong, tidak akan banyak mempengaruhi perubahan data
13. Kolom "country" menghapus prefix (en: .....) dan menggantinya dengan kosong-an
14. Kolom "country" mengubah nama negara (multibahasa) ex: alrgelia; maroc; dll menjadi nama negara standar yang diketahui dlm Bahasa inggris
15. Standarisasi penulisan menggunakan proper \& trim









NOTEEEEE::

Berikut rangkuman yang bisa kamu masukkan ke portfolio:



\---



\## 📊 Project: Data Cleaning — Online Retail Dataset



\*\*Tools:\*\* Microsoft Excel

\*\*Dataset:\*\* 3.000 baris × 8 kolom

\*\*Sumber:\*\* Kaggle (Online Retail Real World Dataset)



\---



\### 🔍 Gambaran Dataset

Dataset berisi data transaksi retail online yang mencakup informasi produk, brand, berat, negara, tanggal order, dan harga. Data mentah mengandung berbagai masalah kualitas yang perlu dibersihkan sebelum bisa dianalisis.



\---



\### ⚠️ Masalah yang Ditemukan



| Kolom | Masalah |

|---|---|

| UnitPrice | 386 nilai kosong |

| Raw\_Weight | 513 nilai kosong + format tidak konsisten |

| Brand | 334 nilai kosong + encoding rusak + kapitalisasi tidak konsisten |

| ProductName | 96 nilai kosong + encoding rusak + simbol trademark |

| OrderDate | 1 nilai kosong |

| Country | 1 nilai kosong + nama multi-bahasa + prefix tidak relevan |



\---



\### 🛠️ Proses Cleaning



\*\*1. UnitPrice — Missing Values\*\*

\- Menghitung median menggunakan Array Formula `=MEDIAN(IF(range>0;range))` untuk mengabaikan sel kosong

\- Median = \*\*13,16\*\*

\- Mengisi 386 sel kosong menggunakan Ctrl+G → Special → Blanks → isi dengan nilai median



\*\*2. Raw\_Weight — Format Tidak Konsisten\*\*

\- Membuat kolom baru `Weight\_Value` untuk mengekstrak angka menggunakan formula LEFT, MIN, FIND

\- Membuat kolom baru `Weight\_Unit` untuk mengekstrak satuan

\- Membuat kolom `Weight\_Unit\_Clean` untuk standardisasi satuan menjadi: `g`, `kg`, `ml`, `l`, atau `unknown`

\- Hasil: 2.394 baris berhasil distandardisasi, 590 ditandai `unknown` (513 memang kosong, 77 tidak dapat ditentukan)



\*\*3. Brand — Encoding Rusak \& Tidak Konsisten\*\*

\- Memperbaiki karakter encoding rusak (Latin) menggunakan Find \& Replace: `Ã©` → `é`, `â€™` → `'`, dll

\- Karakter non-Latin (Arab, Rusia, Emoji) dibiarkan karena di luar scope pembersihan

\- Standardisasi kapitalisasi menggunakan `=PROPER(TRIM())`

\- Mengisi 334 sel kosong dengan `Unknown`



\*\*4. ProductName — Encoding \& Missing Values\*\*

\- Menghapus simbol trademark rusak (`Â®`, `â„¢`) menggunakan Find \& Replace

\- Mengisi 96 sel kosong dengan `Unknown`

\- Standardisasi kapitalisasi menggunakan `=PROPER(TRIM())`



\*\*5. OrderDate — Missing Value\*\*

\- 1 baris kosong dihapus karena tidak signifikan (0,03% dari total data)



\*\*6. Country — Multi-bahasa \& Format\*\*

\- Menghapus prefix tidak relevan (`en:`, `fr:`, `de:`, `es:`) menggunakan Find \& Replace

\- Standardisasi nama negara ke Bahasa Inggris (Maroc → Morocco, Argelia → Algeria, dll)

\- Standardisasi kapitalisasi menggunakan `=PROPER(TRIM())`

\- Mengisi 1 sel kosong dengan `Unknown`



\---



\### ✅ Hasil Akhir



| Kolom | Sebelum | Sesudah |

|---|---|---|

| UnitPrice | 386 kosong | Semua terisi (median 13,16) |

| Raw\_Weight | 513 kosong + format berantakan | Terstandardisasi ke g/kg/ml/l |

| Brand | 334 kosong + encoding rusak | Bersih + kapitalisasi konsisten |

| ProductName | 96 kosong + encoding rusak | Bersih + kapitalisasi konsisten |

| OrderDate | 1 kosong | Baris dihapus (3.000 → 2.999) |

| Country | Multi-bahasa + prefix | Terstandardisasi ke Bahasa Inggris |



\---



\### 💡 Catatan

\- Data mengandung multi-bahasa (Arab, Rusia, Prancis) — pembersihan difokuskan pada standardisasi format dan karakter Latin

\- Kolom Raw\_Weight yang tidak dapat ditentukan satuannya ditandai `unknown` daripada diasumsikan

\- File disimpan dalam 2 versi: `Dataset\_Working.xlsx` (dengan kolom bantu) dan `Dataset\_Final.xlsx` (hasil akhir bersih)



\---



Rangkuman ini bisa kamu copy ke dokumen portfolio, Notion, atau langsung upload ke Sribulancer/Upwork sebagai deskripsi proyek. Mau saya buatkan dalam format PDF atau Word? 😊

