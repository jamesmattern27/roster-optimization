# Fantasy Baseball H2H Optimizer

An optimization-based roster construction tool for **head-to-head fantasy baseball category leagues**.

This project uses **mixed-integer linear programming (MILP)** to build an optimal fantasy roster that maximizes expected weekly category wins, subject to roster, positional, and auction budget constraints.

---

## Problem Statement

In a 10-team H2H categories league, each weekly matchup is decided by winning a majority of statistical categories (e.g. 6 out of 10).

Unlike roto leagues, **excess production in a category does not matter** once it is won. The objective is therefore to:

> **Maximize the expected number of categories won per week**, not total season stats.

This optimizer formalizes that goal mathematically.

---

## Key Features

- Optimizes for **weekly H2H category wins**
- Supports:
  - Auction budget constraints
  - Exact positional requirements
  - Counting and ratio categories (AVG, ERA, WHIP)
- Prevents over-investment in “runaway” categories
- Enables explicit **punt strategies**
- Fully reproducible and extensible

---

## Optimization Approach

### Decision Variables
- Player selection variables (binary)
- Category win indicators (binary)

### Objective
Maximize expected weekly category wins:

\[
\max \sum_{c} z_c
\]

Where \( z_c = 1 \) if the team is projected to win category \( c \).

### Constraints
- Auction budget
- Positional requirements
- Category thresholds relative to an expected opponent baseline
- Ratio categories handled via stat decomposition (e.g. ERA → earned runs)

This is solved as a **mixed-integer linear program (MILP)**.

---

## Data Requirements

You must provide:
- Player stat projections by category
- Projected auction values
- League settings (budget, roster, categories)

Expected input formats are documented in `data/raw/`.

---

## Repository Structure

- `models/` – core MILP formulation
- `optimization/` – solver logic and scenarios
- `data/` – raw and processed inputs
- `notebooks/` – exploratory analysis and validation
- `experiments/` – strategy configurations
- `tests/` – unit tests for constraints and logic

---

## Example Use Cases

- Balanced category build
- Power-heavy builds (HR/RBI focus)
- Explicit punt strategies (e.g. SB, SV)
- Auction budget sensitivity analysis

---

## Future Extensions

- Roto league support
- Playoff-only optimization
- Weekly streaming simulation
- Variance-aware chance constraints

---

## Disclaimer

This project is for educational and personal use. Fantasy outcomes depend on variance, injuries, and managerial decisions beyond the scope of this model.

---

## License

See the LICENSE file for details.
