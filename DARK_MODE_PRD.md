# Dark Mode Feature - Product Requirements Document

## Overview
Implement a dark mode toggle feature for the Memory Game to improve user experience in low-light environments and reduce eye strain.

## Feature Description
A theme toggle button (🌙/☀️) allows users to switch between light and dark color schemes. The user's theme preference is persisted in browser localStorage.

## User Stories

### US-1: Toggle Dark Mode
**As a** player  
**I want to** switch between light and dark themes  
**So that** I can play comfortably in any lighting condition

**Acceptance Criteria:**
- Theme toggle button is visible in the controls panel
- Clicking the button switches between light and dark themes
- Visual feedback indicates the current theme state
- Theme toggle is accessible via keyboard (Tab + Enter)

### US-2: Persist Theme Preference
**As a** player  
**I want to** have my theme preference saved  
**So that** the theme automatically applies when I return to the game

**Acceptance Criteria:**
- Selected theme is stored in browser localStorage
- Theme persists across browser sessions
- Key used: `memoryGameTheme` with values `'light'` or `'dark'`
- Default theme on first visit: `'light'`

## Technical Specifications

### CSS Variables (Theming System)
Light mode (default):
- `--primary-color`: #2196f3 (blue)
- `--background-color`: #f5f5f5 (light gray)
- `--card-back`: #1976d2 (darker blue)
- `--card-front`: #ffffff (white)
- `--text-color`: #333333 (dark gray)
- `--success-color`: #4caf50 (green)

Dark mode (`:root[data-theme="dark"]`):
- `--primary-color`: #90caf9 (light blue)
- `--background-color`: #121212 (near black)
- `--card-back`: #263238 (dark teal)
- `--card-front`: #1e1e1e (dark gray)
- `--text-color`: #e0e0e0 (light gray)
- `--success-color`: #66bb6a (light green)

### HTML Structure
```html
<button class="theme-toggle" aria-pressed="false" title="Toggle dark mode">🌙</button>
```
Location: Controls panel (`.controls` div)

### JavaScript Implementation
Key functions:
- `applyTheme(theme)`: Applies theme by setting `data-theme` attribute on `<html>` element
- Theme toggle event listener: Reads current theme, switches to opposite, and saves to localStorage
- Initialization: Loads saved theme from localStorage on page load

### Accessibility
- Button includes `aria-pressed` attribute (reflects current state)
- Button has descriptive `title` attribute
- Theme applies via `data-theme` attribute on root element (semantic approach)
- Sufficient color contrast maintained in both themes

## Design & UX

### Button Styling
- Location: Top-right of controls panel (flex layout)
- Size: 0.25rem padding, 0.5rem horizontal, 1.1rem font-size
- Appearance: Transparent background, emoji icon (🌙/☀️)
- Hover: Border highlight on active state
- Visual feedback: Icon toggles between 🌙 (light mode) and ☀️ (dark mode)

### Color Contrast
- Light mode: Dark gray text (#333) on light background (#f5f5f5) ✓
- Dark mode: Light gray text (#e0e0e0) on dark background (#121212) ✓
- WCAG AA compliant (≥4.5:1 contrast ratio)

## Testing Checklist
- [ ] Theme toggle button appears in controls panel
- [ ] Clicking button switches between themes
- [ ] Icon changes (🌙 ↔ ☀️) on toggle
- [ ] Theme persists after page reload
- [ ] Theme persists after browser restart
- [ ] All text is readable in both themes
- [ ] Cards are distinguishable in both themes
- [ ] Modal dialog is visible in both themes
- [ ] Keyboard navigation works (Tab to button, Enter to toggle)
- [ ] No console errors on theme switch

## Browser Support
- Chrome/Edge 88+
- Firefox 85+
- Safari 14.1+
- Mobile browsers (iOS Safari, Chrome Mobile)

## Implementation Details
**File modified:** `memory-game.html`
- CSS: 30+ lines (variables, dark mode overrides, button styling)
- HTML: 1 line (theme toggle button)
- JavaScript: 30+ lines (applyTheme, localStorage handling, event listener)

**Dependencies:** None (vanilla JS, no external libraries)

**Performance:** Negligible impact (~1KB)

## Future Enhancements
- System preference detection (`prefers-color-scheme` media query)
- Scheduled theme switching (auto-dark at sunset)
- Additional themes (high contrast, sepia, etc.)
- Theme selector UI (dropdown with multiple options)
