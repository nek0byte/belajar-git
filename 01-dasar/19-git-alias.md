# Git Alias: Membuat Singkatan Command

## Konsep

Mengetik `git checkout` atau `git log --oneline --graph --all` berulang kali bisa membosankan. Git Alias memungkinkan kamu membuat singkatan kustom: misalnya `git co` untuk `git checkout`, atau `git lg` untuk `git log --oneline --graph`.

Alias disimpan di file konfigurasi Git (`~/.gitconfig`). Kamu bisa membuatnya via command atau mengedit file tersebut langsung.

## Perintah / Sintaks

```bash
# Alias sederhana
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status

# Alias dengan argumen (pakai tanda kutip)
git config --global alias.lg "log --oneline --graph --all"

# Alias untuk perintah yang butuh tanda petik
git config --global alias.unstage "reset HEAD --"

# Lihat daftar alias
git config --global --get-regexp alias

# Hapus alias
git config --global --unset alias.co
```

## Contoh Praktik

1. Buat alias untuk `checkout`:

   ```bash
   git config --global alias.co checkout
   ```

2. Buat alias untuk log graph:

   ```bash
   git config --global alias.lg "log --oneline --graph --all"
   ```

3. Gunakan alias:

   ```bash
   git co main       # sama dengan git checkout main
   git lg            # sama dengan git log --oneline --graph --all
   ```

4. Cek file konfigurasi: buka `~/.gitconfig` dan lihat bagian `[alias]`:

   ```ini
   [alias]
       co = checkout
       lg = log --oneline --graph --all
   ```

## Kesalahan Umum

1. **Alias bentrok dengan perintah Git**: jangan buat alias dengan nama yang sama persis dengan perintah Git bawaan (misal `alias.commit = ...`). Pilih nama singkat yang unik seperti `ci` untuk commit.

2. **Lupa `--global`**: tanpa `--global`, alias hanya berlaku untuk repository saat ini. Biasanya alias digunakan secara global.

3. **Alias tidak bekerja di shell lain**: alias Git hanya bekerja di dalam Git. Untuk alias shell (misal `gco` sebagai pengganti `git checkout`), gunakan alias shell di `~/.bashrc` atau `~/.zshrc`.

## Ringkasan

- Git alias membuat singkatan untuk command panjang
- `git config --global alias.<nama> "<perintah>"` untuk membuat alias global
- Alias disimpan di `~/.gitconfig` bagian `[alias]`
- Gunakan `--unset` untuk menghapus alias

## Navigasi

- Sebelumnya: [Git Blame](18-git-blame.md)
- Berikutnya:: (lanjut ke [Branching](../02-lanjutan/01-konsep-branching.md))
