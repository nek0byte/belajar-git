# Latihan 3: Menyelesaikan Merge Conflict

**Level:** Latihan

## Tugas

Kerjakan langkah-langkah berikut. Coba selesaikan sendiri dulu sebelum membuka Solusi.

### 1. Buat Bare Repository & Initial Commit

Buat bare repository `repo-pusat.git`. Clone ke folder `user-a`. Buat file `daftar.txt` dengan isi:

```
Beras
Gula
Telur
Minyak
```

Commit dan push ke `main`.

### 2. Clone ke Folder Kedua

Clone repo pusat ke folder `user-b`.

### 3. User A: Buat & Edit di Branch `fitur-a`

Di folder `user-a`, buat branch baru `fitur-a`. Ubah baris "Telur" menjadi "Susu". Commit.

### 4. User B: Buat & Edit di Branch `fitur-b`

Di folder `user-b`, buat branch baru `fitur-b`. Ubah baris **yang sama** ("Telur") menjadi "Kopi". Commit.

### 5. User A: Merge `fitur-a` ke `main` & Push

Kembali ke branch `main` di `user-a`, merge `fitur-a`, lalu push ke repo pusat.

### 6. User B: Merge `fitur-b` ke `main`

User B kembali ke `main`, lalu mencoba merge `fitur-b`. Karena baris yang sama sudah diubah, Git akan memunculkan **CONFLICT**.

### 7. User B: Selesaikan Konflik Manual

User B membuka file `daftar.txt`, melihat tanda konflik, lalu memutuskan isinya menjadi: "Susu & Kopi" (menggabungkan kedua perubahan). Hapus tanda `<<<<<<<`, `=======`, dan `>>>>>>>`.

### 8. User B: Stage & Commit Hasil Penyelesaian

Setelah file diperbaiki, stage file tersebut dan commit. Jangan lupa push ke repo pusat.

### 9. User A: Tarik Perubahan

Di folder `user-a`, tarik perubahan dari `main`. Pastikan tidak ada konflik baru.

### 10. Verifikasi: Cek Isi File

Buka `daftar.txt` di kedua folder. Isinya harus sama: "Susu & Kopi".

---

## Solusi

### 1. Buat Bare Repository & Initial Commit

```bash
mkdir repo-pusat
cd repo-pusat
git init --bare repo-pusat.git
cd ..

git clone repo-pusat/repo-pusat.git user-a
cd user-a

echo -e "Beras\nGula\nTelur\nMinyak" > daftar.txt

git add daftar.txt
git commit -m "feat: daftar belanja awal"
git push origin main

cd ..
```

### 2. Clone ke Folder Kedua

```bash
git clone repo-pusat/repo-pusat.git user-b
cd ..
```

### 3. User A: Branch & Edit

```bash
cd user-a
git checkout -b fitur-a

# Ganti "Telur" dengan "Susu"
sed -i 's/^Telur$/Susu/' daftar.txt

git add daftar.txt
git commit -m "ubah telur jadi susu"

cd ..
```

### 4. User B: Branch & Edit

```bash
cd user-b
git checkout -b fitur-b

# Ganti "Telur" dengan "Kopi"
sed -i 's/^Telur$/Kopi/' daftar.txt

git add daftar.txt
git commit -m "ubah telur jadi kopi"

cd ..
```

### 5. User A: Merge ke main & Push

```bash
cd user-a
git checkout main
git merge fitur-a
git push origin main

cd ..
```

### 6. User B: Merge (Konflik Muncul)

```bash
cd user-b
git checkout main
git pull origin main
git merge fitur-b
```

Git akan menampilkan pesan konflik:

```
Auto-merging daftar.txt
CONFLICT (content): Merge conflict in daftar.txt
Automatic merge failed; fix conflicts and then commit the result.
```

### 7. User B: Selesaikan Konflik

Buka `daftar.txt`. Isinya akan terlihat seperti ini:

```
Beras
Gula
<<<<<<< HEAD
Susu
=======
Kopi
>>>>>>> fitur-b
Minyak
```

Edit file tersebut menjadi:

```
Beras
Gula
Susu & Kopi
Minyak
```

Hapus semua tanda konflik (`<<<<<<<`, `=======`, `>>>>>>>`).

### 8. User B: Stage & Commit

```bash
git add daftar.txt
git commit -m "resolve conflict: gabung susu dan kopi"
git push origin main

cd ..
```

### 9. User A: Tarik Perubahan

```bash
cd user-a
git pull origin main
```

Seharusnya tidak ada konflik karena kita hanya menarik hasil merge yang sudah diselesaikan.

### 10. Verifikasi

```bash
cat daftar.txt
# Output:
# Beras
# Gula
# Susu & Kopi
# Minyak

cd ../user-b
cat daftar.txt
# Output harus sama
```

---

### Catatan Penting

- Saat konflik, Git **tidak menghapus data**: ia hanya memberi tanda batas. kamu sebagai developer yang memutuskan hasil akhirnya.
- Jangan takut dengan konflik. Konflik itu wajar, bukan error. Git hanya meminta bantuanmu untuk menentukan versi final.
- Selalu cek isi file setelah conflict resolution: jangan asal hapus tanda kurung tanpa membaca isinya.

---

## Navigasi

- Sebelumnya: [Latihan 2: Alur Kerja Tim Kecil](latihan-02-alur-kerja-tim-kecil.md)
- Kembali ke: [README](../README.md)
