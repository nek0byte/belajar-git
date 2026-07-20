# Rename File: Memindahkan dan Mengganti Nama File | **Dasar**

## Konsep

Di Git, mengganti nama file sebenarnya adalah **operasi dua langkah**: hapus file
lama + buat file baru dengan konten sama. Git pintar: saat melihat file baru
mirip dengan file yang dihapus, Git akan menyimpulkan itu adalah **rename**.

Bayangkan kamu punya catatan di buku tulis berjudul "Catatan Lama". Kamu ingin
mengganti judulnya menjadi "Catatan Baru". Kamu harus merobek halaman lama lalu
menulis ulang isinya di halaman baru dengan judul baru. Git membaca ini sebagai
rename karena isinya sama persis.

## Perintah / Sintaks

```bash
# Rename file (cara Git)
git mv <nama-file-lama> <nama-file-baru>

# Pindahkan file ke folder
git mv <file> <folder/>

# Rename manual (tanpa git mv)
mv <lama> <baru>
git rm <lama>
git add <baru>
```

## Contoh Praktik

1. Siapkan repository:

```bash
git init rename-file
cd rename-file

echo "isi file" > catatan.txt
git add catatan.txt
git commit -m "menambah catatan.txt"
```

2. Ganti nama file dengan `git mv`:

```bash
git mv catatan.txt catatan-baru.txt
git status
```

Output akan menunjukkan: `renamed: catatan.txt -> catatan-baru.txt`

3. Commit rename tersebut:

```bash
git commit -m "rename catatan.txt menjadi catatan-baru.txt"
```

4. Pindahkan file ke subfolder:

```bash
git mv catatan-baru.txt dokumen/
git status
git commit -m "pindahkan file ke folder dokumen"
```

5. Lihat riwayat: Git tetap melacak bahwa file yang sama:

```bash
git log --follow -- dokumen/catatan-baru.txt
```

Opsi `--follow` memungkinkan Git menelusuri rename ke belakang.

## Rename Manual (Tanpa `git mv`)

Jika kamu rename lewat file manager atau `mv` biasa:

```bash
mv catatan.txt catatan-baru.txt
git status
```

Git akan melihat `catatan.txt` sebagai **deleted** dan `catatan-baru.txt`
sebagai **untracked**. Kamu harus staging keduanya secara manual:

```bash
git add catatan-baru.txt
git rm catatan.txt
git status  # sekarang terdeteksi sebagai renamed
```

## Kesalahan Umum

| Kesalahan | Penjelasan | Cara Perbaiki |
|-----------|-----------|---------------|
| Rename manual, lalu lupa `git rm` file lama | File lama masih ter-track | Jalankan `git rm <file-lama>` |
| Rename tapi isi file diubah total | Git mungkin tidak mendeteksi sebagai rename | Git tetap bisa melacak, tapi opsi `--follow` mungkin tidak akurat |
| Mengira `git mv` memindahkan isi file | `git mv` hanya memindahkan/mengganti nama, isi file tetap utuh | Cek isi dengan `cat <file>` |

## Ringkasan

- `git mv <lama> <baru>` = rename + stage dalam satu langkah
- Git mendeteksi rename secara otomatis (berdasarkan kesamaan konten)
- `git log --follow <file>` untuk melihat riwayat file yang di-rename
- Rename manual perlu `mv` + `git rm` + `git add` secara terpisah
- `git mv` juga bisa digunakan untuk memindahkan file ke folder lain

## Navigasi

- Sebelumnya: [Compare Commit](11-compare-commit.md)
- Berikutnya: [Reset Commit](13-reset-commit.md)
