# Milestone 1

## Goals

**Milestone 1) Fixed Ranking**

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

## UX

Key Interactions & Features:

- The left side is the ranked player table
- Clicking a player row selects that player
- The selected row gets a highlight so it’s clear which player is active
- The right-hand panel updates to show that player's score breakdown
- "Show all 30 players" expands the table
- The navigation links just show static pages
- The formula cards are display-only for now
- The ranking itself is static, no filtering, sorting, or weight adjustment
- Default to the first row when the page loads

## Desktop

<img src="../_img/milestone-1-desktop.png" alt="milestone-1-desktop" width="600">

## Tablet

<img src="../_img/milestone-1-tablet.png" alt="milestone-1-tablet" width="400">

## Mobile

<img src="../_img/milestone-1-phone.png" alt="milestone-1-phone" width="300">
