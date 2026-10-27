# What real matches say about momentum

Before generating a single match, we measured how momentum behaves in real football, so the generator could reproduce it and the agents could be held to it. The source is the Wyscout open event dataset (Pappalardo et al. 2019, *Scientific Data* 6:236, CC BY 4.0): 380 matches and 643,150 events. It was used only to measure patterns; none of it is shipped and no real names are used. Scripts are in `research/`.

**Momentum shift**, as measured here: a side's share of final-third events over the last 5 minutes differs from the 10 minutes before by at least 30 points.

## Five findings

**1. Swings are real and frequent.** There are **5.6 shifts per match**. Shuffling the same events at random produces only 0.8, so about 85% of detected shifts are genuine changes in play, not noise.

**2. Most swings have no obvious trigger.** In **about 30% of swings (30.8%) there was no goal, card, substitution or half-time in the 15 minutes before.** Even when there was one, it was usually coincidence: substitutions and half-time sit in front of swings no more often than in front of random minutes. So the honest answer to "why did it swing?" is usually *how the play changed*, which is why the play-stats specialists are the core of Swing and the substitution and events specialists are allowed to say "not me".

**3. Big events rarely cause a big swing, but they do change how a team plays.**

| After... | Chance of a sustained 30-point swing |
|---|---|
| a random minute | 21% |
| conceding a goal | 24% |
| a red card | 29% |
| a substitution | 22% |
| half-time | 18% |

Yet after a red card the 10-man side defends lower in 73% of cases and passes less in 86%. The chain is **event → change of plan (common) → visible swing (sometimes)**, so the generator never writes momentum directly: events change plans, plans change play, and momentum comes out of the stats.

**4. A swing has a recognisable signature.** During a swing, compared with random windows, the side taking over gains about 18 points of pass share, defends about 15 m higher and wins about 10 points more of its duels; the side losing it plays far more of its passes in its own half and its pass accuracy drops about 8 points. These are the numbers Swing puts on its cards.

**5. Many swings are recoveries.** Before a swing, the side that goes on to take over is usually *dipping*. So Swing compares against a side's level over the whole match so far, not just the last ten minutes, and labels a bounce-back as a recovery rather than a new shift.

## Smaller effects the generator reproduces

- **Conceding a goal:** the conceding side's territory rises about 10 points over the next 10 minutes.
- **Red card:** the 10-man side's pass share falls about 19 points over the next 15 minutes (rare: about 1 match in 9).
- **Substitute:** in his first 15 minutes a substitute makes 22% more duels and 12% more on-ball actions than the player he replaced. At team level the effect is small (about +4 points when losing).
- **Half-time:** no average shift, but 31 to 44% of teams change territory by 20 points or more between halves, in either direction.
- **Fatigue:** players' on-ball activity dips from 60 to 75 minutes.

Every one of these is a check in the realism gate ([docs/realism.md](../realism.md)).
