# Glossary: Istilah Penting Git

**Branch**: Cabang dari riwayat commit yang memungkinkan pengembangan fitur secara terpisah tanpa mengganggu branch utama (biasanya `main` atau `master`).

**Checkout**: Perintah untuk berpindah antar branch atau mengembalikan file di working directory ke versi tertentu dari repository.

**Clone**: Proses menggandakan repository remote (misalnya dari GitHub) ke komputer lokal untuk pertama kalinya.

**Commit**: Snapshot dari perubahan file yang disimpan ke repository Git, dilengkapi dengan pesan yang menjelaskan perubahan tersebut.

**Conflict (Merge Conflict)**: Kondisi ketika Git tidak bisa menggabungkan dua branch secara otomatis karena ada perubahan yang saling bertabrakan di file yang sama. Perlu diselesaikan secara manual.

**Fast-forward merge**: Jenis merge di mana branch target bisa digerakkan maju secara linear tanpa perlu membuat commit merge baru, karena tidak ada divergensi.

**Fetch**: Perintah untuk mengunduh riwayat commit dan referensi dari repository remote tanpa menggabungkannya ke branch lokal.

**Fork**: Salinan repository milik orang lain ke akun GitHub kita sendiri, biasanya untuk berkontribusi ke proyek open source.

**HEAD**: Pointer khusus yang menunjuk ke commit terakhir pada branch yang sedang aktif. Biasanya digunakan sebagai referensi posisi "sekarang" di repository.

**Index (Staging Area)**: Lihat **Staging Area**.

**Merge**: Proses menggabungkan dua branch menjadi satu, menggabungkan riwayat commit dari kedua cabang.

**Origin**: Nama default untuk remote repository utama saat pertama kali melakukan clone.

**Pull**: Perintah yang menggabungkan `fetch` dan `merge` sekaligus: mengunduh perubahan dari remote lalu menggabungkannya ke branch lokal.

**Push**: Perintah untuk mengirim commit dari repository lokal ke repository remote (misalnya GitHub).

**Rebase**: Memindahkan atau menggabungkan serangkaian commit ke ujung branch lain, menciptakan riwayat yang lebih linear dibandingkan merge.

**Remote**: Versi repository yang disimpan di server lain (bisa di GitHub, GitLab, server pribadi, dll), bukan di komputer lokal.

**Repository (repo)**: Tempat penyimpanan proyek yang berisi seluruh file dan riwayat perubahan (commit) yang telah dilakukan.

**Revert**: Perintah untuk membatalkan efek dari commit tertentu dengan membuat commit baru yang melakukan kebalikan dari commit tersebut.

**Staging Area**: Area antara working directory dan repository. File yang sudah di-`add` akan berada di sini, siap untuk di-commit. Sering disebut juga **Index**.

**Stash**: Fitur untuk menyimpan sementara perubahan yang belum di-commit agar working directory menjadi bersih, lalu bisa diterapkan kembali nanti.

**Tag**: Penanda (label) untuk commit tertentu, biasanya digunakan untuk menandai versi rilis (misalnya `v1.0.0`).

**Tracking Branch**: Branch lokal yang terhubung langsung ke branch di remote. Memudahkan perintah `push` dan `pull` tanpa perlu menyebutkan remote setiap kali.

**Working Directory (Working Tree)**: Folder proyek di komputer lokal tempat kita mengedit file. Perubahan di sini belum tercatat di Git sampai di-`add` dan di-commit.
