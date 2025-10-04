# Preprocessing Starter Pack (Kulino Minggu-3)

Paket ini menyiapkan skrip **`preprocessing.py`** yang sesuai dengan instruksi PPT *Pertemuan 3 – Preprocessing Data*:
- Pembersihan data (imputasi missing untuk numerik & kategori)
- Encoding kategori (OneHotEncoder)
- Split train/test
- Feature scaling (Standard/MinMax/Robust)
- (Opsional) quick training LogisticRegression sebagai sanity-check

## Struktur
```
preprocessing_starter_pack/
├─ preprocessing.py
├─ requirements.txt
└─ README.md
```

## Persiapan
1. Buat/siapkan dataset Anda: `Data.csv` (atau `.xlsx`).
2. Pastikan Anda tahu nama kolom target, misal: `label`, `class`, `target`, dll.
3. (Opsional) Buat virtualenv lalu install:
   ```bash
   pip install -r requirements.txt
   ```

## Menjalankan
Contoh pemakaian:
```bash
python preprocessing.py --csv Data.csv --target target --scaler standard --test-size 0.2 --train-model --stratify
```
Argumen penting:
- `--csv`: path ke file CSV/Excel
- `--target`: nama kolom target/label
- `--scaler`: `standard|minmax|robust|none`
- `--num-impute`: `mean|median|most_frequent|constant` (default `median`)
- `--cat-impute`: `most_frequent|constant` (default `most_frequent`)
- `--impute-constant`: nilai konstanta jika strategi `constant`
- `--train-model`: latih LogisticRegression cepat (opsional)
- `--stratify`: gunakan stratified split jika classification

Output tersimpan di folder **`artifacts/`**:
- `X_train.npy`, `X_test.npy` — matriks fitur (numpy)
- `X_train_processed.csv`, `X_test_processed.csv` — versi CSV dengan **feature names** setelah OHE
- `y_train.csv`, `y_test.csv`
- `preprocessor.joblib` — pipeline sklearn untuk inference nanti
- `metadata.json` — ringkasan konfigurasi dan bentuk data

## Checklist untuk Pengumpulan (sesuai PPT)
- [ ] Gunakan dataset yang Anda koleksi (minggu-2) atau modifikasinya
- [ ] Jalankan tahapan preprocessing (imputasi, encoding, split, scaling)
- [ ] Simpan hasil + pipeline
- [ ] Push repo ke **GitHub**
- [ ] Submit **URL GitHub** ke **Kulino (Minggu ke-3)**

## Tips
- Jika target berupa string (misal "ya"/"tidak"), skrip akan otomatis meng-encode saat opsi `--train-model` digunakan.
- Gunakan `--scaler none` jika model downstream Anda tidak butuh scaling (misal tree-based).
- Periksa `metadata.json` untuk memastikan pipeline sesuai ekspektasi.
