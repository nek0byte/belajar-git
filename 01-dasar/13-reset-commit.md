# Reset Commit: Kembali ke Commit Sebelumnya | **Dasar**

## Konsep

`git reset` adalah perintah untuk **memundurkan** repository ke commit tertentu.
Ini seperti mesin waktu: kamu bisa kembali ke masa lalu dan "menghapus" commit
yang ada di atasnya.

Ada tiga mode reset, yang menentukan apa yang terjadi pada perubahan:

- **--soft**: commit dihapus, staging area dan working directory tetap
- **--mixed** (default): commit dan staging dihapus, working directory tetap
- **--hard**: semua dihapus: commit, staging, **dan perubahan di file**

Bayangkan kamu menulis 3 halaman, lalu ingin kembali ke halaman 1:

- `--soft`: halaman 2-3 tetap di meja (staging), siap di-commit ulang
- `--mixed`: halaman 2-3 dikembalikan ke laci (working directory), belum siap
- `--hard`: halaman 2-3 dibuang sepenuhnya: **tidak bisa kembali**

## Perintah / Sintaks

```bash
# Reset commit terakhir, staging tetap, working directory tetap
git reset --soft HEAD~1

# Reset commit terakhir, staging dikosongkan, working directory tetap (DEFAULT)
git reset --mixed HEAD~1

# Reset commit terakhir, semuanya dihapus: HATI-HATI!
git reset --hard HEAD~1

# Reset ke commit spesifik (bukan HEAD~1)
git reset --hard <hash-commit>

# Batalkan reset: lihat ORIG_HEAD
git reset --hard ORIG_HEAD
```

## Contoh Praktik

1. Siapkan repository dengan beberapa commit:

```bash
git init belajar-reset
cd belajar-reset

echo "baris 1" > file.txt
git add file.txt
git commit -m "commit 1"

echo "baris 2" >> file.txt
git add file.txt
git commit -m "commit 2"

echo "baris 3" >> file.txt
git add file.txt
git commit -m "commit 3"
```

2. Coba `git reset --soft HEAD~1`:

```bash
git reset --soft HEAD~1
git status        # file.txt masih di staging area
git log --oneline # commit 3 sudah hilang
git diff --staged # perubahan "baris 3" masih ada
```

3. Coba `git reset --mixed HEAD~1` (default):

```bash
# Dari posisi setelah soft reset di atas
git reset HEAD~1  # sama dengan --mixed
git status        # perubahan ada di working directory (belum di-stage)
```

4. Coba `git reset --hard HEAD~1`: **PERHATIAN**:

```bash
# Pastikan tidak ada perubahan yang belum di-commit!
git reset --hard HEAD~1
git status        # bersih
cat file.txt      # hanya "baris 1"
```

## Kesalahan Umum

| Kesalahan | Penjelasan | Cara Perbaiki |
|-----------|-----------|---------------|
| `git reset --hard` tanpa commit | Perubahan di working directory hilang permanen | Selalu `git status` dulu sebelum `--hard` |
| Reset terlalu jauh | Tidak sengaja reset lebih dari yang diinginkan | Gunakan `git reflog` untuk menemukan commit yang hilang |
| Mengira reset = delete permanen | Commit yang di-reset masih ada di reflog selama 30-90 hari | Cek `git reflog` dan `git reset --hard <hash>` |
| Reset commit yang sudah di-push | Akan menyebabkan masalah dengan remote | Jangan reset commit yang sudah di-push; gunakan `git revert` |

## Peringatan ⚠️

`git reset --hard` **akan menghapus perubahan yang belum di-commit** secara
permanen. Selalu jalankan `git status` dan pastikan tidak ada perubahan penting
yang belum di-stage sebelum menjalankan `--hard`.

## Ringkasan

- `git reset` memundurkan branch ke commit tertentu
- `--soft`: hapus commit, staging tetap
- `--mixed` (default): hapus commit dan staging, working directory tetap
- `--hard`: hapus commit, staging, **dan perubahan file**: berbahaya!
- ORIG_HEAD menyimpan posisi HEAD sebelum reset: bisa untuk membatalkan reset
- Jangan reset commit yang sudah di-push ke remote

## Navigasi

- Sebelumnya: [Rename File](12-rename-file.md)
- Berikutnya: [Amend Commit](14-amend-commit.md)
