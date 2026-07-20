# Menambah File ke Repository | Dasar

## Konsep

Saat kamu membuat file baru di folder proyek Git, file itu awalnya berada dalam status **untracked**: Git tahu file itu ada, tapi belum "mengawasi" perubahannya. Untuk mulai melacak file, kamu harus melewati dua tahap:

1. **Staging** (`git add`): memberitahu Git: "saya ingin memasukkan file ini ke commit berikutnya"
2. **Commit** (`git commit`): menyimpan snapshot ke repository

Analogi: bayangkan kamu sedang mengemas barang untuk pindah rumah.

- **Untracked** = barang baru yang masih berserakan di lantai, belum diputuskan apakah ikut dibawa atau tidak
- **Staging area** = kardus tempat kamu memasukkan barang yang sudah siap dipindahkan
- **Committed** = kardus sudah diikat dan dimasukkan ke truk: aman tersimpan

Kamu bisa menambahkan satu file, beberapa file, atau semua file sekaligus ke staging area sebelum di-commit.

## Perintah / Sintaks

```bash
# Mengecek status file di repository
git status

# Menambahkan satu file ke staging area
git add <nama-file>

# Menambahkan semua file (baru + yang diubah) ke staging area
git add .

# Menambahkan beberapa file sekaligus
git add file1.txt file2.txt file3.txt

# Membuat commit dengan pesan langsung
git commit -m "Pesan commit"

# Membuat commit: akan membuka editor teks untuk menulis pesan
git commit
```

Opsi penting `git add`:

| Opsi | Fungsi |
|------|--------|
| `.` | Tambahkan semua file dari folder saat ini |
| `-A` / `--all` | Tambahkan semua file dari seluruh repository |
| `-p` | Tambahkan file secara interaktif per bagian (*hunk*) |

## Contoh Praktik

Buka terminal dan ikuti langkah ini:

```bash
# 1. Buat folder proyek baru
cd ~/belajar-git
mkdir proyek-pertama
cd proyek-pertama
git init

# 2. Buat file baru
echo "Halo Dunia" > index.txt

# 3. Cek status: file akan muncul sebagai "untracked"
git status
# Output:
# Untracked files:
#   index.txt

# 4. Tambahkan file ke staging area
git add index.txt

# 5. Cek status lagi: file sekarang "staged"
git status
# Output:
# Changes to be committed:
#   new file:   index.txt

# 6. Commit file tersebut
git commit -m "Menambahkan file index.txt"

# 7. Cek status: sekarang bersih (clean)
git status
# Output:
# nothing to commit, working tree clean
```

Coba juga tambahkan banyak file sekaligus:

```bash
echo "File kedua" > file2.txt
echo "File ketiga" > file3.txt
git add .
git status
git commit -m "Menambahkan dua file sekaligus"
```

## Kesalahan Umum

**1. Lupa `git add` lalu langsung `git commit`**

Git akan menolak commit karena tidak ada yang masuk staging. Solusi: jalankan `git add` dulu, baru `git commit`.

**2. Mengira `git add .` menambahkan semua file termasuk yang tidak diinginkan**

`git add .` hanya menambahkan dari folder saat ini. Gunakan `git add -A` jika ingin mencakup seluruh repository. File yang ada di `.gitignore` tetap tidak ikut.

**3. Menambah file besar (>100 MB) ke repository Git**

Git tidak dirancang untuk file besar. Gunakan Git LFS atau pertimbangkan ulang apakah file besar perlu di-commit. File besar akan memperlambat clone dan fetch.

## Ringkasan

- File baru dimulai sebagai **untracked**: Git belum melacaknya
- `git add` memindahkan file ke staging area
- `git commit` menyimpan snapshot staging area ke repository
- `git status` adalah sahabatmu: cek terus status file sebelum commit
- Siklus dasar: untracked → staged → committed

## Navigasi

- Sebelumnya: [Commit dan Hash: Identitas Unik Setiap Snapshot](05-commit-hash.md)
- Berikutnya: [Mengubah File yang Sudah di-Track](07-mengubah-file.md)
