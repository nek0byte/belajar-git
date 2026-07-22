# Compare Commit: Melihat Perbedaan Antar Commit

## Konsep

`git diff` adalah perintah untuk melihat **perubahan**: apa yang berbeda antara
dua keadaan: working directory vs staging area, staging area vs commit terakhir,
atau dua commit mana pun.

Bayangkan kamu punya dua versi dokumen: versi asli dan versi yang sudah
diedit. Kamu ingin tahu garis mana yang berubah tanpa membaca ulang seluruh
dokumen. `git diff` adalah seperti **fitur "bandingkan"** yang menyoroti
perubahan baris per baris.

## Perintah / Sintaks

```bash
# Bandingkan working directory dengan staging area (file yang belum di-add)
git diff

# Bandingkan staging area dengan commit terakhir (file yang sudah di-add)
git diff --staged

# Bandingkan dua commit spesifik
git diff <hash1> <hash2>

# Bandingkan commit terakhir dengan commit sebelumnya
git diff HEAD~1 HEAD

# Bandingkan branch
git diff branch1 branch2

# Diff hanya untuk file tertentu
git diff -- <nama-file>
```

## Contoh Praktik

1. Siapkan repository dengan satu commit:

```bash
git init bandingkan
cd bandingkan

echo "halo dunia" > file.txt
git add file.txt
git commit -m "commit awal"
```

1. Ubah file tanpa staging:

```bash
echo "baris baru" >> file.txt
git diff
```

Output akan menunjukkan `+baris baru` (tanda `+` = baris ditambahkan).

1. Stage perubahan, lalu diff staged vs commit terakhir:

```bash
git add file.txt
git diff --staged
```

1. Bandingkan commit pertama dengan commit kedua:

```bash
echo "baris ketiga" >> file.txt
git add file.txt
git commit -m "commit kedua"

git log --oneline
git diff <hash-commit1> <hash-commit2>
```

Atau gunakan referensi HEAD:

```bash
git diff HEAD~1 HEAD
```

## Kesalahan Umum

| Kesalahan | Penjelasan | Cara Perbaiki |
| ----------- | ----------- | --------------- |
| `git diff` tidak menampilkan apa-apa | Semua perubahan sudah di-stage | Gunakan `git diff --staged` |
| Output diff kosong setelah add | `git diff` hanya melihat perubahan yang belum di-stage | Gunakan `git diff --staged` untuk melihat perubahan yang sudah di-add |
| Bingung dengan format diff | Baris `+` = tambahan, `-` = hapusan, `@@` = lokasi baris | Fokus pada baris yang dimulai dengan `+` atau `-` |

## Ringkasan

- `git diff` = perubahan yang belum di-stage
- `git diff --staged` = perubahan yang sudah di-stage (siap commit)
- `git diff <hash1> <hash2>` = perbandingan dua commit
- `HEAD` = commit terakhir, `HEAD~1` = satu commit sebelumnya
- Baris dengan `+` artinya ditambahkan, `-` artinya dihapus

## Navigasi

- Sebelumnya: [Commit Log](10-commit-log.md)
- Berikutnya: [Rename File](12-rename-file.md)
