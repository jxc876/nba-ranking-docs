For code see: [nba-ranking-app](https://github.com/jxc876/nba-ranking-app/tree/main)

# Overview

- Status: Draft
- Date: September 2026
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

However, it requires that you agree with what the formula prioritizes.

This app makes the formula interactive, It helps a user answer:

"Given the accomplishments that I value most, how would NBA players rank?"* 

## Project Goals

- A new user can understand the basic premise of the app
- A user can create a ranking that reflects their preferences
- A viewer can explain why one player ranks above another
- Two people using the same dataset and weights receive the same result
- The initial scope is small enough to be a fun learning project

## Details

- See [Scope](Scope.md) for details on the scope of the project.
- See [Architecture](Architecture.md) for details on the data model and ingestion process.
- See [Milestones](./Milestones.md) for details on delivery.
- See [Screens](./Screens.md) for UI / UX details.
- See [Appendix](./Appendix.md) for additional details.
