# Data Wrangling

This project demonstrates basic data-wrangling tasks with diabetes and book datasets. The notebook converts data between CSV, JSON, XML, SQLite, TSV, and Excel formats, and includes basic datetime conversions.

## Project Files

- `datawrangling.ipynb` - Jupyter notebook containing all data-wrangling steps.
- `Dataset_of_Diabetes.csv` - Source diabetes dataset in CSV format.
- `top_50_english_books.xml` - Source book dataset in XML format.
- `diabetes.json` - JSON file generated from `Dataset_of_Diabetes.csv`.
- `books.json` - JSON file generated from `top_50_english_books.xml`.
- `Diabetes.db` - SQLite database generated from the diabetes CSV data.
- `Diabetes.xlsx` - Excel file exported from the SQLite diabetes table.
- `client.csv` - CSV export created from the SQLite diabetes table.
- `client.tsv` - Tab-separated export created from `client.csv`.

The JSON, database, and Excel files are generated outputs. They can be recreated by running the notebook.

## Requirements

- Python 3.9 or newer
- Jupyter Notebook or JupyterLab
- A Python kernel such as `ipykernel`

### Python packages used by the notebook

| Package | Used for |
| --- | --- |
| `agate` | Reading, inspecting, and converting tabular data |
| `xmltodict` | Parsing the XML books file |
| `csvkit` | CSV data-wrangling tools; imported in the notebook |
| `agate-sql` | Providing the `agatesql` module |
| `pandas` | Reading CSV and SQLite data and exporting to Excel |
| `openpyxl` | Excel writer used by `pandas.to_excel()` |
| `jupyter` | Running the notebook environment |
| `ipykernel` | Making the Python environment available as a Jupyter kernel |

The notebook also imports `json`, `sqlite3`, `datetime`, and `getpass`. These are included in Python's standard library and do not need to be installed separately.

## Installation on Windows

Open PowerShell in this project directory and run:

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install jupyter ipykernel agate xmltodict csvkit agate-sql pandas openpyxl
```

If PowerShell blocks virtual-environment activation, run this once for the current PowerShell session and then activate the environment again:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\venv\Scripts\Activate.ps1
```

Register the environment as a Jupyter kernel:

```powershell
python -m ipykernel install --user --name datawrangling --display-name "Python (Data Wrangling)"
```

## Running the Notebook

1. Open `datawrangling.ipynb` in VS Code or Jupyter.
2. Select the `Python (Data Wrangling)` kernel.
3. Run the cells from top to bottom.
4. Keep all input files in the same directory as the notebook.

The notebook contains `%pip install` cells for `xmltodict` and `csvkit`. The installation command above installs them before the notebook starts, so those cells are not required when the environment is already set up.

## Notebook Workflow

### 1. Load CSV data with Agate

`Dataset_of_Diabetes.csv` is loaded with `agate.Table.from_csv()`. The notebook prints the table, column names, inferred column types, and a small preview.

### 2. Convert CSV to JSON

The Agate table is written to `diabetes.json`, then read back with `agate.Table.from_json()`.

### 3. Convert XML to JSON

`top_50_english_books.xml` is parsed with `xmltodict`, converted to JSON with Python's `json` module, and saved as `books.json`. The `Books` section is then loaded with Agate.

### 4. Convert CSV to SQLite

The diabetes CSV file is read with pandas and written to the `diabetes` table in `Diabetes.db` using Python's built-in `sqlite3` module.

### 5. Convert SQLite to Excel

The `diabetes` table is read from `Diabetes.db` with pandas and exported to `Diabetes.xlsx`.

### 6. Convert SQLite to CSV

The `diabetes` table is read from `Diabetes.db` with pandas and exported to `client.csv`.

### 7. Change CSV delimiters

`client.csv` is read with pandas and written to `client.tsv` using a tab character (`\t`) as the delimiter.

### 8. Convert datetime values

The notebook demonstrates two datetime conversions with Python's built-in `datetime` module:

- A Unix timestamp is converted to a date string in `YYYY-MM-DD` format.
- A date and time string in `DD/MM/YY HH:MM` format is converted to ISO 8601 format.

## Notes

- Run the notebook from the project directory so its relative file paths resolve correctly.
- Running the notebook again replaces the generated JSON, database, Excel, CSV, and TSV outputs.
- `Diabetes.db` is created locally and does not require a separate database server.
