# Git Blame: Mencari Siapa yang Mengubah Baris Kode (Dasar)

## Konsep

`git blame` menampilkan setiap baris file beserta: hash commit, author, dan tanggal perubahan terakhir. Ini seperti "forensik" kode: kamu bisa tahu siapa yang menambahkan baris tertentu dan di commit mana.

Fitur ini sangat berguna saat kamu menemukan kode aneh dan ingin bertanya ke penulisnya, atau ingin tahu kapan sebuah baris terakhir diubah.

## Perintah / Sintaks

```bash
# Blame seluruh file
git blame <file>

# Blame hanya baris 10 sampai 20
git blame -L 10,20 <file>

# Blame dengan rentang dari baris 5 sebanyak 15 baris
git blame -L 5,+15 <file>
```

## Contoh Praktik

1. Buat file `app.js` dan commit beberapa kali dengan penulis berbeda:
   ```bash
   git add app.js
   git commit -m "Initial commit"
   # lalu edit baris tertentu dan commit lagi
   ```

2. Jalankan blame:
   ```bash
   git blame app.js
   ```

3. Output (contoh):
   ```
   a1b2c3d (Budi  2025-01-15 10:00:00 +0700  1) const app = express();
   e4f5g6h (Siti  2025-01-16 14:30:00 +0700  2) app.use(logger());
   i7j8k9l (Budi  2025-01-17 09:15:00 +0700  3) app.get('/', handler);
   ```

4. Lihat hanya baris 2-3:
   ```bash
   git blame -L 2,3 app.js
   ```

## Kesalahan Umum

1. **Menyalahkan orang tanpa konteks**: `git blame` hanya menunjukkan pengubah *terakhir*. Bisa jadi baris itu awalnya ditulis orang lain, lalu di-refactor oleh orang terakhir. Selalu cek riwayat commit untuk konteks penuh.

2. **Lupa bahwa whitespace change juga tercatat**: mengubah indentasi atau spasi akan mengubah blame meski logika tidak berubah. Gunakan `git blame -w` untuk mengabaikan whitespace.

3. **Mengira blame bisa untuk file yang belum di-commit**: `git blame` hanya bekerja pada file yang sudah pernah di-commit. File baru atau belum di-add tidak akan muncul.

## Ringkasan

- `git blame <file>` menampilkan author dan commit setiap baris
- `-L` untuk membatasi baris yang diperiksa
- `-w` mengabaikan perubahan whitespace
- Berguna untuk forensic kode dan kolaborasi tim

## Navigasi

- Sebelumnya: [Gitignore](17-gitignore.md)
- Berikutnya: [Git Alias](19-git-alias.md)
