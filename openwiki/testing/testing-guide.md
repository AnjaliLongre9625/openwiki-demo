---
type: guide
title: Testing Guide
description: Learn how to run the existing test suite and contribute new tests to the calculator application.
tags: [testing, development, python, pytest]
verified:
  - by: openwiki/0.7.0
    at: 2026-10-03T13:58:55.877Z
sources:
  - id: openwiki-source-23775c3de52f3ab95a13cb8b
    resource: repo://README.md
  - id: openwiki-source-63fdccb791696f475b33ce12
    resource: repo://tests/test_core.py
generated: { by: "openwiki/0.7.0", at: "2026-10-03T13:58:55.877Z" }
---

# Testing Guide

The Calculator Enterprise Baseline project uses [pytest](https://docs.pytest.org/) to ensure the correctness of the safe calculation engine. All arithmetic logic must be verified through the test suite before submitting changes.

## Test Structure

The project maintains a clean separation between application code and test logic:

- `calc_app/`: Contains the production application code, including the calculation engine (`core.py`).
- `tests/`: Contains the test suite. All tests are located here, with `tests/test_core.py` specifically targeting the `Calculator` class logic (e.g., operator precedence, error handling, and helper methods).

## Running Tests

Ensure you have your virtual environment activated and development dependencies installed:

```bash
# Install development dependencies
python -m pip install -r requirements-dev.txt

# Run the complete test suite
pytest
```

For more granular testing, you can pass arguments to `pytest`:

```bash
# Run tests for a specific file
pytest tests/test_core.py

# Run only tests matching a specific pattern
pytest -k "addition"
```

## Adding New Tests

When adding features or fixing bugs in the `Calculator` engine, follow these steps:

1. **Locate or create a test file**: If testing core logic, use `tests/test_core.py`. For new modules, create a corresponding test file in `tests/`.
2. **Define a fixture (optional)**: If your test requires an instance of the `Calculator` class, use a fixture to keep tests clean.
   ```python
   @pytest.fixture()
   def calculator() -> Calculator:
       return Calculator()
   ```
3. **Write the test case**: Use standard `assert` statements. For expected failures, use `pytest.raises`.
   ```python
   def test_new_feature(calculator: Calculator) -> None:
       assert calculator.evaluate("2+2") == 4.0
   ```
4. **Verify**: Run `pytest` to ensure your new tests pass and do not cause regressions.

## Manual Verification

Before or after automated testing, you can interact with the application directly to verify behavior:

### CLI Usage
Use module mode for reliable execution:
```bash
python -m calc_app.cli "2*(3+4)"
```

### GUI Usage
Launch the Tkinter application with:
```bash
python -m calc_app.ui
```

## Quality Checks

In addition to unit testing, ensure your code adheres to the project's quality standards before committing:

```bash
# Style and type checking
ruff check .
black --check --line-length 88 .
mypy calc_app tests
```
