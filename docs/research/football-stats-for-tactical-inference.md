# Football stats that explain the game

Which stats can tell you what is happening tactically, using event data alone (who did what, where, when, with what outcome), and how Swing turns them into meaning.

## The core idea

Event data is enough to read almost every team-level idea commentators talk about: control, territory, tempo, pressing, danger and momentum. Tracking data adds shape and physical output, but most of the rest can be read from *where* events happen. And the interesting signal is rarely the raw number; it is **the number against that side's own normal, given the score**. "62% possession" is wallpaper. "62%, fifteen points above their level so far, while losing" is a story.

## The stats that carry most of the load

| What it reads | Stat | How it's computed from events |
| --- | --- | --- |
| Who has the ball | **Possession share** | a side's passes ÷ both sides' passes |
| Who has the territory | **Field tilt** | a side's final-third passes ÷ both sides' |
| Safe circulation vs risky progression | **Pass accuracy by third** | completed ÷ attempted, per third |
| Patient vs direct | **Long-ball share, progressive passes** | passes over 30 m; passes moving the ball 10 m+ towards goal |
| Pressing intensity | **PPDA** | opponent passes in their own 60% ÷ our defensive actions there (lower = harder press) |
| Where the block sits | **Defending height** | average position of tackles, interceptions and fouls |
| Is the press working | **High turnovers** | possessions won within 40 m of the opponent's goal |
| Danger, not just volume | **xG, box entries** | chance quality of each shot; passes and carries into the box |
| Who wins the battles | **Duels won** | share of contested duels won |
| Control vs chaos | **Turnovers per minute** | possession changes per minute, both sides |

These combine into readable patterns. Lots of passes at high accuracy, almost all in a side's own half, with no box entries, reads as **controlling but not attacking**. If the opponent's PPDA is also high, the rest of the story is **and the opponent is happy to let them**: a team sitting in a mid or low block.

## What we can't see without tracking

| Idea | Event-only stand-in | Confidence |
| --- | --- | --- |
| Defensive line height | average position of defensive actions | medium |
| Pressing intensity | PPDA, high turnovers | medium to high |
| Compactness and shape | completion into the space between the lines | low |
| Formation | declared line-up only | low |
| Distance and sprints | not in event data, so Swing models them and labels them as modelled | none |

Swing sticks to what event data reads well, and says so where it is modelling.

## Turning numbers into meaning

- **Compare with the side's own match so far,** not a fixed threshold, and measure the change in units of that stat's normal spread. A swing is only interesting if it is unusual for this match.
- **Read the score.** Leading sides give up the ball and drop deeper on purpose; a side 1-0 up with 35% of the ball can be in control.
- **Need enough data.** A ratio from three passes isn't a stat. Swing waits until 15' before explaining anything, and ignores windows with too few events.
- **Explain change, not state.** The card goes up when something *moves* (a shift, a recovery, or the effect of a goal, red card or substitution), never as a stream of standing numbers.

## Sources

- Stats Perform: [how pressure is measured](https://www.statsperform.com/insights/how-we-measure-pressure/)
- Wyscout glossary: [PPDA](https://dataglossary.wyscout.com/ppda/)
- Sportmonks glossary: [field tilt and key data points](https://www.sportmonks.com/glossary/key-data-points)
- Bundesliga Match Facts: [match momentum](https://www.bundesliga.com/en/bundesliga/news/bundesliga-match-facts-aws-match-momentum-34052)
- FIFA: [Enhanced Football Intelligence, phases of play](https://www.fifatrainingcentre.com/media/native/world-cup-2022/Enhanced%20Football%20Intelligence%20EN.pdf)
- Fernandez-Navarro et al. (2016), [Attacking and defensive styles of play in soccer](https://researchonline.ljmu.ac.uk/id/eprint/3791/), *J Sports Sci* 34(24)
- Pappalardo et al. (2019), [A public data set of spatio-temporal match events in soccer competitions](https://doi.org/10.6084/m9.figshare.c.4415000), *Scientific Data* 6:236
