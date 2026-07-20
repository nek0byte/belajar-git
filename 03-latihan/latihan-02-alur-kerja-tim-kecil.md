# Latihan 2: Alur Kerja Tim Kecil

## Tugas

Kerjakan langkah-langkah berikut. Coba selesaikan sendiri dulu sebelum membuka Solusi.

### 1. Buat Repository Pusat (Bare Repository)

Buat folder `repo-pusat.git` sebagai *bare repository* (repo pusat tanpa working directory). Ini akan menjadi pengganti GitHub untuk simulasi.

### 2. User A: Clone & Buat Branch Fitur

Clone repo pusat ke folder `user-a`. Buat branch `fitur-satu`, pindah ke branch itu, lalu buat file `fitur-satu.html` dengan isi HTML sederhana. Commit perubahan tersebut.

### 3. User B: Clone & Buat Branch Fitur Juga

Clone repo pusat ke folder `user-b`. Buat branch `fitur-dua`, pindah ke branch itu, lalu buat file `fitur-dua.html` dengan isi HTML sederhana. Commit.

### 4. User A: Push Branch ke Repo Pusat

Push branch `fitur-satu` ke repo pusat.

### 5. User B: Push Branch ke Repo Pusat

Push branch `fitur-dua` ke repo pusat.

### 6. User A: Merge `fitur-satu` ke `main`

Pindah ke branch `main`, lalu merge `fitur-satu` ke dalamnya. Push `main` yang sudah diperbarui ke repo pusat.

### 7. User B: Merge `fitur-dua` ke `main` (Ada Konflik)

User B juga melakukan hal yang sama: pindah ke `main`, merge `fitur-dua` ke dalamnya, lalu push. Tapi karena `main` sudah berubah, User B harus *pull* dulu. Pull ini akan menghasilkan **merge commit**.

### 8. User B: Push Hasil Merge

Setelah merge berhasil, User B push `main` ke repo pusat.

### 9. User A: Tarik Perubahan Terbaru

User A menarik perubahan terbaru dari `main` di repo pusat ke folder `user-a`.

### 10. Verifikasi: Cek Log

Di folder `user-a` dan `user-b`, jalankan `git log --oneline --graph --all` untuk melihat riwayat branching dan merging.

---

## Solusi

Jalankan perintah-perintah di bawah secara berurutan. Buka dua terminal atau lakukan satu per satu.

### 1. Buat Repository Pusat

```bash
mkdir repo-pusat
cd repo-pusat
git init --bare repo-pusat.git
cd ..
```

Sekarang kita punya `repo-pusat/repo-pusat.git` sebagai remote pusat.

### 2. User A: Clone & Branch Fitur

```bash
git clone repo-pusat/repo-pusat.git user-a
cd user-a

git checkout -b fitur-satu

echo '<!DOCTYPE html>
<html>
<head><title>Fitur Satu</title></head>
<body>
  <h1>Fitur Satu</h1>
</body>
</html>' > fitur-satu.html

git add fitur-satu.html
git commit -m "feat: halaman keranjang belanja"

cd ..
```

### 3. User B: Clone & Branch Fitur

```bash
git clone repo-pusat/repo-pusat.git user-b
cd user-b

git checkout -b fitur-dua

echo '<!DOCTYPE html>
<html>
<head><title>Fitur Dua</title></head>
<body>
  <h1>Fitur Dua</h1>
</body>
</html>' > fitur-dua.html

git add fitur-dua.html
git commit -m "feat: halaman login"

cd ..
```

### 4. User A: Push Branch

```bash
cd user-a
git push origin fitur-satu
cd ..
```

### 5. User B: Push Branch

```bash
cd user-b
git push origin fitur-dua
cd ..
```

### 6. User A: Merge ke main & Push

```bash
cd user-a
git checkout main
git merge fitur-satu
git push origin main
cd ..
```

### 7. User B: Merge ke main (Pull Dulu)

```bash
cd user-b
git checkout main
git pull origin main
git merge fitur-dua
```

Jika tidak ada konflik, lanjut:

```bash
git push origin main
cd ..
```

### 8. User B: Push (Sudah di atas)

### 9. User A: Tarik Perubahan

```bash
cd user-a
git pull origin main
cd ..
```

### 10. Verifikasi

```bash
cd user-a
git log --oneline --graph --all --decorate
```

Kamu akan melihat grafik seperti ini:

```
*   abc1234 (HEAD -> main, origin/main) Merge branch 'fitur-dua'
|\
| * def5678 (origin/fitur-dua) feat: halaman login
* |   fed4321 (origin/fitur-satu) Merge branch 'fitur-satu'
|\ \
| */  ghi9012 feat: halaman keranjang belanja
|/
o   awal1234 Initial commit
```

---

## Navigasi

- Sebelumnya: [Latihan 1: Repository Pertama](latihan-01-repository-pertama.md)
- Selanjutnya: [Latihan 3: Menyelesaikan Merge Conflict](latihan-03-menyelesaikan-conflict.md)
