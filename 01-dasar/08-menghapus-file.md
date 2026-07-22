# Menghapus File dari Repository

## Konsep

Menghapus file di Git tidak cukup hanya dengan `rm file.txt` (hapus manual). Hapus manual memang menghilangkan file dari working directory, tapi Git masih menganggap file itu ada. Kamu tetap harus memberi tahu Git bahwa file itu sengaja dihapus.

Ada dua cara:

1. **Hapus manual + `git add`**: hapus file dengan `rm`, lalu stage penghapusan itu dengan `git add`
2. **`git rm`**: hapus file dari disk dan langsung stage penghapusannya dalam satu langkah

`git rm` sebenarnya sama dengan `rm file && git add file`: tapi lebih praktis karena sekali jalan.

Ada satu varian penting: `git rm --cached`. Perintah ini menghapus file dari **staging area dan repository** (pada commit berikutnya), tapi **tidak menyentuh file di working directory**. Ini berguna ketika kamu ingin berhenti melacak file tertentu tanpa menghapusnya dari komputer.

Analogi: bayangkan kamu punya foto di album, dan fotonya juga ditempel di dinding.

- `git rm` = mencabut foto dari dinding **dan** membuang fotonya
- `git rm --cached` = mencabut foto dari dinding saja, fotonya tetap aman di album
- Hapus manual (`rm`) = membuang foto dari album tanpa bilang ke siapa-siapa: fotonya hilang dari dinding, tapi album tetap mencatatnya

## Perintah / Sintaks

```bash
# Hapus file dari working directory + staging (langsung)
git rm <nama-file>

# Hapus file dari staging saja, tetap di working directory
git rm --cached <nama-file>

# Hapus folder beserta isinya
git rm -r <nama-folder>

# Hapus beberapa file sekaligus
git rm file1.txt file2.txt file3.txt

# Setelah git rm, jangan lupa commit
git commit -m "Hapus file yang tidak diperlukan"
```

Opsi penting `git rm`:

| Opsi | Fungsi |
|------|--------|
| `--cached` | Hapus dari index/staging, file tetap di working directory |
| `-r` | Hapus folder secara rekursif |
| `-n` | Simulasi (dry-run): lihat file apa yang akan dihapus tanpa benar-benar menghapus |

## Contoh Praktik

### Contoh 1: `git rm`: Hapus file sekaligus

```bash
# 1. Buat proyek
cd ~/belajar-git
mkdir latihan-hapus
cd latihan-hapus
git init

# 2. Buat beberapa file
echo "Ini file A" > file-a.txt
echo "Ini file B" > file-b.txt
echo "Rahasia" > rahasia.txt
git add .
git commit -m "Commit awal: tiga file"

# 3. Hapus file-a dengan git rm
git rm file-a.txt
# Output: rm 'file-a.txt'

# 4. Cek status: langsung ter-staging
git status
# Output:
# Changes to be committed:
#   deleted:    file-a.txt

# 5. Commit penghapusan
git commit -m "Hapus file-a.txt yang tidak diperlukan"
```

### Contoh 2: `git rm --cached`: Hapus dari tracking saja

```bash
# Katakanlah rahasia.txt tidak sengaja ikut di-commit
# Tapi kamu ingin file-nya tetap ada di komputer

git rm --cached rahasia.txt

# Cek status: rahasia.txt masih ada di folder!
ls
# Output: file-b.txt  rahasia.txt

git status
# Output:
# Changes to be committed:
#   deleted:    rahasia.txt
# Untracked files:
#   rahasia.txt  <-- file masih ada, tapi sekarang tidak di-track

git commit -m "Berhenti melacak rahasia.txt"
```

### Contoh 3: Hapus manual vs `git rm`

```bash
# Hapus manual
rm file-b.txt
git status
# Output:
# Changes not staged for commit:
#   deleted:    file-b.txt
# Perhatikan: statusnya "not staged": kamu masih harus git add

git add file-b.txt
git commit -m "Hapus file-b.txt secara manual"
```

## Kesalahan Umum

**1. Hanya `rm file` tanpa commit**

File memang hilang dari folder, tapi Git masih menyimpan snapshot terakhir yang berisi file itu. Commit penghapusan diperlukan agar Git tahu bahwa file itu sengaja dihapus.

**2. Mengira `git rm --cached` akan menghapus file dari hard disk**

Tidak! `--cached` hanya menghapus file dari index Git. File fisik tetap utuh. Gunakan `--cached` jika kamu ingin Git berhenti melacak file, bukan menghapusnya.

**3. `git rm` pada file yang belum di-commit**

`git rm` hanya bekerja pada file yang sudah di-track (pernah di-commit). Untuk file untracked, cukup hapus manual dengan `rm`.

## Ringkasan

- `git rm` = hapus file dari disk + stage penghapusan, sekali jalan
- `git rm --cached` = hapus dari index/staging saja, file tetap di disk
- Hapus manual (`rm`) tetap perlu `git add` untuk mencatat penghapusan
- Setelah `git rm`, jangan lupa commit
- Gunakan `git rm --cached` untuk berhenti melacak file tanpa menghapusnya

## Navigasi

- Sebelumnya: [Mengubah File yang Sudah di-Track](07-mengubah-file.md)
- Berikutnya: [Membatalkan Perubahan: Restore dan Checkout](09-membatalkan-perubahan.md)
