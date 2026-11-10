# Prezekc Hemat Token

Skill untuk membuat agen AI bekerja dengan **token lebih sedikit tanpa mengorbankan ketepatan**: jawaban ringkas, membaca file seperlunya, tidak mengulang, dan menjaga konteks tetap ramping.

Seluruh aturan ada di [`SKILL.md`](./SKILL.md), yang sengaja dibuat pendek karena isinya ikut memakai token saat dimuat.

## Apa yang dihemat

- **Token keluaran:** tanpa basa-basi, tanpa pengulangan, panjang jawaban mengikuti kebutuhan.
- **Token masukan:** membaca bagian file yang perlu saja, membatasi output perintah, tidak membaca ulang file yang sudah ada di konteks.
- **Konteks percakapan:** memori proyek ringkas (`working.md`), ringkasan sebelum ganti topik.

## Perintah

| Perintah | Fungsi |
|---|---|
| `hemat on` / `hemat lite` | Jawaban ringkas tanpa basa-basi |
| `hemat ultra` | Sangat singkat: inti + kode/perintah saja |
| `hemat off` | Kembali ke gaya normal |
| `hemat status` | Lihat tingkat aktif dan kebiasaan hemat utama |
| `hemat ringkas` | Ringkas pekerjaan sejauh ini untuk dibawa ke percakapan baru |
| `hemat reset` | Saran memulai percakapan baru dengan ringkasan |

## Kebiasaan hemat utama

| Boros | Hemat |
|---|---|
| Membaca seluruh file besar | Cari dulu, baca bagian yang perlu |
| Menulis ulang seluruh file | Edit bagian yang berubah |
| Output log panjang | Batasi dengan `head`, `tail`, `grep` |
| Panggilan tool berurutan | Jalankan paralel bila independen |
| Riwayat percakapan panjang | Ringkas ke `working.md`, mulai percakapan baru |

## Cara memakai

> Lokasi folder skill dapat berbeda antarversi. Cek dokumentasi aplikasi yang kamu pakai bila langkah ini tidak cocok.

**Claude Code**
```bash
mkdir -p .claude/skills/prezekc-hemat-token
cp SKILL.md .claude/skills/prezekc-hemat-token/
```
Untuk semua proyek, gunakan `~/.claude/skills/prezekc-hemat-token/`. Lalu ketik `hemat on`.

**Claude.ai**
Kemas folder (berisi `SKILL.md`) menjadi ZIP, unggah lewat pengaturan Skills, dan aktifkan.

**Agen/editor lain**
Tempel isi `SKILL.md` sebagai instruksi proyek.

## Yang tidak dikorbankan

Peringatan keamanan, langkah berisiko, pengujian, dan bukti debugging tetap lengkap. Hemat berarti membuang yang tidak perlu, bukan memotong yang penting.

## Batasan

- Penghematan bergantung pada tugas dan kebiasaan pemakaian; tidak ada angka pasti yang dijanjikan.
- Skill hanya mengatur perilaku agen. Batas pemakaian dan harga tetap ditentukan penyedia layanan.
- Pada percakapan yang sangat panjang, cara paling efektif tetap memulai percakapan baru membawa ringkasan.

## Keluarga Prezekc

Skill pendamping dari [`prezekc-developer`](https://github.com/Hasanah977/prezekc-developer), kerangka kerja membangun sistem berbasis tata kelola SI. Keduanya bisa dipakai bersamaan: `hemat on` lalu `prezekc build ...`.

## Lisensi

Tentukan lisensi (misalnya MIT) dengan menambahkan berkas `LICENSE`.
