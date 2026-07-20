# Konsep Branching: Cabang Parallel Pengerjaan

**Level:** Lanjutan

## Konsep

Branch adalah fitur yang memungkinkan kamu membuat **cabang parallel** dari kode tanpa mengganggu cabang utama. Di Git, branch sebenarnya hanyalah **pointer ringan** yang menunjuk ke sebuah commit. Setiap commit baru pada branch akan menggeser pointer tersebut ke commit terbaru.

**Analogi:** Bayangkan kamu sedang menulis novel. Cabang utama (main) adalah naskah final yang sudah diterbitkan. Branch adalah **draf alternatif** atau **spin-off** yang kamu tulis di buku terpisah: kamu bisa bereksperimen dengan alur cerita berbeda tanpa merusak naskah asli. Kalau ternyata bagus, kamu bisa menggabungkannya kembali ke naskah utama.

Secara default, saat pertama kali membuat repository, Git membuat branch bernama `main` (atau `master` di versi lama). Setiap commit baru yang kamu buat otomatis berada di branch aktif saat itu.

## Perintah / Sintaks

```bash
# Melihat daftar branch lokal
git branch

# Melihat branch dengan detail commit terakhir
git branch --list

# Melihat posisi HEAD (branch aktif saat ini)
git show HEAD

# Melihat branch yang sudah di-merge ke branch aktif
git branch --merged

# Melihat branch yang belum di-merge
git branch --no-merged
```

| Perintah | Kegunaan |
|----------|----------|
| `git branch` | Tampilkan semua branch lokal, tanda `*` menandai branch aktif |
| `git branch --list` | Sama seperti `git branch`, opsi eksplisit |
| `git branch --merged` | Branch yang sudah digabungkan ke branch aktif |
| `git branch --no-merged` | Branch yang belum digabungkan |

**HEAD** adalah pointer khusus yang menunjukkan posisi kamu saat ini: branch mana yang sedang aktif. Saat kamu `git log`, HEAD menunjuk ke branch yang sedang kamu gunakan.

## Contoh Praktik

1. Buat repository baru dan cek branch default:

```bash
git init repo-branch
cd repo-branch
echo "# Demo Branch" > README.md
git add README.md
git commit -m "commit pertama"
git branch
```

Keluaran akan menunjukkan `* main`: tanda bintang berarti branch aktif adalah `main`.

2. Lihat posisi HEAD:

```bash
git show HEAD
```

Perhatikan bahwa HEAD menunjuk ke `main`, dan `main` menunjuk ke commit ID terbaru. Inilah yang dimaksud "branch adalah pointer ke commit."

3. Buat branch baru tanpa berpindah:

```bash
git branch eksperimen
git branch --list
```

Sekarang ada dua branch: `main` dan `eksperimen`. Kamu masih berada di `main`.

## Kesalahan Umum

1. **Mengira branch adalah folder terpisah**: Branch bukan direktori berbeda; semua file di working directory sama, hanya isinya berbeda tergantung commit yang di-checkout.

2. **Lupa branch aktif**: Selalu cek dengan `git branch` sebelum commit agar tidak salah menaruh commit di branch yang tidak diinginkan.

3. **Mengira `git branch` akan memindahkan branch**: `git branch nama` hanya membuat branch baru, tidak berpindah ke branch itu. Gunakan `git checkout` atau `git switch` untuk pindah.

## Ringkasan

- Branch adalah pointer ringan ke sebuah commit
- `git branch` untuk melihat daftar branch
- `HEAD` menunjuk ke branch yang sedang aktif
- Branch default adalah `main` (sebelumnya `master`)
- Branch memungkinkan pengembangan parallel tanpa mengganggu cabang utama

## Navigasi

- Sebelumnya: [Git Alias](../01-dasar/19-git-alias.md)
- Berikutnya: [Membuat dan Berpindah Branch](02-membuat-dan-berpindah-branch.md)
