# Jev Game Classification — Without Other

## Probabilities

Probabilities range from 0 to 1. Row maxima are bold.

| Example | True Game | Breakout | Pong | Pac-Man | Freeway |
| --- | --- | --- | --- | --- | --- |
| 1 | Breakout | 0.00 | 0.01 | **0.71** | 0.28 |
| 2 | Pong | 0.00 | 0.00 | **0.72** | 0.28 |
| 3 | Pac-Man | 0.00 | 0.00 | **0.79** | 0.21 |
| 4 | Freeway | 0.00 | 0.00 | **0.78** | 0.22 |

## Predictions and Confidence

Confidence measures distribution concentration, not accuracy or a statistical confidence interval.

| Example | True Game | Predicted Game | confidence | Model |
| --- | --- | --- | --- | --- |
| 1 | Breakout | Pac-Man | 0.61 | jev-1.14.0 |
| 2 | Pong | Pac-Man | 0.63 | jev-1.14.0 |
| 3 | Pac-Man | Pac-Man | 0.72 | jev-1.14.0 |
| 4 | Freeway | Pac-Man | 0.71 | jev-1.14.0 |

## Confusion Matrix

Rows are true labels; columns are predictions. Cells contain example counts.

| True / Predicted | Breakout | Pong | Pac-Man | Freeway |
| --- | --- | --- | --- | --- |
| Breakout | 0 | 0 | 1 | 0 |
| Pong | 0 | 0 | 1 | 0 |
| Pac-Man | 0 | 0 | 1 | 0 |
| Freeway | 0 | 0 | 1 | 0 |
| other | 0 | 0 | 0 | 0 |

## Examples by Classification Pair

| True Game | Predicted Game | Example IDs |
| --- | --- | --- |
| Breakout | Breakout | — |
| Breakout | Pong | — |
| Breakout | Pac-Man | 1 |
| Breakout | Freeway | — |
| Pong | Breakout | — |
| Pong | Pong | — |
| Pong | Pac-Man | 2 |
| Pong | Freeway | — |
| Pac-Man | Breakout | — |
| Pac-Man | Pong | — |
| Pac-Man | Pac-Man | 3 |
| Pac-Man | Freeway | — |
| Freeway | Breakout | — |
| Freeway | Pong | — |
| Freeway | Pac-Man | 4 |
| Freeway | Freeway | — |
| other | Breakout | — |
| other | Pong | — |
| other | Pac-Man | — |
| other | Freeway | — |

## Input Files

| Example | File |
| --- | --- |
| 1 | lm_understand-logs/exp1_which_game/runs/breakout/prompt.txt |
| 2 | lm_understand-logs/exp1_which_game/runs/pong/prompt.txt |
| 3 | lm_understand-logs/exp1_which_game/runs/pacman/prompt.txt |
| 4 | lm_understand-logs/exp1_which_game/runs/freeway/prompt.txt |
