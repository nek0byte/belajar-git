# Kolaborasi dengan GitHub

## Konsep

GitHub adalah platform kolaborasi yang dibangun di atas Git. Git sendiri sudah mendukung kolaborasi (siapa pun bisa push/pull ke repo yang sama), tapi GitHub menambahkan lapisan manajemen yang memudahkan kerja tim.

### Workflow Kolaborasi Standar

Alur kolaborasi di GitHub umumnya mengikuti pola ini:

1. **Fork**: salin repo orang lain ke akun GitHub kamu
2. **Clone**: salin fork ke komputer lokal
3. **Branch**: buat branch baru untuk fitur/perbaikan
4. **Commit**: buat perubahan secara bertahap
5. **Push**: kirim branch ke GitHub
6. **Pull Request (PR)**: minta pemilik repo asli menggabungkan perubahan kamu
7. **Code Review**: tim meninjau kode, memberi komentar
8. **Merge**: setelah disetujui, PR digabungkan ke branch utama
9. **Sync**: tarik perubahan terbaru dari repo asli

Bayangkan seperti **mengerjakan tugas kelompok di Google Docs**:

- Fork = bikin salinan dokumen ke akun kamu sendiri
- Clone = download salinan ke laptop
- Branch = bikin halaman draft terpisah
- Commit = simpan perubahan
- Push = upload draft ke akun kamu
- Pull Request = bilang "tugas saya sudah selesai, cek dulu"
- Code Review = teman memberi komentar di draft
- Merge = draft resmi digabung ke dokumen utama

### Kolaborasi di Repo yang Sama (tanpa fork)

Kalau kamu adalah anggota tim dengan akses langsung ke repo, fork tidak diperlukan. Cukup clone langsung, buat branch, push, dan buat PR. Workflow-nya lebih sederhana:

1. Clone repo
2. `git checkout -b fitur-baru`
3. Commit dan push
4. Buat Pull Request dari branch tersebut

## Perintah / Sintaks

**Fork repo**: lakukan via web GitHub (tombol Fork di kanan atas).

**Clone fork ke lokal:**

```bash
git clone https://github.com/username/nama-repo.git
cd nama-repo
```

**Tambahkan upstream (repo asli):**

```bash
git remote add upstream https://github.com/original-owner/nama-repo.git
```

**Buat branch fitur:**

```bash
git checkout -b fix-typo
```

**Commit dan push:**

```bash
git add .
git commit -m "fix: perbaiki typo di README"
git push -u origin fix-typo
```

**Buat Pull Request via GitHub CLI (`gh`):**

```bash
gh pr create --title "fix: perbaiki typo di README" --body "Menambahkan huruf yang hilang"
```

**Melihat daftar PR:**

```bash
gh pr list
```

**Merge PR via CLI:**

```bash
gh pr merge 123
```

**Sync fork dengan upstream:**

```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

## Contoh Praktik

### Skenario 1: Kontribusi ke Repo Open Source

1. Buka repo yang ingin dikontribusi di GitHub, klik **Fork**.
2. Clone fork ke lokal:

```bash
git clone https://github.com/username/repo-yang-di-fork.git
cd repo-yang-di-fork
git remote add upstream https://github.com/original-owner/repo-yang-di-fork.git
```

1. Buat branch:

```bash
git checkout -b perbaiki-dokumentasi
```

1. Edit file, commit:

```bash
echo "dokumentasi diperbaiki" >> README.md
git add README.md
git commit -m "perbaiki dokumentasi"
```

1. Push:

```bash
git push -u origin perbaiki-dokumentasi
```

1. Buka GitHub, akan muncul banner "perbaiki-dokumentasi had recent push". Klik **Compare & pull request**.
2. Isi judul dan deskripsi PR, klik **Create pull request**.
3. Tunggu review dari maintainer. Jika ada komentar, perbaiki dan push lagi ke branch yang sama: PR akan ter-update otomatis.
4. Setelah disetujui, maintainer akan merge PR.

### Skenario 2: Kolaborasi 2 Orang di Repo yang Sama

**Anggota A (repo owner):**

```bash
git clone https://github.com/tim/proyek.git
cd proyek
git checkout -b fitur-login
# ... coding ...
git add .
git commit -m "tambah fitur login"
git push -u origin fitur-login
# buka GitHub → buat PR
```

**Anggota B (reviewer):**

```bash
git clone https://github.com/tim/proyek.git
cd proyek
git fetch origin
git checkout -b review-fitur-login origin/fitur-login
# lihat kode, beri komentar di GitHub
# di halaman PR, klik tab "Files changed" → comment on line tertentu
```

**Anggota A (memperbaiki review):**

```bash
# edit file sesuai review
git add .
git commit -m "perbaiki sesuai review"
git push
# PR ter-update otomatis
```

**Anggota A atau maintainer (merge setelah disetujui):**

Di GitHub, klik **Merge pull request** → **Confirm merge**.

## Kesalahan Umum

1. **Lupa sync fork sebelum mulai**: Fork yang sudah ketinggalan dari upstream bisa menyebabkan conflict saat PR. Selalu sync dulu: `git fetch upstream`, `git merge upstream/main`.

2. **Push langsung ke main/master**: Bekerja langsung di branch `main` lalu push membuat riwayat jadi berantakan dan sulit di-review. Selalu buat branch fitur terpisah.

3. **PR terlalu besar**: Satu PR dengan 50 file berubah sulit di-review. Pisahkan perubahan logis ke PR terpisah. Satu PR = satu fitur/perbaikan.

4. **Lupa pull sebelum mulai kerja**: Bisa menyebabkan konflik yang tidak perlu. Biasakan `git pull` (atau `git fetch && git merge`) di branch `main` sebelum buat branch baru.

## Ringkasan

- Fork → Clone → Branch → Commit → Push → PR → Review → Merge
- Fork diperlukan jika kamu tidak punya akses write ke repo asli
- Pull Request adalah mekanisme untuk meminta penggabungan perubahan
- Code review dilakukan melalui tab "Files changed" di PR
- Selalu sync fork dengan upstream secara berkala
- Branch fitur terpisah untuk setiap perubahan

## Navigasi

- Sebelumnya: [Tracking Branch](./11-tracking-branch.md)
- (Materi ini adalah topik terakhir di sesi Git Lanjutan. Lanjutkan ke [Latihan](../03-latihan/latihan-01-repository-pertama.md) untuk praktik.)
