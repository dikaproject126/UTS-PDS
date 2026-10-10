# UTS Pemodelan dan Simulasi: Soal No. 4

Optimasi paket layanan analisis kerentanan siber (**Penetration Testing** vs **Security Audit**) menggunakan *Linear Programming*.

> Ujian Tengah Semester, mata kuliah Pemodelan dan Simulasi
> Program Studi Informatika, FMIPA, Universitas Udayana
> Pengampu: I Gede Surya Rahayuda, M.Kom.

---

## Deskripsi Masalah

Sebuah perusahaan konsultan keamanan siber menawarkan dua layanan analisis kerentanan. Waktu kerja konsultan terbatas setiap minggu, dan perusahaan ingin menentukan jumlah paket tiap layanan agar keuntungan maksimum.

| Layanan | Jam senior / paket | Jam junior / paket | Keuntungan / paket |
|---|---|---|---|
| Penetration Testing | 4 | 2 | Rp 12.000.000 |
| Security Audit | 2 | 3 | Rp 10.000.000 |
| **Kapasitas per minggu** | **40 jam** | **36 jam** | - |

## Model Matematika

- **Variabel keputusan:** `x1` = jumlah paket Penetration Testing, `x2` = jumlah paket Security Audit
- **Fungsi tujuan:** maksimumkan `Z = 12.000.000·x1 + 10.000.000·x2`
- **Kendala:**
  - `4·x1 + 2·x2 <= 40` (jam konsultan senior)
  - `2·x1 + 3·x2 <= 36` (jam konsultan junior)
  - `x1, x2 >= 0`

## Hasil

| Metode | x1 | x2 | Z (Rp) |
|---|---|---|---|
| Grafik (titik sudut) | 6 | 8 | 152.000.000 |
| Simpleks manual | 6 | 8 | 152.000.000 |
| `scipy.optimize.linprog` (HiGHS) | 6 | 8 | 152.000.000 |

**Kesimpulan:** ambil **6 paket Penetration Testing** dan **8 paket Security Audit** per minggu untuk keuntungan maksimum **Rp 152.000.000 per minggu**. Seluruh jam konsultan senior dan junior terpakai penuh.

![Daerah layak dan solusi optimal](grafik_solusi.png)

## Isi Repositori

```
UTS-PDS/
├── README.md                                  # dokumen ini
├── solusi_no4.py                              # program penyelesaian (grafik, simpleks, linprog)
├── grafik_solusi.png                          # grafik daerah layak (dihasilkan program)
└── Laporan_UTS_Pemodelan_Simulasi_No4.pdf     # laporan lengkap
```

> Sesuaikan struktur di atas dengan lokasi file yang sebenarnya, misalnya bila file diletakkan di dalam folder `StudiKasus/`.

## Cara Menjalankan

**Prasyarat:** Python 3.9 atau lebih baru.

```bash
# 1. Clone repositori
git clone https://github.com/dikaproject126/UTS-PDS.git
cd UTS-PDS

# 2. Pasang pustaka yang dibutuhkan
pip install numpy scipy matplotlib

# 3. Jalankan program
python solusi_no4.py
```

Program akan mencetak hasil metode grafik, tabel iterasi simpleks, dan verifikasi `linprog` di terminal, lalu menyimpan `grafik_solusi.png` di folder yang sama.

**Menjalankan di Google Colab:** unggah `solusi_no4.py`, lalu jalankan `!python solusi_no4.py` pada sel baru. Grafik tersimpan sebagai file `grafik_solusi.png` di penyimpanan Colab.

## Penjelasan Program

| Bagian | Fungsi |
|---|---|
| `corner_points()` | Mencari semua perpotongan garis kendala, menyaring titik layak, lalu mengevaluasi `Z` di tiap titik sudut (metode grafik) |
| `simplex_max()` | Implementasi tabel simpleks manual dengan variabel slack hingga solusi optimal |
| `linprog(...)` | Verifikasi hasil dengan solver HiGHS dari SciPy |
| Matplotlib | Menggambar garis kendala, daerah layak, titik sudut, titik optimal, dan garis isoprofit |

## Anggota Kelompok

| No | Nama | NIM | Bagian |
|---|---|---|---|
| 1 | ................ | ................ | Identifikasi masalah dan daftar pustaka |
| 2 | ................ | ................ | Metode grafik |
| 3 | ................ | ................ | Metode simpleks |
| 4 | ................ | ................ | Implementasi program dan repositori |
| 5 | ................ | ................ | Analisa hasil, kesimpulan, dan finalisasi |

## Referensi

[1] F. S. Hillier and G. J. Lieberman, *Introduction to Operations Research*, 11th ed. New York, NY, USA: McGraw-Hill Education, 2021.

[2] H. A. Taha, *Operations Research: An Introduction*, 10th ed., Global ed. Harlow, U.K.: Pearson Education, 2017.

[3] P. Virtanen *et al.*, "SciPy 1.0: Fundamental algorithms for scientific computing in Python," *Nat. Methods*, vol. 17, no. 3, pp. 261–272, 2020, doi: 10.1038/s41592-019-0686-2.

[4] Q. Huangfu and J. A. J. Hall, "Parallelizing the dual revised simplex method," *Math. Program. Comput.*, vol. 10, no. 1, pp. 119–142, 2018, doi: 10.1007/s12532-017-0130-5.

[5] C. R. Harris *et al.*, "Array programming with NumPy," *Nature*, vol. 585, no. 7825, pp. 357–362, Sep. 2020, doi: 10.1038/s41586-020-2649-2.

[6] J. D. Hunter, "Matplotlib: A 2D graphics environment," *Comput. Sci. Eng.*, vol. 9, no. 3, pp. 90–95, 2007, doi: 10.1109/MCSE.2007.55.

---

*Repositori ini dibuat untuk keperluan akademik (Ujian Tengah Semester).*
