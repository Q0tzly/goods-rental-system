# Architecture

## Overview

A local system for managing the lending status of physical items, more safety instead of a paper-based lending sheet.
Also, it's specific that instead of using a database, it stores logs and state in files, and uses Git for tamper prevention and history tracking.
As a result, It can split save the data. then it can be more safety at local environments.

---

## Requirements

### System Overview

- Runs locally (offline use assumed)
- Provides a browser-accessible Web UI
- Prevents tampering by managing logs and state files with Git
- Pushes changes to a locally hosted GitLab server

### Data Management

- No database; uses file-based storage (JSON/YAML)
- Keeps chronological logs of lending and returning
- Maintains a file representing the current status of each item (lent/in stock)
- Lending item definitions and required fields are configurable via a config file

---

## Directory Structure

```
.
├── cmd
│   └── main.go
├── config
├── docs
│   └── architecture.md
├── go.mod
├── internal
├── LICENSE
├── logs
├── README.md
├── scripts
│   └── run.sh
└── state
```

---

## Technical Specifications

| Component         | Technology                       |
| ----------------- | -------------------------------- |
| Backend           | Go                               |
| Frontend          | HTML + JS + Chota CSS            |
| Data Format       | JSON, YAML                       |
| Git Operations    | Performed within Go `os/exec`    |
| Config Management | YAML (e.g., `config/items.yaml`) |

---

## Data Files

### config/items.yaml

``` yaml
items:
  - name: CardGame
    count: 2
  - name: BoardGame
    count: 1

required_fields:
  - Borrower Name
  - Data
  - Borrowed One
```

---

## Tamper Prevention & History Management (Git Integration)

- All logs and state files are managed in Git
- Automatically runs git add, commit, and push after file updates
- Pushes changes to a local GitLab server for centralized and dispersion version control
- Tags and branches can be used to track and restore specific periods

---

## Notes

- Initial deployment is intended for full offline use, with no external dependencies
