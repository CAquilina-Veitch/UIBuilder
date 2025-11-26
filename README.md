# UI Builder

A visual UI mockup tool for creating user interface layouts that can later be implemented in Unity.

## Getting Started

1. Open `index.html` in a web browser (Chrome, Firefox, or Edge recommended)
2. Select a canvas resolution or enter a custom size
3. Start designing!

## Features

### Element Types

| Element | Description |
|---------|-------------|
| **Container** | Empty box for grouping elements. Can have children. |
| **Button** | Clickable button with text. Can trigger variable changes. |
| **Image** | Placeholder for images (displays checkered pattern). |
| **Text** | Text label with customizable font size and alignment. |

### Layout

- **Left Panel**: Element palette (top) and hierarchy tree (bottom)
- **Center**: Canvas area with grid
- **Right Panel**: Properties (top) and variables (bottom)
- **Bottom Bar**: Grid size configuration

### Canvas

- Resolution is set at project creation (e.g., 1920x1080)
- Canvas scales to fit the viewport while maintaining aspect ratio
- Grid snapping for precise placement (configurable grid size)

### Positioning & Sizing

- **Position**: Percentage-based (0-100% of parent width/height)
- **Size**: Pixel-based (fixed dimensions)

This allows elements to be relatively positioned but maintain consistent sizes.

### Hierarchy & Parenting

- Drag elements in the hierarchy to reorder siblings
- Drag an element onto a **Container** to parent it (or hold Ctrl while dropping)
- Double-click an item in the hierarchy to rename it
- Children render in front of parents
- Lower items in sibling list render in front

### Element Properties

All elements have:
- **Name**: Identifier for the element
- **Position X/Y**: Percentage of parent (or canvas if root)
- **Size W/H**: Pixel dimensions

Type-specific properties:
- **Container**: Background color (supports rgba), border, padding, clip children toggle
- **Button**: Text, text color, background color, border, border radius
- **Image**: Placeholder color, border
- **Text**: Content, text color, font size, text alignment

### Variables (Enums)

Create global enum variables in the Variables panel:

1. Click **+ Add Variable**
2. Edit the variable name
3. Add/remove values
4. Set a default value (radio button)

Variables are used for logic conditions and button actions.

### Logic System

#### Button Actions (onClick)

Buttons can set variable values when clicked:

```
Set [MenuState] to [Settings]
```

Multiple actions can be added to a single button.

#### Visibility Conditions (all other elements)

Elements can have conditional visibility based on variable values:

```
If [MenuState] is [Settings, Options]
AND If [UserType] is [Admin]
Then: Enable this element
```

- Multiple values can be checked for a single variable (OR within the value set)
- Multiple conditions can be chained with AND/OR operators
- Result can be "Enable" or "Disable"

### Preview Mode

1. Click the **Preview** button (or press `P`)
2. Click buttons to trigger their actions
3. Watch elements show/hide based on variable conditions
4. Click **Reset** to restore default variable values
5. Click **Stop** (or press `Escape`/`P`) to exit

### Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `P` | Toggle preview mode |
| `Escape` | Exit preview mode / Deselect element |
| `Delete` / `Backspace` | Delete selected element |
| `Ctrl+Z` | Undo |
| `Ctrl+Y` | Redo |
| `Ctrl+C` | Copy selected element |
| `Ctrl+V` | Paste element |
| `Arrow Keys` | Nudge selected element by grid size |

### Save & Load

- **Auto-save**: Project automatically saves to browser localStorage
- **Export**: Click Export to download a `.json` file
- **Import**: Click Import to load a `.json` file
- On startup, you can continue an existing project or start fresh

## Example Project

See `examples/sample-menu.json` for a demo UI featuring:
- Main menu with Play, Settings, and Quit buttons
- Game mode selection panel (appears when Play is clicked)
- Settings panel (appears when Settings is clicked)
- Variable-driven visibility logic

To load the example:
1. Open UI Builder
2. Click **Import**
3. Select `examples/sample-menu.json`
4. Press **P** to enter preview mode and try clicking the buttons

## Future Enhancements (Not Yet Implemented)

- Unity export/import integration
- Custom fonts
- Animation previews
- More element types (sliders, toggles, input fields)
- Layer/group management
- Alignment tools
- Responsive layout options

## Browser Compatibility

Tested and works in:
- Google Chrome (recommended)
- Mozilla Firefox
- Microsoft Edge

## File Format

Projects are saved as JSON with the following structure:

```json
{
  "canvasWidth": 1920,
  "canvasHeight": 1080,
  "gridSize": 10,
  "elements": [...],
  "variables": [...],
  "nextElementId": 1
}
```

This format is designed to be easily parsed for future Unity integration.
