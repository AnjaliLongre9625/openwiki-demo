---
type: architecture
title: Architecture Overview
description: A high-level overview of the calculator application, describing the interaction between the core logic and interface layers.
tags: [architecture, calculator, python]
verified:
  - by: openwiki/0.7.0
    at: 2026-10-03T13:40:46.570Z
sources:
  - id: openwiki-source-8d788d289cb7a8229c5c0a78
    resource: repo://calc_app/cli.py
  - id: openwiki-source-c6a07b2614cdc2c84675e756
    resource: repo://calc_app/core.py
  - id: openwiki-source-ed2dc92a5cc96cd18b8ce106
    resource: repo://calc_app/ui.py
generated: { by: "openwiki/0.7.0", at: "2026-10-03T13:40:46.570Z" }
---

# Architecture Overview

The calculator application is designed with a clear separation between business logic and presentation layers. This decoupled architecture allows the application to support multiple interfaces (CLI and GUI) while sharing a single, robust arithmetic core.

## System Components

### 1. Core Logic (`calc_app/core.py`)
The `Calculator` class acts as the system's engine. It is responsible for parsing arithmetic expressions and performing calculations using Python's `ast` (Abstract Syntax Tree) module to ensure safe evaluation. It is completely independent of any input or output mechanisms, making it portable and testable in isolation.

### 2. User Interfaces
The application provides two entry points that interact with the `Calculator` core:

*   **CLI (`calc_app/cli.py`)**: A command-line interface that accepts expressions as arguments and prints the results directly to the standard output.
*   **GUI (`calc_app/ui.py`)**: A graphical user interface built with `tkinter`. It provides a visual calculator keypad and display area, mapping button events to the `Calculator` core methods.

## Component Interaction

The following diagram illustrates how the interface layers communicate with the `Calculator` core:

```mermaid
graph TD
    CLI[CLI Layer] -->|Call| Core
    UI[GUI Layer] -->|Call| Core
    
    subgraph Core[Calculator Core]
        Eval[evaluate method]
        Logic[Operations: +, -, *, /, %]
        Eval --> Logic
    end
```

## Data Flow and Control

1.  **Input Collection**: User input is captured via the interfaces (`argparse` in CLI or `tkinter.Entry` widgets in the GUI).
2.  **Expression Processing**: The UI/CLI layer passes the raw input string to the `Calculator.evaluate()` method.
3.  **Safe Evaluation**: The core utilizes `ast.parse` to convert the string into an AST, walks the tree to evaluate nodes, and returns the result as a float.
4.  **Error Handling**: If the input is invalid or a mathematical error occurs (e.g., division by zero), the core raises a `CalculationError`, which the interface layers catch and display to the user appropriately.
5.  **Output**: The resulting value is formatted (e.g., stripping unnecessary decimals for integers) and presented to the user.
