# Fantasy Premier League Linear Optimisation Tool

### How the tool functions
*   The FPL Team Optimiser is a linear optimisation tool that aims to maximise the points returned by 11 starting players subject to budget and positional constraints. The objective function is the combination of each FPL player's mean points scored over the past gameweeks.
*   The budget is set at £83m which forms the cost constraints (total FPL budget is £100m, which leaves £17m to select bench players). An FPL team formation must consist of 1 goalkeeper, at least 3 defenders and at least forward; which sets the positional constraint.
*   Player performance is judged on mean points scored during the last 5 gameweeks. A standard deviation is calculated, however it is only used for visualisation purposes.
*   For a player to be eligible to be selected in the team, they must play in at least 3 of the last 5 gameweeks.
*   Each player's gameweek also needs to pass a threshold where a player must play a certain amount. This is because it is important that the team is made up of regular starters that maximise the opportunity to return points.
*   As such the player must be at least 60 minutes or score at least 4 points for their gameweek performance to be eligible.
*   Sixty minutes is the lower threshold of what starters tend to play and is also the minimum time required for defending players to get clean sheet points.
*   At times high-level players come off the bench (starters getting rested or 'super-subs'). Their performance needs to be factored in otherwise there is the risk of missing these players. To cover this case, a gameweek performance will be eligible if they score at least 4 points (they have returned).

### Limitations and future development

#### Metrics used
*   The tool is based on maximising the mean points based on recent performance, which is not necessarily an indicator of future performance. FPL points is highly variable and a better assessor of performance is xFPL. This is how many points the player would have expected to score based on their performance. In theory, this should remove the effect of 'lucky' and 'unlucky' performance. However, a limitation is that elite players would be expected to exceed their expected performance as xFPL is based on the performance of average players carrying actions.

#### Team constraints
*   FPL has a rule that only up to 3 players can be selected from each team. This rule has yet to be implemented, although the tool has not yet output an optimised team that has violated this rule.
*   The rule would be fairly straightforward to implement, by creating 20 additional constraints (one for each team) similarly to how the positional constraints are done.

#### Optimised team's upcoming fixture difficulties
*   The difficulties used are from data from the FPL which: a) Are a static rating  that is not necessarily accurate over the course of a season. b) Do not necessarily reflective of a 'good' FPL fixture e.g. there may be very good teams (high fixture difficulty) that still concede large amounts of goals (good FPL fixtures).  
*   Implementing stats like xG (expected goals) and xGA (expected goals against) would be a better way to target future fixtures.
*   Attacking players should target fixtures against teams with high xGA i.e. they concede a lot of goals, leading to more goals and assists.
*   Defending players should target fixtures against teams with low xG i.e. they do not score a lot of goals, leading to more cleansheets. 

#### Captaincy
*   Each gameweek an FPL captain can be assigned, and the captain's score is multiplied by 2.
*   FPL has 'premium' players which are the most expensive players (>£10m), that generally perform highly over the the season, but tend to not have the highest value-for-money. However, their upside is that they are consistently good captaincy choices, and so when they are selected their value-for-money is effectively doubled.
*   The current version of the tool does not account for captaincy during the optimisation process. If there are N players in the league, it could be factored in by running the optimisation N times. Each iteration of the optimisation would involve doubling a single player's points contribution in the objective function (i.e. they are captained). The iteration with the highest total score would then be selected as the optimal team.
