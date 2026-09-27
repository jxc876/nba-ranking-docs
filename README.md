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

See [Scope](Scope.md) for details on the scope of the project.

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

# Milestones

See [Milestones](./Milestones.md) for details on delivery.

# Screens

See [Screens](./Screens.md) for UI / UX details.

# Appendix

See [Appendix](./Appendix.md) for additional details.
