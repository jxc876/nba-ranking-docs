# Milestones

Project Milestones.

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
