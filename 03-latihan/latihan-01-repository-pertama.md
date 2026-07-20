# Latihan 1: Repository Pertamaku

## Tugas

Kerjakan langkah-langkah berikut di terminal kamu. **Jangan lihat solusi dulu**: coba selesaikan sendiri. Jika benar-benar buntu, baru buka bagian Solusi di bawah.

### 1. Inisialisasi Repository

Buat folder baru bernama `latihan-1`, masuk ke dalam folder tersebut, lalu inisialisasi repository Git di dalamnya.

### 2. Buat File Index HTML

Buat file `index.html` dengan isi HTML dasar (judul "Aplikasi Saya"). Simpan file tersebut ke dalam staging area, lalu commit dengan pesan "feat: tambah halaman utama".

### 3. Buat File README

Buat file `README.md` yang berisi deskripsi singkat tentang proyek latihan. Commit file tersebut dengan pesan "docs: tambah README".

### 4. Ubah Index HTML

Edit `index.html`: tambahkan satu paragraf `<p>Selamat datang di aplikasiku!</p>` setelah `<body>`. Simpan perubahan ke staging area lalu commit dengan pesan "feat: tambah paragraf selamat datang".

### 5. Lihat Riwayat Commit

Gunakan perintah untuk melihat seluruh riwayat commit yang sudah kamu buat. Perhatikan pesan, hash, author, dan tanggal setiap commit.

### 6. Ubah Nama File

Ubah nama `index.html` menjadi `utama.html` menggunakan Git (bukan `mv` biasa). Commit perubahan nama tersebut dengan pesan "rename: index.html ke utama.html".

### 7. Buat File .gitignore

Buat file `.gitignore` yang berisi aturan untuk mengabaikan:

- Semua file `.log`
- Folder `cache/`
- File `.env`

Commit file `.gitignore` tersebut.

### 8. Hapus File

Hapus file `utama.html` menggunakan Git. Commit penghapusan tersebut.

### 9. Lihat Log dalam Format Singkat

Gunakan opsi `--oneline` atau `--pretty=oneline` untuk melihat log dalam format satu baris per commit.

### 10. Cek Status

Di akhir latihan, jalankan `git status` untuk memastikan working directory bersih (tidak ada file yang belum di-track atau belum di-commit).

---

## Solusi

Gunakan solusi di bawah ini **setelah** kamu mencoba sendiri. Solusi ini hanya salah satu cara: tidak harus persis sama selama tujuannya tercapai.

### 1. Inisialisasi Repository

```bash
mkdir latihan-1
cd latihan-1
git init
```

Output:

```
Initialized empty Git repository in /home/kamu/latihan-1/.git/
```

### 2. Buat File Index HTML

```bash
echo '<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Aplikasi Saya</title>
</head>
<body>
  <h1>Aplikasi Saya</h1>
</body>
</html>' > index.html

git add index.html
git commit -m "feat: tambah halaman utama"
```

### 3. Buat File README

```bash
echo "# Aplikasi Saya

Ini adalah proyek latihan untuk belajar Git." > README.md

git add README.md
git commit -m "docs: tambah README"
```

### 4. Ubah Index HTML

```bash
# Edit index.html: tambahkan baris setelah <body>
# Bisa pakai echo >> atau editor teks
sed -i '/<body>/a\  <p>Selamat datang di aplikasiku!</p>' index.html

git add index.html
git commit -m "feat: tambah paragraf selamat datang"
```

### 5. Lihat Riwayat Commit

```bash
git log
```

Perhatikan ada 3 commit: halaman utama, README, dan paragraf selamat datang.

### 6. Ubah Nama File

```bash
git mv index.html utama.html
git commit -m "rename: index.html ke utama.html"
```

### 7. Buat File .gitignore

```bash
echo '*.log
cache/
.env' > .gitignore

git add .gitignore
git commit -m "chore: tambah gitignore"
```

### 8. Hapus File

```bash
git rm utama.html
git commit -m "hapus utama.html"
```

### 9. Lihat Log Singkat

```bash
git log --oneline
```

Output kurang lebih:

```
a1b2c3d hapus utama.html
d4e5f6g chore: tambah gitignore
h7i8j9k rename: index.html ke utama.html
l0m1n2o feat: tambah paragraf selamat datang
p3q4r5s docs: tambah README
t6u7v8w feat: tambah halaman utama
```

### 10. Cek Status

```bash
git status
```

Output: `nothing to commit, working tree clean`

---

## Navigasi

- Sebelumnya: [Git Alias](../01-dasar/19-git-alias.md)
- Selanjutnya: [Latihan 2: Alur Kerja Tim Kecil](latihan-02-alur-kerja-tim-kecil.md)
