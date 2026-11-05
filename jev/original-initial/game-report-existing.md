# Jev Game Classification (Saved Results)

## Probabilities

Probabilities range from 0 to 1 and sum to approximately 1 per row. The highest probability in each row is bold.

| Example | True Game | Breakout | Pong | Pac-Man | Freeway | other |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Breakout | 0.00 | 0.00 | 0.09 | 0.03 | **0.88** |
| 2 | Pong | 0.00 | 0.00 | 0.09 | 0.04 | **0.87** |
| 3 | Pac-Man | 0.00 | 0.00 | 0.11 | 0.04 | **0.85** |
| 4 | Freeway | 0.00 | 0.00 | 0.10 | 0.07 | **0.83** |

## Predictions and Confidence

Confidence measures the concentration of the returned probability distribution; it is not accuracy or a statistical confidence interval.

| Example | True Game | Predicted Game | Confidence | Model |
| --- | --- | --- | --- | --- |
| 1 | Breakout | other | 0.85 | jev-1.14.0 |
| 2 | Pong | other | 0.84 | jev-1.14.0 |
| 3 | Pac-Man | other | 0.81 | jev-1.14.0 |
| 4 | Freeway | other | 0.79 | jev-1.14.0 |

## Confusion Matrix

Rows show true games; columns show predicted games. Cells contain example counts.

| True / Predicted | Breakout | Pong | Pac-Man | Freeway | other |
| --- | --- | --- | --- | --- | --- |
| Breakout | 0 | 0 | 0 | 0 | 1 |
| Pong | 0 | 0 | 0 | 0 | 1 |
| Pac-Man | 0 | 0 | 0 | 0 | 1 |
| Freeway | 0 | 0 | 0 | 0 | 1 |
| other | 0 | 0 | 0 | 0 | 0 |

## Examples by Classification Pair

| True Game | Predicted Game | Example IDs |
| --- | --- | --- |
| Breakout | Breakout | — |
| Breakout | Pong | — |
| Breakout | Pac-Man | — |
| Breakout | Freeway | — |
| Breakout | other | 1 |
| Pong | Breakout | — |
| Pong | Pong | — |
| Pong | Pac-Man | — |
| Pong | Freeway | — |
| Pong | other | 2 |
| Pac-Man | Breakout | — |
| Pac-Man | Pong | — |
| Pac-Man | Pac-Man | — |
| Pac-Man | Freeway | — |
| Pac-Man | other | 3 |
| Freeway | Breakout | — |
| Freeway | Pong | — |
| Freeway | Pac-Man | — |
| Freeway | Freeway | — |
| Freeway | other | 4 |
| other | Breakout | — |
| other | Pong | — |
| other | Pac-Man | — |
| other | Freeway | — |
| other | other | — |

## Input Files

| Example | File |
| --- | --- |
| 1 | lm_understand-logs/exp1_which_game/runs/breakout/prompt.txt |
| 2 | lm_understand-logs/exp1_which_game/runs/pong/prompt.txt |
| 3 | lm_understand-logs/exp1_which_game/runs/pacman/prompt.txt |
| 4 | lm_understand-logs/exp1_which_game/runs/freeway/prompt.txt |
