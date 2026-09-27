# Milestone 2

**Milestone 2) Personal Formula**

## Goal

Validate the interaction of creating a personal formula.

- Show the current weight for every supported accomplishment
- Allow weights to be increased, decreased, or set to zero
- Recalculate and reorder the ranking after changes are applied
- Keep the curated local dataset and client-only architecture

Success

- A user can change the formula
- See a predictable change in the rankings
- Understand why the result changed

## UX

Key Interactions & Features:

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


## Desktop

- On desktop/tablet, the user sees the current weights first
- Then rankings are displayed in a table below the weights
- The player detail view sits to the right of the table

<img src="../_img/milestone-2-desktop.png" alt="milestone-2-desktop" width="800">

## Tablet

- The player detail view stacks below the rankings
- When a player is tapped
    - Scroll smoothly to the detail card
    - Or open the details as an expandable row/card directly underneath
    - Otherwise the interaction might be hidden below the fold
    - Preference for the expandable interaction

<img src="../_img/milestone-2-tablet.png" alt="milestone-2-tablet" width="400">

## Mobile

<img src="../_img/milestone-2-phone.png" alt="milestone-2-phone" width="300">

