# Fast-Forward vs 3-Way Merge

## Konsep

Saat melakukan merge, Git punya dua strategi utama:

**1. Fast-Forward Merge**: Terjadi jika branch tujuan **tidak memiliki commit baru** sejak branch sumber dibuat. Git cukup menggeser pointer branch tujuan ke posisi branch sumber. Riwayat tetap linear, tidak ada merge commit.

**2. Three-Way Merge**: Terjadi jika kedua branch **sama-sama memiliki commit baru** setelah titik percabangan. Git membuat **merge commit** baru yang memiliki dua parent (dari kedua branch). Riwayat tidak linear dan menunjukkan percabangan.

**Analogi:** Fast-forward seperti menyambung tali: kamu tinggal menggeser simpul ke ujung tali yang baru. 3-way seperti menyatukan dua ujung tali berbeda dengan simpul baru (merge commit) di tengah.

```
Fast-Forward:
  A --- B --- C   (main)
               \
                D --- E   (fitur)
  Setelah merge: A --- B --- C --- D --- E   (main)

3-Way Merge:
  A --- B --- C ---------- F   (main, F = merge commit)
               \          /
                D --- E ---     (fitur)
```

![Animasi fast-forward merge](https://gitgifs.com/images/fast-forward-merge.gif)

![Diagram 3-way merge](https://marklodato.github.io/visual-git-guide/merge.svg.png)

## Perintah / Sintaks

```bash
# Git otomatis memilih fast-forward jika memungkinkan
git merge <branch>

# Paksa 3-way merge (buat merge commit meski bisa ff)
git merge --no-ff <branch>

# Merge hanya jika bisa fast-forward
git merge --ff-only <branch>

# Nonaktifkan fast-forward secara global
git config --global merge.ff false
```

| Flag | Efek |
|------|------|
| (tanpa flag) | Fast-forward jika mungkin, 3-way jika tidak |
| `--no-ff` | Selalu buat merge commit |
| `--ff-only` | Gagal jika tidak bisa fast-forward |

## Contoh Praktik

### Demo Fast-Forward

```bash
git init repo-ff
cd repo-ff
echo "A" > file.txt
git add file.txt && git commit -m "commit A"

git switch -c fitur
echo "B" >> file.txt && git commit -am "commit B"
echo "C" >> file.txt && git commit -am "commit C"

git switch main
git merge fitur   # fast-forward!
git log --oneline --graph
```

Hasil: riwayat linear A → B → C. `main` sekarang di commit C.

### Demo 3-Way Merge

```bash
git init repo-3way
cd repo-3way
echo "A" > file.txt
git add file.txt && git commit -m "commit A"

git switch -c fitur
echo "B" >> file.txt && git commit -am "commit B (fitur)"

git switch main
echo "C" >> file.txt && git commit -am "commit C (main)"

# Sekarang kedua branch punya commit baru: divergen
git merge fitur   # 3-way merge, muncul editor untuk pesan merge commit
git log --oneline --graph
```

Hasil: riwayat bercabang dengan merge commit.

## Kesalahan Umum

1. **Mengira fast-forward selalu lebih baik**: Fast-forward menghasilkan riwayat linear yang rapi, tetapi jika kamu ingin melacak bahwa fitur tertentu pernah digabung, merge commit lebih informatif. Gunakan `--no-ff` untuk branch fitur.

2. **Tidak sengaja fast-forward padahal ingin merge commit**: Riwayat jadi hilang jejak percabangannya. Solusi: biasakan `git merge --no-ff` untuk branch fitur.

3. **Bingung melihat riwayat graph**: Gunakan `git log --oneline --graph --all` untuk melihat semua branch dan posisi merge commit dengan jelas.

## Ringkasan

- **Fast-forward**: pointer digeser, riwayat linear, tanpa merge commit
- **3-way merge**: merge commit dengan dua parent, riwayat bercabang
- `--no-ff` memaksa 3-way merge (disarankan untuk branch fitur)
- `--ff-only` memaksa fast-forward (gagal jika divergen)
- Tidak ada yang "lebih baik": pilih sesuai kebutuhan tim

## Navigasi

- Sebelumnya: [Merge Branch](03-merge-branch.md)
- Berikutnya: [Menyelesaikan Merge Conflict](05-menyelesaikan-merge-conflict.md)
