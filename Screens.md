# Screens

The main page contains:

- Navigation and a brief explanation of the ranking
- The scoring formula
- The ranked player list
- A selected player's score breakdown
- A footer with methodology and source links

We likely need the following UI components

- Navigation
- Header
- ScoringFormula
- PlayerRankings
- PlayerCard
- Footer

## Milestone 1 Screens

Description

- The left side is the ranked player table
- Clicking a player row selects that player
- The selected row gets a highlight so it’s clear which player is active
- The right-hand panel updates to show that player's score breakdown
- "Show all 30 players" expands the table
- The navigation links just show static pages
- The formula cards are display-only for now
- The ranking itself is static, no filtering, sorting, or weight adjustment
- Default to the first row when the page loads

Desktop

<img src="../_img/milestone-1-desktop.png" alt="milestone-1-desktop" width="600">

Tablet

<img src="../_img/milestone-1-tablet.png" alt="milestone-1-tablet" width="400">

Mobile

<img src="../_img/milestone-1-phone.png" alt="milestone-1-phone" width="300">


## Milestone 2 Screens


Description

- The user sees the current weights and then current ranking below
- Accomplishments have a minus + plus button and display the current value
- The user can Apply Weights after making edits

Applying Weights

- Tap `+` / `-` to change the value
- Optionally support direct numeric input too, ex: `5`
- Clicking "Apply Weights" recalculates scores & re-sorts the ranking
- Update the selected player card to the first row after re-sorting
- When the weights are in pristine state, disable the Apply Weights button
- When the weights have been edited, enable the Apply Weights button

Desktop

- On desktop/tablet, the user sees the current weights first
- Then rankings are displayed in a table below the weights
- The player detail view sits to the right of the table

<img src="../_img/milestone-2-desktop.png" alt="milestone-2-desktop" width="800">

Tablet

- The player detail view stacks below the rankings
- When a player is tapped
    - Scroll smoothly to the detail card
    - Or open the details as an expandable row/card directly underneath
    - Otherwise the interaction might be hidden below the fold
    - Preference for the expandable interaction

<img src="../_img/milestone-2-tablet.png" alt="milestone-2-tablet" width="400">

Mobile

<img src="../_img/milestone-2-phone.png" alt="milestone-2-phone" width="300">


## Milestone 3 Screens

Milestone 3 adds:

- A title and description
- save/share action
- stable ranking URL
- The ability to copy or fork


Desktop

<img src="../_img/milestone-3-desktop.png" alt="milestone-3-desktop" width="800">

Tablet

<img src="../_img/milestone-3-tablet.png" alt="milestone-3-tablet" width="500">

Mobile

<img src="../_img/milestone-3-phone.png" alt="milestone-3-phone" width="300">
