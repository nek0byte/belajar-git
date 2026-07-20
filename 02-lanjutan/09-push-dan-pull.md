# Push dan Pull: Sinkronisasi Perubahan: Level: Lanjutan

## Konsep

Push dan pull adalah dua operasi sinkronisasi antara repository lokal dan remote.

**Push:** mengirim commit yang ada di lokal tapi belum ada di remote, ke remote. Bayangkan seperti **mengupload file ke Google Drive**: perubahan di laptop kamu dikirim ke server agar tim lain bisa melihatnya.

**Pull:** mengambil commit dari remote yang belum ada di lokal, lalu menggabungkannya (merge) ke branch lokal yang aktif. Bayangkan seperti **mendownload versi terbaru dari Google Drive**: kamu mendapat perubahan yang dibuat orang lain.

Alur kerja dasar: `commit` (lokal) → `push` (ke remote) → orang lain `pull` (dari remote).

### fast-forward vs merge saat pull

Saat pull, Git melakukan fetch + merge. Kalau branch lokal dan remote tidak divergen (tidak ada commit di lokal yang tidak ada di remote, atau sebaliknya), Git akan melakukan fast-forward merge: ini mulus tanpa konflik. Tapi kalau ada divergensi, Git akan membuat merge commit, dan potensi conflict bisa muncul.

## Perintah / Sintaks

**Push ke remote:**

```bash
git push origin nama-branch
```

**Push sekaligus set upstream (branch tracking):**

```bash
git push -u origin nama-branch
```

Setelah `-u` dipakai sekali, push berikutnya cukup:

```bash
git push
```

**Pull dari remote:**

```bash
git pull origin nama-branch
```

Kalau upstream sudah di-set:

```bash
git pull
```

**Push force (HATI-HATI!):**

```bash
git push --force origin nama-branch
```

Hanya gunakan jika kamu benar-benar yakin, karena ini menimpa riwayat di remote.

## Contoh Praktik

**Skenario: membuat branch baru, push ke remote, lalu pull perubahan.**

1. Clone atau buat repo yang sudah terhubung ke remote.

```bash
git clone https://github.com/username/proyek.git
cd proyek
```

2. Buat branch baru dan buat commit:

```bash
git checkout -b fitur-abc
echo "fitur baru" > fitur.txt
git add fitur.txt
git commit -m "tambah fitur abc"
```

3. Push branch baru ke remote (pertama kali):

```bash
git push -u origin fitur-abc
```

4. Sekarang branch `fitur-abc` ada di remote. Cek di GitHub.

5. Pull perubahan dari remote (misal ada yang mengubah branch `main`):

```bash
git checkout main
git pull origin main
```

6. Gabungkan fitur ke main:

```bash
git merge fitur-abc
git push origin main
```

**Simulasi pull dengan perubahan dari orang lain:**

1. Di terminal 1 (teman), push commit ke `main`.
2. Di terminal 2 (kamu), jalankan `git pull origin main`.
3. Git akan mendownload commit baru dan menggabungkannya ke branch kamu.

## Kesalahan Umum

1. **Push ditolak karena remote lebih maju**: Error: `! [rejected]` karena remote punya commit yang belum kamu punya. Solusi: `git pull` dulu untuk mengambil perubahan remote, resolve conflict jika ada, lalu push lagi.

2. **Lupa `-u` saat pertama push branch baru**: Git akan kasih warning: `fatal: The current branch ... has no upstream branch`. Solusi: ikuti saran Git, gunakan `git push --set-upstream origin nama-branch`.

3. **Push force merusak riwayat tim**: `git push --force` tanpa koordinasi bisa menghapus commit rekan setim. Gunakan `--force-with-lease` yang lebih aman:

```bash
git push --force-with-lease origin nama-branch
```

## Ringkasan

- `git push` mengirim commit lokal ke remote
- `git pull` mengambil + menggabungkan commit dari remote
- `-u` atau `--set-upstream` mengatur tracking branch untuk push/pull otomatis
- Push bisa ditolak kalau remote lebih maju: pull dulu
- `--force` berbahaya: gunakan `--force-with-lease`

## Navigasi

- Sebelumnya: [Clone Repository](./08-clone-repository.md)
- Berikutnya: [Fetch vs Pull](./10-fetch-vs-pull.md)
