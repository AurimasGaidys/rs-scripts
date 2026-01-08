# Wasp Alcher Bot

A modular, well-structured alchemy bot for Old School RuneScape using WaspLib and SRL-T.

## 📁 Project Structure

The bot has been completely restructured into smaller, focused modules for better maintainability and organization:

```
alcher/
├── alcher.simba           # Main entry point and runner
├── types.simba            # Type definitions and enumerations
├── config.simba           # Configuration management
├── alchemyhandler.simba   # Core alchemy casting logic
├── helpers.simba          # Helper functions and initialization
├── actions.simba          # Bot action methods
├── statemachine.simba     # State determination logic
├── core.simba             # Main execution loop
├── gui.simba              # GUI components and interface
├── wasp_alcher.simba      # Legacy monolithic version (backup)
└── AlchHelper.simba       # Legacy helper file (backup)
```

## 🎯 Module Descriptions

### **types.simba**
Contains all type definitions:
- `EAlcherState`: State machine enumeration
- `TAlcher`: Main bot record
- `TRSAlchHandler`: Alchemy handler record

### **config.simba**
Manages configuration:
- Save/load item configurations
- Default item list management
- JSON configuration handling

### **alchemyhandler.simba**
Core alchemy logic:
- Item selection from inventory
- Spell casting with timing
- Profit tracking
- Magic spell overrides

### **helpers.simba**
Helper functions:
- Antiban setup
- Bot initialization
- Bank item setup

### **actions.simba**
Bot actions:
- Warning dialog handling
- Alchemy casting with error handling
- Script termination

### **statemachine.simba**
State determination:
- Analyzes game state
- Returns appropriate action state
- Handles banking, walking, casting

### **core.simba**
Main execution:
- Main bot loop
- State execution
- Antiban integration

### **gui.simba**
User interface:
- Alchemy item list management
- Item search functionality
- Add/remove item buttons
- Configuration interface

### **alcher.simba**
Main runner:
- Script metadata and ID
- GUI configuration form
- Script initialization
- Entry point

## ✨ Features

- **High/Low Alchemy Support**: Choose between high and low level alchemy spells
- **Smart Item Selection**: Automatically finds and alchs items from a configurable list
- **Profit Tracking**: Monitors GP profit from alchemy
- **Loss Prevention**: Option to prevent alching items at a loss
- **GE Walking**: Optional walking to Grand Exchange in Varrock
- **Banking Support**: Automatically banks for nature runes and coins
- **Collection Box**: Handles GE collection box for items
- **GUI Management**: Easy-to-use interface for managing alch items
- **Antiban**: Built-in antiban with random camera movements and actions

## 🚀 Usage

1. **Start the Script**: Run `alcher.simba` in Simba
2. **Configure Settings**:
   - Select alchemy spell (High/Low)
   - Enable loss prevention if desired
   - Enable GE walking for Varrock location
3. **Manage Alch List**:
   - Go to "Alchemy Settings" tab
   - Add items you want to alch from the item list
   - Remove items you don't want to alch
4. **Start Bot**: Click "Start" button

## 📋 Requirements

- Simba with SRL-T
- WaspLib
- Standard spellbook
- Nature runes in bank/inventory
- Coins in bank/inventory (for GE trades)
- Items to alch in inventory or bank

## 🎨 Modular Architecture Benefits

### **Maintainability**
- Each module has a single, clear responsibility
- Easy to locate and fix bugs
- Changes to one module rarely affect others

### **Readability**
- Smaller files are easier to understand
- Clear separation of concerns
- Well-documented code sections

### **Extensibility**
- Easy to add new features
- Modules can be enhanced independently
- New states can be added to state machine easily

### **Reusability**
- Alchemy handler can be used by other scripts
- GUI components can be copied to other bots
- Helper functions are modular and reusable

## 🔧 Development

### Adding New Items to Alch
Items can be added through the GUI or by modifying the default list in `config.simba`.

### Adding New States
1. Add state to `EAlcherState` enum in `types.simba`
2. Add state detection logic in `statemachine.simba`
3. Add state handling in `core.simba`
4. Add required action methods in `actions.simba`

### Modifying GUI
All GUI components are in `gui.simba`. The main configuration form is in `alcher.simba`.

## 📝 Notes

- Keep the alch item list short for better performance
- The bot uses WaspLib's banking and walking systems
- Profit calculation uses ItemData API for alch values
- Timer delays prevent spam clicking (3s for low alch, 5s for high alch)

## 🐛 Troubleshooting

**Bot won't cast alchemy:**
- Check you're on Standard spellbook
- Ensure you have nature runes
- Verify items are in the alch list

**Can't find items:**
- Check item names match exactly (case-sensitive)
- Verify items are in inventory or bank
- Check the alch list in GUI

**Banking issues:**
- Ensure you're near a bank or GE
- Check bank has nature runes and coins
- Verify WalkGE setting matches your location

## 📜 Version History

**v41** (Current)
- Complete modular restructure
- Separated into 9 focused files
- Improved code organization
- Enhanced maintainability

## 👨‍💻 Credits

Original script by Wasp (WaspLib)
Modular restructure: 2026

---

**Happy Alching! 🔥✨**
