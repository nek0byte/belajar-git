# Merge Branch: Menggabungkan Cabang

## Konsep

Merge adalah proses menggabungkan riwayat dari dua branch menjadi satu. Biasanya kamu punya branch utama (`main`) dan branch fitur (`fitur-login`). Setelah fitur selesai, kamu ingin menggabungkan perubahan dari `fitur-login` ke `main`.

**Analogi:** Bayangkan kamu dan teman mengerjakan puzzle yang sama. Kamu mengerjakan bagian pinggir (branch kamu), teman mengerjakan bagian tengah (branch teman). **Merge** adalah menyatukan potongan kalian ke meja utama: hasilnya puzzle utuh dengan kontribusi dari dua sumber berbeda.

Saat merge, Git melihat tiga titik:
- **Base commit**: titik terakhir di mana kedua branch memiliki riwayat yang sama
- **Branch tujuan** (misal `main`): posisi terakhir branch yang akan menerima perubahan
- **Branch sumber** (misal `fitur-login`): posisi terakhir branch yang perubahannya akan digabung

![Animasi merge commit dengan balok](https://gitgifs.com/images/merge-commit.gif)

## Perintah / Sintaks

```bash
# Standar: gabungkan branch lain ke branch aktif
git merge <nama-branch>

# Merge dengan pesan custom
git merge <nama-branch> -m "merge fitur X ke main"

# Merge tanpa fast-forward (paksa bikin merge commit)
git merge --no-ff <nama-branch>

# Merge hanya jika bisa fast-forward (gagal jika tidak)
git merge --ff-only <nama-branch>

# Abort merge jika terjadi konflik
git merge --abort
```

| Perintah | Kegunaan |
|----------|----------|
| `git merge <branch>` | Gabungkan `<branch>` ke branch aktif |
| `git merge --no-ff <branch>` | Paksa buat merge commit meski bisa fast-forward |
| `git merge --ff-only <branch>` | Merge hanya jika fast-forward mungkin |
| `git merge --abort` | Batalkan merge yang sedang berlangsung (misal karena konflik) |

## Contoh Praktik

1. Setup repository dengan dua branch:

```bash
git init repo-merge
cd repo-merge
echo "# Aplikasi" > README.md
git add README.md
git commit -m "init: readme"

git switch -c fitur-login
echo "form login" > login.html
git add login.html
git commit -m "feat: halaman login"

git switch main
echo "Halaman utama" > index.html
git add index.html
git commit -m "feat: halaman utama"
```

Sekarang riwayatnya terpisah: `main` punya 2 commit (init + index), `fitur-login` punya 2 commit (init + login).

2. Merge branch `fitur-login` ke `main`:

```bash
git switch main         # pastikan di branch tujuan
git merge fitur-login   # gabungkan fitur-login ke main
```

Perhatikan pesan di terminal. Git akan membuat **merge commit** (karena riwayat divergen) atau melakukan **fast-forward** jika branch tidak divergen.

3. Verifikasi hasil merge:

```bash
ls -la          # sekarang ada README.md, index.html, dan login.html
git log --oneline --graph
```

Semua file dari kedua branch sekarang ada di `main`.

## Kesalahan Umum

1. **Lupa checkout ke branch tujuan**: Salah satu kesalahan paling umum. Jika kamu `git merge main` saat sedang di `fitur-login`, yang terjadi adalah `fitur-login` menyerap `main`, bukan sebaliknya. Selalu pastikan kamu sudah di branch yang akan menerima.

2. **Merge saat ada perubahan belum di-commit**: Git akan menolak merge jika ada file yang dimodifikasi tapi belum di-commit. Solusi: commit atau stash dulu.

3. **Takut konflik**: Konflik bukan akhir dunia. Konflik terjadi wajar saat dua branch mengubah file yang sama. Pelajari cara menyelesaikannya di materi selanjutnya.

## Ringkasan

- `git merge <branch>` menggabungkan `<branch>` ke branch aktif
- Selalu pastikan kamu berada di branch **tujuan** sebelum merge
- Merge menghasilkan merge commit jika riwayat divergen
- Gunakan `--no-ff` untuk memaksa merge commit
- Gunakan `--abort` untuk membatalkan merge yang bermasalah

## Navigasi

- Sebelumnya: [Membuat dan Berpindah Branch](02-membuat-dan-berpindah-branch.md)
- Berikutnya: [Fast-Forward vs 3-Way Merge](04-fast-forward-vs-3-way-merge.md)
