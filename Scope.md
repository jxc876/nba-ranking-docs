# Scope

There are two main scenarios that users of the app can take.

## View a Ranking

Someone has shared a link with me, I can:

- See the ranking's title, description, and ordered player list
- See the formula and weights used to produce it
- Inspect a player's score breakdown
- See which dataset version the ranking used
- Start a new ranking by copying the shared formula
- No account is required to view a public ranking

## Create a Ranking

I can create a new ranking

- I can start with the default formula or copy an existing ranking
- Change the weight assigned to each supported accomplishment
- Apply the changes and see the ranking recalculate immediately
- Add a title and optional description
- Save the ranking and receive a shareable link


## Player Pool

Let's focus on the modern NBA era, beginning with the 1979–80 season.

This roughly aligns with the introduction of the three-point line and the Magic Johnson/Larry Bird era.

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
