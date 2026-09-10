# BrickBlast — Coding Style Guide

## JavaScript Style
- Use `const` for values that never change, `let` for values that do
- Never use `var`
- Use arrow functions for callbacks: `() => {}`
- Use template literals for string concatenation: `\`Score: ${score}\``
- Always use semicolons at the end of statements
- Use camelCase for variable and function names: `playerScore`, `drawBricks()`
- Use UPPER_SNAKE_CASE for true constants: `CANVAS_WIDTH`, `BRICK_ROWS`

## Comments
- Every function must have a comment explaining what it does
- Complex logic should have inline comments
- Comments should explain WHY, not just WHAT

## Code Organisation (game.js)
Organise code in this order:
1. Constants (canvas size, game settings)
2. Game state variables
3. Initialisation functions
4. Drawing functions (prefixed with `draw`)
5. Update/logic functions (prefixed with `update`)
6. Event handlers
7. Game loop

## HTML/CSS Style
- Use semantic HTML elements where appropriate
- CSS class names use kebab-case: `.score-container`, `.game-canvas`
- Group related CSS properties together