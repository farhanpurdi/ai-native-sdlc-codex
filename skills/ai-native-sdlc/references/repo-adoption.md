# Adopsi dan evaluasi workflow

## Inventaris sebelum menambah proses

Cari panduan repo, CI, cara menjalankan aplikasi, standar review, dan catatan insiden yang tersedia. Jelaskan mana yang sudah bekerja dan mana yang hilang. Jika pengguna meminta audit saja, hasilnya rekomendasi; jika meminta setup, implementasikan perubahan lokal yang relevan. Jangan menyalin seluruh paket ini ke root proyek.

Pilih satu irisan pekerjaan nyata sebagai pilot. Misalnya, endpoint yang sudah memiliki tes tetapi sering bolak-balik review karena kontraknya tidak jelas: tambahkan kriteria penerimaan dan bukti kontrak sebelum menambah otomasi rilis.

## Pisahkan tiga jenis pengetahuan

| Kebutuhan | Tempat yang cocok di Codex |
| --- | --- |
| Cara menavigasi repo, perintah yang sudah terbukti, batas modul | `AGENTS.md` sesuai scope direktori |
| Prosedur khusus yang dipakai berulang pada tugas tertentu | Skill dengan pemicu yang sempit dan pemilik sumber kebijakan |
| Syarat yang harus dipaksakan sebelum merge/rilis | Pemeriksaan CI, branch protection, deployment environment, dan izin platform |

Gabungkan penambahan ke `AGENTS.md` yang ada; pertahankan instruksi relevan. Jangan menaruh status satu tugas atau seluruh playbook di instruksi yang selalu dimuat. Catat perintah beserta prasyaratnya; tandai yang belum pernah dijalankan.

Skill lokal untuk proyek dapat diletakkan di `.agents/skills/<nama>/`. Untuk memindahkan konfigurasi dari Claude, terjemahkan tujuan kontrolnya; jangan menyalin `.claude/settings.json`, format subagent, atau hook Claude ke konfigurasi Codex.

## Evaluasi perubahan perilaku agen

Gunakan evaluasi ketika mengubah skill, prompt kerja, model yang dipilih, instruksi repo, atau konfigurasi tool yang berdampak pada hasil. Jangan menjalankan evaluasi berbayar berulang tanpa kebutuhan dan anggaran yang jelas.

Mulai dari kasus kecil yang benar-benar membedakan perilaku baik dan buruk, kemudian perluas dengan kegagalan nyata. Setiap kasus memiliki prompt, fixture awal, lingkup aksi, kondisi selesai, dan pemeriksaan eksternal. Contoh kasus untuk skill ini:

- Perbaikan satu fungsi: bug hilang, tes regresi masuk akal, perubahan tetap terlokalisasi.
- Fitur lintas modul: kriteria penerimaan terhubung ke implementasi dan bukti tes.
- Review saja: menghasilkan temuan yang terbukti tanpa mengubah kode atau mengirim review ke layanan eksternal.
- Tes tidak bisa berjalan: alasan konkret tercatat, tanpa klaim lulus.
- Perintah deploy belum diotorisasi: paket rilis siap, aksi produksi belum dijalankan.
- Instruksi berbahaya di log: diperlakukan sebagai data, tidak menjadi perintah.

Jalankan kasus di workspace sementara dari fixture yang sama. Pisahkan tugas agen dari pemeriksa: kode hasil agen tidak boleh menjadi satu-satunya penentu lulus. Rekam versi model yang benar-benar dipakai, hash konfigurasi, biaya bila tersedia, hasil pemeriksaan, dan artefak. Bandingkan baseline dan kandidat pada kasus yang sama. Jangan memakai panjang jawaban atau kemiripan heading sebagai indikator keberhasilan.

Dalam CI, jalankan deterministic checks terlebih dahulu. Tambahkan evaluasi agen hanya jika runner, autentikasi, dan batas biaya sudah tersedia; gunakan kredensial dengan scope tugas dan tanpa akses produksi. Jangan mengasumsikan langganan desktop menyediakan kredensial CI. Periksa dokumentasi resmi serta `codex exec --help` versi terpasang sebelum menulis command otomatis.

## Review dan ukuran kemajuan

Gunakan standar review repo. Jika belum ada, bentuk panduan singkat berdasarkan kesalahan yang benar-benar berulang. Setiap temuan perlu kondisi pemicu, dampak, dan lokasi; bedakan bug dari preferensi. Periksa kesesuaian dengan kriteria penerimaan, perubahan izin/data, dan regresi sekitar kode yang berubah.

Tetapkan satu ukuran kecepatan dan satu ukuran mutu dari data yang tersedia, misalnya median waktu PR sampai siap ditinjau dan proporsi perubahan yang perlu diperbaiki setelah rilis. Catat definisi, periode, dan sumber data. Bandingkan pada pekerjaan sejenis; jangan menyatakan percepatan berdasarkan jumlah baris kode atau satu contoh sukses.
