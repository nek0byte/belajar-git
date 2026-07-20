# Git Stash: Menyimpan Perubahan Sementara

**Level:** Lanjutan

## Konsep

Saat kamu sedang mengerjakan sesuatu tetapi belum siap commit, lalu tiba-tiba perlu pindah branch untuk memperbaiki bug darurat, apa yang harus dilakukan? Commit setengah jadi tidak ideal. Solusinya: **stash**.

Git stash menyimpan perubahan pada working directory (tracked files) ke dalam **stack** sementara, membuat working directory kembali bersih seperti commit terakhir. Nanti, setelah urusan lain selesai, kamu bisa mengembalikan perubahan tersebut.

**Analogi:** Bayangkan kamu sedang merakit model pesawat di meja kerja (working directory). Bos datang minta kamu urus dokumen mendesak. Kamu tidak mau berantakan, jadi kamu **masukkan semua komponen pesawat ke dalam laci** (stash): meja kembali rapi. Setelah urusan selesai, kamu **ambil lagi dari laci** (stash pop) dan lanjutkan merakit.

Penting: stash hanya menyimpan **tracked files** (file yang sudah pernah di-add). File baru yang belum pernah di-add tidak otomatis ikut ke stash: kamu perlu flag `--include-untracked` atau `-u`.

## Perintah / Sintaks

```bash
# Simpan perubahan (tracked files)
git stash

# Simpan perubahan dengan pesan
git stash push -m "pesan deskriptif"

# Simpan termasuk file untracked
git stash -u

# Melihat daftar stash
git stash list

# Mengembalikan stash TERAKHIR + hapus dari stack
git stash pop

# Mengembalikan stash tertentu tanpa hapus
git stash apply stash@{n}

# Hapus stash tertentu dari stack
git stash drop stash@{n}

# Hapus semua stash
git stash clear

# Lihat isi stash tanpa apply
git stash show stash@{n}
git stash show -p stash@{n}   # lihat detail diff
```

| Perintah | Kegunaan |
|----------|----------|
| `git stash` | Simpan tracked files ke stack |
| `git stash -u` | Simpan termasuk untracked files |
| `git stash push -m "msg"` | Simpan dengan pesan (lebih eksplisit) |
| `git stash list` | Tampilkan semua stash |
| `git stash pop` | Kembalikan stash teratas + hapus |
| `git stash apply` | Kembalikan stash tanpa hapus |
| `git stash drop` | Hapus stash tertentu |
| `git stash clear` | Hapus semua stash |
| `git stash show` | Ringkasan file yang berubah di stash |

## Contoh Praktik

1. Setup repository dan buat perubahan setengah jadi:

```bash
git init repo-stash
cd repo-stash
echo "Halaman utama" > index.html
git add index.html && git commit -m "init: index"
```

2. Mulai fitur baru: belum selesai, tapi ada bug darurat:

```bash
echo "<h1>Judul Baru</h1>" >> index.html
echo "style.css" > style.css   # file baru, untracked
```

3. Simpan perubahan ke stash:

```bash
git stash -u -m "WIP: fitur judul dan style"
git stash list
```

Working directory sekarang bersih: `index.html` kembali ke isi commit terakhir.

4. Pindah branch, perbaiki bug, commit:

```bash
git switch -c hotfix
echo "<fix>Bug diperbaiki</fix>" >> index.html
git add index.html && git commit -m "hotfix: perbaiki bug"
git switch main
```

5. Kembalikan stash:

```bash
git stash pop   # mengembalikan stash@{0} dan menghapusnya dari stack
```

File `index.html` kembali berisi tambahan `<h1>Judul Baru</h1>`, dan `style.css` (untracked) kembali muncul.

### Multiple Stash

Kamu bisa punya beberapa stash sekaligus:

```bash
git stash push -m "WIP fitur A"
git stash push -m "WIP fitur B"
git stash list
```

Hasil:
```
stash@{0}: On main: WIP fitur B
stash@{1}: On main: WIP fitur A
```

Stash bersifat LIFO (Last In, First Out): seperti tumpukan piring. `stash@{0}` adalah yang terbaru. Untuk mengembalikan stash lama: `git stash apply stash@{1}`.

## Kesalahan Umum

1. **Lupa bahwa file untracked tidak ikut stash**: File baru (belum pernah `git add`) tidak otomatis ikut `git stash`. Gunakan `git stash -u` atau `git stash --include-untracked` jika ingin menyertakannya.

2. **Stash pop di branch yang salah**: Jika kamu `stash pop` di branch berbeda, perubahan bisa tercampur. Tidak salah secara teknis, tapi bisa membingungkan. Biasakan periksa branch tujuan dengan `git branch` sebelum `stash pop`.

3. **Menumpuk terlalu banyak stash**: Stash mudah terlupakan. Gunakan `git stash push -m "deskripsi"` agar jelas. Jika stash sudah tidak terpakai, bersihkan dengan `git stash clear`.

4. **Lupa bahwa stash tidak terikat branch**: Stash bisa di-pop dari branch mana pun. Ini berguna (misal: lupa pindah branch sebelum mulai kerja), tapi bisa membingungkan jika tidak hati-hati.

## Ringkasan

- `git stash` menyimpan perubahan sementara dan membersihkan working directory
- `git stash pop` mengembalikan stash terbaru + hapus dari stack
- `git stash apply` mengembalikan stash tanpa hapus dari stack
- `git stash list` melihat semua stash
- Gunakan `-u` untuk menyertakan untracked files
- Stash bersifat LIFO, beri pesan agar mudah diingat

## Navigasi

- Sebelumnya: [Menyelesaikan Merge Conflict](05-menyelesaikan-merge-conflict.md)
- Berikutnya: [Konsep Remote Repository](07-konsep-remote-repository.md)
