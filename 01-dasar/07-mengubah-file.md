# Mengubah File yang Sudah di-Track | Dasar

## Konsep

Setelah sebuah file di-track (pernah di-commit), Git mulai mengawasi setiap perubahannya. Saat kamu mengubah isi file tersebut, statusnya berubah menjadi **modified**.

Siklus untuk file yang sudah di-track:

```
Modified → (git add) → Staged → (git commit) → Committed
```

Berbeda dengan file baru (untracked), file yang sudah di-track tidak akan muncul sebagai "untracked": Git sudah tahu keberadaannya dan langsung mendeteksi perubahannya.

Analogi: bayangkan daftar belanja di ponselmu.

- **Committed** = daftar belanja yang sudah final dan tersimpan
- **Modified** = kamu mengedit daftar belanja, menambah atau menghapus item: perubahannya terlihat, tapi belum disimpan
- **Staged** = kamu mencentang item yang sudah yakin ingin disimpan
- **Committed** lagi = kamu menekan tombol simpan, daftar baru tersimpan

Kamu bisa mengecek **apa yang berubah** sebelum menambahkan ke staging dengan `git diff`. Ini sangat berguna untuk memastikan perubahan yang kamu buat memang yang kamu inginkan.

## Perintah / Sintaks

```bash
# Melihat status file
git status

# Melihat perubahan yang belum di-stage
git diff

# Melihat perubahan yang sudah di-stage
git diff --staged

# Menambahkan file yang diubah ke staging area
git add <nama-file>

# Menambahkan semua file yang diubah
git add .

# Commit perubahan
git commit -m "Pesan commit"
```

## Contoh Praktik

Ikuti langkah ini di terminal:

```bash
# 1. Buat proyek baru
cd ~/belajar-git
mkdir latihan-ubah
cd latihan-ubah
git init

# 2. Buat file pertama dan commit
echo "Baris 1: Halo Dunia" > catatan.txt
git add catatan.txt
git commit -m "Commit awal: menambah catatan.txt"

# 3. Sekarang ubah file tersebut
echo "Baris 2: Halo dari Git" >> catatan.txt

# 4. Cek status: file muncul sebagai "modified"
git status
# Output:
# Changes not staged for commit:
#   modified:   catatan.txt

# 5. Lihat apa yang berubah
git diff
# Output:
# --- a/catatan.txt
# +++ b/catatan.txt
# @@ -1 +1,2 @@
#  Baris 1: Halo Dunia
# +Baris 2: Halo dari Git

# 6. Stage perubahan dan commit
git add catatan.txt
git commit -m "Menambahkan baris kedua ke catatan.txt"

# 7. Verifikasi riwayat
git log --oneline
# Output:
# def4567 Menambahkan baris kedua ke catatan.txt
# abc1234 Commit awal: menambah catatan.txt
```

Coba ubah beberapa file sekaligus:

```bash
echo "File baru" > tambahan.txt
echo "Baris baru" >> catatan.txt
git status
# Ada modified dan untracked
git add .
git status
# Semua masuk staging
git commit -m "Menambah file baru dan mengubah catatan"
```

## Kesalahan Umum

**1. Langsung commit tanpa `git add`**

Perubahan file hanya ada di working directory, belum di staging. Commit tidak akan menyertakan perubahan itu. Selalu `git add` dulu.

**2. Lupa mengecek perubahan dengan `git diff`**

Kamu kira yang berubah hanya satu baris, ternyata ada perubahan lain yang tidak sengaja. Biasakan `git diff` sebelum `git add`.

**3. Mengira `git add .` hanya menambahkan file yang diubah**

`git add .` menambahkan semua perubahan: file baru (untracked), file diubah (modified), dan file dihapus (deleted). Gunakan dengan hati-hati, atau `git add -p` untuk seleksi manual.

## Ringkasan

- File yang sudah di-track berubah status menjadi **modified** saat diubah
- Siklus: modified → `git add` → staged → `git commit` → committed
- `git diff` menunjukkan perubahan baris per baris sebelum di-stage
- Selalu cek `git status` untuk tahu posisi filemu
- `git add .` menambahkan semua perubahan sekaligus

## Navigasi

- Sebelumnya: [Menambah File ke Repository](06-menambah-file.md)
- Berikutnya: [Menghapus File dari Repository](08-menghapus-file.md)
