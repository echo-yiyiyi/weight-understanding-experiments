# Jev Game Classification — With Other

## Probabilities

Probabilities range from 0 to 1. Row maxima are bold.

| Example | True Game | Breakout | Pong | Pac-Man | Freeway | other |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Breakout | 0.00 | 0.00 | 0.36 | 0.21 | **0.43** |
| 2 | Pong | 0.00 | 0.00 | 0.36 | 0.25 | **0.39** |
| 3 | Pac-Man | 0.00 | 0.00 | 0.38 | 0.13 | **0.49** |
| 4 | Freeway | 0.00 | 0.00 | 0.35 | 0.22 | **0.43** |

## Predictions and Confidence

Confidence measures distribution concentration, not accuracy or a statistical confidence interval.

| Example | True Game | Predicted Game | confidence | Model |
| --- | --- | --- | --- | --- |
| 1 | Breakout | other | 0.29 | jev-1.14.0 |
| 2 | Pong | other | 0.24 | jev-1.14.0 |
| 3 | Pac-Man | other | 0.36 | jev-1.14.0 |
| 4 | Freeway | other | 0.29 | jev-1.14.0 |

## Confusion Matrix

Rows are true labels; columns are predictions. Cells contain example counts.

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
