# Masters 2026 Fantasy Challenge — Project Brief

## Overview
A live fantasy golf dashboard for 10 friends tracking the 2026 Masters Tournament. Hosted on Vercel, auto-refreshes scores every 3 minutes via a server-side API proxy.

## Architecture
- **Frontend:** Single `public/index.html` — React via CDN (no build step), Babel for JSX
- **Backend:** `/api/scores.js` — Vercel serverless function that proxies ESPN/masters.com leaderboard JSON (avoids browser CORS issues)
- **Hosting:** Vercel free tier, deployed via GitHub integration
- **No database** — teams are hardcoded, scores fetched live

## Current State
- Basic leaderboard working with 10 teams, auto-refresh, expandable team cards
- API proxy tries masters.com JSON feed first, ESPN endpoints as fallback
- Fuzzy name matching handles accent differences (Åberg, Højgaard etc.)
- Pre-tournament withdrawals already handled in commit `418504e`:
  - Louis Browne: Bezuidenhout → Fred Couples
  - Dave Gregory: Sahith Theegala → J.J. Spaun
  - Will Emerson: Sahith Theegala → Robert MacIntyre
  - The roster table further down in this brief is the *original* draft and is intentionally NOT edited — `public/index.html` is the source of truth for current rosters
- **NOT YET DEPLOYED:** No live Vercel URL yet — deployment is the immediate next step. Vercel CLI/plugin is installed locally.
- **NOT YET IMPLEMENTED:** Transfer window, missed-cut penalty scoring, rules display

---

## Game Rules (from organiser's images)

1. **Budget:** Each player has a £10m budget to pick 4 golfers
2. **Value tiers:** Golfers cost £4m, £3m, £2m, or £1m
3. **Constraints:** Max one £4m player, max two £3m players per team
4. **Scoring:** At the end of each round, each golfer's score relative to par is summed for the team total. Lowest total wins.
5. **Cut rule:** After the cut (end of Round 2), each team gets ONE free transfer — swap a player who missed the cut for another player of the same or lower value who IS still in the tournament
6. **Missed cut penalty:** If after the free transfer a team still has player(s) who missed the cut, those players are assigned the WORST score of the round (i.e., the highest score shot by any player that round) for Rounds 3 and 4

---

## The 10 Teams

| Team | Player 1 (cost) | Player 2 (cost) | Player 3 (cost) | Player 4 (cost) |
|------|-----------------|-----------------|-----------------|-----------------|
| Adam Rowden | Xander Schauffele (4) | Matt Fitzpatrick (3) | Sungjae Im (2) | Rasmus Højgaard (1) |
| Dave Gregory | Scottie Scheffler (4) | Tommy Fleetwood (3) | Sahith Theegala (2) | Wyndham Clark (1) |
| Tom Seymour | Jon Rahm (4) | Chris Gotterup (2) | Sepp Straka (2) | Adam Scott (2) |
| Ludo Webb | Matt Fitzpatrick (3) | Tommy Fleetwood (3) | Russell Henley (2) | Corey Conners (2) |
| Louis Browne | Ludvig Åberg (4) | Matt Fitzpatrick (3) | Sungjae Im (2) | Christiaan Bezuidenhout (1) |
| Will Emerson | Bryson DeChambeau (4) | Viktor Hovland (3) | Sahith Theegala (2) | Wyndham Clark (1) |
| Darren Teague | Tommy Fleetwood (3) | Justin Rose (3) | Robert MacIntyre (2) | Tyrrell Hatton (2) |
| Dan Harris | Scottie Scheffler (4) | Cameron Young (3) | Chris Gotterup (2) | Carlos Ortiz (1) |
| Dave Hudson | Scottie Scheffler (4) | Matt Fitzpatrick (3) | Sungjae Im (2) | Dustin Johnson (1) |
| Grant Reed | Scottie Scheffler (4) | Patrick Reed (3) | Corey Conners (2) | Keegan Bradley (1) |

---

## Full Player Value List

### £4m Players
Scottie Scheffler, Rory McIlroy, Bryson DeChambeau, Jon Rahm, Xander Schauffele, Ludvig Åberg

### £3m Players
Matt Fitzpatrick, Cameron Young, Tommy Fleetwood, Collin Morikawa, Justin Rose, Patrick Reed, Hideki Matsuyama, Brooks Koepka, Jordan Spieth, Viktor Hovland, Shane Lowry, Justin Thomas, Patrick Cantlay, Sam Burns, Cameron Smith, Tony Finau

### £2m Players
Robert MacIntyre, Min Woo Lee, Christopher Gotterup, Russell Henley, Sepp Straka, Joaquin Niemann, Akshay Bhatia, Si Woo Kim, Corey Conners, Gary Woodland, Jason Day, Tyrrell Hatton, Adam Scott, Jake Knapp, Jacob Bridgeman, Sungjae Im, Rickie Fowler, Marco Penge, Sahith Theegala, Nicolai Hojgaard, Harris English, Will Zalatoris, Daniel Berger, J.J. Spaun, Maverick McNealy, Thomas Detry, Max Homa, Casey Jarvis

### £1m Players
Stephan Jaeger, Aaron Rai, Joohyung Kim, Ben Griffin, Ryan Fox, Anthony Kim, Dustin Johnson, Rasmus Hojgaard, Brian Harman, Wyndham Clark, Sergio Garcia, Billy Horschel, Keegan Bradley, Ryan Gerard, Alex Noren, Tom Hoge, Nico Echavarria, Max Greyserman, Byeong-Hun An, Davis Thompson, Kurt Kitayama, Matt McCarty, Taylor Pendrith, Rasmus Neergaard-Petersen, Lucas Glover, Aldrich Potgieter, Jayden Schaper, Tom McKibbin, Webb Simpson, Adam Hadwin, Nick Dunlap, Tiger Woods, Christiaan Bezuidenhout, Pierceson Coody, Phil Mickelson, Hao Tong Li, Sam Stevens, Harry Hall, John Keefer, Nick Taylor, Carlos Ortiz, Andrew Novak, Denny McCarthy, Bubba Watson, Michael Kim, Charl Schwartzel, Michael Brennan, Kristoffer Reitan, Sami Valimaki, Zach Johnson, Danny Willett, Davis Riley, Brian Campbell, Pongsapak Laopakdee, Naoyuki Kataoka, Brandon Holtz, Jackson Herrington, Ethan Fang, Mason Howell, Fifa Laopakdee, Fred Couples, Mateo Pulcini, Vijay Singh, Angel Cabrera, Mike Weir, Jose Maria Olazabal

---

## Players NOT in the 2026 Masters Field (cannot be transfer targets)
Tiger Woods, Phil Mickelson, Tony Finau, Joaquin Niemann, Rickie Fowler, Will Zalatoris, Harris English, Marco Penge, Thomas Detry, Lucas Glover, Webb Simpson, Nick Dunlap, Adam Hadwin, Jayden Schaper, Billy Horschel, Anthony Kim, Taylor Pendrith, Ben Griffin, Joohyung Kim, Stephan Jaeger, Tom Hoge, Byeong-Hun An, Davis Thompson, Denny McCarthy, Pierceson Coody

Note: Christiaan Bezuidenhout was originally listed as £1m but withdrew from the tournament. Louis Browne has him on his team — this will need to be handled (either as a missed-cut equivalent or flagged for transfer).

---

## Features Still To Build

### 1. Transfer Window UI
- Opens after Round 2 cut
- Each team can make ONE transfer
- Can only swap a player who missed the cut
- Replacement must be same or lower value tier
- Replacement must be in the actual field AND have made the cut
- Store transfers (probably in a simple JSON file or Vercel KV)

### 2. Missed Cut Penalty Scoring
- After the cut, identify which players missed it
- If a team used their free transfer, remove the cut player and add the new one
- Any remaining cut players on a team: assign worst score of the round for R3 and R4
- "Worst score of the round" = highest individual round score shot by any player still playing

### 3. Rules Page / Section
- Display the game rules on the dashboard
- Show the player value tiers

### 4. Visual Polish
- The organiser's original cards had a green/yellow/dark colour scheme with player photos
- Consider matching that aesthetic more closely

---

## Data Source Details

### API Proxy (`/api/scores.js`)
The serverless function tries these sources in order:
1. `https://www.masters.com/en_US/scores/feeds/2026/scores.json` — masters.com CDN feed
2. `https://site.web.api.espn.com/apis/site/v2/sports/golf/pga/leaderboard` — ESPN leaderboard API
3. `https://site.api.espn.com/apis/site/v2/sports/golf/pga/scoreboard` — ESPN scoreboard API

These are called SERVER-SIDE from Vercel's edge, so no CORS issues. The response is normalised into:
```json
{
  "source": "masters.com",
  "updated": "2026-04-09T18:30:00Z",
  "playerCount": 91,
  "players": [
    { "name": "Scottie Scheffler", "total": -3, "thru": "F", "r1": -3, "r2": null, "r3": null, "r4": null, "pos": "T1", "status": null }
  ]
}
```

### Important Notes
- Masters.com scores.json format: scores are raw strokes (e.g., 69), need to subtract par (72) to get relative-to-par
- ESPN format: scores may already be relative to par
- Player names may differ slightly between sources — fuzzy matching by last name handles this
- The `thru` field: "F" = finished round, "MC" = missed cut, number = holes completed

---

## Tournament Schedule (all times ET / BST)
- **Round 1:** Thursday April 9 (first tee 7:40am ET)
- **Round 2:** Friday April 10
- **Cut:** After Round 2 (top 50 and ties)
- **Round 3:** Saturday April 11
- **Round 4:** Sunday April 12

---

## Quick Start for Claude Code

```bash
# Clone your repo
git clone <your-repo-url>
cd masters-fantasy

# Copy the project files from the zip into the repo
# The structure should be:
# ├── api/
# │   └── scores.js
# ├── public/
# │   └── index.html
# ├── vercel.json
# ├── package.json
# └── README.md

# Deploy
npx vercel

# Or link to GitHub and auto-deploy
npx vercel link
git add -A && git commit -m "initial deploy" && git push
```
