# World Cup Database

**freeCodeCamp Relational Database Certification** — Project #2

A PostgreSQL database project that parses World Cup tournament data from a CSV file and runs analytical queries. Demonstrates data import automation with bash scripting and complex SQL queries including joins, aggregations, and subqueries.

---

## Features

- **CSV data import** — reads games.csv and inserts teams and matches into PostgreSQL
- **Duplicate prevention** — checks for existing teams before inserting (UNIQUE constraint on team names)
- **Foreign key relationships** — games table references teams twice (winner_id, opponent_id)
- **12 analytical queries** — total goals, averages, champions, round filters, pattern matching
- **Self-contained scripts** — insert_data.sh + queries.sh handle the full workflow

## Technologies

| Tech | Purpose |
|------|---------|
| PostgreSQL | Relational database (2 tables: teams, games) |
| Bash | Data import and query execution scripts |
| psql | PostgreSQL CLI client |

## Database Schema

```
worldcup
+-- teams
|   +-- team_id  SERIAL PRIMARY KEY
|   +-- name     VARCHAR UNIQUE NOT NULL
+-- games
    +-- game_id         SERIAL PRIMARY KEY
    +-- year            INT NOT NULL
    +-- round           VARCHAR NOT NULL
    +-- winner_id       INT -> teams(team_id)
    +-- opponent_id     INT -> teams(team_id)
    +-- winner_goals    INT NOT NULL
    +-- opponent_goals  INT NOT NULL
```

## How to Run

```bash
# 1. Create the database
psql -U postgres -c "CREATE DATABASE worldcup;"

# 2. Restore schema and data
psql -U postgres -d worldcup -f worldcup.sql

# 3. Run analytical queries
chmod +x queries.sh
./queries.sh
```

To re-import from the CSV (for testing the import script):

```bash
chmod +x insert_data.sh
./insert_data.sh
```

To test with a clean database (as the fCC test suite does):

```bash
psql -U postgres -c "CREATE DATABASE worldcuptest;"
./insert_data.sh test
```

## Files

| File | Description |
|------|-------------|
| insert_data.sh | Parses games.csv and populates the database |
| queries.sh | Executes analytical SQL queries |
| games.csv | Source data (World Cup 2014 + 2018) |
| worldcup.sql | PostgreSQL dump (schema + data + constraints) |
| expected_output.txt | Reference output for verification |
| README.md | This file |

## Certification

This project is part of freeCodeCamp's **Relational Database Certification**.