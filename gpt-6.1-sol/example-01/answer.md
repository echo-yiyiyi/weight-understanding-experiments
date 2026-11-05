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