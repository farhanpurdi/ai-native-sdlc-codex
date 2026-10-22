# Format kerja yang dapat disesuaikan

Ambil bagian yang berguna saja. Teks dalam kurung siku adalah petunjuk yang diganti dengan data aktual. Jangan membuat identitas, timestamp, persetujuan, atau angka baseline yang belum tersedia. Tambahkan referensi relatif antarartefak.

## intent.md

```markdown
# [Judul perubahan]
Status: draft
Sumber permintaan: [pesan/tiket/insiden]
Pemilik keputusan: [bila diketahui]

## Keadaan dan tujuan
[Perilaku saat ini, pengguna terdampak, dan hasil yang diinginkan.]

## Lingkup
[Yang dikerjakan dan batas yang disepakati.]

## Ukuran keberhasilan
[Indikator yang dapat diperiksa; baseline hanya jika tersedia.]

## Batasan dan ketidakpastian
[Kompatibilitas, data, operasional, asumsi, keputusan terbuka.]
```

## spec.md

```markdown
# Spesifikasi [judul]
Intent: [tautan]
Status: draft

## Kriteria penerimaan
| ID | Kondisi awal dan tindakan | Hasil yang dapat diamati |
| --- | --- | --- |
| AC-01 | [skenario] | [hasil] |

## Pendekatan
[Komponen, kontrak, perubahan data atau tampilan, serta alasan pilihan.]

## Perilaku gagal dan kompatibilitas
[Masukan invalid, izin, timeout, data lama, atau dampak yang relevan.]

## Keputusan yang belum selesai
[Dampak masing-masing opsi dan siapa yang dapat memutuskan.]
```

## plan.md

```markdown
# Rencana [judul]
Spesifikasi: [tautan]
Status: draft

| Urutan | File/komponen | Perubahan | AC terkait | Pemeriksaan |
| --- | --- | --- | --- | --- |
| 1 | [path] | [tindakan] | AC-01 | [tes/observasi] |

## Risiko dan pemulihan
[Bagian paling berisiko, deteksi kegagalan, cara membatalkan perubahan.]

## Keputusan pelaksanaan
[Dasar otorisasi yang tersedia dan perubahan pendekatan bila ada.]
```

## verification.md

```markdown
# Bukti [judul]
Revisi yang diperiksa: [SHA atau keadaan working tree yang dijelaskan]

| Kriteria | Perintah/observasi | Hasil | Bukti |
| --- | --- | --- | --- |
| AC-01 | [pemeriksaan] | PASS / FAIL / BLOCKED / NOT RUN | [hasil/link log] |

## Review
[Temuan, perbaikan, dan risiko residual; identitas reviewer hanya jika nyata.]

## Status pengiriman
[Perubahan lokal / PR dibuka / merged / deployed; pilih yang terbukti.]
```

## incident.md

```markdown
# Insiden [judul]
Sumber sinyal: [tautan dan waktu beserta zona waktu]
Layanan/revisi terdampak: [bukti yang tersedia]

## Fakta dan hipotesis
[Pisahkan observasi, dugaan penyebab, dan bukti pembeda.]

## Tindakan dan hasil
[Perintah/runbook, dasar otorisasi, hasil, metrik sesudah tindakan.]

## Tindak lanjut
[Tautan intent baru, regression test/eval, penanggung jawab bila diketahui.]
```
