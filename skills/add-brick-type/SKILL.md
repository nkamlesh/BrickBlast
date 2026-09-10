---
name: add-brick-type
description: Adds a new type of brick to BrickBlast with consistent structure, visual style, and scoring behaviour
---

## Instructions

When asked to add a new brick type to BrickBlast, follow these steps:

### 1. Define the Brick Configuration
Add a new entry to the `BRICK_TYPES` constant object in game.js:
```javascript
BRICK_TYPE_NAME: {
    color: '#HEXCOLOR',      // The brick's fill colour
    points: NUMBER,          // Points awarded when destroyed
    hits: NUMBER,            // How many hits to destroy (1 for normal)
    label: 'Display Name'    // Human-readable name for debugging
}
```

### 2. Update the Brick Grid Initialisation
In the `initBricks()` function, ensure the new brick type can be assigned to grid positions. If it's a special brick, document the condition under which it appears (e.g., random chance, specific row).

### 3. Update the Draw Function
In `drawBricks()`, add a case for the new brick type that:
- Sets `ctx.fillStyle` to the brick's colour
- Draws the brick rectangle
- Optionally adds a label or visual indicator for special bricks

### 4. Update Collision Handling 
In the collision detection function, ensure the new brick type:
- Decrements its `hits` counter when struck
- Only marks as destroyed when `hits` reaches 0
- Awards the correct `points` value to the score

### 5. Add a Comment
Add a JSDoc comment above the new brick type definition explaining its special behaviour (if any).

## Example

**User request**: "Add an armoured brick that takes 2 hits to destroy and is worth 30 points"
**Expected output additions to game.js**:
```javascript
// In BRICK_TYPES constant:
ARMOURED: {
    color: '#708090',   // Slate grey - looks tough
    points: 30,         // Worth more because it takes 2 hits
    hits: 2,            // Requires 2 ball contacts to destroy
    label: 'Armoured'
}

// In drawBricks() - show damage state:
// When hits === 1 (damaged), draw with a crack pattern or lighter colour
if (brick.type === 'ARMOURED' && brick.currentHits === 1) {
    ctx.fillStyle = '#A9A9A9'; // Lighter grey when damaged
}
```
