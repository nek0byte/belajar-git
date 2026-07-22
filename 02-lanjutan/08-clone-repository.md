# Clone Repository: Menyalin Repo dari Remote

## Konsep

`git clone` adalah perintah untuk membuat salinan **utuh** repository remote ke komputer lokal. Berbeda dengan `git init` yang membuat repo kosong dari nol, `git clone` menyalin semua riwayat commit, semua branch, dan semua file dari repo yang sudah ada.

Bayangkan seperti **mendownload zip project**: tapi bedanya, kamu mendapat seluruh sejarah project, bukan hanya file terbaru. Kamu juga otomatis terhubung ke remote aslinya.

Saat clone, Git secara otomatis:

1. Membuat folder baru (nama diambil dari nama repo)
2. Inisialisasi `git init` di dalamnya
3. Menambahkan remote `origin` yang mengarah ke URL yang di-clone
4. Mendownload semua objek (commit, tree, blob) dari remote
5. Checkout ke branch default (biasanya `main` atau `master`)

Hasilnya: kamu punya repo lokal yang siap pakai, lengkap dengan koneksi ke remote.

## Perintah / Sintaks

**Clone ke folder dengan nama default (nama repo):**

```bash
git clone https://github.com/username/nama-repo.git
```

**Clone ke folder dengan nama kustom:**

```bash
git clone https://github.com/username/nama-repo.git nama-folder-saya
```

**Clone menggunakan protokol SSH:**

```bash
git clone git@github.com:username/nama-repo.git
```

SSH lebih disarankan karena tidak perlu memasukkan password setiap kali push (setelah setup SSH key).

## Contoh Praktik

**Skenario: clone repository publik dari GitHub.**

1. Buka browser, cari repository publik (contoh: `github.com/facebook/react`).
2. Klik tombol hijau **Code**, salin URL HTTPS.
3. Di terminal:

```bash
cd ~/projects
git clone https://github.com/facebook/react.git
```

4. Masuk ke folder hasil clone dan lihat strukturnya:

```bash
cd react
ls -la
```

5. Cek bahwa remote sudah terisi otomatis:

```bash
git remote -v
# origin  https://github.com/facebook/react.git (fetch)
# origin  https://github.com/facebook/react.git (push)
```

6. Cek riwayat commit (lengkap!):

```bash
git log --oneline -5
```

**Clone dengan folder kustom:**

```bash
git clone https://github.com/username/nama-repo.git salinan-saya
cd salinan-saya
```

**Clone branch tertentu (tidak semua branch):**

```bash
git clone --branch nama-branch --single-branch https://github.com/username/nama-repo.git
```

Ini berguna kalau repo besar dan kamu hanya butuh satu branch.

## Kesalahan Umum

1. **Clone repo privat tanpa akses**: error `fatal: Authentication failed`. Pastikan kamu punya akses ke repo tersebut. Kalau pakai HTTPS, gunakan Personal Access Token (PAT) sebagai password, bukan password akun GitHub.

2. **Lupa beda protokol HTTPS vs SSH**: HTTPS kadang minta login setiap operasi (kecuali caching credential). SSH lebih praktis setelah setup. Pilih salah satu sesuai kebutuhan.

3. **Clone ke folder yang sudah ada isinya**: `git clone` akan membuat folder baru. Kalau folder target sudah ada dan tidak kosong, clone akan gagal. Gunakan folder kosong atau biarkan Git yang membuat folder baru.

4. **Clone repo besar terasa lambat**: Untuk repo besar, gunakan `--depth 1` untuk clone hanya commit terakhir (shallow clone). Tapi kamu tidak akan punya riwayat lengkap.

```bash
git clone --depth 1 https://github.com/username/repo-besar.git
```

## Ringkasan

- `git clone` menyalin seluruh repository remote ke lokal
- Remote `origin` otomatis terkonfigurasi
- Branch default otomatis di-checkout
- Bisa tentukan nama folder dengan argumen kedua
- Protokol HTTPS (mudah) atau SSH (lebih aman, tanpa password)

## Navigasi

- Sebelumnya: [Konsep Remote Repository](./07-konsep-remote-repository.md)
- Berikutnya: [Push dan Pull](./09-push-dan-pull.md)
