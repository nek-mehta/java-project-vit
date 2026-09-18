# Personal Expense Tracker & Budget Analyzer

A console-based Java application for logging personal expenses, generating spending
reports, and getting real-time alerts when spending crosses a budget limit — built
as a course project to demonstrate core Java concepts: OOP, Collections, File I/O,
custom exceptions, and multithreading.

## Overview

The application is split into three functional modules that work together:

1. **Expense Entry & Categorization** — add, delete, and browse expenses, organized
   by a fixed set of categories (Food, Transport, Utilities, Entertainment, Health,
   Education, Shopping, Other).
2. **Persistence & Reporting** — every change is saved to disk immediately (Java
   object serialization), and expenses can be summarized into monthly, category-wise
   reports or exported to CSV.
3. **Budget Alerts (multithreaded)** — set a monthly spending limit per category. A
   background daemon thread independently re-checks all budgets every 15 seconds and
   prints an alert the moment a limit is crossed, in addition to an immediate check
   right after every new expense.

## Features

- Add / delete / view expenses with input validation
- Browse expenses by category
- Monthly spending report, broken down by category
- CSV export for opening in Excel/Sheets
- Per-category budget limits with live, background-monitored alerts
- All data persisted automatically — nothing is lost between runs

## Technologies / Tools Used

- **Java 21** (plain `javac`/`java` — no external build tool or libraries required)
- `java.io` object serialization for persistence
- `java.util.concurrent` (`ConcurrentHashMap`) for thread-safe alert tracking
- Git for version control

## Project Structure

```
expense-tracker/
├── src/
│   ├── main/java/com/expensetracker/
│   │   ├── Main.java                  # console entry point / menu
│   │   ├── model/                     # Expense, Category, Budget
│   │   ├── service/                   # ExpenseManager, BudgetManager, BudgetMonitorThread
│   │   ├── persistence/               # FilePersistenceManager (File I/O)
│   │   ├── report/                    # ReportGenerator
│   │   └── exception/                 # custom checked/unchecked exceptions
│   └── test/java/com/expensetracker/
│       └── ExpenseManagerTest.java    # self-contained validation tests
├── docs/diagrams/                     # UML + workflow diagrams
├── data/                              # created automatically on first run
└── .gitignore
```

## Steps to Install & Run

Requires a JDK (21 or later recommended).

```bash
# 1. Clone the repo
git clone <your-repo-url>
cd expense-tracker

# 2. Compile
find src/main/java -name "*.java" > sources.txt
javac -d out @sources.txt

# 3. Run
java -cp out com.expensetracker.Main
```

On first run it creates a `data/` folder with `expenses.dat` and `budgets.dat` —
these are your saved records, recreated automatically if deleted.

## Instructions for Testing

The project includes a small, dependency-free validation test suite (no JUnit
required, so there's nothing extra to install):

```bash
find src/main/java src/test/java -name "*.java" > sources.txt
javac -d out @sources.txt
java -cp out com.expensetracker.ExpenseManagerTest
```

This runs 7 checks covering valid/invalid input handling, deletion, monthly
category totals, and budget-alert triggering, and prints a `PASS`/`FAIL` line for
each.

## Screenshots

See `docs/diagrams/` for the system's UML diagrams (Use Case, Class, Sequence) and
the process workflow diagram. Run the app as shown above for a live console demo.

