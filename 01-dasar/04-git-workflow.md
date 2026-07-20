# Git Workflow: Working Directory, Staging Area, Repository: Dasar

## Konsep

Git memiliki tiga area kerja yang membentuk alur penyimpanan perubahan:

```
Working Directory  →  Staging Area  →  Repository (.git)
     (file kamu)        (meja sortir)     (commit tersimpan)
```

**Working Directory**: folder proyek yang kamu lihat dan edit. Semua file yang kamu buka dan ubah ada di sini.

**Staging Area**: area persiapan sebelum commit. Kamu memilih file mana saja yang akan dimasukkan ke commit berikutnya.

**Repository**: tempat commit tersimpan secara permanen di folder `.git`.

**Analogi:** Bayangkan kamu lagi masak. Working directory = dapur dengan bahan makanan. Staging area = meja sortir tempat kamu memilih bahan yang akan dimasak. Repository = kulkas tempat makanan jadi disimpan. Kamu tidak langsung memasukkan semua bahan dari dapur ke kulkas: kamu sortir dulu di meja (staging), baru simpan.

### Siklus Hidup File

- **Untracked**: file baru yang belum dikenal Git
- **Modified**: file yang sudah di-track dan diubah, tapi belum di-stage
- **Staged**: file yang sudah ditambahkan ke Staging Area, siap di-commit
- **Committed**: perubahan sudah tersimpan di repository

![Diagram alur dasar Git: working directory, staging area, repository](https://marklodato.github.io/visual-git-guide/basic-usage.svg.png)

## Perintah / Sintaks

```bash
git status                   # lihat status semua file
git add <file>               # stage file tertentu
git add .                    # stage semua file di folder saat ini
git commit -m "pesan commit" # simpan perubahan ke repository
git log --oneline            # lihat daftar commit
```

## Contoh Praktik

(Lanjutkan dari repo yang dibuat di materi sebelumnya: `~/belajar-git-saya`)

1. Buat file baru:
   ```bash
   echo "Hello Git" > readme.txt
   ```
2. Cek status:
   ```bash
   git status
   ```
   Output: `readme.txt` berwarna merah: **untracked**.

3. Stage file:
   ```bash
   git add readme.txt
   git status
   ```
   Output: `readme.txt` berwarna hijau: **staged**.

4. Commit perubahan:
   ```bash
   git commit -m "commit pertama: menambahkan readme.txt"
   ```
   Output:
   ```
   1 file changed, 1 insertion(+)
   create mode 100644 readme.txt
   ```

5. Cek log:
   ```bash
   git log --oneline
   ```
   Output:
   ```
   abc1234 (HEAD -> master) commit pertama: menambahkan readme.txt
   ```

6. Ubah file dan ulangi siklus:
   ```bash
   echo "Baris kedua" >> readme.txt
   git status                # modified (merah)
   git add readme.txt
   git commit -m "menambah baris kedua"
   ```

## Kesalahan Umum

1. **Lupa `git add` lalu langsung `git commit`**: commit hanya akan menyimpan file yang sudah di-stage. File yang belum di-add tidak masuk commit. Cek dulu dengan `git status`.
2. **Menggunakan `git commit` tanpa `-m`**: Git akan membuka editor. Jika tidak tahu cara keluar dari Vim, ketik `:q` lalu Enter. Gunakan `-m` untuk langsung menulis pesan.
3. **Pesan commit tidak deskriptif**: `"fix bug"` atau `"perbaikan"` terlalu umum. Buat pesan yang jelas: `"memperbaiki bug login saat input email kosong"`.

## Ringkasan

- Tiga area Git: Working Directory, Staging Area, Repository
- Alur: edit file → `git add` → `git commit`
- `git status` untuk cek keadaan file
- `git add` memindahkan file ke staging area
- `git commit` menyimpan snapshot ke repository
- File melalui siklus: untracked → modified → staged → committed

## Navigasi

Sebelumnya: [03-membuat-repository.md](./03-membuat-repository.md)

Berikutnya: [05-commit-hash.md](./05-commit-hash.md)
