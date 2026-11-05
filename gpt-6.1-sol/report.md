# GPT-6.1 Sol — Original Game Prompts

Reasoning effort: high. Tools: none.

## Example 1

Source: `lm_understand-logs/exp1_which_game/runs/breakout/prompt.txt`

Status: completed. Model: gpt-6.1-sol.

## Observations

Hidden-unit indices below are zero-based.

- **Channel 0 — agent:** Substantial weights are concentrated on **row 8, columns 1–8**, the bottom playable row. For example, at `(8,1)`, input 405 has weights **4.066** to hidden unit 15 and **−4.013** to unit 31. At `(8,8)`, input 440 has **3.855** to unit 5 and **−4.701** to unit 13. Agent-channel weights above this row are generally small. This strongly suggests a **bottom-mounted paddle**, rather than a character navigating the whole board.

- **Channel 1 — moving objects:** Large weights occur throughout the interior **above the paddle, rows 1–7**, with considerable position-dependent variation. At `(2,2)`, input 111 has **−6.356** to unit 7 and **4.570** to unit 8; at `(4,3)`, input 216 has **7.879** to unit 8 and **6.421** to unit 17. Conversely, this channel is small on row 8. This fits a **ball moving around the space above a paddle**.

- **Channel 2 — reward targets:** Learned structure is concentrated in the **top three playable rows**, unlike the moving-object channel, which remains strong farther down. Examples include **2.148** from `(1,5)` to unit 1, **−4.811** from `(3,1)` to unit 0, and **−4.640** from `(3,7)` to unit 0. Below this upper band, reward-channel weights are generally background-sized. That suggests an **upper field of bricks or blocks**, not collectibles scattered throughout the arena.

- **Channel 3 — obstacles:** Border inputs have a repeated, modest weight pattern: for example, weights to unit 1 are **0.255**, **0.193**, and **0.312** at border cells `(0,0)`, `(0,1)`, and `(0,2)`. Interior obstacle weights are mostly small: at `(4,1)`, weights to units 7 and 8 are only **0.017** and **0.025**, whereas the moving-object weights there are **−5.880** and **6.095**. There is little evidence of a meaningful internal maze. The constant border can also supply an effective bias, so its weights do not establish active wall avoidance.

- **Channel 4 — previous frame:** Strong structure follows the moving-object region, with additional structure along the paddle row. At `(1,3)`, current moving-object weights to units 7 and 8 are **−4.791, 3.436**; previous-frame weights at that same cell are **−4.301, 3.057**. The policy therefore uses temporal information consistent with **tracking ball motion and anticipating its arrival**.

- **Output layer:** The network chiefly distinguishes **left and right**. No-op, up, and down often have similar output weights: unit 17 has **1.534, 1.461, 1.447** for those actions. Left has especially strong specialized connections, including **4.057** from unit 11 and **−5.336** from unit 22; right has **3.031** from unit 24 and **1.380** from unit 30. The biases, **[1.221, 1.008, 1.024, 0.897, 1.298]**, are comparatively similar and do not alone impose a dominant action. This fits horizontal paddle control, with up/down effectively redundant or unhelpful.

## Reasoning

The combination is highly characteristic: **a horizontally controlled bottom paddle, a moving ball above it, an upper band of reward-bearing blocks, and substantial previous-frame processing**.

Pong explains a paddle and ball but not the distinct upper reward-target field. Ordinary catching or dodging games explain bottom-row horizontal control, but their relevant falling items would normally occupy a broader vertical range rather than leave a separate three-row target band. Maze games, Pac-Man, and Snake are poor fits because the agent would occupy many rows and require meaningful vertical control; they would also commonly produce more interior obstacle structure.

The upper targets distinguish a brick-breaking game from these alternatives.

## Game

**Breakout — a grid-based brick-breaker.**

## Description

The agent moves a paddle left and right along the bottom to keep a bouncing ball in play and send it toward the bricks above. Breaking bricks gives reward; missing the ball loses a life or ends the episode.

## Confidence

**98%**

## Example 2

Source: `lm_understand-logs/exp1_which_game/runs/pong/prompt.txt`

Status: completed. Model: gpt-6.1-sol.

## Observations:
- **Channel 0 — agent:** The substantial weights are concentrated in **column 1, rows 1–8**, rather than throughout the playable area. For example, input 55, representing `(1,1,agent)`, has weights **2.697** to hidden unit 11 and **−2.474** to unit 15. At `(2,1,agent)`, input 105 has **−3.588** to unit 1. Agent inputs farther across the board are generally small. This strongly suggests a **paddle constrained to the left side**.

- **Channel 1 — moving objects:** Large, position-dependent weights cover the area to the paddle’s right, **columns 2–8 across the playable rows**. For example, `(1,2,moving)`, input 61, includes **−3.169, 2.039, −2.772**, while `(1,5,moving)`, input 76, includes **2.305, 3.278**. This is consistent with a **ball moving through the arena**, not an agent navigating those cells.

- **Channel 2 — reward targets:** The playable interior has mostly small, unstructured weights; there is no conspicuous field of collectible targets or bricks. The **right border** instead has a repeated, modest, bias-like pattern: at `(1,9,reward)`, input 97, weights include **0.316** to unit 3 and **−0.283** to unit 8. This suggests a **fixed scoring-side marker**, though constant inputs cannot reveal the exact reward rule.

- **Channel 3 — obstacles:** The outer border has a repeated pattern, while interior obstacle inputs are mostly small. For example, obstacle inputs at `(0,0)` and `(0,1)` have **0.275** and **0.277** to unit 3, close to that unit’s bias, **0.271**. This looks like a fixed rectangular arena, not a maze or changing obstacle layout. The shared border pattern is largely a constant-input effect.

- **Channel 4 — previous frame:** Large weights occur both along the paddle strip and throughout the ball’s region. At `(1,1,previous)`, input 59 includes **−1.578**; at `(1,5,previous)`, input 79 includes **3.115, 5.236, 3.913**. The policy therefore has substantial machinery for combining current and previous positions—particularly useful for estimating **ball direction and interception point**.

- **Output layer:** **Up and down are the distinct control actions.** No-op, left and right have remarkably similar output weights. For example, W3 row 16 is  
  **`−0.056, 1.178, 1.165, −0.032, −0.068`**,  
  making no-op/left/right nearly interchangeable. Other units distinguish the vertical directions sharply: row 18 is  
  **`−1.399, −1.370, 1.587, −1.283, −1.215`**,  
  strongly separating down from the other actions. The output biases are **`0.931, 1.261, 1.065, 0.861, 0.855`**: a modest upward preference, with almost identical left/right biases.

## Reasoning:
The combination is highly characteristic: a left-edge paddle, a moving ball to its right, strong previous-frame processing, and effectively only **up/down/stay** controls.

Ordinary **Breakout** or a falling-object catching game would normally have a bottom paddle and distinct left/right controls. A rotated Breakout could match the paddle orientation, but there is no corresponding interior brick-target structure. Snake, Pac-Man and maze navigation are poor fits because the agent would occupy a two-dimensional region and need meaningful horizontal actions.

The weights identify the paddle-and-ball geometry much more securely than they identify the precise scoring mechanics or whether an opposing paddle is simulated.

## Game:
**Pong — a grid-based version with the player’s paddle on the left, possibly a single-paddle wall-Pong variant.**

## Description:
The agent moves its paddle up and down to intercept and return a bouncing ball toward the right-hand side. Successful returns or scoring at the opposite side give reward, while missing the ball loses or ends the rally.

## Confidence:
96%

## Example 3

Source: `lm_understand-logs/exp1_which_game/runs/pacman/prompt.txt`

Status: completed. Model: gpt-6.1-sol.

## Observations:
*Hidden-unit indices below are zero-based.*

- **Channel 0 — agent:** Large weights occupy a **corridor-shaped subset of the interior**, rather than a paddle row or an unrestricted open board. Row 1 has strong weights across columns 1–8, while positions such as `(2,2)` and `(2,3)` remain near the small background scale. Examples:
  - `(1,1)`: weights to hidden units 12 and 29 are **3.377** and **4.081**.
  - `(1,3)`: weight to unit 0 is **4.742**.
  - `(2,4)`: weight to unit 17 is **5.140**.
  - `(2,5)`: weights to units 18 and 24 are **5.290** and **−5.361**.
  
  This strongly suggests movement through a **fixed maze**, with substantial position-specific decision-making.

- **Channel 1 — moving objects:** This channel is also strongly trained throughout the apparent corridors, not merely along one edge. At `(1,1)`, weights include **−1.619** to unit 9 and **2.453** to unit 11; at `(2,4)`, **3.745** to unit 2; at `(2,5)`, **−5.209** to unit 5. Thus other moving entities matter considerably—consistent with enemies moving through the same maze.

- **Channel 2 — reward targets:** Its weights are generally much smaller than the agent weights, with conspicuous exceptions concentrated toward the upper-left corridors. For example, weights to unit 6 are **−1.490**, **−2.361**, and **−1.905** at `(1,1)`, `(1,2)`, and `(1,3)`, and **−4.876** at `(2,4)`. This fits stationary collectibles distributed through a fixed maze, rather than a single freely moving ball or target.

- **Channel 3 — obstacles:** Interior obstacle weights mostly remain around the small background scale. For example, the obstacle row at `(1,1)` begins **0.057, 0.106, 0.006, 0.008**. In contrast to the large agent-position weights, there is little evidence of learning to interpret changing obstacle layouts. A **fixed wall arrangement**, already implicit in the accessible-position pattern, is a natural explanation. The always-present border cannot by itself identify the game.

- **Channel 4 — previous frame:** There is clear learned structure along the corridors, although typically weaker than the current-agent weights. At `(1,1)`, the weight to unit 9 is **−1.316**; at `(1,8)`, it is **−2.849**. Temporal information therefore matters, consistent with reacting to moving enemies rather than solving only a static maze.

- **Outputs:** All four movement directions have substantial, differentiated output weights. For example, hidden unit 2 contributes **2.307** to down and **−1.683** to left; unit 28 contributes **2.500** to right. The output biases are **[−0.873, 0.703, 0.712, 0.595, −0.092]**: no-op is disfavoured relative to movement, and there is no simple two-action paddle signature. These biases alone do not establish actual action frequencies.

## Reasoning:
The combination is most characteristic of **maze navigation with stationary collectibles and independently moving enemies**.

A paddle game such as Pong or Breakout would normally concentrate agent inputs along a boundary and emphasize one movement axis. An open-board collection or dodging game would not naturally explain the corridor-shaped agent-weight footprint. A purely static maze-navigation game does not explain the extensive moving-object and previous-frame structure.

Snake is less convincing because the independently moving-object channel is so prominent. Sokoban could explain a fixed maze and movable objects, but the comparatively weak, localized target representation and substantial temporal structure fit roaming enemies and collectible food better than box-to-goal planning.

The strongest match is therefore **Pac-Man**. The weights support that game family much more clearly than they establish details such as power pellets, enemy count, or scoring bonuses.

## Game:
**A small fixed-maze Pac-Man-style game.**

## Description:
The agent moves through maze corridors collecting pellets or food for reward while avoiding moving ghosts. It must choose routes that gather the collectibles without being caught.

## Confidence:
**92%**

## Example 4

Source: `lm_understand-logs/exp1_which_game/runs/freeway/prompt.txt`

Status: completed. Model: gpt-6.1-sol.

## Observations

Hidden-unit indices below are zero-based.

- **Channel 0 — agent:** Substantial learned weights cover **rows 2–8**, especially the central columns, rather than just a paddle-sized region along one edge. For example, at **(4,5)** the weight to unit 0 is **−6.691**, and at **(8,4)** the weight to unit 5 is **4.958**. Row 1’s agent weights look comparatively small and unstructured. This suggests a player navigating from the bottom through the interior, with reaching row 1 ending the crossing.

- **Channel 1 — moving objects:** Strong structure occupies **rows 2–7**, while the bottom playable row, row 8, looks unused by moving objects. Crucially, there are **four-column repetitions within individual rows**:
  - At **(2,1)** and **(2,5)**, the weights to unit 18 are **−1.898** and **−1.879**.
  - At **(3,2)** and **(3,6)**, the weights to unit 12 are **6.639** and **6.689**.
  - At **(6,4)** and **(6,8)**, the weights to unit 15 are **4.041** and **4.057**.
  
  These are characteristic of regularly spaced objects in horizontal lanes—not a single freely moving ball.

- **Channel 2 — reward targets:** The conspicuous structure is an **entire goal strip across row 1, columns 1–8**. Those inputs have similar weight vectors: for example, the weights to unit 3 at **(1,1)** and **(1,8)** are **−0.550** and **−0.473**, with corresponding unit-25 weights **0.440** and **0.479**. Elsewhere this channel mostly looks like small initialization-scale noise. That suggests “reach the top,” not collecting food scattered around the board.

- **Channel 3 — obstacles:** The repeated learned vector follows the **outer wall border**; the interior lacks comparable obstacle structure. For example, border cells **(0,0)** and **(0,9)** have unit-3 weights **−0.477** and **−0.598**. The border vectors also resemble `b1`, whose unit-3 bias is **−0.492**—consistent with always-active inputs receiving shared updates. There is little evidence of an internal maze.

- **Channel 4 — previous frame:** This is strongly structured throughout the moving-object lanes and also carries bottom-row agent history. Some lane weights closely match a shifted current-object input: previous-frame **(2,1)** has unit-11 weight **−2.266**, versus **−2.373** for the current moving object at **(2,2)**. Previous-frame **(2,3)** has unit-15 weight **2.042**, versus **2.140** for the current moving object at **(2,4)**. This is consistent with predictable horizontal traffic motion.

- **Outputs:** The output biases strongly favor upward progress:
  **`[-0.029, 3.142, -1.862, 0.173, -1.269]`**
  for no-op, up, down, left, right. The hidden contribution can override these biases, and lateral decisions are substantial: output unit 29 has left/right weights **−1.691 / 2.315**, while unit 20 has **1.314 / −1.687**. Thus this is not simply an “always up” policy; it can maneuver sideways around hazards.

## Reasoning

The combination is unusually specific: **a safe bottom starting row, six horizontal moving-object lanes, a top goal strip, and a strong preference for upward movement**. Regularly spaced traffic and previous-frame processing fit a road-crossing game.

Pong and Breakout do not fit the agent’s broad two-dimensional occupancy or the repeated lane structure. Snake and Pac-Man would normally require distributed food targets, and Pac-Man would also show internal maze walls. A falling-object catcher would usually keep the agent near the bottom rather than navigate it through the whole board toward a top goal.

There is no clear separate river/log section, so this looks like a simplified **traffic-only** version rather than every feature of the original arcade game.

## Game

**Frogger — a simplified grid-based, traffic-only road-crossing version.**

## Description

The agent moves from the bottom of the board toward the top, crossing lanes of horizontally moving cars and using sideways movement or waiting to avoid collisions. Reaching the goal strip at the top gives reward.

## Confidence

**98%**

