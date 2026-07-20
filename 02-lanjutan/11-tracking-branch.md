# Tracking Branch: Hubungan Branch Lokal dan Remote: Level: Lanjutan

## Konsep

Tracking branch (atau upstream branch) adalah hubungan antara branch lokal dengan branch di remote. Ketika sebuah branch lokal "melacak" branch remote, Git tahu kemana harus push dan darimana harus pull tanpa perlu menyebutkan remote dan branch setiap kali.

Bayangkan tracking branch seperti **shortcut di ponsel**. Kamu nggak perlu mengetik nomor telepon lengkap setiap kali mau nelpon seseorang: cukup tekan nama kontak. Tracking branch adalah "kontak" untuk remote branch: cukup `git push` atau `git pull`, tanpa perlu `git push origin nama-branch` setiap saat.

Saat clone, Git otomatis mengatur tracking: branch `main` lokal melacak `origin/main`. Tapi kalau kamu membuat branch baru, branch tersebut belum punya upstream: harus diatur secara eksplisit.

## Perintah / Sintaks

**Melihat tracking branch:**

```bash
git branch -vv
```

Output menunjukkan branch lokal, hash commit terakhir, pesan commit, dan status terhadap upstream.

**Mengatur upstream untuk branch yang sudah ada:**

```bash
git branch -u origin/nama-branch
```

Atau:

```bash
git branch --set-upstream-to=origin/nama-branch
```

**Push pertama kali + set upstream sekaligus:**

```bash
git push -u origin nama-branch-baru
```

**Menghapus tracking (tanpa menghapus branch):**

```bash
git branch --unset-upstream
```

**Melihat upstream dari branch tertentu:**

```bash
git rev-parse --abbrev-ref --symbolic-full-name @{upstream}
```

## Contoh Praktik

**Skenario: membuat branch baru, mengatur upstream, dan verifikasi.**

1. Clone repo dengan branch `main` yang sudah ter-track:

```bash
git clone https://github.com/username/proyek.git
cd proyek
git branch -vv
# * main  a1b2c3d [origin/main] commit terbaru
```

2. Buat branch baru:

```bash
git checkout -b fitur-edit
git branch -vv
# * fitur-edit  a1b2c3d commit terbaru  ← belum ada upstream
#   main        a1b2c3d [origin/main] commit terbaru
```

3. Push pertama dengan set upstream:

```bash
git push -u origin fitur-edit
# Branch 'fitur-edit' set up to track remote branch 'fitur-edit' from 'origin'.
```

4. Verifikasi tracking:

```bash
git branch -vv
# * fitur-edit  a1b2c3d [origin/fitur-edit] commit terbaru
```

5. Sekarang push cukup:

```bash
git push    # sudah tau tujuan → origin/fitur-edit
git pull    # sudah tau sumber → origin/fitur-edit
```

**Mengatur upstream manual (tanpa -u):**

```bash
git branch -u origin/main
# Branch 'main' set up to track remote branch 'main' from 'origin'.
```

**Menghapus upstream:**

```bash
git branch --unset-upstream
git branch -vv
# * main  a1b2c3d  ← sudah tidak tracking
```

## Kesalahan Umum

1. **Lupa set upstream, push ditolak**: Git akan bilang: `fatal: The current branch ... has no upstream branch`. Solusi: ikuti saran Git, jalankan `git push --set-upstream origin nama-branch`.

2. **Branch lokal tracking ke branch remote yang sudah dihapus**: Ini menyebabkan error saat push/pull. Solusi: `git fetch --prune` untuk membersihkan, lalu set upstream baru atau hapus tracking.

3. **Kebingungan antara origin/nama dan nama saja**: `git branch -u origin/fitur` itu berbeda dengan `git branch -u fitur`. Yang pertama merujuk ke branch remote, yang kedua mencoba merujuk ke branch lokal. Selalu gunakan `origin/` untuk remote.

## Ringkasan

- Tracking branch = hubungan branch lokal dengan remote branch
- `git branch -vv` untuk melihat status tracking semua branch
- `git push -u` mengatur upstream saat push pertama
- Tracking membuat push/pull tidak perlu argumen tambahan
- `git branch --unset-upstream` untuk menghapus tracking

## Navigasi

- Sebelumnya: [Fetch vs Pull](./10-fetch-vs-pull.md)
- Berikutnya: [Kolaborasi dengan GitHub](./12-kolaborasi-dengan-github.md)
