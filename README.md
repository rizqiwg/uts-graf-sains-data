# UTS Graf Sains Data: Rekomendasi Item dengan Neo4j (RetailRocket)

**Nama:** Rizqi Wahyu Gusniadi · **NIM:** 24031554203 · **Prodi:** S1 Sains Data, Universitas Negeri Surabaya · **Mata kuliah:** Graf Sains Data (UTS Gasal 2026/2027, individu)

Notebook ini mengerjakan UTS Graf Sains Data: data interaksi RetailRocket dimuat ke graf Neo4j, direpresentasikan dengan Vector Space Model, dihitung similarity antar item (cosine), lalu dipakai untuk rekomendasi KNN item-based dan dievaluasi dengan Hit@5 dan NDCG@5.

- **Periode (ditetapkan dosen):** P1 / training = 18–31 Mei 2015, P2 / testing = 16–31 Juli 2015 (UTC, batas akhir inklusif).
- **Penjelasan lengkap** (jawaban tiap soal, penjelasan Cypher, interpretasi hasil) ada di dalam notebook, di sel Markdown di atas dan di bawah tiap sel kode.

## Isi repositori

```
.
├── 203_UTS_Graf_Sains_Data.ipynb   # notebook utama: kode, output, dan penjelasan
├── data/
│   ├── events_P1.csv         # hasil filter P1 (training)
│   └── events_P2.csv         # hasil filter P2 (testing)
├── requirements.txt
├── README.md
└── .gitignore
```

`events.csv` asli (94 MB) tidak diunggah. Unduh dari Kaggle bila ingin menjalankan sel filter periode dari awal.

## Cara menjalankan

1. Buat environment dan pasang paket (contoh PowerShell; Linux/macOS memakai `source myvenv/bin/activate`):

   ```powershell
   uv venv myvenv --python 3.10
   myvenv\Scripts\Activate.ps1
   uv pip install -r requirements.txt
   ```

2. (Opsional) Unduh dataset dan taruh `events.csv` di folder `data/`:

   ```powershell
   curl.exe -L -o ecommerce-dataset.zip https://www.kaggle.com/api/v1/datasets/download/retailrocket/ecommerce-dataset
   Expand-Archive ecommerce-dataset.zip -DestinationPath data -Force
   ```

3. Jalankan Neo4j (diuji dengan Neo4j Desktop, instance lokal `neo4j://127.0.0.1:7687`, user `neo4j`, database `neo4j`).
4. Buka `203_UTS_Graf_Sains_Data.ipynb`, pilih kernel dari environment tadi, lalu *Run All*. Password Neo4j diminta lewat `getpass` dan tidak disimpan di notebook.
5. Kalau database sudah berisi graf dari proses sebelumnya, ubah `RESET_GRAPH = True` pada sel reset (bagian no. 3). **Hati-hati: ini menghapus seluruh graf pada database tersebut.**

## Ringkasan hasil

| Hal | Hasil |
|---|---|
| Graf P1 | 159.344 Visitor, 78.812 Item, 294.333 relasi aktivitas |
| Proyeksi terpilih | Item–Item (simpul separuh, vektor lebih kaya informasi) |
| Similarity (cosine) | 1.347.962 pasangan item dengan nilai > 0 |
| Item acuan (7a) | 370653; 5 tetangga teratas: 10132, 84160, 335975, 378621, 91755 |
| User acak (seed 42) | visitor 121532 |
| 3 item yang diiklankan (k = 5) | 12315, 33645, 39037 |
| Hit@5 / NDCG@5 | 0 / 0 (rata-rata 1.337 user layak: 0,0075 / 0,0039) |

## Lingkungan

Python 3.10.4, pandas 2.3.3, Neo4j 2026.09.0 (Neo4j Desktop 2.2.1), Windows.

## Sumber data

Roman Zykov, *Retailrocket recommender system dataset*, Kaggle: https://www.kaggle.com/datasets/retailrocket/ecommerce-dataset
