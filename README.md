# AI-native SDLC untuk Codex

Skill berbahasa Indonesia untuk membantu Codex membawa pekerjaan software dari kebutuhan sampai implementasi yang terverifikasi. Nama skill: **`ai-native-sdlc`**. Pemanggilan di Codex: **`$ai-native-sdlc`**.

Repository ini menjadi sumber skill yang dapat diunduh ulang ketika pindah komputer. Isinya berupa instruksi, referensi, dan template Markdown; tidak memerlukan library atau API key tambahan untuk memuat skill. Tool dan dependency yang diperlukan untuk mengerjakan proyek tetap mengikuti proyek tersebut.

## Latar belakang

Skill ini terinspirasi [The AI-native SDLC playbook dari Anthropic](https://claude.com/resources/articles/the-ai-native-sdlc-playbook). Gagasannya adalah memperbaiki seluruh alur pengembangan ketika AI sudah mempercepat penulisan kode: kebutuhan harus jelas, implementasi harus dapat diperiksa, dan temuan dari penggunaan software harus menjadi masukan untuk perbaikan berikutnya.

Adaptasi ini ditujukan untuk **Codex**. Konteks repository memakai `AGENTS.md`; praktik khusus Claude diterjemahkan sesuai kemampuan Codex dan tool yang tersedia. Skill ini merupakan implementasi independen, bukan produk resmi Anthropic atau OpenAI. Sumber dan batas adaptasi dicatat di [references/origin.md](skills/ai-native-sdlc/references/origin.md).

## Informasi skill

Skill menyesuaikan proses dengan lingkup pekerjaan:

- **Alur ringkas:** perbaikan kecil dan terlokalisasi. Tujuan, rencana, serta bukti dapat dicatat di chat atau PR yang sudah ada.
- **Alur lengkap:** fitur lintas komponen, perubahan kontrak publik, migrasi, atau perubahan operasional. Gunakan artefak yang relevan agar kebutuhan, keputusan, kode, dan hasil pemeriksaan dapat ditelusuri.

| Tahap | Hasil yang dibantu oleh skill |
| --- | --- |
| Plan | Tujuan, ruang lingkup, batasan, dan asumsi dalam `intent.md`. |
| Design | Pendekatan serta kriteria penerimaan dalam `spec.md`. |
| Build | Rencana file dan urutan kerja dalam `plan.md`, lalu implementasi. |
| Test | Pemeriksaan yang relevan dan bukti dalam `verification.md` atau PR. |
| Deploy | Review perubahan, kesiapan rilis, dan rencana pemulihan. |
| Maintain | Diagnosis insiden atau metrik serta tindak lanjut yang terukur. |

Tidak semua pekerjaan membutuhkan semua tahap atau semua file. Jika hanya diminta review atau rencana, skill mengikuti batas tersebut. Jika lokasi dokumen belum ditentukan, pekerjaan lengkap menggunakan `docs/changes/<slug>/` pada proyek yang dikerjakan.

## Struktur repository

```text
ai-native-sdlc-codex/
├── README.md
└── skills/
    └── ai-native-sdlc/
        ├── SKILL.md
        ├── agents/
        │   └── openai.yaml
        ├── assets/
        │   └── change-templates.md
        └── references/
            ├── origin.md
            ├── repo-adoption.md
            └── operations.md
```

`SKILL.md` adalah instruksi utama. `agents/openai.yaml` berisi nama tampilan dan contoh prompt. Referensi tambahan dimuat sesuai jenis pekerjaan; template menjadi bahan untuk dokumen perubahan.

## Instalasi di komputer baru

### Pilihan 1 — melalui Codex

Buka Codex pada komputer baru, lalu kirim prompt berikut:

```text
$skill-installer install https://github.com/farhanpurdi/ai-native-sdlc-codex/tree/main/skills/ai-native-sdlc
```

Installer bawaan akan mengambil folder skill beserta file pendukungnya. Jika sudah ada pemasangan bernama sama, periksa lokasi dan versinya terlebih dahulu sebelum menggantinya. Setelah selesai, mulai chat baru; jika belum muncul pada pemilih skill, mulai ulang Codex.

### Pilihan 2 — clone Git dan tautkan folder (macOS/Linux)

Cara ini memudahkan pembaruan: folder skill yang dibaca Codex menunjuk langsung ke clone Git. Jalankan dari direktori tempat Anda ingin menyimpan source:

```bash
git clone https://github.com/farhanpurdi/ai-native-sdlc-codex.git
cd ai-native-sdlc-codex
mkdir -p "$HOME/.agents/skills"
ln -s "$PWD/skills/ai-native-sdlc" "$HOME/.agents/skills/ai-native-sdlc"
```

Pertahankan clone pada lokasi tersebut; memindahkan atau menghapusnya akan memutus tautan. Jika tujuan tautan sudah ada, periksa pemasangan lama terlebih dahulu. Jangan memasang salinan lain dengan nama sama di beberapa lokasi discovery.

Lokasi pribadi `~/.agents/skills` serta dukungan symlink mengikuti [dokumentasi resmi skill Codex](https://learn.chatgpt.com/docs/build-skills). Installer bawaan pada beberapa versi juga menggunakan `~/.codex/skills`. Gunakan satu pemasangan yang terdeteksi oleh Codex Anda.

### Pilihan 3 — salin folder (Windows PowerShell)

Jalankan dari direktori tempat Anda ingin menyimpan clone:

```powershell
git clone https://github.com/farhanpurdi/ai-native-sdlc-codex.git
Set-Location ai-native-sdlc-codex
$skillDest = Join-Path $HOME '.agents\skills\ai-native-sdlc'
if (Test-Path $skillDest) { throw "Skill sudah ada di $skillDest; periksa sebelum menggantinya." }
New-Item -ItemType Directory -Force (Split-Path $skillDest) | Out-Null
Copy-Item -Recurse '.\skills\ai-native-sdlc' $skillDest
```

Setelah menyalin, mulai chat baru di Codex. Source Git dan folder skill terpasang merupakan dua salinan; `git pull` saja belum memperbarui salinan terpasang.

## Cara menggunakan

Buka proyek yang ingin dikerjakan di Codex. Sebutkan `$ai-native-sdlc` bersama tujuan yang konkret. Sertakan batas lingkup dan cara menilai keberhasilan bila sudah diketahui.

### Menyiapkan workflow repository

```text
Gunakan $ai-native-sdlc untuk memeriksa repo ini. Sesuaikan workflow
dengan stack dan CI yang ada, lalu implementasikan perbaikan lokal
yang paling berguna. Tunjukkan hasil dan bukti pemeriksaannya.
```

### Membangun fitur

```text
Gunakan $ai-native-sdlc untuk menambahkan pencarian produk berdasarkan
nama dan kategori. Pertahankan kontrak API yang ada. Susun artefak
yang diperlukan, implementasikan, dan uji perilaku normal serta input invalid.
```

### Memperbaiki bug

```text
Gunakan $ai-native-sdlc untuk memperbaiki pagination yang menerima
page=0. Input tersebut harus menghasilkan ValueError; perilaku halaman
valid harus tetap sama. Implementasikan dan tambahkan tes regresi.
```

### Review tanpa mengubah kode

```text
Gunakan $ai-native-sdlc untuk review perubahan ini saja.
Periksa kesesuaian dengan kebutuhan dan laporkan bug dengan lokasi,
kondisi pemicu, serta dampaknya.
```

### Menindaklanjuti insiden

```text
Gunakan $ai-native-sdlc untuk menganalisis log insiden terlampir.
Pisahkan fakta dan hipotesis, lalu tulis usulan perbaikan beserta
cara memverifikasinya. Mulai dari diagnosis baca-saja.
```

Skill dapat dipilih otomatis ketika permintaan sesuai deskripsinya. Pemanggilan eksplisit membantu memastikan alur ini digunakan pada tugas yang Anda pilih.

## Memperbarui dan memakai ulang

Jika menggunakan symlink dari clone Git:

```bash
cd /lokasi/clone/ai-native-sdlc-codex
git pull --ff-only
```

Tinjau perubahan sebelum memakainya. Karena Codex membaca source yang sama melalui tautan, Anda tidak perlu menyalin folder lagi. Mulai chat baru agar menggunakan instruksi terbaru.

Jika memakai installer atau salinan manual, minta Codex memperbarui skill dari repository ini setelah memeriksa pemasangan yang ada. Simpan modifikasi pribadi sebelum penggantian. Untuk memakai versi tertentu secara konsisten, gunakan commit atau tag yang tersedia dan simpan referensinya.

Pada komputer baru, ulangi salah satu cara instalasi di atas. Login dengan akun yang sama tidak menggantikan proses mengambil skill dari repository ini.

## Pemakaian khusus satu proyek dan Codex Cloud

Untuk membagikan skill bersama source sebuah proyek, salin `skills/ai-native-sdlc/` dari repository ini ke `.agents/skills/ai-native-sdlc/` pada proyek tujuan, lalu commit seluruh folder tersebut. Dengan demikian, referensi dan template ikut tersedia pada checkout proyek.

Skill yang berada di repository proyek dapat digunakan oleh tugas cloud yang membaca repository tersebut. Skill pribadi pada komputer lokal tidak otomatis tersinkron ke cloud. Lihat [batas lingkungan cloud](https://learn.chatgpt.com/docs/environments/cloud-environments#current-limitations).

## Batas penggunaan dan verifikasi

Skill membantu proses kerja; hasil akhirnya bergantung pada konteks proyek dan tool yang tersedia. Pemasangan skill tidak mengaktifkan scheduler, deployment, monitoring produksi, atau layanan scan. Tindakan tersebut mengikuti permintaan pengguna dan kontrol proyek.

Bukti pemeriksaan harus membedakan `PASS`, `FAIL`, `BLOCKED`, dan `NOT RUN`. Tes yang tidak dapat dijalankan tidak boleh disebut lulus. Review AI tetap menjadi masukan bagi pemilik kode dan kebijakan review proyek.

Versi awal telah melewati validasi format skill dan uji terpisah berupa perbaikan pagination: dua tes regresi yang semula gagal menjadi lulus, dengan total delapan tes lulus. Uji tersebut mencakup alur perbaikan kecil; tetap jalankan verifikasi yang relevan pada proyek Anda.

## Referensi

- [The AI-native SDLC playbook — Anthropic](https://claude.com/resources/articles/the-ai-native-sdlc-playbook)
- [Kursus pendamping Claude Academy](https://academy.claude.com/courses/ai-native-sdlc-playbook)
- [Build skills — dokumentasi OpenAI](https://learn.chatgpt.com/docs/build-skills)
- [Skill Installer — source resmi OpenAI](https://github.com/openai/skills/tree/main/skills/.system/skill-installer)
