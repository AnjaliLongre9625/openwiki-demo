---
type: guide
title: Feature Addition Guide
description: Step-by-step instructions for extending the calculator core logic or user interface safely.
tags: [operations, development, calculator]
verified:
  - by: openwiki/0.7.0
    at: 2026-10-03T13:58:55.877Z
sources:
  - id: openwiki-source-c6a07b2614cdc2c84675e756
    resource: repo://calc_app/core.py
  - id: openwiki-source-ed2dc92a5cc96cd18b8ce106
    resource: repo://calc_app/ui.py
generated: { by: "openwiki/0.7.0", at: "2026-10-03T13:58:55.877Z" }
---

# Feature Addition Guide

To safely introduce new features to the calculator, follow these patterns to maintain the separation between the arithmetic engine and the graphical interface.

## Architectural Boundaries

The application is structured to isolate business logic from UI concerns:

*   **`Calculator` (Core Logic)**: Located in `repo://calc_app/core.py`. The `Calculator` class provides an independent arithmetic engine using Python's `ast` module, intentionally decoupled from the GUI. It is responsible for expression parsing, arithmetic evaluation, and state transformations. It has no dependency on `tkinter`.
*   **`CalculatorApp` (UI)**: Located in `repo://calc_app/ui.py`. Manages the `tkinter` window, event bindings, and display state. It delegates mathematical operations to the `Calculator`.

## Workflow for Extending Features

### 1. Extending Core Logic
If the new feature is a mathematical operation (e.g., exponentiation) or a state-manipulation utility:

1.  **Update `Calculator`**: Modify `repo://calc_app/core.py`.
2.  **Update `evaluate`**: If it is a new operator, update the `_eval_node` recursive parser and `_apply_binary_operator` method.
3.  **Ensure Safety**: Always validate inputs. The `evaluate` method uses `ast.parse` to convert strings into a safe, restricted AST, protecting against arbitrary code execution by only permitting specific nodes (literals, unary operations, binary operations).
4.  **Testing**: Verify the logic using standalone unit tests that instantiate `Calculator` without requiring a UI.

### 2. Extending the User Interface
If the new feature adds visual interaction or a new button:

1.  **Update `CalculatorApp`**: Modify `repo://calc_app/ui.py`.
2.  **Define Action**: If the button triggers core logic, call the `Calculator` instance (`self.calculator`).
3.  **Update `_build_buttons`**: Add the new `tk.Button` to the `button_frame` grid.
4.  **Formatting**: If the feature produces a new type of output, update `_format_result` to handle the display representation properly.

## Recommended Control Flow

The following diagram illustrates how the components interact during a standard calculation:

```mermaid
sequenceDiagram
    participant User
    participant UI as CalculatorApp
    participant Engine as Calculator

    User->>UI: Clicks "="
    UI->>UI: Gets current expression
    UI->>Engine: call evaluate(expression)
    Engine->>Engine: Parse and calculate
    Engine-->>UI: Returns result (float)
    UI->>UI: Formats result
    UI-->>User: Updates display
```

## Maintenance Invariants

*   **Exceptions**: When core logic fails, raise `CalculationError` from `repo://calc_app/core.py`. The UI is designed to catch this and display "Error". Never leak internal Python exceptions directly to the user.
*   **Decoupling**: Keep `core.py` free of `tkinter` imports. This allows for easier testing and potential future ports to other UI frameworks (like CLI or web).
