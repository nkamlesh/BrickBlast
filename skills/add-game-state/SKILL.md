---
name: add-game-state
description: Adds a new game state (like PAUSED, GAME_OVER, LEVEL_COMPLETE) to BrickBlast with consistent handling
---

## Instructions

BrickBlast tracks its run state in a single string variable, `gameState`.
The existing states are `"start"` (waiting to begin), `"running"` (actively
playing), `"paused"`, and `"over"` (game finished). Messages are shown to the
player through the HTML `#overlay` element (via `showOverlay()` /
`hideOverlay()`), not by drawing text on the canvas. The main `loop()` only
schedules the next frame while `gameState === "running"`, so entering any
non-running state naturally halts gameplay.

When adding a new state, follow these steps:

### 1. Document the new state value
`gameState` uses plain string values, so there is no enum to edit — just add
the new value to the comment above the declaration so the set stays documented:
```javascript
// Run state: "start", "running", "paused", "over", or "your_new_state".
let gameState = "start";
```

### 2. Add transition functions
Create functions to enter (and, if needed, leave) the state. Guard the
transition so it only runs from a valid prior state, and stop the loop by
cancelling the pending frame when the state should freeze gameplay:
```javascript
/**
 * Transitions the game into [state]. Called when [trigger condition].
 */
const enterYourState = () => {
  if (gameState !== "running") {
    return; // Only valid from a running game (adjust as needed).
  }
  gameState = "your_new_state";
  // Stop the loop so no further frames advance the game while in this state.
  if (animationId !== null) {
    cancelAnimationFrame(animationId);
    animationId = null;
  }
  showOverlay("Your message here");
};
```

### 3. Resume the loop when leaving the state
To return to play, hide the overlay, set `gameState` back to `"running"`, and
call `loop()` again:
```javascript
const leaveYourState = () => {
  if (gameState !== "your_new_state") {
    return;
  }
  gameState = "running";
  hideOverlay();
  loop();
};
```

### 4. Wire up the trigger and the overlay click
Add the key handling in `handleKeyDown`, and make sure `handleOverlayClick`
does the right thing for the new state (resume vs. restart) so a click on the
overlay doesn't accidentally reset the game.

## Example

**User request**: "Add a PAUSED state toggled with the P key"

**Implemented in game.js**:
```javascript
/**
 * Pauses a running game: stops scheduling frames and shows the pause overlay.
 */
const pauseGame = () => {
  if (gameState !== "running") {
    return;
  }
  gameState = "paused";
  if (animationId !== null) {
    cancelAnimationFrame(animationId);
    animationId = null;
  }
  showOverlay("Paused — press P to resume");
};

/**
 * Resumes a paused game: hides the overlay and restarts the loop.
 */
const resumeGame = () => {
  if (gameState !== "paused") {
    return;
  }
  gameState = "running";
  hideOverlay();
  loop();
};

// In handleKeyDown — P toggles pause while a game is in progress:
} else if (event.key === "p" || event.key === "P") {
  if (gameState === "running") {
    pauseGame();
  } else if (gameState === "paused") {
    resumeGame();
  }
}

// In handleOverlayClick — resume when paused, otherwise start/restart:
if (gameState === "paused") {
  resumeGame();
} else if (gameState !== "running") {
  startGame();
}
```
