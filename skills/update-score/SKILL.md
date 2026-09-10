---
name: update-score
description: Correctly updates the BrickBlast score variable and synchronises the DOM display element
---

## Instructions

In BrickBlast, the `score` variable is the game's internal state and the
`#score` DOM element is what the player sees. These must always stay in sync.
The code centralises this in helper functions — use them rather than touching
the DOM directly, so the current score and high score never drift apart.

### 1. Update the score, then refresh the display
Add points to the `score` variable, then call `updateScoreDisplay()`, which
writes both the current score (`#score`) and the best score (`#high-score`)
into the HUD:
```javascript
score += points;
updateScoreDisplay();
```

### 2. Check for a new high score
Call `updateHighScore()` after changing the score. It compares against the
stored best, and when beaten it updates `highScore`, persists it, and
refreshes the display:
```javascript
updateHighScore();
```

For reference, the existing helpers look like this:
```javascript
/**
 * Writes the current score and high score into the HUD.
 */
const updateScoreDisplay = () => {
  scoreElement.textContent = score;        // scoreElement === #score
  highScoreElement.textContent = highScore; // highScoreElement === #high-score
};

/**
 * Updates the high score if the current score beats it, and persists it.
 */
const updateHighScore = () => {
  if (score > highScore) {
    highScore = score;
    saveHighScore(highScore); // persists to localStorage under HIGH_SCORE_KEY
    updateScoreDisplay();
  }
};
```

## Example
Context: the ball destroys a brick, awarding that brick type's points.
This mirrors how `updateBrickCollisions()` scores a destroyed brick:
```javascript
// Inside the collision handler, when a brick is destroyed:
score += BRICK_TYPES[brick.type].points;
updateScoreDisplay(); // sync #score (and #high-score) with the new value
updateHighScore();    // promote + persist if this is a new best
```
