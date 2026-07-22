# Membuat Repository Git

## Konsep

Repository (repo) adalah folder proyek yang "diawasi" oleh Git: semua perubahan di dalamnya akan dicatat. Git menyimpan data tracking-nya di dalam subfolder bernama `.git`.

**Analogi:** Repository seperti lemari arsip. Folder proyekmu adalah isi lemari, dan folder `.git` adalah sistem katalog yang mencatat setiap kali kamu menambah, mengubah, atau menghapus dokumen. Tanpa `.git`, proyekmu cuma folder biasa. Dengan `git init`, kamu memasang sistem katalog itu.

Perintah `git init` membuat repository kosong. Setelah itu, kamu bisa mulai menambahkan file dan membuat commit.

## Perintah / Sintaks

```bash
git init                     # buat repository baru di folder saat ini
git init nama-folder         # buat folder baru + repository sekaligus
ls -la .git                  # lihat isi folder .git (tempat data Git)
```

## Contoh Praktik

1. Buat folder proyek baru dan init repository:

   ```bash
   mkdir ~/belajar-git-saya
   cd ~/belajar-git-saya
   git init
   ```

2. Output yang muncul:

   ```
   Initialized empty Git repository in /home/user/belajar-git-saya/.git/
   ```

3. Lihat isi folder `.git`:

   ```bash
   ls -la .git
   ```

   Akan terlihat struktur seperti ini:

   ```
   HEAD
   config
   description
   hooks/
   info/
   objects/
   refs/
   ```

   File-file ini adalah "mesin" Git: jangan diedit manual.

4. Cek status repository:

   ```bash
   git status
   ```

   Output: `On branch master` (atau `main`): artinya repository siap digunakan.

## Kesalahan Umum

1. **Menginisialisasi repo di folder yang sudah ada repo-nya**: `git init` di repo yang sudah ada tidak berbahaya (hanya reinit), tapi bisa membingungkan. Cek dulu dengan `git status`.
2. **Menghapus folder `.git`**: kalau terhapus, seluruh sejarah commit hilang. Folder `.git` adalah nyawa repository.
3. **Menginisialisasi repo di folder home (`~`)**: jangan pernah `git init` di home folder. Semua file di home akan ter-track. Buat folder proyek khusus.

## Ringkasan

- Repository = folder proyek yang diawasi Git
- `git init` membuat repository baru
- Folder `.git` menyimpan semua data tracking Git
- Jangan edit atau hapus folder `.git` secara manual
- Cek status dengan `git status` untuk memastikan repo aktif

## Navigasi

Sebelumnya: [02-instalasi-dan-konfigurasi.md](./02-instalasi-dan-konfigurasi.md)

Berikutnya: [04-git-workflow.md](./04-git-workflow.md)
