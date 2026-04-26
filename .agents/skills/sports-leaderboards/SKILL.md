---
name: sports-leaderboards
description: Fetch top leaderboard positions (default top 10) for a specific competition and season, such as IPL Orange Cap, IPL Purple Cap, or UEFA Champions League goalscorers.
---

Use this skill when the user asks for leaderboard-style stats like:
- Top 10 orange cap holders ipl 2026
- Top 10 purple cap holders ipl 2026
- Top 10 goalscorers UCL 2026
- Top N wickets/scorers/assists standings for a named tournament and season

## Workflow

1. Parse the request into:
- `count` (default `10` if omitted)
- `metric` (orange cap, purple cap, goalscorers, assists, wickets, etc.)
- `competition` (IPL, UCL, etc.)
- `season` (year or season label)

2. Fetch data from web sources, prioritizing official/primary sources first:
- IPL: `iplt20.com` (official IPL site)
- UCL: `uefa.com` (official UEFA site)
- If official pages are unavailable or incomplete, use reputable secondary sources such as ESPN/Cricinfo, Cricbuzz, BBC Sport, Sky Sports, or FBref.

3. Validate that the page matches the requested season and competition.
- If multiple seasons are present, use the exact requested season.
- If the season is not available yet, say that clearly and provide the nearest available season as a fallback.

4. Return only the requested top `N` rows, ordered by rank, in a compact table:
- Rank
- Player
- Team/Club
- Stat value
- Source

5. Include source links for transparency and mention the retrieval date.

## Notes

- If the request is ambiguous (for example, "top scorers 2026" without a competition), ask one concise clarification question.
- Prefer current-season stats when the user asks for "latest".
