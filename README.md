# World Cup Database Project

## Overview
This project is a PostgreSQL database system that stores and queries data from the final three rounds of the FIFA World Cup tournaments since 2014. The project involves creating the database, inserting data from a CSV file, and querying the database to extract meaningful statistics.

## Features
- A `worldcup` database that stores teams and games information.
- `teams` table with unique team names.
- `games` table containing match details such as year, round, winner, opponent, and goals scored.
- An `insert_data.sh` script to populate the database efficiently.
- A `queries.sh` script to extract useful statistics about the World Cup matches.

## Database Schema
### `teams` Table
| Column   | Type    | Constraints    |
|----------|--------|---------------|
| team_id  | SERIAL | PRIMARY KEY    |
| name     | TEXT   | UNIQUE, NOT NULL |

### `games` Table
| Column         | Type    | Constraints                        |
|---------------|--------|----------------------------------|
| game_id       | SERIAL | PRIMARY KEY                      |
| year          | INT    | NOT NULL                         |
| round         | TEXT   | NOT NULL                         |
| winner_id     | INT    | NOT NULL REFERENCES teams(team_id) |
| opponent_id   | INT    | NOT NULL REFERENCES teams(team_id) |
| winner_goals  | INT    | NOT NULL                         |
| opponent_goals| INT    | NOT NULL                         |

## Setup Instructions
1. **Create the Database:**
   ```sh
   psql --username=freecodecamp --dbname=postgres -c "CREATE DATABASE worldcup;"
   ```
2. **Connect to the Database:**
   ```sh
   psql --username=freecodecamp --dbname=worldcup
   ```
3. **Run the `insert_data.sh` Script:**
   ```sh
   ./insert_data.sh
   ```
4. **Run Queries to Get Statistics:**
   ```sh
   ./queries.sh
   ```

## Queries Implemented
- Total number of goals scored by winning teams.
- Number of games where the winning team scored more than two goals.
- List of unique winning team names.
- Year and team name of all World Cup champions.
- List of teams that played in the 2014 Eighth-Final round.

## Backup and Restore
To save your database:
```sh
pg_dump -cC --inserts -U freecodecamp worldcup > worldcup.sql
```
To restore:
```sh
psql -U postgres < worldcup.sql
```

## Author
This project was completed as part of freeCodeCamp's Relational Database Certification.

## License
This project is open-source and available for personal and educational use.

