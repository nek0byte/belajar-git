# Gitignore: Mengabaikan File yang Tidak Perlu (Dasar)

## Konsep

Tidak semua file perlu masuk ke repository: file log, folder `node_modules`, file `.env` berisi password, atau file hasil kompilasi. File-file ini hanya mengotori `git status` dan bikin repository membengkak.

`.gitignore` adalah file khusus yang memberi tahu Git: "Abaikan file-file ini, jangan tracking dan jangan tampilkan di status." Pola penulisan mirip glob pattern (`*` untuk wildcard, `!` untuk pengecualian, `/` di akhir untuk folder).

## Perintah / Sintaks

```bash
# Buat file .gitignore (di root repository)
touch .gitignore
```

Contoh isi `.gitignore`:

```
# abaikan semua file .log
*.log

# abaikan folder node_modules
node_modules/

# abaikan file .env
.env

# kecuali important.log: tetap di-track
!important.log

# abaikan folder build/ di root (bukan di subfolder)
/build/
```

## Contoh Praktik

1. Buat file `.gitignore` di root repository:
   ```bash
   touch .gitignore
   ```

2. Isi dengan pola sederhana (pakai editor teks):
   ```gitignore
   *.log
   .env
   ```

3. Buat file `.env` dan `debug.log`:
   ```bash
   echo "SECRET=abc" > .env
   echo "log debug" > debug.log
   ```

4. Cek status:
   ```bash
   git status
   ```

   File `.env` dan `debug.log` tidak muncul. Git mengabaikannya.

5. Tambahkan dan commit `.gitignore`:
   ```bash
   git add .gitignore
   git commit -m "Tambah .gitignore"
   ```

## Kesalahan Umum

1. **File sudah di-track sebelum ditambahkan ke .gitignore**: `.gitignore` tidak berpengaruh pada file yang sudah pernah di-add/commit. Hentikan tracking dengan `git rm --cached <file>` dulu.

2. **Pola folder lupa tanda /**: `build` (tanpa `/`) akan cocok dengan file maupun folder bernama `build` di mana saja. `build/` hanya mencocokkan folder.

3. **Mengira .gitignore melindungi rahasia**: jika file sudah pernah di-commit (misal `.env`), riwayat commit tetap menyimpannya. Hapus dari riwayat dengan `git filter-branch` atau BFG Repo-Cleaner.

## Ringkasan

- `.gitignore` memberi tahu Git file apa yang harus diabaikan
- Gunakan glob pattern: `*`, `!`, `/` untuk folder
- File yang sudah di-track harus di-`git rm --cached` dulu
- Jangan andalkan `.gitignore` untuk mengamankan rahasia yang sudah pernah di-commit

## Navigasi

- Sebelumnya: [Revert Commit](16-revert-commit.md)
- Berikutnya: [Git Blame](18-git-blame.md)
