# Pengenalan Git

## Konsep

Git adalah Version Control System terdistribusi yang dibuat oleh **Linus Torvalds** pada tahun **2005**. Awalnya Git dibuat untuk mengelola pengembangan kernel Linux karena VCS sebelumnya (BitKeeper) tidak bisa digunakan gratis lagi.

**Analogi:** Git seperti **mesin waktu untuk kode kamu**. Setiap kali kamu merasa "kode ini bekerja, jangan sampai rusak", kamu bisa membuat *snapshot* (commit). Kalau nanti ada yang error, cukup mundur ke snapshot sebelumnya. Git juga seperti **Google Docs untuk kode**: banyak orang bisa mengedit file yang sama tanpa saling timpa.

Perbedaan utama Git dengan VCS lain (seperti SVN):

| Aspek | SVN (Terpusat) | Git (Terdistribusi) |
| --- | --- | --- |
| Server mati | Sejarah hilang, kerja berhenti | Tetap kerja, punya salinan penuh |
| Kecepatan | Lambat karena tiap operasi ke server | Cepat karena hampir semua operasi lokal |
| Branching | Berat dan lambat | Ringan dan cepat |
| Offline | Tidak bisa commit | Bisa commit, push nanti |

Keunggulan Git:

- **Snapshot, bukan patch**: VCS lain menyimpan perubahan (delta). Git menyimpan snapshot seluruh file setiap commit.
- **Hampir semua operasi lokal**: karena setiap clone adalah full repository, sebagian besar perintah berjalan tanpa jaringan.
- **Integritas data**: semuanya di-checksum dengan SHA-1 hash. Git tidak bisa berubah tanpa ketahuan.
- **Branching murah**: bikin branch di Git hanya membuat pointer, bukan copy file.

## Perintah / Sintaks

### Instalasi

**Linux (Debian/Ubuntu):**

```bash
sudo apt update
sudo apt install git
```

**Linux (Fedora/RHEL):**

```bash
sudo dnf install git
```

**macOS (pakai Homebrew):**

```bash
brew install git
```

**Windows:** Unduh installer dari [git-scm.com](https://git-scm.com) lalu jalankan. Centang "Git Bash" saat instalasi.

### Cek Versi

```bash
git --version
```

## Contoh Praktik

1. Buka terminal/command prompt
2. Ketik `git --version`
3. Jika muncul seperti `git version 2.40.0`, Git sudah siap
4. Jika muncul `command not found`, kamu perlu install Git (lihat materi selanjutnya)

## Kesalahan Umum

1. **Mengira Git = GitHub**: Git adalah *tools*-nya, GitHub adalah *layanan hosting*-nya. Kamu bisa pakai Git tanpa GitHub.
2. **Takut pakai Git karena banyak perintah**: cukup kuasai 5-6 perintah dasar dulu, sisanya dipelajari bertahap.
3. **Menganggap Git sulit karena konsep hash dan tree**: pahami alur kerja (workflow) dulu, detail teknis bisa menyusul.

## Ringkasan

- Git dibuat Linus Torvalds (2005) untuk kernel Linux
- VCS terdistribusi: setiap orang punya salinan repository penuh
- Snapshot-based, hampir semua operasi lokal, integritas tinggi
- Branching di Git cepat dan ringan
- Git beda dengan GitHub

## Navigasi

Sebelumnya: [00-pengenalan-version-control.md](./00-pengenalan-version-control.md)

Berikutnya: [02-instalasi-dan-konfigurasi.md](./02-instalasi-dan-konfigurasi.md)
