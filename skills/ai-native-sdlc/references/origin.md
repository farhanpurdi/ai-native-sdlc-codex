# Sumber dan batas adaptasi

Ditinjau 22 Oktober 2026. Paket ini bukan produk resmi Anthropic atau OpenAI dan tidak menyertakan salinan artikel.

Sumber gagasan: [The AI-native SDLC playbook — Anthropic](https://claude.com/resources/articles/the-ai-native-sdlc-playbook), Louis Claxton, 21 Agustus 2026; [kursus pendamping Claude Academy](https://academy.claude.com/courses/ai-native-sdlc-playbook).

Playbook memandang SDLC sebagai siklus Plan, Design, Build, Test, Deploy, dan Maintain. Dokumen intent, spesifikasi, dan rencana menghubungkan permintaan dengan implementasi. Pengetahuan tim dipelihara dalam instruksi dan skills; pemeriksaan berulang memberi umpan balik; review serta kontrol rilis menjaga akuntabilitas; temuan operasional menjadi pekerjaan berikutnya. Urutan adopsi mengikuti prasyarat, bukan keharusan menjalankan semua tahap pada semua tugas.

Paket ini menerapkan gagasan tersebut ke Codex dengan keputusan desain tersendiri: alur ringkas/lengkap, ID kriteria penerimaan, status bukti, template minimal, dan batas otomasi yang eksplisit. Gunakan `AGENTS.md` untuk konteks Codex. Perintah Claude, layanan Claude Security/Tag, konfigurasi `.claude`, serta contoh kredensial vendor tidak dibawa ke paket ini. Format markdown tidak menggantikan enforcement platform.

Rujukan implementasi Codex: [Build skills](https://learn.chatgpt.com/docs/build-skills), [Agent Skills](https://developers.openai.com/codex/skills), dan [Skills in ChatGPT](https://help.openai.com/en/articles/20001066-skills-in-chatgpt). Dukungan lokal, cloud, dan workspace tidak boleh diasumsikan identik. Periksa dokumentasi terbaru ketika membuat integrasi spesifik versi.
