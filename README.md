# PlacementIQ — Student Placement & Salary Prediction

Dashboard Streamlit dengan arsitektur monolithic untuk memprediksi status placement mahasiswa dan estimasi salary. UI, feature engineering, pemuatan model, dan inferensi berada dalam satu aplikasi.

## Features

- Form profil, nilai akademik, skill, dan pengalaman mahasiswa.
- Klasifikasi **Placed / Not Placed** beserta probabilitas.
- Estimasi salary berlabel LPA ketika mahasiswa diprediksi Placed dan regressor tersedia.
- Gauge probabilitas dan ringkasan academic average, overall skill, serta experience score.
- Status pemuatan classifier dan regressor pada sidebar.

## Architecture

```text
Streamlit input → feature engineering → local classifier → status & probability
                                                    └→ regressor (if Placed)
```

Feature engineering membentuk academic average, overall skill, experience score, indikator CGPA tinggi, clean record, serta encoding gender dan kegiatan ekstrakurikuler. Model menerima 20 fitur dengan urutan eksplisit di `FEATURE_COLS`.

## Project structure

| Path | Fungsi |
| --- | --- |
| [app.py](app.py) | UI, feature engineering, dan inferensi |
| [B.csv](B.csv) | File dataset yang disertakan |
| [models/best_classifier.pkl](models/best_classifier.pkl) | Model klasifikasi |
| [models/best_regressor.pkl](models/best_regressor.pkl) | Model regresi |
| [models/feature_columns.txt](models/feature_columns.txt) | Daftar fitur |
| [requirements.txt](requirements.txt) | Dependensi Python |

Aplikasi menggunakan urutan fitur yang ditulis di kode; `feature_columns.txt` tidak dibaca saat inferensi.

## Getting started

```bash
git clone https://github.com/hoseaoc/Student-Placement-and-Salary-Prediction.git
cd Student-Placement-and-Salary-Prediction
python -m venv .venv
```

Aktifkan environment dengan `source .venv/bin/activate` (macOS/Linux) atau `.venv\Scripts\Activate.ps1` (PowerShell).

```bash
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

Pastikan kedua artefak tetap berada dalam folder `models/`. Isi form dan tekan **Prediksi Sekarang**.

## Scope & limitations

- Repository menyertakan artefak inferensi, tetapi tidak menyertakan training pipeline atau metrik evaluasi.
- `B.csv` tidak dibaca oleh alur prediksi aplikasi.
- Estimasi salary tidak ditampilkan untuk prediksi Not Placed.
- Versi library saat model diserialisasi tidak dicatat; versi Scikit-learn yang berbeda dapat memengaruhi pemuatan artefak.
- Rentang input dan satuan mengikuti UI proyek, termasuk CGPA dalam skala 10 dan salary berlabel LPA; jangan menganggapnya sebagai gaji dalam rupiah.

## Related project

[Versi decoupled dengan FastAPI dan Streamlit](https://github.com/hoseaoc/Student-Placement-and-Salary-Prediction-decoupled) memisahkan UI dari inferensi melalui HTTP API.

## Author

[Hosea Christian](https://github.com/hoseaoc) · [Portfolio](https://hosea-christian-portfolio.vercel.app)
