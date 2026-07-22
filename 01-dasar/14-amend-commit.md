# Amend Commit: Memperbaiki Commit Terakhir

## Konsep

`git commit --amend` adalah perintah untuk **mengubah commit terakhir**: baik
pesan commit-nya, isinya (file yang di-commit), atau keduanya. Ini bukan
membuat commit baru, melainkan **mengganti** commit terakhir dengan versi yang
diperbaiki.

Bayangkan kamu mengirim surat, lalu sadar ada typo di amplopnya. Daripada
menulis surat baru, kamu buka amplop, perbaiki typo, lalu rekatkan lagi.
Amend adalah seperti itu: commit lamanya digantikan dengan yang baru
(termasuk hash baru).

## Perintah / Sintaks

```bash
# Perbaiki pesan commit terakhir
git commit --amend -m "pesan yang sudah diperbaiki"

# Tambahkan file yang terlupa ke commit terakhir
git add <file-terlupa>
git commit --amend --no-edit

# Amend + ubah pesan sekaligus
git add <file-terlupa>
git commit --amend -m "pesan baru dengan file tambahan"

# Amend tanpa mengubah pesan
git commit --amend --no-edit
```

## Contoh Praktik

1. Siapkan repository:

```bash
git init belajar-amend
cd belajar-amend

echo "file pertama" > file1.txt
git add file1.txt
git commit -m "manambah file1.txt"  # typo: "manambah"
```

1. Perbaiki pesan commit yang typo:

```bash
git commit --amend -m "menambah file1.txt"
```

1. Tambah file yang terlupa:

```bash
echo "file kedua" > file2.txt
git add file2.txt

# Gabungkan dengan commit terakhir tanpa ubah pesan
git commit --amend --no-edit
```

1. Cek: commit terakhir sekarang berisi kedua file:

```bash
git log --oneline
git show HEAD
```

Hash commit akan **berbeda** dari sebelumnya karena commit diganti.

## Melihat Hasil Amend

```bash
git log --oneline -1
git show HEAD --stat
```

## Kesalahan Umum

| Kesalahan | Penjelasan | Cara Perbaiki |
| ----------- | ----------- | --------------- |
| Amend commit yang sudah di-push | Mengubah riwayat yang sudah publik: menyulitkan kolaborator | Jangan amend commit yang sudah di-push. Gunakan `git revert` atau commit baru |
| Bingung hash berubah setelah amend | Wajar: amend menggantikan commit lama dengan yang baru | Hash pasti berubah. Jika perlu hash lama, cek `git reflog` |
| Lupa `git add` sebelum amend | Amend hanya mengubah staging terakhir | Stage dulu dengan `git add`, baru `git commit --amend` |

## Peringatan ⚠️

**Jangan amend commit yang sudah di-push ke remote!** Karena amend mengubah
riwayat (hash baru), push berikutnya akan ditolak. Jika terpaksa, gunakan
`git push --force-with-lease`: tapi pastikan timmu tahu.

## Ringkasan

- `git commit --amend` memperbaiki commit terakhir
- Bisa mengubah pesan commit, menambah file, atau keduanya
- Hash commit akan berubah setelah amend
- Aman digunakan untuk commit yang belum di-push
- Jangan amend commit yang sudah di-push ke remote

## Navigasi

- Sebelumnya: [Reset Commit](13-reset-commit.md)
- Berikutnya: [Melihat Versi Sebelumnya](15-melihat-versi-sebelumnya.md)
