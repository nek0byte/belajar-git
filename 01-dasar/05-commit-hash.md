# Commit dan Hash: Identitas Unik Setiap Snapshot | Dasar

## Konsep

Setiap kali kamu membuat commit, Git secara otomatis memberikan sebuah **tanda tangan digital** unik yang disebut **hash** (atau *commit hash*). Hash ini adalah string sepanjang **40 karakter** yang terdiri dari angka heksadesimal (0–9 dan a–f).

Bayangkan setiap commit seperti sebuah buku di perpustakaan raksasa. Setiap buku punya **nomor ISBN** yang berbeda: tidak ada dua buku yang punya ISBN sama. Begitu juga dengan commit: setiap commit punya hash yang **unik secara global**. Git menggunakan algoritma **SHA-1** untuk menghasilkan hash ini.

Yang membuat hash istimewa: hash dihitung dari **seluruh isi commit**: termasuk file apa saja yang berubah, siapa pembuatnya, pesan commit, dan bahkan hash commit sebelumnya. Artinya, jika ada satu bit data pun yang berubah di masa depan, hash commit itu akan berbeda. Inilah cara Git menjaga **integritas data**: kamu bisa tahu apakah suatu commit pernah diubah atau tidak.

Kamu tidak perlu menghafal hash sepanjang 40 karakter itu. Git menyediakan **hash pendek** (*short hash*) yang cukup 7 karakter pertama: sudah unik di repository kamu.

## Perintah / Sintaks

```bash
# Melihat daftar commit dengan hash pendek (7 karakter)
git log --oneline

# Melihat detail commit dengan hash penuh
git log

# Melihat hash spesifik
git show <hash-pendek>
git show <hash-panjang>
```

Opsi penting `git log`:

| Opsi | Fungsi |
|------|--------|
| `--oneline` | Tampilkan tiap commit dalam 1 baris: hash pendek + pesan |
| `--graph` | Tampilkan grafik branching |
| `--all` | Tampilkan semua branch, bukan cuma branch aktif |

## Contoh Praktik

Buka terminal dan ikuti langkah-langkah ini:

```bash
# 1. Buat folder proyek baru
mkdir belajar-hash
cd belajar-hash
git init

# 2. Buat file pertama
echo "Hello Git" > hello.txt
git add hello.txt
git commit -m "Commit pertama"

# 3. Lihat hash commit yang baru dibuat
git log --oneline
# Output: abc1234 (7 karakter): Commit pertama

# 4. Lihat hash panjang
git log
# Output: commit abc1234def5678... (40 karakter)

# 5. Buat commit kedua
echo "Baris kedua" >> hello.txt
git add hello.txt
git commit -m "Commit kedua"

# 6. Lihat kedua commit
git log --oneline
# Output:
# def5678 Commit kedua
# abc1234 Commit pertama
```

Coba lihat perubahan pada commit tertentu dengan hash pendek:

```bash
git show abc1234
```

## Kesalahan Umum

**1. Mencoba menghafal hash commit**

Tidak perlu! Gunakan hash pendek (7 karakter) atau biarkan Git yang mengelola. Gunakan `git log --oneline` untuk melihat daftar yang mudah dibaca.

**2. Mengira hash bisa berubah setelah commit dibuat**

Hash commit bersifat **immutable** (tidak bisa diubah). Jika ada yang berubah, hash-nya juga berubah total: artinya itu commit yang berbeda.

**3. Bingung membedakan hash dengan pesan commit**

Hash adalah identitas unik (40 karakter), pesan commit adalah deskripsi buatan manusia. Gunakan `git log --oneline` untuk melihat keduanya berdampingan.

## Ringkasan

- Setiap commit memiliki hash SHA-1 unik sepanjang 40 karakter
- Hash pendek (7 karakter pertama) sudah cukup untuk penggunaan sehari-hari
- Hash menjaga integritas data: jika data diubah, hash berubah
- Gunakan `git log --oneline` untuk melihat daftar commit dengan hash pendek
- Hash bersifat immutable: tidak bisa diubah setelah commit dibuat

## Navigasi

- Sebelumnya: [Git Workflow: Working Directory, Staging Area, Repository](04-git-workflow.md)
- Berikutnya: [Menambah File ke Repository](06-menambah-file.md)
