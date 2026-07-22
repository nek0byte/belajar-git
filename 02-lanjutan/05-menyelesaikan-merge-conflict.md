# Menyelesaikan Merge Conflict

## Konsep

Merge conflict terjadi ketika Git tidak bisa secara otomatis menggabungkan perubahan dari dua branch karena **keduanya mengubah baris yang sama pada file yang sama**. Git tidak tahu versi mana yang benar: kamu harus memutuskan secara manual.

**Analogi:** Bayangkan dua orang sekaligus mengedit paragraf yang sama di dokumen Google Docs. Orang pertama menulis "warna merah", orang kedua menulis "warna biru". Google Docs tidak bisa memilih; ia akan menunjukkan kedua versi dan memintamu memutuskan. Git melakukan hal yang sama: menandai area konflik dengan marker khusus.

Saat konflik terjadi, Git:
1. Menghentikan proses merge
2. Menandai file yang konflik dengan marker `<<<<<<<`, `=======`, `>>>>>>>`
3. Membiarkanmu mengedit file untuk memilih versi final
4. Setelah selesai, kamu `git add` file tersebut dan `git commit` untuk menyelesaikan merge

## Perintah / Sintaks

```bash
# Melihat file yang konflik
git status

# Melihat detail konflik (diff)
git diff

# Membatalkan merge dan kembali ke keadaan sebelum merge
git merge --abort

# Setelah menyelesaikan konflik secara manual
git add <file>
git commit
```

## Contoh Praktik

1. Buat situasi konflik:

```bash
git init repo-conflict
cd repo-conflict
echo "Warna favorit saya: merah" > warna.txt
git add warna.txt && git commit -m "init: warna"

git switch -c fitur-biru
echo "Warna favorit saya: biru" > warna.txt
git add warna.txt && git commit -m "ubah ke biru"

git switch main
echo "Warna favorit saya: hijau" > warna.txt
git add warna.txt && git commit -m "ubah ke hijau"
```

2. Coba merge: akan terjadi konflik:

```bash
git merge fitur-biru
```

Output:
```
Auto-merging warna.txt
CONFLICT (content): Merge conflict in warna.txt
Automatic merge failed; fix conflicts and then commit the result.
```

3. Lihat status dan isi file:

```bash
git status
cat warna.txt
```

Isi `warna.txt` akan seperti ini:
```
<<<<<<< HEAD
Warna favorit saya: hijau
=======
Warna favorit saya: biru
>>>>>>> fitur-biru
```

- `<<<<<<< HEAD`: versi dari branch tujuan (main)
- `=======`: pemisah antara dua versi
- `>>>>>>> fitur-biru`: versi dari branch sumber

4. Selesaikan konflik: edit file untuk memilih satu versi:

```bash
echo "Warna favorit saya: biru" > warna.txt
```

5. Finalisasi merge:

```bash
git add warna.txt
git commit -m "resolve conflict warna: pilih biru"
git log --oneline --graph
```

Merge selesai dengan konflik terselesaikan.

### Alternatif: Batalkan merge

Jika kamu merasa bingung atau salah langkah, batalkan merge:

```bash
git merge --abort
```

Ini mengembalikan repository ke keadaan sebelum `git merge` dijalankan.

## Kesalahan Umum

1. **Tidak sengaja meninggalkan marker konflik**: Setelah edit, pastikan tidak ada `<<<<<<<`, `=======`, atau `>>>>>>>` yang tersisa. Cari dengan `grep` jika perlu.

2. **Panik dan hapus semua isi file**: Baca dulu kedua versi, pahami perbedaannya. Jangan asal hapus. Gunakan `git diff` untuk melihat konflik dengan lebih jelas.

3. **Lupa `git add` setelah memperbaiki konflik**: Git hanya tahu konflik selesai setelah kamu `git add` file yang diperbaiki. Setelah `git add`, lanjutkan dengan `git commit`.

## Ringkasan

- Konflik terjadi saat dua branch mengubah baris yang sama
- Marker konflik: `<<<<<<< HEAD`, `=======`, `>>>>>>> <branch>`
- Edit file secara manual untuk memilih versi final
- `git add <file>` → `git commit` untuk menyelesaikan merge
- `git merge --abort` untuk membatalkan merge kapan saja
- Konflik itu wajar, bukan kesalahan: latihan membuatmu terbiasa

## Navigasi

- Sebelumnya: [Fast-Forward vs 3-Way Merge](04-fast-forward-vs-3-way-merge.md)
- Berikutnya: [Git Stash](06-git-stash.md)
