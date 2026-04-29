# 🏀 Pickup Queue

A mobile-friendly web app for managing fair basketball pickup game rotations. Ensures everyone gets equal playing time by automatically tracking who's sat out and prioritizing them for the next game.

## Features

### Queue Management
- **Fair rotation system**: Automatically prioritizes players who've sat out the most games
- **10-player games**: Designed for full-court 5v5 basketball
- **Manual reordering**: Use ✏️ Reorder or 🔄 Swap to manually adjust queue positions
- **Player statistics**: Track games played and games sat out for each player

### Game Control
- **16-minute game timer**: Built-in countdown with pause/resume functionality
- **Visual warnings**: Timer changes color at 3 minutes (warning) and 1 minute (danger)
- **Vibration alerts**: Phone vibrates when timer reaches zero (on supported devices)

### Organization
- **Active/inactive lists**: Move players who left to "Left" section with easy return option
- **Next up preview**: See who's playing in the next 1-2 games before starting
- **Game history**: View all past games and who played

### Sharing & Transfer
- **Copy queue summary**: Export formatted game history and player stats
- **Copy player list**: Share a simple numbered list of all players
- **Transfer codes**: Export/import entire queue state to transfer between devices
- **LocalStorage persistence**: Queue automatically saves and restores on page reload

## How to Use

1. **Add players**: Enter names and tap "Add" to build your player list
2. **Start game**: Once you have 10+ players, tap "🏀 Start Game"
3. **Manage timer**: Tap the timer to pause/resume during games
4. **End game**: When finished, tap "🔔 End Game" to rotate players
5. **Repeat**: The app automatically queues the next 10 players based on priority

## Priority System

Players are prioritized using this formula:
1. **Games sat out** (primary): More games sat = higher priority
2. **Games played** (secondary): Fewer games played = higher priority among same sat-out count
3. **Arrival order** (tiebreaker): Earlier arrivals win ties

You can override automatic priority using the Reorder or Swap features.

## Technical Details

- **No dependencies**: Pure HTML/CSS/JavaScript
- **Mobile-optimized**: Responsive design with touch-friendly controls
- **Offline-capable**: Works without internet after initial load
- **LocalStorage**: All data saved locally in browser
- **Progressive Web App ready**: Can be added to home screen on iOS/Android

## Installation

Simply open `index.html` in any modern web browser. For best experience on mobile:

1. Open in Safari (iOS) or Chrome (Android)
2. Tap Share → Add to Home Screen
3. Launch from home screen for full-screen app experience

## Browser Support

- Safari (iOS 13+)
- Chrome (Android 6+)
- Any modern browser with ES6 support and LocalStorage

## Configuration

Edit these constants in the JavaScript to customize:

```javascript
const PLAYERS_PER_GAME = 10;        // Players per game
const GAME_DURATION = 16 * 60;      // Game duration in seconds
```

## Use Cases

- Pickup basketball games at gyms or courts
- Recreational leagues with rotating rosters
- Community sports events
- Any scenario requiring fair rotation among 10+ participants

## License

Open source - use freely for any purpose.
