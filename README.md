# Zoo_Database_Project
# 🦁 Zoo Management Database

A relational database project for managing a zoo: animals, staff, veterinary care, shows, food supply, and visitor interaction. Built with **Oracle SQL** (tested in Oracle SQL Developer).



## Overview

The database models the daily operations of a zoo:

- **Staff** – employees (trainers, caretakers, veterinarians, etc.), each with exactly one contract
- **Animals** – classified as mammals, birds, or fish, each living in one climate sector
- **Health** – veterinary consultations with diagnosis, treatment, and measured weight
- **Shows** – trainers and animals taking part in public performances
- **Logistics** – food stock and the suppliers who provide it
- **Visitors** – tickets purchased and reviews left for each sector

## Database Design

The project includes an ER diagram, a conceptual diagram, and relational schemas (see the project documentation).

**Main design choices**

- `ANIMAL` is a supertype with three subtypes (`MAMIFER`, `PASARE`, `PESTE`) sharing the same primary key.
- Many-to-many relationships are resolved through associative tables.
- `PARTICIPA_LA` is a ternary relationship linking animals, trainers, and shows.

## Tables (18)

| Group | Tables |
|---|---|
| Staff | `CONTRACT`, `ANGAJAT` |
| Animals | `SECTOR`, `ANIMAL`, `MAMIFER`, `PASARE`, `PESTE` |
| Health | `CONSULTATIE` |
| Food & suppliers | `HRANA`, `FURNIZOR`, `MANANCA`, `FURNIZEAZA` |
| Shows & care | `SPECTACOL`, `PARTICIPA_LA`, `INGRIJESTE` |
| Visitors | `VIZITATOR`, `BILET`, `RECENZIE` |

## Constraints (examples)

- `PRIMARY KEY`, `FOREIGN KEY`, and `UNIQUE` (e.g. employee CNP, supplier CUI)
- `CHECK` constraints, e.g.:
  - `data_venirii >= data_nasterii` for animals
  - review rating between 1 and 5
  - positive salary, surface area, and food quantity
  - restricted value lists for animal type, ticket type/status, water type, and diet
- `ON DELETE CASCADE` for subtypes, tickets, and reviews
- `DEFAULT SYSDATE` for arrival, consultation, and review dates

## Getting Started

1. Open Oracle SQL Developer (or any Oracle-compatible client).
2. Run the table creation script. Order matters because of foreign keys:
   `CONTRACT → ANGAJAT → SECTOR → ANIMAL → MAMIFER / PASARE / PESTE → HRANA → FURNIZOR → SPECTACOL → VIZITATOR → BILET → RECENZIE → CONSULTATIE → PARTICIPA_LA → INGRIJESTE → MANANCA → FURNIZEAZA`
3. Run the insert script to load the sample data (12 contracts and employees, 30 animals, 10 sectors, 15 tickets, etc.).
4. Check the data, e.g.:

```sql
SELECT * FROM ANIMAL;
```

## Tech Stack

- Oracle SQL / PL-SQL dialect (`VARCHAR2`, `NUMBER`, `SYSDATE`)
- Oracle SQL Developer
