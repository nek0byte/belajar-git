# Commit Log: Melihat Riwayat Commit

## Konsep

Setiap kali kamu melakukan `git commit`, Git menyimpan snapshot dari project-mu
beserta metadata-nya (siapa yang commit, kapan, dan pesan apa). Kumpulan commit
ini membentuk riwayat (history) yang bisa kamu lihat kapan saja: seperti buku
harian yang mencatat setiap perubahan yang pernah terjadi.

Bayangkan git log seperti **daftar isi buku harian**: kamu bisa melihat tanggal,
judul entry, dan penulisnya. Dengan opsi tambahan, kamu bahkan bisa melihat
detail isi entry-nya.

## Perintah / Sintaks

```bash
# Tampilkan semua commit (dari yang terbaru)
git log

# Tampilkan commit dalam satu baris per commit
git log --oneline

# Tampilkan commit dengan grafik branching
git log --graph

# Tampilkan commit dari semua branch
git log --all

# Tampilkan commit dengan patch (detail perubahan)
git log -p

# Filter commit berdasarkan author
git log --author="Nama Author"

# Batasi jumlah commit yang tampil
git log -5
```

## Contoh Praktik

1. Buat beberapa file dan commit untuk melihat riwayat:

```bash
git init riwayat-commit
cd riwayat-commit

echo "baris pertama" > file1.txt
git add file1.txt
git commit -m "commit pertama: menambah file1.txt"

echo "baris kedua" >> file1.txt
git add file1.txt
git commit -m "commit kedua: mengubah file1.txt"

echo "file baru" > file2.txt
git add file2.txt
git commit -m "commit ketiga: menambah file2.txt"
```

1. Lihat semua riwayat commit:

```bash
git log
```

1. Lihat dengan format satu baris:

```bash
git log --oneline
```

1. Lihat detail perubahan setiap commit:

```bash
git log -p
```

1. Filter author (ganti dengan nama kamu):

```bash
git log --author="$(git config user.name)"
```

## Kesalahan Umum

| Kesalahan | Penjelasan | Cara Perbaiki |
| ----------- | ----------- | --------------- |
| Log terlalu panjang | `git log` menampilkan semua commit: bisa puluhan halaman | Gunakan `git log --oneline -5` untuk membatasi jumlah |
| Tidak ada commit muncul | Mungkin kamu lupa commit, atau ada di branch lain | Coba `git log --all` untuk lihat semua branch |
| Bingung membaca hash | Hash commit panjang (40 karakter) | Cukup gunakan 7 karakter pertama untuk operasi Git |

## Ringkasan

- `git log` menampilkan riwayat commit secara kronologis (terbaru di atas)
- `--oneline` memadatkan setiap commit jadi satu baris
- `--graph` menampilkan hubungan antar branch secara visual
- `--all` menampilkan commit dari semua branch
- `-p` menampilkan diff untuk setiap commit
- `--author` memfilter commit berdasarkan penulis

## Navigasi

- Sebelumnya: [Membatalkan Perubahan](09-membatalkan-perubahan.md)
- Berikutnya: [Compare Commit](11-compare-commit.md)
