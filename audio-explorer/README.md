# Audio Explorer

An interactive Web Audio API playground and game sound library for developers and audio enthusiasts.

## 🎮 How to Play

1. **Explore Preset Sounds**: Click any of the 24+ preset sound buttons to hear common game audio effects
2. **View Generated Code**: Check the browser console to see the exact code needed to recreate each sound
3. **Build Custom Sounds**: Use the Custom Sound Builder to experiment with:
   - Frequency (pitch) - 50Hz to 2000Hz
   - Duration (length) - 0.1 to 3 seconds  
   - Waveform (timbre) - Sine, Square, Triangle, Sawtooth
   - Volume - 0.1 to 1.0
4. **Copy Code**: Generated code appears in real-time and can be copied directly into your games
5. **Learn & Experiment**: Understand how Web Audio API parameters affect sound characteristics

## ✨ Features

- 24+ professionally designed preset game sound effects
- Interactive parameter controls with real-time feedback
- Live code generation and syntax highlighting
- Three organized sound categories (Game Effects, UI Effects, Musical Elements)
- Educational tooltips and explanations
- Copy-paste ready code snippets for developers
- Responsive design for desktop and mobile
- Standard navigation compliance
- Console logging for development workflow

## 🎯 Game Details

- **Players**: 1 player (educational/exploration tool)
- **Difficulty**: Beginner-friendly with advanced customization options
- **Duration**: Open-ended exploration (typically 5-30 minutes per session)
- **Platform**: Desktop & Mobile (responsive)
- **Technology**: HTML5, CSS3, Vanilla JavaScript, Web Audio API

## 🎵 Audio

### Game Effects (8 sounds)
- Hit Target, Power Up, Explosion, Victory, Fail/Error, Laser Shoot, Shield Block, Electric Zap

### UI Effects (8 sounds)  
- Button Click, Confirm, Notification, Transition, Warning, Menu Open, Whoosh, Celebrate

### Musical Elements (6 sounds)
- C Major Scale, Major Chord, Arpeggio Up, Arpeggio Down, Bell Toll, Fanfare

All sounds use the standardized Web Audio API implementation for consistency across the game collection.

## 📱 Controls

### Desktop
- **Mouse Click**: Play preset sounds and interact with controls
- **Slider Drag**: Adjust frequency, duration, and volume parameters
- **Dropdown Select**: Choose waveform types
- **Button Click**: Play custom sounds and navigate

### Mobile
- **Tap**: Play sounds and interact with all controls
- **Slider Touch**: Adjust parameters with touch-friendly controls
- **Scroll**: Browse different sound categories

## 🏆 Scoring

This is an educational tool rather than a competitive game. Success is measured by:
- Understanding of Web Audio API concepts
- Ability to create desired sound effects
- Knowledge gained about audio programming
- Code snippets successfully integrated into other projects

## 🛠️ Technical Implementation

### Key Technologies
- **Web Audio API**: Core audio synthesis and playback
- **ES6+ JavaScript**: Modern async/await patterns for sound sequencing
- **CSS Grid & Flexbox**: Responsive layout system
- **CSS Custom Properties**: Theming and design consistency
- **Promise-based Audio**: Non-blocking sound generation

### Performance Optimizations
- Lazy audio context initialization (user interaction required)
- Efficient oscillator cleanup after sound completion
- Minimal DOM manipulation for real-time updates
- CSS hardware acceleration for smooth animations

### Accessibility Features
- High contrast color schemes
- Touch-friendly targets (44px minimum)
- Keyboard navigation support
- Screen reader compatible semantic HTML
- Clear visual feedback for all interactions

### Educational Architecture
- Modular sound creation functions
- Commented code examples
- Progressive complexity (simple to advanced sounds)
- Real-time parameter visualization
- Console logging for debugging workflow

## 📚 Educational Value

This game serves as a comprehensive learning resource for:

### Web Audio API Concepts
- Oscillator creation and configuration
- Gain node usage for volume control
- Audio context management
- ADSR envelope implementation
- Waveform characteristics and applications

### Game Development Skills
- Sound effect timing and sequencing
- Audio feedback for user interactions  
- Performance considerations for real-time audio
- Code organization for audio libraries
- Cross-browser audio compatibility

### JavaScript Programming
- Promise-based asynchronous programming
- Event handling and DOM manipulation
- Modern ES6+ syntax and patterns
- Modular function design
- Error handling for audio operations

## 🔗 Related Games

- **[Chili Dog Match](../chili-dog-match/)**: Uses several preset sounds from this library for game feedback
- **Future Games**: All upcoming games in the collection will utilize this standardized sound library

### Integration with Other Games
The Audio Explorer serves as the central sound library for the entire game collection. Other games should import and use the preset functions defined here to maintain audio consistency and quality across the platform.

### For Developers
Visit Audio Explorer first when building new games to:
1. Choose appropriate sounds for different game events
2. Copy proven, tested audio code
3. Understand Web Audio API best practices
4. Maintain consistency with the existing game collection