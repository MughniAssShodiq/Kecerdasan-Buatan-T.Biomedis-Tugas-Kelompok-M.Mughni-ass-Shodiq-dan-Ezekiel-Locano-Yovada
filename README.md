
# Segmentasi Polip pada Citra Kolonoskopi dengan U-Net

<!--
  TEMPLATE LAPORAN — Tugas P10 Kecerdasan Buatan (BM25-41204), Teknik Biomedis ITERA.
  Petunjuk lengkap: https://mctm.web.id/ai-bm/tugas

  Cara memakai:
  - Ganti semua teks yang diawali "✍️" dengan tulisan kelompokmu, lalu hapus tanda ✍️-nya.
  - Blok komentar seperti ini adalah petunjuk; tidak tampil di GitHub. Boleh dihapus.
  - Gambar diambil dari folder hasil/ yang dibuat otomatis oleh notebook.
  - Jangan hapus judul-judul bagian (##).
-->

**Tugas P10 — Kecerdasan Buatan (BM25-41204), Teknik Biomedis ITERA**

## Anggota kelompok

| Nama | NIM | Username GitHub | Kontribusi utama |
|---|---|---|---|
| Ezekiel Locano Yovada | 123430019 | Ezekiel2506 | menjalankan eksperimen |
| M.Mughni Ass Shodiq | 123430059 | MughniAssHodiq | menjalankan eksperimen|
| - | - | - | - |

## 1. Pertanyaan

Augmentasi apa yang membantu U-Net menemukan polip pada citra kolonoskopi, dan augmentasi apa yang tidak? Kenapa?

## 2. Data & pengaturan

<!-- Isi dari Bagian 2 notebook. Pastikan CEPAT = False untuk hasil akhir. -->

- Dataset: Kvasir-SEG (1000 citra kolonoskopi + mask polip), diperkecil ke 128 × 128 piksel.
- Data uji: 200 citra (tetap). Data latih: 250 citra per ulangan.
- Model: U-Net mini (±0,5 juta parameter), 45 epoch, 5 ulangan per skenario.
- Dijalankan di: Google Colab T4.

<img width="1870" height="363" alt="augmentasi_kecerahan_dan_kontras" src="https://github.com/user-attachments/assets/102279e7-f17f-4640-b0b8-bb0eda81f6ab" />
<img width="1870" height="363" alt="augmentasi_geser_dan_perbesaran" src="https://github.com/user-attachments/assets/f99a4e39-1812-49b0-9854-79117aa81cd7" />
<img width="1920" height="816" alt="contoh_data" src="https://github.com/user-attachments/assets/96891cb9-136f-46aa-9e07-af7af20c10e3" />


## 3. Skenario augmentasi & hipotesis

<!-- Tulis bagian ini SEBELUM menjalankan eksperimen. Commit dulu, baru jalankan.
     Alasan klinis = kenapa variasi ini mungkin (atau tidak mungkin) terjadi pada kolonoskopi sungguhan. -->

| Skenario | Augmentasi (kode) | Alasan klinis | Hipotesis: Dice naik/turun/sama? |
|---|---|---|---|
| Tanpa augmentasi | — | Pembanding | — |
| Geser dan pembesaran | v2.RandomAffine(degrees=0, translate=(0.1, 0.1), scale=(0.8, 1.2))` | variasi orientasi posisi | 0.335 |
| Rotasi | v2.RandomRotation(degrees=180) | Variasi Orientasi posisi | 0.398 |

Contoh augmentasi yang dicoba:

<img width="1870" height="363" alt="augmentasi_geser_dan_perbesaran" src="https://github.com/user-attachments/assets/e6620819-d9dc-4622-9807-c65ebbe16b00" />
<img width="1870" height="363" alt="augmentasi_rotasi" src="https://github.com/user-attachments/assets/9fc6defb-2ebe-4b85-b99a-10d877cba0d1" />


<!-- Ganti nama file sesuai skenario kalian (lihat isi folder hasil/). -->

## 4. Hasil

<!-- Tempel isi hasil/ringkasan.md di sini. -->

<img width="792" height="504" alt="perbandingan" src="https://github.com/user-attachments/assets/26749b39-75a2-4501-8d5c-cb0623e00da8" />
<img width="792" height="504" alt="perbandingan" src="https://github.com/user-attachments/assets/f4dca7bc-c331-4e2a-909f-46423b433ee2" />




## 5. Analisis peta kesalahan

<img width="1595" height="1320" alt="peta_kesalahan" src="https://github.com/user-attachments/assets/a8127f18-83f7-4654-a2c1-0951ad2389df" />
<img width="1595" height="1320" alt="peta_kesalahan" src="https://github.com/user-attachments/assets/1c51470d-301d-4a2a-ad7c-7a6e1eb8a81b" />
<!-- Hijau = benar, merah = false positive, biru = false negative.
     Pertanyaan pemandu: Polip seperti apa yang sering terlewat (kecil? datar? warna mirip dinding usus?)
     Apa yang sering dikira polip padahal bukan? Apakah augmentasi memperbaiki kasus sulit? -->

✍️

## 6. Pembahasan & kesimpulan

<!-- Bandingkan hasil dengan hipotesis di Bagian 3. Hipotesis yang ternyata salah tetap bernilai,
     asalkan dijelaskan kenapa. Perbedaan kecil (lebih kecil dari simpangan baku) belum tentu berarti. -->

✍️

## 7. Pembagian kerja

<!-- Siapa mengerjakan apa. Penilaian proses kerja dilihat dari riwayat commit tiap anggota. -->

M.Mughni Ass Shodiq = Membuat REPO dan commit di Gitbash, karena laptop anggota 1 lagi C nya full jadi ga begitu bisa make git


Ezekiel Locano Yovada = Yang menjalankan eksperimen, Ngerun Koding, milih augmentasi, hipotesis, sampai buat hasil

untuk eksperimen itu kami belajar barengan lewat uji coba dan juga untuk Gitpull dan gitpush belajar dari panduan yang diberikan dan dibantu sedikit AI.

## 8. Penggunaan AI

<!-- Wajib diisi, walau tidak memakai AI (tulis "Tidak memakai AI").
     Contoh: "Claude Code (CLI) untuk menulis skenario augmentasi dan memperbaiki error di Bagian 4.
     Draf Bagian 6 ditulis sendiri, lalu dirapikan bahasanya dengan bantuan AI." -->

Kami menggunakan AI untu membantu memehami saja, sempat nyoba CLI gemini di terminal cumin ga gitu ngerti cara kerjanya. Untuk kodingan kami memahami lewat nyobain 1 1 augmentasinya, dan pengaruh beberapa kode kalau diubah.

## Cara menjalankan ulang

```bash
uv sync
uv run jupyter lab segmentasi_polip.ipynb
```

Atau buka notebook di Google Colab (Runtime → Change runtime type → T4 GPU).

## Referensi

- Jha, D., dkk. (2020). Kvasir-SEG: A Segmented Polyp Dataset. *MultiMedia Modeling (MMM 2020)*, 451–462.
- Ronneberger, O., Fischer, P., & Brox, T. (2015). U-Net: Convolutional Networks for Biomedical Image Segmentation. *MICCAI*. arXiv:1505.04597.
- ✍️ tambahkan referensi lain yang kalian pakai
