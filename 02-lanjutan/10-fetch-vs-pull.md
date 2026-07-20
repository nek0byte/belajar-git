# Fetch vs Pull: Memahami Perbedaannya: Level: Lanjutan

## Konsep

`git fetch` dan `git pull` sama-sama mengambil data dari remote, tapi ada perbedaan fundamental:

| Operasi | Download data | Merge ke branch lokal |
|---------|--------------|----------------------|
| `git fetch` | Ya | Tidak |
| `git pull` | Ya | Ya (otomatis) |

Bayangkan seperti ini: remote repo adalah **perpustakaan**. `git fetch` adalah **melihat daftar buku baru yang tersedia**: kamu tahu ada buku baru, judulnya apa, tapi belum kamu pinjam. `git pull` adalah **meminjam bukunya langsung**: buku itu sudah ada di tanganmu.

Dengan `git fetch`, kamu bisa melihat perubahan yang dilakukan orang lain tanpa mengubah kondisi branch kerja kamu saat ini. Sangat berguna untuk **inspeksi dulu sebelum merge**.

Setelah fetch, perubahan tersimpan di remote tracking branch: `origin/nama-branch`. Kamu bisa membandingkannya dengan branch lokal menggunakan `git log` atau `git diff`, lalu memutuskan apakah akan merge.

## Perintah / Sintaks

**Fetch dari remote tertentu:**

```bash
git fetch origin
```

**Fetch semua remote:**

```bash
git fetch --all
```

**Fetch sambil hapus remote tracking branch yang sudah tidak ada:**

```bash
git fetch --prune
```

**Pull (fetch + merge langsung):**

```bash
git pull origin main
```

**Melihat perbedaan setelah fetch:**

```bash
git log --oneline main..origin/main
git diff main origin/main
```

## Contoh Praktik

**Skenario: fetch untuk lihat perubahan sebelum merge.**

1. Mulai dari repo yang terhubung ke remote:

```bash
git clone https://github.com/username/proyek.git
cd proyek
```

2. Anggap ada rekan tim yang sudah push ke `main`. Kita fetch dulu:

```bash
git fetch origin
```

3. Lihat apa saja yang berubah di remote:

```bash
git log --oneline main..origin/main
```
Ini menampilkan commit yang ada di `origin/main` tapi belum ada di `main` lokal.

4. Cek file-file yang berubah:

```bash
git diff --stat main origin/main
```

5. Setelah yakin, merge manual:

```bash
git merge origin/main
```

Atau lakukan pull langsung di langkah awal (yang menggabungkan fetch + merge dalam satu langkah).

**Fetch all untuk repo dengan banyak remote:**

```bash
git remote add upstream https://github.com/original/repo.git
git fetch --all
git log --oneline main..upstream/main
```

Ini berguna kalau kamu bekerja dengan fork (repo punya sendiri + repo asli/upstream).

**Menggunakan fetch untuk cek branch orang lain:**

```bash
git fetch origin
git checkout -b fitur-teman origin/fitur-teman
```

Ini membuat branch lokal yang melacak branch remote milik teman.

## Kesalahan Umum

1. **Lupa branch yang mau di-fetch**: `git fetch` tanpa argumen akan fetch semua branch dari remote. Kadang kamu cuma butuh satu branch. Gunakan `git fetch origin nama-branch` untuk fetch spesifik.

2. **Fetch, lupa merge, lanjut kerja**: Kamu fetch, lihat perubahan, lalu lupa merge dan mulai nulis kode baru. Nanti saat pull, baru sadar ada divergensi. Biasakan: setelah fetch, segera merge atau catat untuk di-merge nanti.

3. **Mengira fetch sudah memperbarui file kerja**: Fetch tidak mengubah file di working directory. Kalau kamu ingin file aktual berubah, kamu harus merge atau checkout setelah fetch. Pull melakukan ini otomatis.

## Ringkasan

- `git fetch` = download data tanpa merge → aman, tidak mengganggu kerja
- `git pull` = fetch + merge langsung → praktis tapi bisa timbul conflict
- Setelah fetch, perubahan ada di `origin/nama-branch`
- Gunakan `git log main..origin/main` untuk melihat perbedaan
- Fetch dulu, inspeksi, baru merge: workflow yang lebih terkontrol

## Navigasi

- Sebelumnya: [Push dan Pull](./09-push-dan-pull.md)
- Berikutnya: [Tracking Branch](./11-tracking-branch.md)
