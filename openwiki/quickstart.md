---
type: documentation
title: Quickstart
description: An introduction to the Calculator Enterprise Baseline project with steps for local environment setup, execution, and testing.
tags: [getting-started, setup, installation, usage]
sources:
  - id: openwiki-source-23775c3de52f3ab95a13cb8b
    resource: repo://README.md
generated: { by: "openwiki/0.7.0", at: "2026-10-03T13:40:46.570Z" }
---

# Quickstart

Welcome to the **Calculator Enterprise Baseline** project. This project provides a robust, Python-based calculator featuring a safe expression evaluation engine, a Tkinter GUI, and a CLI interface.

## Prerequisites

Ensure you have the following installed on your system:
- Python 3.10+
- `pip`

## Getting Started

Follow these steps to set up your local development environment.

### 1. Project Setup
Clone the repository and prepare your virtual environment:

```bash
# Clone the repository
git clone <your-repo-url>
cd python

# Create and activate a virtual environment
# macOS/Linux
python3 -m venv .venv
source .venv/bin/activate

# Windows (PowerShell)
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 2. Install Dependencies
Install both runtime and development dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements-dev.txt
```

### 3. Verification
Verify the installation by running the CLI evaluator:

```bash
python -m calc_app.cli "2*(3+4)"
# Output: 14
```

## Running the Application

The calculator supports two modes of operation:

- **GUI Interface:** Launch the Tkinter desktop application:
  ```bash
  python -m calc_app.ui
  ```

- **CLI Interface:** Evaluate expressions directly from your terminal:
  ```bash
  python -m calc_app.cli "(8+2)*5"
  ```

## Project Domain Overview

To dive deeper into the project, consult these documentation sections:

*   **Architecture:** Learn about the design principles in the [Architecture Overview](architecture/overview.md) and the [Core Logic](architecture/core-logic.md) engine.
*   **Testing:** Understand how to validate changes in the [Testing Guide](testing/testing-guide.md).
*   **Operations:** Explore how to add new functionality in the [Feature Addition Guide](operations/feature-addition.md).
