# Instalasi dan Konfigurasi Git: Dasar

## Konsep

Sebelum bisa memakai Git, kamu perlu menginstallnya dan melakukan konfigurasi identitas. Identitas ini akan tercantum di setiap commit: penting untuk kolaborasi agar tahu siapa yang membuat perubahan.

**Analogi:** Instalasi Git seperti membeli buku catatan baru. Konfigurasi `user.name` dan `user.email` seperti menulis nama di sampul buku: semua orang tahu buku itu milik siapa. Git menyimpan konfigurasi di tiga level: `--system` (semua user), `--global` (satu user), dan `--local` (satu repository).

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

### Konfigurasi Awal

```bash
git config --global user.name "Nama Kamu"
git config --global user.email "email@example.com"
git config --global core.editor "code --wait"   # pakai VS Code
git config --global --list                       # lihat semua konfigurasi
```

### Cek Versi

```bash
git --version
```

## Contoh Praktik

1. Buka terminal (atau Git Bash di Windows)
2. Cek apakah Git sudah terinstal:
   ```bash
   git --version
   ```
3. Jika belum terinstal, ikuti perintah instalasi sesuai OS kamu
4. Setelah terinstal, atur identitas:
   ```bash
   git config --global user.name "Budi Santoso"
   git config --global user.email "budi@example.com"
   ```
5. Verifikasi konfigurasi:
   ```bash
   git config --global --list
   ```
   Output akan menampilkan:
   ```
   user.name=Budi Santoso
   user.email=budi@example.com
   ```

Tips: Gunakan email yang sama dengan akun GitHub/GitLab kamu agar commit tercantum di profil.

## Kesalahan Umum

1. **Lupa set `user.name` dan `user.email`**: Git akan memperingatkan atau menggunakan nama sistem yang mungkin tidak sesuai. Selalu set konfigurasi global dulu.
2. **Salah set `core.editor`**: Jika pakai VS Code, gunakan `"code --wait"` (dengan --wait). Jika pakai nano: `git config --global core.editor "nano"`.
3. **Mengira `git config` harus diulang setiap repo**: `--global` cukup sekali. Konfigurasi global berlaku untuk semua repository di komputer kamu.

## Ringkasan

- Install Git via package manager (Linux), Homebrew (macOS), atau git-scm.com (Windows)
- Setelah install, konfigurasi `user.name` dan `user.email`
- Gunakan `git config --global --list` untuk verifikasi
- Konfigurasi cukup sekali, berlaku untuk semua repository

## Navigasi

Sebelumnya: [01-pengenalan-git.md](./01-pengenalan-git.md)

Berikutnya: [03-membuat-repository.md](./03-membuat-repository.md)
