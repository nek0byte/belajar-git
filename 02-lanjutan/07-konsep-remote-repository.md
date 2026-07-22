# Konsep Remote Repository

## Konsep

Remote repository adalah versi repository Git yang disimpan di server lain: bisa di internet (GitHub, GitLab, Bitbucket) atau di jaringan lokal tim kamu.

Bayangkan remote repository seperti **Google Drive untuk kode**. Kamu punya file di laptop sendiri (repository lokal). Kalau laptop rusak, file-nya hilang. Tapi kalau kamu upload ke Google Drive, file-nya aman dan bisa diakses dari mana saja. Remote repo melakukan hal yang sama untuk kode: tempat aman, bisa diakses banyak orang, dan jadi sumber kebenaran bersama.

Perbedaan utama local vs remote:

| Lokal | Remote |
|-------|--------|
| Ada di mesin kamu sendiri | Ada di server |
| Hanya kamu yang bisa akses (kecuali berbagi laptop) | Bisa diakses oleh tim / publik |
| Bekerja offline penuh | Butuh internet untuk sinkronisasi |
| Cepat karena lokal | Operasi network lebih lambat |

GitHub, GitLab, dan Bitbucket adalah penyedia layanan hosting untuk remote repository. Mereka menambahkan fitur di atas Git standar: GUI web, issue tracker, pull request, code review, CI/CD, dan manajemen tim.

## Perintah / Sintaks

**Menambahkan remote baru:**

```bash
git remote add <nama> <url-repository>
```

**Melihat daftar remote:**

```bash
git remote
git remote -v   # lebih detail, lihat URL
```

**Menghapus remote:**

```bash
git remote remove <nama>
```

**Mengganti URL remote:**

```bash
git remote set-url <nama> <url-baru>
```

Nama remote paling umum adalah `origin`. Ini konvensi standar, bukan aturan mutlak.

## Contoh Praktik

**Skenario: membuat repository lokal lalu menghubungkannya ke GitHub.**

1. Buat repo kosong di GitHub (jangan centang "Initialize with README").
2. Di terminal, buat repo lokal:

```bash
mkdir proyek-ku
cd proyek-ku
git init
echo "# Proyek Ku" > README.md
git add README.md
git commit -m "commit pertama"
```

3. Tambahkan remote:

```bash
git remote add origin https://github.com/username/proyek-ku.git
```

4. Verifikasi:

```bash
git remote -v
# Output:
# origin  https://github.com/username/proyek-ku.git (fetch)
# origin  https://github.com/username/proyek-ku.git (push)
```

5. Kirim perubahan ke remote:

```bash
git push -u origin main
```

**Melihat detail remote:**

```bash
git remote show origin
```
Perintah ini menampilkan URL, branch yang di-track, dan status sinkronisasi.

## Kesalahan Umum

1. **Salah URL remote**: typo di URL mengakibatkan error saat push/pull. Selalu verifikasi dengan `git remote -v` setelah menambahkan remote.

2. **Lupa menambahkan remote**: setelah `git init` langsung coba `git push`, dapat error "fatal: No configured push destination". Solusi: tambahkan remote dulu dengan `git remote add`.

3. **Menambahkan remote dengan nama yang sudah ada**: Git akan menolak. Gunakan `git remote rename` atau hapus dulu yang lama.

## Ringkasan

- Remote repository adalah salinan repo di server jarak jauh
- `git remote add` untuk menghubungkan repo lokal ke remote
- `git remote -v` melihat URL remote yang terdaftar
- `origin` adalah nama konvensi default untuk remote utama
- GitHub/GitLab/Bitbucket adalah layanan hosting remote repo

## Navigasi

- Sebelumnya: [Git Stash](./06-git-stash.md)
- Berikutnya: [Clone Repository](./08-clone-repository.md)
