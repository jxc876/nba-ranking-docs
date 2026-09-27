For code see: [nba-ranking-app](https://github.com/jxc876/nba-ranking-app/tree/main)

# Overview

## Metadata

- Status: Draft
- Created: September 2026
- Purpose: High-level vision and architecture design

## Objective

Let's build a web application that lets basketball fans create and share rankings of the greatest NBA players.

Users can decide how much certain accomplishments matter, then generate their own rankings. 

<img src="_img/milestone-2-desktop.png" alt="milestone-2-desktop" width="800">

## Background

Debating the greatest NBA players is part of basketball culture. 

Ask a fan for their top ten list and familiar questions quickly appear:

- Who is number one: Michael Jordan or LeBron James?
- Who ranks higher: Magic Johnson or Larry Bird?
- How much do championships matter compared with individual awards?

Most published rankings ultimately reflect the author's hidden preferences. 

Some systems, such as John Hollinger's "GOAT Points", try to answer the question using a formula. 

However, it still requires that you agree with what the formula deems to be important.

This app makes the formula interactive. It helps a user answer:

*Given the accomplishments that I value, how would NBA players rank?* 

## Goals

- A new user can understand the premise without additional explanation
- A user can create a ranking that reflects their stated preferences
- A viewer can explain why one player ranks above another
- Two people using the same dataset and weights receive the same result
- The initial scope is small enough to implement as a learning project
- The results are intended to be a fun conversation starter

# Scope

## Player Pool

The app focuses on the modern NBA era, beginning with the 1979–80 season. 

This boundary roughly aligns with the introduction of the three-point line and the start of the Magic Johnson/Larry Bird era.

This limits the scope of the app and makes getting the data easier

It also avoids some of the issues of comparing different eras

- Ex: The NBA consisted of 8 teams from 1956 to 1961, 14 in 1969, etc
- https://en.wikipedia.org/wiki/Expansion_of_the_NBA

## Accomplishments

The initial ranking formula uses the following countable accomplishments:

- NBA championship
- NBA Most Valuable Player (MVP)
- NBA Finals MVP
- NBA Defensive Player of the Year (DPOY)
- All-NBA First Team
- All-NBA Second Team
- All-NBA Third Team
- All-Defensive teams
- NBA Finals appearance
- NBA Rookie of the Year

Later iterations might include the following:

- Career Totals (Points, Rebounds, Assists, etc)
- Career Averages (PPG, RPG, APG, etc)
- All-Star selections (maybe, but mostly popularity based)
- Statistical milestones, such as triple-doubles
- Leading the league (ex: Scoring titles)

One reason for deferring averages is because they use different scales and require normalization to account for pace and era.

## Ranking Model

Each accomplishment type has a (non-negative) numeric weight chosen by the ranking's creator. A player's score is the sum of their accomplishment counts multiplied by those weights.

```text
player score = Σ (accomplishment count × accomplishment weight)
```

For example, if an MVP is worth 10 points and a championship is worth 8 points, a player with two MVPs and three championships receives 44 points from those two categories.

The UI should show both the total score and its breakdown so that viewers can understand the result. A weight of zero means an accomplishment does not affect that ranking.

Players with the same score share the same rank. They are displayed alphabetically within the tie.

Some accomplishments overlap by design. A DPOY winner will often also receive an All-Defensive selection, just as an MVP winner will often receive an All-NBA selection. The model treats these as separate accomplishments because they represent different honors, but the default weights should account for the overlap so that related achievements are not unintentionally overemphasized.

##  Questions

- What are good default weights for the different achievements?
- How do we handle awards that did not exist in previous eras?
- Do eligible player’s pre-1980 accomplishments count (ex: Kareem’s earlier awards)
- How can values with different scales be normalized 
- How do we keep the formulas fun without making it hard to understand them
- How do we handle ongoing data ingestions, and how often?
- How do we handle data corrections, are old rankings immutable?

# Scenarios

There are two main scenarios that users of the app can take.

## 1. View a Ranking

 Someone has shared a link with me, I can:

- See the ranking's title, description, and ordered player list
- See the formula and weights used to produce it
- Inspect a player's score breakdown
- See which dataset version the ranking used
- Start a new ranking by copying the shared formula
- No account is required to view a public ranking

## 2. Create a Ranking

I can create a new ranking

- I can start with the default formula or copy an existing ranking
- Change the weight assigned to each supported accomplishment
- Apply the changes and see the ranking recalculate immediately
- Add a title and optional description
- Save the ranking and receive a shareable link

# Architecture

See [Architecture](Architecture.md) for details on the data model and ingestion process.

# Project Milestones

## Milestone 1) Fixed Ranking

Goal: Validate the presentation & explainability of a weighted ranking

- Use predetermined fixed weights 
- Use a curated dataset of  ~30 notable players
- Show the ranked list on page load
- Show an individual player's score breakdown

Technical Notes

- Can be a React application or server side web app
- The data can come from a hardcoded `data.json` file
- No database, accounts, ingestion automation, or durable sharing

Success

- A reviewer can understand the formula and explain why one player ranks above another. 
- Validate the sample data and default weights have no obvious errors 

## Milestone 2) Custom Weights

Goal: Validate the interaction of creating a personal formula.

- Show the current weight for every supported accomplishment
- Allow weights to be increased, decreased, or set to zero
- Recalculate and reorder the ranking after changes are applied
- Keep the curated local dataset and client-only architecture

Success 

- A user can change the formula
- See a predictable change in the rankings
- Understand why the result changed

## Milestone 3) Save & Share

Goal: Allow Saving & Sharing Ranking

- Store players, accomplishments, dataset versions, and saved rankings
- Save configuration (weights, results) & metadata (title, description), immutable?
- View and share using URLs, ex: `site.com/ranking/<UUID>`
- Ability to fork a shared URL

Technical Notes

- Ingest and validate a broader modern-era dataset
- Player images can be packaged and hosted with the web app. 

# Screens

See [Screens](./Screens.md) for UI / UX details.

# Appendix

## Routes

Milestone 1

- `/` — home page, shows static page
- `/about` — information about the project

Milestone 3

- `/rankings/<uuid>` — saved ranking, shareable URL

Future Ideas

- `/players/<slug>` — possible future player profile

## Domain Names

Let's avoid using NBA in the name, some ideas:

- `hoopsrank.com`
- `hooprankings.com`
- `ringstomvps.com`
- `hoopsformula.com`
- `hoopscore.com`
- `mygoatformula.com`
- `rankthegreats.com`
- `buildyourgoat.com`

## Docs

How to Write an Effective Software Design Document

- https://refactoringenglish.com/excerpts/write-an-effective-design-doc

The Basketball 100 (GOAT Points), John Hollinger

- https://www.nytimes.com/athletic/5940794/2024/11/26/the-basketball-100-goat-points-book-excerpt
