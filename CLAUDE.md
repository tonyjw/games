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
All games should use the standardized sound library from Audio Explorer. Use these preset sounds for consistency:

```javascript
const audioContext = new (window.AudioContext || window.webkitAudioContext)();

// Core sound function - copy this to every game
function createTone(frequency, duration, type = 'sine', volume = 0.3) {
    return new Promise(resolve => {
        const oscillator = audioContext.createOscillator();
        const gainNode = audioContext.createGain();
        
        oscillator.connect(gainNode);
        gainNode.connect(audioContext.destination);
        
        oscillator.frequency.setValueAtTime(frequency, audioContext.currentTime);
        oscillator.type = type;
        
        gainNode.gain.setValueAtTime(volume, audioContext.currentTime);
        gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + duration);
        
        oscillator.start(audioContext.currentTime);
        oscillator.stop(audioContext.currentTime + duration);
        
        oscillator.onended = resolve;
    });
}

// Standard game sounds - use these presets for consistency
function playButtonClick() { createTone(600, 0.1, 'square'); }
function playSuccess() { createTone(800, 0.15, 'sine'); }
function playError() { 
    createTone(400, 0.2, 'triangle');
    setTimeout(() => createTone(350, 0.3, 'triangle'), 200);
}
function playPowerUp() {
    createTone(523, 0.15, 'square');
    setTimeout(() => createTone(659, 0.15, 'square'), 150);
    setTimeout(() => createTone(784, 0.2, 'square'), 300);
}
function playVictory() {
    createTone(523, 0.3, 'triangle');
    setTimeout(() => createTone(659, 0.3, 'triangle'), 300);
    setTimeout(() => createTone(784, 0.3, 'triangle'), 600);
    setTimeout(() => createTone(1047, 0.5, 'triangle'), 900);
}

// Initialize audio context on first user interaction
function initAudio() {
    if (audioContext.state === 'suspended') {
        audioContext.resume();
    }
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
- [ ] Sound effects work properly using standard library
- [ ] Local storage saves/loads correctly
- [ ] No console errors
- [ ] Smooth 60fps performance
- [ ] Navigation elements present and functional
- [ ] "Back to Games" button works from main game screen
- [ ] "Restart/New Game" button works during gameplay

### Audio Development Resource

The **Audio Explorer** game serves as both a playable experience and a development tool for this project:

#### Purpose
- **Sound Library Reference**: Browse 24+ preset game sound effects
- **Code Generation**: Get copy-paste ready code for any sound
- **Parameter Experimentation**: Adjust frequency, duration, waveform, and volume
- **Educational Tool**: Learn Web Audio API through interactive examples

#### Using Audio Explorer for Development
1. **Visit `/audio-explorer/` to explore available sounds**
2. **Click any preset sound to hear it and see the code in console**
3. **Use the Custom Sound Builder to create new effects**
4. **Copy the generated code directly into your games**
5. **Maintain consistency by using the standard sound presets**

#### Standard Sound Categories
- **Game Effects**: Hit targets, power-ups, explosions, victory, failure, laser, shield, electric
- **UI Effects**: Button clicks, confirmations, notifications, transitions, warnings, menu sounds
- **Musical Elements**: Scales, chords, arpeggios, bells, fanfares

#### Integration Example
```javascript
// In your game, include the core createTone function and use presets:
function initGameAudio() {
    // Use standard button click for UI
    document.addEventListener('click', (e) => {
        if (e.target.closest('.btn')) {
            playButtonClick();
        }
    });
    
    // Use standard success sound for achievements
    function onPlayerSuccess() {
        playSuccess();
        // or playPowerUp() for bigger achievements
    }
}
```

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
4. **Create comprehensive game-specific `README.md`** (see template below)
5. Update main portal (`index.html`) with new game card
6. **Update main repository `README.md`** with new game entry
7. Update game count statistics in main portal footer
8. Ensure all navigation links work correctly

### Game README Template
Each game directory must include a `README.md` with this structure:

```markdown
# Game Name

Brief one-line description of the game.

## 🎮 How to Play

Clear, step-by-step instructions on how to play the game.

## ✨ Features

- Feature 1
- Feature 2
- Feature 3
- etc.

## 🎯 Game Details

- **Players**: Number of players (1 player, 2 players, etc.)
- **Difficulty**: Easy/Medium/Hard or difficulty options available
- **Duration**: Typical game session length
- **Platform**: Desktop & Mobile (responsive)
- **Technology**: HTML5, CSS3, Vanilla JavaScript, Web Audio API

## 🎵 Audio

- List of sound effects used
- Reference to Audio Explorer for sound library

## 📱 Controls

### Desktop
- Describe mouse/keyboard controls

### Mobile
- Describe touch controls

## 🏆 Scoring (if applicable)

Explain how scoring works, win conditions, etc.

## 🛠️ Technical Implementation

Brief overview of interesting technical aspects:
- Key algorithms used
- Web APIs utilized
- Performance optimizations
- Accessibility features

## 📚 Educational Value (if applicable)

What can developers learn from this game's code?

## 🔗 Related Games

Links to similar games in the collection.
```

### Main Repository README Updates
When adding games, the main `README.md` must be updated with:

1. **Game count in header statistics**
2. **New game entry in the games list** with:
   - Game name and emoji
   - Brief description (1-2 sentences)
   - Key features (3-4 bullet points)
   - Link to play the game
3. **Updated "Getting Started" instructions if needed**
4. **Technology stack updates if new APIs are used**

### Quality Standards
- Complete feature implementation
- Responsive design tested
- Accessibility compliance
- Performance benchmarks met
- Browser compatibility verified
- **Documentation complete** - Both game README and main README updated
- **Navigation compliance** - Required navigation elements implemented and tested
- **Sound library compliance** - Uses standard audio presets from Audio Explorer

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