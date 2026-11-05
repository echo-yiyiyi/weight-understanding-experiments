# GPT-6.1 Sol — Section Ablations

Each condition uses four independent requests, high reasoning effort, no tools, and the original output instructions and weights.

- no-observation: remove THE OBSERVATION up to THE ACTIONS; retain actions.
- no-actions: remove THE ACTIONS up to THE NETWORK; retain observation.

Only those sections are removed. Later mentions of grid, channels, or actions remain unchanged, so these are section-removal ablations, not removal of all related information.
