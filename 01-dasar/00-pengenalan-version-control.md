# Pengenalan Version Control System (VCS)

## Konsep

Version Control System (VCS) adalah sistem yang mencatat setiap perubahan pada file atau kumpulan file dari waktu ke waktu. Dengan VCS, kamu bisa tahu siapa yang mengubah apa, kapan perubahannya terjadi, dan bisa kembali ke versi tertentu kapan saja.

**Analogi:** Bayangkan kamu menulis skripsi. Kamu menyimpan file `skripsi_v1.docx`, lalu `skripsi_v2_revisi.docx`, lalu `skripsi_v3_fix_final.docx`, lalu `skripsi_v4_final_beneran.docx`. Ribet, bukan? VCS mengelola semua versi itu secara otomatis: cukup satu file, dan setiap perubahan dicatat sebagai *revision* atau *commit*. Kamu bisa melompat ke versi kapan saja tanpa perlu membuat puluhan file duplikat.

Ada tiga generasi VCS:

1. **VCS Lokal**: database versi disimpan di harddisk sendiri. Sederhana, tapi tidak bisa kolaborasi. Contoh: RCS.
2. **VCS Terpusat (Centralized)**: semua versi disimpan di server pusat. Kolaborasi jadi mungkin, tapi kalau server mati, sejarah perubahan hilang. Contoh: Subversion (SVN), CVS.
3. **VCS Terdistribusi (Distributed)**: setiap komputer menyimpan *seluruh* salinan repository (termasuk sejarah). Tidak bergantung server pusat. Contoh: Git, Mercurial.

## Kesalahan Umum

1. **Menyimpan file dengan nama `-final-final`**: ini tanda kamu butuh VCS. Jika kamu masih membuat folder `project-revisi-2/`, segera gunakan Git.
2. **Mengira VCS hanya untuk programmer**: padahal VCS berguna untuk penulis, desainer, siapa pun yang bekerja dengan file digital.
3. **Menganggap backup = version control**: backup hanya menyimpan salinan terbaru. VCS menyimpan *setiap versi* dan perubahannya.

## Ringkasan

- VCS mencatat setiap perubahan file secara otomatis
- Tiga jenis VCS: lokal, terpusat, terdistribusi
- Git termasuk VCS terdistribusi: setiap orang punya salinan penuh repository
- VCS membantu kolaborasi, melacak sejarah, dan kembali ke versi sebelumnya

## Navigasi

Berikutnya: [01-pengenalan-git.md](./01-pengenalan-git.md)
