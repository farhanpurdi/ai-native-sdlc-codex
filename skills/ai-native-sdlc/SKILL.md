---
name: ai-native-sdlc
description: "Terapkan AI-native SDLC di Codex untuk delivery fitur lintas tahap, menyiapkan workflow SDLC sebuah repo, atau membawa insiden menjadi perbaikan teruji. Use for intent/spec/plan workflows and end-to-end software delivery. Jangan aktif untuk pertanyaan kode umum, terjemahan, atau edit sepele kecuali diminta."
---

# AI-native SDLC untuk Codex

Jalankan pekerjaan yang diminta sampai hasilnya bisa diperiksa. Sesuaikan kedalaman proses dengan dampak perubahan. Gunakan bahasa pengguna. Ini implementasi independen yang terinspirasi playbook Anthropic; pemetaan dan sumber ada di [references/origin.md](references/origin.md).

## Mulai dari keadaan repo

1. Baca instruksi `AGENTS.md` yang berlaku, status git, dokumen terkait, manifest, dan konfigurasi CI. Temukan perintah verifikasi dari repo; jangan menebak package manager atau framework.
2. Tentukan hasil yang diminta, tahap saat ini, batas pekerjaan, dan bukti keberhasilan. Manfaatkan jawaban serta persetujuan yang sudah ada. Tanyakan hanya keputusan yang benar-benar menghalangi; lanjutkan pekerjaan independen.
3. Pilih kedalaman: **ringkas** untuk perbaikan terlokalisasi dan mudah dibatalkan; **lengkap** untuk fitur lintas komponen, kontrak publik, migrasi, autentikasi, atau perubahan operasional. Jika pengguna hanya meminta review/rencana, berhenti pada hasil itu.
4. Gunakan lokasi dokumen yang sudah ada. Jika belum ada, simpan pekerjaan lengkap di `docs/changes/<slug>/`; gunakan slug unik untuk mencegah tabrakan. Alur ringkas cukup mencatat tujuan, rencana, dan bukti di chat/PR yang sudah ada. Jangan membuat lima file kosong untuk perbaikan kecil.

## Kerjakan tahap yang diperlukan

| Tahap | Tindakan dan hasil yang bisa diperiksa |
| --- | --- |
| Plan | Tulis `intent.md`: masalah nyata, hasil yang diinginkan, batas lingkup, serta hal yang belum diketahui. Pisahkan fakta pengguna dari asumsi. |
| Design | Susun `spec.md` dari konteks repo; beri ID pada kriteria penerimaan, jelaskan kontrak/data/UI yang berubah, serta pilihan yang membutuhkan keputusan. |
| Build | Buat `plan.md` berisi file sasaran, urutan dependensi, risiko, dan pemeriksaan yang membuktikan tiap kriteria. Implementasikan dalam lingkup izin yang ada; perbarui rencana jika pendekatan berubah. |
| Test | Jalankan pemeriksaan yang relevan, baca hasilnya, perbaiki penyebab kegagalan, lalu ulangi pemeriksaan yang terdampak. Catat bukti di `verification.md` atau PR. |
| Deploy | Bandingkan diff terhadap kebutuhan, periksa regresi dan risiko, siapkan ringkasan rilis serta cara pemulihan. Lakukan tindakan eksternal sesuai otorisasi dan gate yang benar-benar berlaku. |
| Maintain | Gunakan bukti insiden/metric untuk diagnosis, dokumentasikan ketidakpastian, dan turunkan tindak lanjut yang terukur. Verifikasi pemulihan jika observabilitas tersedia. |

Gunakan [assets/change-templates.md](assets/change-templates.md) hanya untuk artefak yang dibutuhkan; isi dengan konteks proyek, jangan menyalin petunjuk pengisian ke hasil akhir. Pertahankan ID tiket dan tautan sistem pencatatan yang sudah dipakai. Jangan menciptakan sumber kebenaran kedua tanpa menjelaskan hubungannya.

## Jaga kelancaran dan bukti

- Merencanakan pekerjaan tidak memerlukan klaim bahwa mode Plan UI sedang aktif. Jika mode aplikasi membatasi edit, patuhi batas tersebut. Dalam mode yang mengizinkan implementasi, permintaan implementasi yang jelas cukup untuk melanjutkan pekerjaan rutin; jangan menambah gerbang persetujuan di setiap dokumen.
- Status `draft`, `ready-for-review`, dan `accepted` harus mencerminkan kenyataan. Catat keputusan pengguna yang tersedia; jangan mengarang persetujuan, penanggung jawab, commit, atau hasil pengujian. Kebijakan review wajib milik proyek tetap berlaku.
- Lindungi perubahan pengguna yang sudah ada. Pisahkan subtask independen dengan kepemilikan file yang jelas; gunakan worktree untuk implementasi paralel yang berpotensi bertabrakan. Jika tool subagent tidak tersedia, kerjakan berurutan.
- Verifikasi perilaku dan kriteria penerimaan, bukan hanya kecocokan teks implementasi. Tambahkan regresi yang bermakna untuk bug. Perubahan kosmetik kecil cukup dengan inspeksi yang sesuai. Jalankan juga pemeriksaan wajib repo.
- Jangan melemahkan assertion atau menghapus tes agar hasil hijau. Jika ekspektasi tes memang perlu berubah, hubungkan perubahan itu ke kebutuhan yang berubah dan jelaskan alasannya.
- Bedakan `PASS`, `FAIL`, `BLOCKED`, dan `NOT RUN`. Sertakan perintah, hasil penting, dan alasan keterbatasan. Build berhasil tidak membuktikan seluruh perilaku benar.
- Untuk perubahan berisiko, gunakan review independen jika tersedia. Berikan diff, kebutuhan, dan akses baca/tes; minta temuan dengan bukti, dampak, dan lokasi. Review AI bukan persetujuan pemilik kode.
- Akhiri dengan hasil, bukti verifikasi, risiko yang tersisa, dan tindakan berikut yang memang diperlukan. Jangan menyebut deployed/merged/monitored bila hanya menyiapkan artefaknya.

## Saat memperbaiki workflow repo

Baca [references/repo-adoption.md](references/repo-adoption.md) ketika diminta menyiapkan SDLC, `AGENTS.md`, evaluasi agen, atau standar review. Identifikasi hambatan yang nyata, lalu implementasikan perubahan terkecil yang bisa diukur.

Baca [references/operations.md](references/operations.md) untuk CI/CD, gate produksi, monitoring, scan berkala, atau insiden. Persiapkan hasil konkret sebelum meminta izin yang belum tersedia. Skill ini tidak memasang scheduler, membuka akses produksi, mengubah kebijakan keamanan, atau menyinkronkan akun dengan sendirinya.
