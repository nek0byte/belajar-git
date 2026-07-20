# Melihat Versi Sebelumnya: Checkout Commit Lama (Dasar)

## Konsep

Bayi Git menyimpan setiap commit sebagai **snapshot utuh** dari seluruh file proyek. Dengan `git checkout <hash>`, kamu bisa "teleport" ke snapshot lama. Git akan mengubah isi folder kerja persis seperti saat commit itu dibuat.

Saat kamu berada di commit lama, HEAD terlepas dari branch: ini disebut **detached HEAD state**. Kamu bisa melihat-lihat, tapi jika kamu membuat commit baru di sini, commit itu tidak terhubung ke branch mana pun dan bisa hilang. Untuk kembali aman, cukup `git checkout main`.

## Perintah / Sintaks

```bash
# Melihat seluruh isi proyek pada commit tertentu
git checkout <hash-commit>

# Mengembalikan satu file dari commit lama (tanpa pindah commit)
git checkout <hash-commit> -- <file>

# Kembali ke branch utama
git checkout main
```

## Contoh Praktik

1. Lihat riwayat commit:
   ```bash
   git log --oneline
   # a1b2c3d (HEAD -> main) Update index.html
   # e4f5g6h Tambah style.css
   # i7j8k9l Inisialisasi proyek
   ```

2. Checkout ke commit kedua (`e4f5g6h`):
   ```bash
   git checkout e4f5g6h
   ```

   Output akan memberitahu: *You are in 'detached HEAD' state.*

3. Lihat file-file yang ada: isinya sesuai snapshot lama.

4. Kembali ke branch main:
   ```bash
   git checkout main
   ```

5. Ambil satu file dari commit lama tanpa pindah:
   ```bash
   git checkout e4f5g6h -- index.html
   ```
   File `index.html` sekarang berisi versi dari commit `e4f5g6h`.

## Kesalahan Umum

1. **Membuat commit di detached HEAD**: commit baru tidak terhubung ke branch mana pun. Saat kembali ke main, commit itu seolah "hilang". Solusi: buat branch baru dengan `git branch <nama-branch>` sebelum checkout kalau ingin menyimpan perubahan.

2. **Lupa kembali ke branch**: setelah checkout commit lama, jangan edit file lalu commit tanpa sadar. Selalu `git checkout main` dulu.

3. **Mengira checkout menghapus riwayat**: checkout hanya mengubah isi folder kerja. Riwayat commit tetap aman.

## Ringkasan

- `git checkout <hash>` menampilkan snapshot lama dalam *detached HEAD*
- Jangan membuat commit baru di detached HEAD tanpa membuat branch
- `git checkout <hash> -- <file>` mengambil satu file dari commit tertentu
- Kembali ke branch dengan `git checkout <nama-branch>`

## Navigasi

- Sebelumnya: [Amend Commit](14-amend-commit.md)
- Berikutnya: [Revert Commit](16-revert-commit.md)
