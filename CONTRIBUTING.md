# Contributing to Text-to-SQL Benchmark Indonesia

Terima kasih atas minat Anda untuk berkontribusi! 🎉

## Cara Berkontribusi

### 🐛 Melaporkan Bug
- Buka [Issue](https://github.com/Galih-Hermawan-Unikom/text2sql-benchmark-id/issues/new) dengan label `bug`
- Sertakan ID skenario yang bermasalah (contoh: `RES-A3-01`)
- Jelaskan perilaku yang diharapkan vs aktual

### ➕ Menambah Skenario Baru
1. Fork repositori ini
2. Tambahkan skenario baru ke `gold-standard.json` dengan format:
   ```json
   {
     "id": "SAK-X1-01",
     "db": "sakila",
     "category": "KategoriBaru",
     "question_id": "Pertanyaan dalam Bahasa Indonesia",
     "question_en": "Question in English",
     "solution_sql": "SELECT ...",
     "expected_rows": [...],
     "ordering": null,
     "notes": "Catatan tentang skenario"
   }
   ```
3. Pastikan `solution_sql` sudah diuji dan menghasilkan output yang benar
4. Kirim Pull Request

### 🤖 Berbagi Hasil Model LLM Baru
1. Jalankan skenario terhadap model baru Anda
2. Simpan output ke folder `luaran-model/` dengan format:
   `{SCENARIO_ID}_{model-name}.json`
   Contoh: `RES-A3-01_my-model.json`
3. Jika model menghasilkan nama kolom berbeda, tambahkan mapping di `semantic_map.yaml`
4. Kirim Pull Request dengan hasil dan ringkasan performa

### 📝 Memperbaiki Dokumentasi
- Perbaiki typo, tambahkan contoh, atau perjelas instruksi
- Semua kontribusi dokumentasi sangat dihargai

## Pull Request

1. Buat branch dari `main` untuk perubahan Anda
2. Pastikan file JSON valid (buka di JSON validator)
3. Jelaskan perubahan Anda di deskripsi PR
4. Tunggu review dari maintainer

## Kode Etik

Bersikaplah hormat dan konstruktif dalam semua interaksi. Kami menghargai kontribusi dari semua kalangan.

## Pertanyaan?

Buka [Discussion](https://github.com/Galih-Hermawan-Unikom/text2sql-benchmark-id/discussions) atau kirim email ke galih.hermawan@email.unikom.ac.id.
