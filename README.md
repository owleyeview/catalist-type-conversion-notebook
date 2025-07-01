# MAP Schema Migration Repo

Convert **Airtable CSV exports** of the Catalist schema into the **canonical MAP JSON import format**.

---

## 📁 Repo Layout

| Path         | What it holds                                                              |
| ------------ | -------------------------------------------------------------------------- |
| `notebooks/` |  `MAP_Migration_Pipeline.ipynb` – the guided notebook                      |
| `data/`      | **Ignored** folder for `MAP Types-Grid View.csv` or any other private CSVs  |
| `generated/` | JSON output files like `catalist_schema_YYYYMMDD_HHMMSS.json`              |
| `.gitignore` | already excludes `data/` and timestamped JSONs                             |

---

## 🔧 Prerequisites

```bash
python -m venv .venv && source .venv/bin/activate
pip install pandas jupyterlab
```

---

## 🚀 Running the Pipeline

1. **Export** your MAP Types Airtable view to CSV and save it as `data/MAP Types-Grid View.csv`.
2. Launch Jupyter:

   ```bash
   jupyter lab
   ```
3. Open `notebooks/MAP_Migration_Pipeline.ipynb` and run all cells top‑to‑bottom.
4. When complete, a timestamped JSON (e.g. `generated/catalist_schema_20250609_143500.json`) appears in `generated/`.

---

## 📝 What the Notebook Does

1. **Load CSV** from `data/` 
2. **Normalise** booleans / text 
3. **Build** a `schema` block and a `types[]` array (HolonType, PropertyType, ValueType, RelationshipType) 
4. **Flatten** former CollectionType fields into each RelationshipType spec 
5. **Validate** basic integrity (row counts, empty required fields) 
6. **Write** a timestamped, canonical JSON file ready for the two‑pass MAP loader.

