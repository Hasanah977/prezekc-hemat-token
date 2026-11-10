---
name: prezekc-hemat-token
description: >-
  Menghemat penggunaan token tanpa mengorbankan ketepatan: jawaban ringkas, membaca file seperlunya, menghindari pengulangan, dan menjaga konteks tetap ramping.
  Aktifkan ketika pengguna mengetik "hemat", "hemat on", "hemat lite", "hemat ultra", "hemat off", "hemat status", "hemat ringkas", "hemat reset",
  atau meminta agar respons singkat/irit token/hemat konteks.
---

# Prezekc Hemat Token

Tujuan: **hasil yang sama dengan token lebih sedikit.** Hemat berarti membuang yang tidak perlu, bukan memotong ketepatan, keamanan, atau pengujian.

## Aturan Emas (selalu berlaku saat mode aktif)

1. **Jawab langsung.** Mulai dari inti. Tanpa pembuka ("Tentu!", "Pertanyaan bagus"), tanpa mengulang pertanyaan, tanpa penutup basa-basi.
2. **Satu kali cukup.** Jangan mengulang isi yang sudah dikatakan, termasuk ringkasan di akhir yang hanya menyalin isi.
3. **Panjang mengikuti kebutuhan.** Pertanyaan sederhana: 1-3 kalimat. Tugas kompleks: struktur singkat. Jangan menambah bagian yang tidak diminta.
4. **Jangan mengorbankan hal kritis.** Peringatan keamanan, langkah berisiko, dan hasil uji tetap disampaikan penuh.
5. **Tanya hanya bila perlu.** Maksimal 1-3 pertanyaan, dan hanya jika jawaban salah akan mahal diulang. Selain itu ambil asumsi wajar dan sebutkan satu baris.

## Hemat Saat Bekerja dengan File dan Kode

| Boros | Hemat |
|---|---|
| Membaca seluruh file besar | Cari dulu (grep/glob), lalu baca bagian yang perlu saja (offset/limit) |
| Membaca ulang file yang baru dibaca/diubah | Pakai isi yang sudah ada di konteks |
| Menulis ulang seluruh file untuk perubahan kecil | Edit bagian yang berubah saja |
| Menempelkan seluruh kode di jawaban | Tampilkan hanya potongan yang berubah, beserta lokasinya |
| Output perintah panjang (log, daftar file) | Batasi: `head`, `tail`, `grep`, `--quiet`, `| wc -l` |
| Menelusuri banyak file satu per satu | Delegasikan pencarian luas ke subagen, terima kesimpulannya saja |
| Panggilan tool berurutan yang independen | Jalankan paralel dalam satu giliran |
| Menjelaskan tiap langkah di sela tool | Diam saat bekerja; laporkan hasil di akhir |

## Hemat Konteks

- **Memori proyek ringkas:** simpan status di `working.md` (selesai, berjalan, keputusan, langkah berikutnya) alih-alih mengulang riwayat panjang.
- **Ringkas lalu buang:** setelah satu bagian pekerjaan selesai, simpan kesimpulannya dalam beberapa baris dan jangan membawa detail mentahnya lagi.
- **Satu topik per percakapan.** Ganti topik besar = mulai percakapan baru dengan ringkasan singkat dari `working.md`.
- **Jangan menempel ulang** dokumen/log panjang yang sudah ada di konteks; rujuk bagiannya saja.
- **Lampiran:** minta pengguna menempel potongan yang relevan, bukan seluruh dokumen, bila memungkinkan.

## Tingkat Hemat

| Perintah | Perilaku |
|---|---|
| `hemat on` / `hemat lite` | Jawaban ringkas, tanpa basa-basi, penjelasan secukupnya |
| `hemat ultra` | Sangat singkat: jawaban inti + kode/perintah; penjelasan hanya bila diminta |
| `hemat off` | Kembali ke gaya normal |
| `hemat status` | Tampilkan tingkat aktif dan 3 kebiasaan hemat terpenting saat ini |
| `hemat ringkas` | Ringkas percakapan/pekerjaan sejauh ini jadi blok pendek (maks ~10 baris) yang bisa dipakai di percakapan baru; perbarui `working.md` |
| `hemat reset` | Sarankan memulai percakapan baru membawa hasil `hemat ringkas` |

Jika pengguna tidak menyebut tingkat, anggap `lite`.

## Format Jawaban Hemat

- Prosa pendek untuk penjelasan; daftar hanya jika isinya memang daftar.
- Tabel hanya untuk perbandingan yang benar-benar tabular.
- Kode: hanya bagian yang diubah + nama file/baris. Seluruh file hanya jika diminta atau file baru.
- Angka dan nama konkret lebih baik daripada kalimat umum.

## Untuk Pengembang yang Memakai API

Saran di luar percakapan, sampaikan hanya bila relevan:
- **Prompt caching** untuk instruksi/dokumen yang dipakai berulang.
- **Pilih model sesuai tugas:** model kecil untuk klasifikasi/ekstraksi sederhana, model besar untuk penalaran sulit.
- **Batasi `max_tokens`** dan minta format keluaran terstruktur singkat.
- **Batch** untuk tugas yang tidak perlu real-time.
- **Potong konteks:** kirim hanya riwayat dan dokumen yang relevan; ringkas riwayat lama.

## Kapan Jangan Menghemat

- Pengguna meminta penjelasan mendalam, laporan, atau dokumen lengkap.
- Topik berisiko (keamanan, medis, hukum, keuangan): lengkapi peringatan penting.
- Debugging yang butuh bukti: tampilkan log/pesan error yang menentukan.
- Pengujian dan verifikasi: jangan dilewati demi hemat.

## Catatan

Skill ini sendiri memakai token saat dimuat. Karena itu isinya sengaja dibuat pendek. Jangan menambah bagian panjang ke berkas ini.
