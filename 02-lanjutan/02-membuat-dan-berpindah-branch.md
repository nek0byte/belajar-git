# Membuat dan Berpindah Branch

**Level:** Lanjutan

## Konsep

Setelah paham bahwa branch adalah pointer ke commit, langkah selanjutnya adalah membuat dan berpindah antar branch. Git menyediakan beberapa cara untuk ini: gaya lama (`checkout`) dan gaya baru (`switch`) yang diperkenalkan di Git 2.23 untuk membuat perintah lebih intuitif.

**Analogi:** Bayangkan kamu punya beberapa tab buku catatan. Tab `main` berisi catatan resmi. Kamu membuat tab baru bernama `fitur-login` (`git branch fitur-login`), lalu membalik halaman ke tab itu (`git switch fitur-login`). Semua tulisan setelahnya akan masuk ke tab `fitur-login`, bukan `main`. Tab `main` tetap aman seperti saat terakhir kamu tinggalkan.

## Perintah / Sintaks

```bash
# Membuat branch baru (tanpa pindah)
git branch <nama-branch>

# Berpindah ke branch (gaya lama)
git checkout <nama-branch>

# Berpindah ke branch (gaya baru: direkomendasikan)
git switch <nama-branch>

# Membuat branch sekaligus pindah (gaya lama)
git checkout -b <nama-branch>

# Membuat branch sekaligus pindah (gaya baru)
git switch -c <nama-branch>

# Kembali ke branch sebelumnya
git switch -
```

| Perintah | Keterangan |
|----------|------------|
| `git branch <nama>` | Buat branch baru, tetap di branch saat ini |
| `git checkout <nama>` | Pindah ke branch (gaya lama, multi-fungsi) |
| `git switch <nama>` | Pindah ke branch (gaya baru, fokus) |
| `git checkout -b <nama>` | Buat + pindah (gaya lama) |
| `git switch -c <nama>` | Buat + pindah (gaya baru) |

**Rekomendasi:** Gunakan `git switch` untuk berpindah branch dan `git switch -c` untuk membuat+pindah. Perintah `checkout` masih berfungsi penuh, tetapi `switch` lebih eksplisit dan tidak mudah tertukar dengan perintah lain.

## Contoh Praktik

1. Buat repository dan commit awal:

```bash
git init repo-switch
cd repo-switch
echo "Halaman utama" > index.html
git add index.html
git commit -m "init: halaman utama"
```

2. Buat branch fitur tanpa pindah:

```bash
git branch fitur-navbar
git branch   # * main, fitur-navbar
```

3. Pindah ke branch fitur menggunakan `switch`:

```bash
git switch fitur-navbar
git branch   # main, * fitur-navbar
```

4. Buat perubahan di branch fitur:

```bash
echo "<nav>Menu</nav>" >> index.html
git add index.html
git commit -m "tambah navbar"
```

5. Kembali ke `main` dan lihat perbedaannya:

```bash
git switch main
cat index.html  # hanya "Halaman utama": perubahan navbar tidak ada di sini
```

6. Buat branch baru sekaligus pindah (shortcut):

```bash
git switch -c fitur-footer
echo "<footer>Footer</footer>" >> index.html
git add index.html
git commit -m "tambah footer"
git switch main
```

Setiap branch memiliki **riwayat commit yang independen**. Perubahan di satu branch tidak memengaruhi branch lain sampai kamu menggabungkannya (merge).

## Kesalahan Umum

1. **Lupa commit sebelum pindah**: Jika ada perubahan yang belum di-commit, Git biasanya menolak pindah untuk menjaga konsistensi. Solusi: `git stash` (simpan sementara) atau commit dulu.

2. **Menggunakan `checkout` tanpa sadar untuk hal lain**: `git checkout` juga bisa digunakan untuk mengembalikan file. Jika tidak hati-hati, kamu bisa menimpa file. Gunakan `switch` untuk menghindari kebingungan ini.

3. **Bingung antara `git branch` dan `git checkout -b`**: `git branch` hanya membuat; `git checkout -b` atau `git switch -c` membuat sekaligus pindah.

## Ringkasan

- `git branch <nama>`: membuat branch baru (tetap di branch saat ini)
- `git switch <nama>`: pindah ke branch (gaya baru, direkomendasikan)
- `git switch -c <nama>`: buat dan pindah dalam satu langkah
- `git checkout <nama>`: pindah branch (gaya lama)
- `git checkout -b <nama>`: buat dan pindah (gaya lama)
- Setiap branch memiliki riwayat commit sendiri-sendiri

## Navigasi

- Sebelumnya: [Konsep Branching](01-konsep-branching.md)
- Berikutnya: [Merge Branch](03-merge-branch.md)
