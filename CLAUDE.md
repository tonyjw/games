# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a games collection repository focused on building fun, interactive games using **vanilla web technologies**. The project emphasizes simplicity, performance, and accessibility without relying on frameworks or heavy dependencies.

## Technology Stack & Philosophy

### Core Technologies (ONLY)
- **HTML5** - Semantic markup and modern web standards
- **CSS3** - Native styling with Flexbox, Grid, animations, and custom properties
- **Vanilla JavaScript (ES6+)** - Modern JavaScript without frameworks
- **Web APIs** - Native browser APIs (Web Audio, LocalStorage, Canvas when needed)

### What We DON'T Use
- ❌ **No Frameworks** - No React, Vue, Angular, or similar
- ❌ **No Build Tools** - No Webpack, Vite, Parcel, or bundlers
- ❌ **No Package Managers** - No npm, yarn dependencies for runtime
- ❌ **No CSS Frameworks** - No Bootstrap, Tailwind, Material UI
- ❌ **No JavaScript Libraries** - No jQuery, Lodash, or utility libraries
- ❌ **No External CDNs** - Everything should work offline

## Development Principles

### 1. Native Web Platform First
- Use modern browser APIs instead of polyfills or libraries
- Leverage CSS Grid and Flexbox for layouts
- Use Web Audio API for sound instead of audio libraries
- Utilize CSS animations and transitions over animation libraries

### 2. Self-Contained Games
- Each game should be a single HTML file with embedded CSS and JS
- No external dependencies or imports
- Games should work offline and be easily shareable
- Maximum file size per game: ~2MB including all assets

### 3. Progressive Enhancement
- Start with semantic HTML that works without JavaScript
- Layer on CSS for visual enhancement
- Add JavaScript for interactivity
- Ensure graceful degradation on older browsers

### 4. Performance Standards
- Target 60fps animations on mobile devices
- First paint under 1 second
- Total load time under 3 seconds on slow connections
- Memory usage under 50MB per game
- Smooth performance on 3-year-old mobile devices

### 5. Accessibility Requirements
- Semantic HTML elements and proper ARIA labels
- Keyboard navigation support for all interactive elements
- Color contrast ratios meeting WCAG 2.1 AA standards
- Screen reader compatible
- Touch-friendly targets (minimum 44px)

## Project Structure

```
games/
├── index.html              # Main portal (single file)
├── README.md              # Project documentation
├── CLAUDE.md              # This development guide
├── .gitignore             # Git exclusions
└── {game-name}/           # Individual game directories
    ├── index.html         # Complete game (HTML + CSS + JS)
    └── README.md          # Game-specific documentation
```

## Development Patterns

### HTML Structure
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Name</title>
    <style>
        /* All CSS embedded here */
    </style>
</head>
<body>
    <!-- Game HTML -->
    <script>
        /* All JavaScript here */
    </script>
</body>
</html>
```

### CSS Guidelines
- Use CSS Custom Properties for theming
- Mobile-first responsive design
- CSS Grid for complex layouts, Flexbox for components
- Prefer `transform` and `opacity` for animations (GPU acceleration)
- Use `rem` and `em` for scalable typography
- Implement dark mode support where appropriate

### JavaScript Patterns
- Use modern ES6+ features (const/let, arrow functions, destructuring)
- Prefer event delegation over individual event listeners
- Use Local Storage for persistence
- Implement proper error handling
- Use Web Audio API for dynamic sound generation
- Favor functional programming patterns over classes when appropriate

### Example Code Patterns

#### Font Embedding (Fredoka)
```css
@font-face {
    font-family: 'Fredoka';
    font-style: normal;
    font-weight: 400;
    font-display: swap;
    /* For offline: replace empty base64 with actual font data */
    src: url('data:font/woff2;base64,') format('woff2'),
         url('https://fonts.gstatic.com/s/fredoka/v14/...') format('woff2');
}

body {
    font-family: 'Fredoka', 'Nunito', 'Quicksand', 'Varela Round', 
                 'Comfortaa', 'Balsamiq Sans', 'Comic Sans MS', 
                 system-ui, sans-serif;
}
```

#### Sound Effects (Web Audio API)
```javascript
const audioContext = new (window.AudioContext || window.webkitAudioContext)();

function createTone(frequency, duration, type = 'sine') {
    const oscillator = audioContext.createOscillator();
    const gainNode = audioContext.createGain();
    // Implementation...
}
```

#### Local Storage Management
```javascript
function saveGameData(data) {
    try {
        localStorage.setItem('gameData', JSON.stringify(data));
    } catch (error) {
        console.warn('Could not save game data:', error);
    }
}
```

#### Responsive CSS Grid
```css
.game-board {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    gap: 1rem;
    padding: 1rem;
}

@media (max-width: 768px) {
    .game-board {
        grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
        gap: 0.5rem;
    }
}
```

## Game Design Guidelines

### Visual Design
- Bright, vibrant color palettes suitable for all ages
- Rounded corners and soft shadows for friendly appearance
- Consistent design language across all games
- Font stack: `'Fredoka', 'Nunito', 'Quicksand', 'Varela Round', 'Comfortaa', 'Balsamiq Sans', 'Comic Sans MS', system-ui, sans-serif` for modern, playful feel
- Use emojis for icons when appropriate

### User Experience
- Immediate feedback for all user actions
- Encouraging, positive messaging (no penalties for mistakes)
- Clear visual hierarchy and intuitive navigation
- Smooth animations that enhance rather than distract
- Loading states and progress indicators

### Navigation Requirements
Every game must include standard navigation elements for consistency and usability:

#### Required Navigation Elements
1. **Back to Games Portal** - On the main game screen, include a prominent link/button to return to the main games collection (`../index.html`)
2. **Restart Game** - When inside a game (playing), provide a clear way to restart/return to the beginning of the current game
3. **Consistent Styling** - Navigation elements should match the game's visual design while remaining clearly identifiable

#### Navigation Implementation Examples
```html
<!-- Back to games portal (on main game screen) -->
<button class="nav-btn" onclick="window.location.href='../index.html'">🏠 All Games</button>

<!-- Restart game (during gameplay) -->
<button class="nav-btn" onclick="restartGame()">🔄 New Game</button>
```

#### Navigation CSS Standards
```css
.nav-btn {
    background: linear-gradient(45deg, #FF6B35, #FFD700);
    border: none;
    border-radius: 12px;
    padding: 10px 20px;
    font-size: 1rem;
    font-family: inherit;
    color: white;
    cursor: pointer;
    transition: all 0.3s ease;
    margin: 10px;
}

.nav-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 15px rgba(255, 107, 53, 0.3);
}
```

### Interaction Design
- Large, touch-friendly buttons (minimum 44px)
- Hover states for desktop users
- Visual feedback for all interactive elements
- Consistent interaction patterns across games
- Support for both mouse and keyboard navigation

## Browser Compatibility

### Target Support
- **Modern Browsers**: Chrome 80+, Firefox 75+, Safari 13+, Edge 80+
- **Mobile**: iOS Safari 13+, Chrome Mobile 80+
- **Features**: ES6+, CSS Grid, Flexbox, Web Audio API

### Graceful Degradation
- Provide fallbacks for unsupported features
- Test on older devices when possible
- Use feature detection instead of browser detection

## Testing Requirements

### Manual Testing Checklist
- [ ] Works on desktop (Chrome, Firefox, Safari)
- [ ] Works on mobile (iOS, Android)
- [ ] Responsive at all screen sizes
- [ ] Keyboard navigation functional
- [ ] Sound effects work properly
- [ ] Local storage saves/loads correctly
- [ ] No console errors
- [ ] Smooth 60fps performance
- [ ] Navigation elements present and functional
- [ ] "Back to Games" button works from main game screen
- [ ] "Restart/New Game" button works during gameplay

### Performance Testing
- Test on slower devices and connections
- Verify memory usage stays reasonable
- Check for memory leaks in long play sessions
- Ensure animations remain smooth under load

## Adding New Games

### Process
1. Create new directory: `{game-name}/`
2. Build complete game in single `index.html` file
3. Follow all development patterns and guidelines
4. Add game-specific `README.md`
5. Update main portal (`index.html`) with new game card
6. Update repository `README.md`

### Quality Standards
- Complete feature implementation
- Responsive design tested
- Accessibility compliance
- Performance benchmarks met
- Browser compatibility verified
- Documentation complete
- **Navigation compliance** - Required navigation elements implemented and tested

## Common Development Tasks

### Running Games Locally
```bash
# Open main portal
open index.html

# Open specific game
open chili-dog-match/index.html

# Or use any local server
python -m http.server 8000
# Navigate to http://localhost:8000
```

### Debugging
- Use browser DevTools for debugging
- Test performance with DevTools Performance tab
- Check accessibility with DevTools Lighthouse
- Validate HTML with W3C validator
- Test responsive design with device simulation

## Code Quality Standards

### JavaScript
- Use `'use strict';` mode
- Prefer `const` over `let`, avoid `var`
- Use meaningful variable and function names
- Comment complex algorithms and game logic
- Handle errors gracefully
- Avoid global variables when possible

### CSS
- Use consistent naming conventions
- Group related properties
- Comment complex calculations or hacks
- Use CSS custom properties for reusable values
- Optimize for performance (avoid expensive properties)

### HTML
- Use semantic elements
- Provide proper alt text for images
- Include proper meta tags
- Ensure proper heading hierarchy
- Add ARIA labels where needed

## Notes for Claude Code

- **Priority**: Always prefer native web technologies over any framework
- **Simplicity**: If a feature can be built with vanilla JS, don't suggest libraries
- **Performance**: Consider mobile performance in all recommendations
- **Accessibility**: Include accessibility considerations in all implementations
- **Self-Contained**: Each game should work as a standalone file
- **Educational**: Code should be readable and educational for learning purposes
- **Future-Proof**: Use modern web standards that will age well