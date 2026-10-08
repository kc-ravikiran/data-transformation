# Data Transformation

This project demonstrates basic **data transformation and format conversion** using diabetes and book datasets. The notebook converts data between CSV, JSON, XML, SQLite, TSV, and Excel formats. It also demonstrates basic datetime conversions using Python.

## Project Files

* `data_transformation.ipynb` - Jupyter notebook containing all data transformation and conversion steps.
* `Dataset_of_Diabetes.csv` - Source diabetes dataset in CSV format.
* `top_50_english_books.xml` - Source book dataset in XML format.
* `diabetes.json` - JSON file generated from `Dataset_of_Diabetes.csv`.
* `books.json` - JSON file generated from `top_50_english_books.xml`.
* `Diabetes.db` - SQLite database generated from the diabetes CSV data.
* `Diabetes.xlsx` - Excel file exported from the SQLite diabetes table.
* `client.csv` - CSV export created from the SQLite diabetes table.
* `client.tsv` - Tab-separated export created from `client.csv`.

The JSON, database, Excel, CSV, and TSV files are generated outputs. They can be recreated by running the notebook.

## Requirements

* Python 3.9 or newer
* Jupyter Notebook or JupyterLab
* A Python kernel such as `ipykernel`

### Python Packages Used by the Notebook

| Package     | Used for                                                    |
| ----------- | ----------------------------------------------------------- |
| `agate`     | Reading, inspecting, and converting tabular data            |
| `xmltodict` | Parsing the XML books file                                  |
| `csvkit`    | Working with CSV data                                       |
| `agate-sql` | Providing the `agatesql` module                             |
| `pandas`    | Reading CSV and SQLite data and exporting data to Excel     |
| `openpyxl`  | Excel writer used by `pandas.to_excel()`                    |
| `jupyter`   | Running the notebook environment                            |
| `ipykernel` | Making the Python environment available as a Jupyter kernel |

The notebook also imports `json`, `sqlite3`, `datetime`, and `getpass`. These modules are part of Python's standard library and do not require separate installation.

## Installation on Windows

Open PowerShell in the project directory and run:

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install jupyter ipykernel agate xmltodict csvkit agate-sql pandas openpyxl
```

If PowerShell blocks virtual-environment activation, run the following command once for the current PowerShell session and then activate the environment again:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\venv\Scripts\Activate.ps1
```

Register the environment as a Jupyter kernel:

```powershell
python -m ipykernel install --user --name datatransformation --display-name "Python (Data Transformation)"
```

## Running the Notebook

1. Open `data_transformation.ipynb` in VS Code or Jupyter.
2. Select the **Python (Data Transformation)** kernel.
3. Run the cells from top to bottom.
4. Keep all input files in the same directory as the notebook.

The notebook contains `%pip install` cells for `xmltodict` and `csvkit`. The installation command above installs these packages before the notebook starts, so those cells are not required when the environment is already configured.

## Notebook Workflow

### 1. Load CSV Data with Agate

`Dataset_of_Diabetes.csv` is loaded using `agate.Table.from_csv()`.

The notebook displays:

* The loaded table
* Column names
* Inferred column types
* A small data preview

### 2. Convert CSV to JSON

The diabetes CSV data is loaded into an Agate table and exported as `diabetes.json`.

The generated JSON file is then read back using `agate.Table.from_json()`.

This demonstrates conversion between **CSV and JSON formats**.

### 3. Convert XML to JSON

`top_50_english_books.xml` is parsed using `xmltodict`.

The parsed data is converted to JSON using Python's built-in `json` module and saved as `books.json`.

The `Books` section is then loaded into an Agate table.

This demonstrates conversion between **XML and JSON formats**.

### 4. Convert CSV to SQLite

The diabetes CSV file is read using pandas and written to the `diabetes` table in `Diabetes.db`.

Python's built-in `sqlite3` module is used to create and manage the local SQLite database.

This demonstrates transferring tabular data from a **CSV file into a relational database**.

### 5. Convert SQLite to Excel

The `diabetes` table is read from `Diabetes.db` using pandas.

The resulting DataFrame is exported to `Diabetes.xlsx`.

This demonstrates conversion from **relational database data to Excel format**.

### 6. Convert SQLite to CSV

The `diabetes` table is read from the SQLite database and exported to `client.csv`.

This demonstrates exporting database records into a standard CSV format.

### 7. Convert CSV to TSV

`client.csv` is read using pandas and written to `client.tsv`.

A tab character (`\t`) is used as the delimiter.

This demonstrates how the same tabular data can be represented using different delimiters.

### 8. Convert Datetime Values

The notebook demonstrates basic datetime transformations using Python's built-in `datetime` module.

The examples include:

* Converting a Unix timestamp to a date string in `YYYY-MM-DD` format.
* Converting a date and time string in `DD/MM/YY HH:MM` format to ISO 8601 format.

These examples demonstrate how datetime values can be transformed into standardized representations.

## Transformation Flow

The project demonstrates the following data transformation flows:

```text
CSV ──────────────► JSON
 │
 │
 └───────────────► SQLite ───────► Excel
                     │
                     └───────────► CSV ───────► TSV

XML ───────────────► JSON

Datetime ──────────► Standardized Date/Time Format
```

## Notes

* Run the notebook from the project directory so that relative file paths resolve correctly.
* Running the notebook again replaces the generated JSON, database, Excel, CSV, and TSV output files.
* `Diabetes.db` is created locally and does not require a separate database server.
* The project focuses on **data transformation, format conversion, and data representation**, rather than comprehensive data cleaning or exploratory data analysis.
