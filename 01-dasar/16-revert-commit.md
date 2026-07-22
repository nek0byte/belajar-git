# Revert Commit: Membatalkan Commit dengan Aman

## Konsep

`git revert` adalah cara aman untuk membatalkan perubahan. Alih-alih menghapus commit dari riwayat (seperti `git reset`), revert membuat **commit baru** yang isinya adalah kebalikan dari commit yang ingin dibatalkan.

Anggap saja seperti menulis surat pembetulan di buku tamu: alih-alih merobek halaman sebelumnya, kamu menambahkan halaman baru yang isinya "Maaf, yang tadi tidak jadi." Riwayat tetap utuh dan semua orang bisa melihat apa yang terjadi.

## Perintah / Sintaks

```bash
# Membatalkan commit terakhir
git revert HEAD

# Membatalkan commit tertentu
git revert <hash-commit>

# Membatalkan tanpa langsung membuat commit (staging dulu)
git revert --no-commit HEAD
```

## Contoh Praktik

1. Cek log commit:

   ```bash
   git log --oneline
   # a1b2c3d (HEAD -> main) Tambah banner iklan
   # e4f5g6h Perbaiki navbar
   ```

2. Commit terakhir (`a1b2c3d`) ternyata salah. Batalkan dengan revert:

   ```bash
   git revert HEAD
   ```

3. Git akan membuka editor untuk pesan commit revert (default: "Revert 'Tambah banner iklan'"). Simpan dan tutup.

4. Lihat log lagi: ada commit baru:

   ```bash
   git log --oneline
   # x9y8z7w (HEAD -> main) Revert "Tambah banner iklan"
   # a1b2c3d Tambah banner iklan
   # e4f5g6h Perbaiki navbar
   ```

   File `banner iklan` sudah hilang, tapi riwayat tetap lengkap.

## Kesalahan Umum

1. **Mengira revert menghapus commit**: revert justru *menambah* commit baru. Commit asli tetap ada di log.

2. **Revert commit yang sudah di-push**: tidak masalah. Karena revert cuma tambah commit baru, `git push` tetap aman. Berbeda dengan reset yang bisa bermasalah jika sudah di-push.

3. **Revert tapi lupa ada conflict**: jika commit yang direvert bersinggungan dengan perubahan lain, Git akan minta selesaikan conflict dulu, sama seperti merge biasa.

## Ringkasan

- `git revert` membatalkan perubahan dengan membuat commit baru
- Riwayat tetap utuh: cocok untuk commit yang sudah di-push
- `git reset` menghapus commit, `git revert` menambahkan commit pembatalan
- Bisa pakai `--no-commit` untuk menggabungkan beberapa revert dalam satu commit

## Navigasi

- Sebelumnya: [Melihat Versi Sebelumnya](15-melihat-versi-sebelumnya.md)
- Berikutnya: [Gitignore](17-gitignore.md)
