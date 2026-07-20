# Membatalkan Perubahan: Restore dan Checkout | Dasar

## Konsep

Kadang kamu membuat perubahan, lalu sadar itu salah. Atau kamu tidak sengaja menambahkan file ke staging area yang belum siap di-commit. Git menyediakan cara untuk **membatalkan perubahan** di berbagai tahap.

Ada tiga skenario umum:

1. **File sudah diubah (modified) tapi belum di-stage**: kamu ingin mengembalikannya ke versi terakhir yang di-commit
2. **File sudah di-stage, tapi belum di-commit**: kamu ingin mengeluarkannya dari staging, tapi tetap menyimpan perubahan di working directory
3. **File sudah di-stage, dan kamu ingin membatalkan semuanya sekaligus**: kembalikan ke kondisi commit terakhir

Sebelum Git 2.23 (2019), semua ini dilakukan dengan `git checkout -- <file>`. Sekarang Git menyarankan menggunakan `git restore` yang lebih intuitif.

Analogi: bayangkan kamu sedang melukis.

- **Working directory** = kanvas yang sedang kamu lukis
- **Staging area** = meja di sampingmu tempat kamu meletakkan kuas yang sudah siap
- **Commit** = foto hasil lukisan yang sudah jadi

Kalau kamu tidak suka coretan di kanvas (modified), kamu ambil kanvas baru dari foto terakhir (`git restore`). Kalau kamu tidak jadi menaruh kuas di meja (staged), kamu ambil saja kuasnya kembali: coretan di kanvas tetap ada (`git restore --staged`).

![Diagram checkout: memulihkan file dari staging ke working directory](https://marklodato.github.io/visual-git-guide/checkout-files.svg.png)

## Perintah / Sintaks

```bash
# [CARA BARU - Git >= 2.23] Kembalikan file yang diubah ke versi commit terakhir
git restore <nama-file>

# Keluarkan file dari staging area (perubahan tetap ada di working directory)
git restore --staged <nama-file>

# Keluarkan dari staging DAN kembalikan ke versi commit terakhir
git restore --staged --worktree <nama-file>
# Atau
git restore -SW <nama-file>

# [CARA LAMA] Masih berfungsi di semua versi Git
git checkout -- <nama-file>
```

Opsi penting `git restore`:

| Opsi | Fungsi |
|------|--------|
| `--staged` / `-S` | Targetkan index (staging area) saja |
| `--worktree` / `-W` | Targetkan working directory saja |
| `--source=<tree>` / `-s` | Ambil konten dari commit tertentu (bukan HEAD) |

## Contoh Praktik

### Skenario 1: Batalkan perubahan di working directory (modified)

```bash
# 1. Setup
cd ~/belajar-git
mkdir latihan-restore
cd latihan-restore
git init
echo "Isi asli" > dokumen.txt
git add dokumen.txt
git commit -m "Commit awal"

# 2. Ubah file: sengaja salah
echo "Isi yang salah" > dokumen.txt

# 3. Cek status
git status
# Output: modified: dokumen.txt

# 4. Batalkan perubahan: kembalikan ke versi commit terakhir
git restore dokumen.txt

# 5. Cek file: kembali ke "Isi asli"
cat dokumen.txt
# Output: Isi asli
```

### Skenario 2: Keluarkan file dari staging area

```bash
# 1. Ubah file
echo "Perubahan baru" > dokumen.txt

# 2. Stage file
git add dokumen.txt

# 3. Eits, ternyata belum siap di-commit
git restore --staged dokumen.txt

# 4. Cek status: file masih modified, tapi sudah tidak di stage
git status
# Output: modified: dokumen.txt (not staged)
```

### Skenario 3: Batalkan semuanya (dari staging + working directory)

```bash
# 1. Ubah dan stage
echo "Perubahan lain" > dokumen.txt
git add dokumen.txt

# 2. Batalkan total: staging + perubahan
git restore --staged --worktree dokumen.txt

# 3. Cek: bersih, file kembali ke "Isi asli"
cat dokumen.txt
# Output: Isi asli
git status
# Output: nothing to commit
```

### Skenario 4: Kembalikan ke versi dari commit tertentu

```bash
# Buat commit kedua
echo "Commit kedua" > dokumen.txt
git add dokumen.txt
git commit -m "Commit kedua"

# Sekarang ubah lagi
echo "Isi rusak" > dokumen.txt

# Kembalikan ke versi commit pertama (bukan HEAD)
git restore --source=HEAD~1 dokumen.txt
cat dokumen.txt
# Output: Isi asli
```

## Kesalahan Umum

**1. Mengira `git restore` akan menghapus perubahan yang sudah di-commit**

Tidak. `git restore` hanya bekerja pada file yang **belum di-commit**. Untuk membatalkan commit, gunakan `git reset` atau `git revert`.

**2. Lupa menambahkan nama file: menjalankan `git restore` tanpa argumen**

`git restore` tanpa nama file akan error. Kamu harus menyebutkan file spesifik atau gunakan `git restore .` untuk semua file.

**3. Tidak sengaja kehilangan perubahan karena belum di-commit**

`git restore` akan **menimpa** file di disk dengan versi dari commit. Jika perubahanmu belum di-commit, perubahan itu **hilang permanen**. Pastikan benar-benar yakin sebelum menjalankan `git restore` tanpa `--staged`.

## Ringkasan

- `git restore <file>`: batalkan perubahan di working directory
- `git restore --staged <file>`: keluarkan file dari staging, perubahan tetap ada
- `git restore --staged --worktree <file>`: batalkan staging + perubahan file
- `git checkout -- <file>`: cara lama, masih berfungsi
- `git restore` tidak bisa membatalkan commit: gunakan `git reset` atau `git revert`
- Hati-hati: perubahan yang belum di-commit bisa hilang permanen

## Navigasi

- Sebelumnya: [Menghapus File dari Repository](08-menghapus-file.md)
- Berikutnya: [Commit Log: Melihat Riwayat Repository](10-commit-log.md)
