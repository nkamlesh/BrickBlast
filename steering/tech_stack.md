# BrickBlast — Technology Stack

## Core Technologies
- **HTML5**: Single file (index.html) with semantic markup
- **CSS3**: Single file (style.css) for all styling
- **JavaScript (ES6+)**: Single file (game.js) for all game logic

## Canvas API
The game is rendered using the HTML5 Canvas API (2D context).
All game drawing happens on a <canvas> element.

## What We Are NOT Using
- No JavaScript frameworks (no React, Vue, Angular, etc.)
- No CSS preprocessors (no Sass, Less)
- No build tools (no Webpack, Vite, Parcel)
- No npm packages or node_modules
- No TypeScript

## Browser Target
Modern browsers only (Chrome, Firefox, Edge). No IE11 support needed.

## File Structure
brickblast/
├── index.html      (game HTML structure)
├── style.css       (all styling)
├── game.js         (all game logic)
└── .kiro/
    └── steering/   (Kiro configuration files)