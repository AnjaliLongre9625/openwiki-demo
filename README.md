# Calculator Enterprise Baseline

A Python calculator project with a Tkinter GUI, safe expression evaluation core, tests, and CI quality gates.

## Features

- Tkinter-based GUI calculator
- CLI expression evaluation
- Safe arithmetic parser (AST-based, no direct `eval`)
- Automated checks: Ruff, Black, MyPy, Pytest

## Project Structure

```text
.
├── calc_app/
│   ├── __init__.py
│   ├── core.py              # Safe calculation engine
│   ├── ui.py                # Tkinter application
│   └── cli.py               # CLI entrypoint
├── tests/
│   └── test_core.py
├── .github/workflows/ci.yml
├── requirements.txt
├── requirements-dev.txt
├── mypy.ini
├── pytest.ini
└── .ruff.toml
```

## Requirements

- Python 3.10+
- `pip` (usually included with Python)

## Detailed Local Setup

### 1. Clone and enter project

```bash
git clone <your-repo-url>
cd python
```

### 2. Create a virtual environment

macOS/Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Windows (PowerShell):

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

Runtime and development tools are managed through requirements files.

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements-dev.txt
```

### 4. Verify installation

```bash
python -m calc_app.cli "2*(3+4)"
```

Expected output:

```text
14
```

## Run

### GUI

```bash
python -m calc_app.ui
```

### CLI

Module mode (recommended):

```bash
python -m calc_app.cli "(8+2)*5"
```

## Quality Checks

Run these before committing or opening a PR.

```bash
ruff check .
black --check --line-length 88 .
mypy calc_app tests
pytest
```

## Local Development Workflow

1. Activate virtual environment.
2. Make code changes.
3. Run quality checks.
4. Run GUI/CLI smoke checks.
5. Commit and push.

## Troubleshooting

### `ImportError` when running `calc_app/cli.py` directly

Do not run this:

```bash
python calc_app/cli.py
```

Use module mode instead:

```bash
python -m calc_app.cli "2+2"
```

### Missing dependency errors (for example `pytest` not found)

Install development dependencies in the active environment:

```bash
python -m pip install -r requirements-dev.txt
```

### Exit virtual environment

```bash
deactivate
```

## Security Note

Expression evaluation only allows numeric literals, parentheses, and these operators: `+`, `-`, `*`, `/`, `%`.
#
