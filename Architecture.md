# Architecture

## Data Model

We can use a relation database — ex: Postgres

- https://www.postgresql.org

Players and accomplishment types should be modeled separately

- We should avoid using a column per achievement
- Adding a new accomplishment should not require a schema change

```
players
-------
id
name
championships ❌
mvps ❌
finals_mvps ❌
all_nba_first ❌
...
```

## Tables

`players` — contains player information (id, name, etc)

```
players
-------
id
name
external_id
```


`accomplishment_types` — contains the different accomplishments (ex: MVP)

```
accomplishment_types
-------
id 
code
name
description
```


`player_accomplishments` — is a joining table

```
player_accomplishments
-------
id 
player_id 
accomplishment_type_id 
season 
team
```


A persisted ranking is conceptually a snapshot containing:

- The important part is that a shared ranking retains the formula and dataset version used

```
ranking
-------
id
title
description
weights
dataset_version
created_at
```

## Sample Data

Initial accomplishment data:

| Code                | Name                         |
| ------------------- | ---------------------------- |
| `championship`      | NBA Championship             |
| `mvp`               | Most Valuable Player         |
| `finals_mvp`        | Finals MVP                   |
| `dpoy`              | Defensive Player of the Year |
| `all_nba_first`     | All-NBA First Team           |
| `all_nba_second`    | All-NBA Second Team          |
| `all_nba_third`     | All-NBA Third Team           |
| `all_defensive_first`  | All-Defensive First Team  |
| `all_defensive_second` | All-Defensive Second Team |
| `finals_appearance` | NBA Finals Appearance        |
| `roy`               | Rookie of the Year           |
|                     |                              |

Example for Jordan:

| player_id | accomplishment_type_id | season |
| --------- | ---------------------- | ------ |
| 23        | 2 (mvp)                | 1991   |
| 23        | 1 (championship)       | 1991   |
| 23        | 3 (finals_mvp)         | 1991   |
| 23        | 2 (mvp)                | 1992   |

## Data Ingestion

One of the biggest questions is where should we source our data from.

There are few high quality sources, see notes below

- Basketball Reference & NBA API (with several wrappers)

We can query an external API in realtime, however a better option is to ingest the data

- The data rarely changes, we can store it in our own relational database (Postgres)
- We don't want to be rate limited
- Or break if the external API changes

```
Data Source -> ingestion script -> Database -> API -> UI
```

The ingestion process should:
1. Fetch or parse records from the selected source
2. Map external players and awards to canonical application records
3. Validate duplicates, missing seasons, and unexpected values
4. Produce a versioned dataset that can be reviewed before publication
5. Record source and import metadata so incorrect records can be traced and corrected

Automated ingestion is useful, but a small curated dataset is acceptable for the first prototype.

## NBA API

The official NBA API available at `stats.nba.com`

- The HTML pages seem to load fine, I get timeouts when using  `requests` or `fetch`
- It's possible NBA.com allows calls from their own frontend, but blocks others...
- https://www.nba.com/stats/players/traditional
- https://www.nba.com/stats/player/203999/career — HTML page for Jokic
- https://stats.nba.com/stats/playerawards?PlayerID=203999 — Call for Jokic, times out

<img src="_img/nba-awards-screenshot.png" alt="nba-awards-screenshot" width="900">

`nba_api` — A Python client for accessing NBA.com

- https://github.com/swar/nba_api

`nba-api` — A Python client for accessing NBA.com

- https://nba-apidocumentation.knowledgeowl.com
- https://nba-apidocumentation.knowledgeowl.com/help/playerawards

## Basketball Reference

The following URLs from Basketball Reference contain data that can be parsed if necessary.

Some Basketball Reference awards pages combine NBA and ABA records. The app should ingest NBA records only; ABA accomplishments are outside the initial scope.

(1) Championships (Count by Player)

* https://www.basketball-reference.com/leaders/most_championships.html

(2) MVP Award (by year)

* https://www.basketball-reference.com/awards/mvp.html

(3) Defensive Player (by year)

* https://www.basketball-reference.com/awards/dpoy.html

(4) All-NBA selections by player (1st, 2nd, 3rd team)

* https://www.basketball-reference.com/awards/all_league_by_player.html

(5) All-NBA selection by year

* https://www.basketball-reference.com/awards/all_league.html

(6) Rookie of the Year, All Rookie Teams

* https://www.basketball-reference.com/awards/roy.html
* https://www.basketball-reference.com/awards/all_rookie.html

(7) All-Defensive selections by player

* https://www.basketball-reference.com/awards/all_defense_by_player.html

(8) All-Defensive teams by season

* https://www.basketball-reference.com/awards/all_defense.html

Finals Appearances (By Team)

* https://www.basketball-reference.com/playoffs
* https://www.basketball-reference.com/playoffs/series.html
* https://www.basketball-reference.com/playoffs/2026-nba-finals-knicks-vs-spurs.html
* Note: Player final appearance might need to be derived

Awards Index

* https://www.basketball-reference.com/awards

NBA 75th Anniversary Team

* https://www.basketball-reference.com/awards/nba_75th_anniversary.html


## Web Stack

**Milestone 1**

- Can be a simple React application with no backend
- Data can come from a simple `.json` and be limited to ~30 players
- The objective is to validate if the default ranking is fun or has any glaring problems

```
nba-rankings/
	src/ 
		components/ 
	data/ 
		players.json 
	lib/ 
		scoring.ts 
		App.tsx 
	public/
	
	package.json
```

**Milestone 2**

- We need to ingest external data into our own database
- The ingestion script can be a Node or Python script
- The web app can use React + Node + Postgres (Drizzle ORM)
- We can structure the project as a monorepo

```
nba-rankings/
  apps/
    web/       — React (Vite)
    api/       — Express 
  packages/
    shared/   - shared TS types/schemas

  ingestion/  — Node or Python
    scripts/

  package.json
  pnpm-workspace.yaml
```

Images — Let's keep it simple and include images inside the web app

- We won't have enough images to need external storage (ex: S3 object storage)
- We can start with a generic image for all players, ex: `default-player.png`
- Then add more images, ex: `LebronJames.png`, `NikolaJokic`
- Or we can name the images after IDs, ex: `203999.png`
- ex: https://cdn.nba.com/headshots/nba/latest/1040x760/203999.png — Jokic
- In either case we should host them and not rely on external resources

Deferred Decisions — we can decide this later

- Plain CSS vs Tailwind
- UI/UX System, ex: Material
- Component Library: Shadcn, Radix, etc
