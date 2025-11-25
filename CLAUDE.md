# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

MMM-Keyboard is a MagicMirror² module that provides a virtual on-screen keyboard for touch input. It allows other MagicMirror modules to request text input from users via the notification system.

## Commands

```bash
# Install dependencies
npm install
```

No build step, linting, or tests are configured for this project.

## Architecture

This is a frontend-only MagicMirror² module with no backend/Node helper component.

### Key Files

- **MMM-Keyboard.js** - Main module file implementing the MagicMirror `Module.register()` pattern
- **layouts.json** - Keyboard layout definitions for supported languages (en, de)
- **keyboard.css** - Styling including show/hide animations

### Module Communication

The keyboard uses MagicMirror's notification system:

1. **Opening the keyboard**: Other modules send `KEYBOARD` notification with payload:
   ```js
   { key: "uniqueKey", style: "default"|"numbers", data: {} }
   ```

2. **Receiving input**: Keyboard broadcasts `KEYBOARD_INPUT` notification:
   ```js
   { key: "uniqueKey", message: "user input text", data: {} }
   ```

### Dependencies

Uses `simple-keyboard` NPM package for the keyboard UI component. The library is loaded directly from node_modules in the browser.

### Keyboard State

- `shiftState`: 0 = lowercase, 1 = shift (single uppercase), 2 = caps lock
- Layouts: "default", "shift", "numbers"
- Show/hide is controlled via CSS class `show-keyboard` with transition animation
