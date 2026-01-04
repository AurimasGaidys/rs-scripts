# SuperHeater - Modular Architecture

A professional, well-architected OSRS bot script for automatically casting the Superheat Item spell to create bars from ores.

## 📁 Project Structure

```
superHeater/
├── superheater.simba    # Main entry point - Run this file
├── config.simba         # Configuration settings and constants
├── types.simba          # Type definitions and enums
├── helpers.simba        # Helper functions and method overrides
├── core.simba           # Core initialization and item setup
├── actions.simba        # Action methods (casting, banking, etc.)
├── statemachine.simba   # State management logic
├── runner.simba         # Main execution loop
├── gui.simba            # GUI configuration interface
└── README.md            # This file
```

## 🏗️ Architecture Overview

The script has been split into **8 modular files**, each with a specific responsibility:

### 1. **config.simba** - Configuration Hub
- Script metadata (ID, revision)
- Bar type constants
- Global settings (mouse speed, coal bag usage, GUI toggle)
- Cast attempt reset threshold
- Rune type configuration

### 2. **types.simba** - Type Definitions
- `EState` enumeration (script states)
- `TSuperHeater` record (main script class)
- `TSuperHeaterConfig` record (GUI configuration class)

### 3. **helpers.simba** - Utility Functions
- `GetOreQuantity()` - Calculates ore amounts based on coal bag usage
- `Inventory.ClickItem()` override - Improved inventory interaction
- `TAntiban.Setup()` override - Custom antiban configuration

### 4. **core.simba** - Core Functionality
- `TSuperHeater.SetupItems()` - Configures ores/bars for selected type
- `TSuperHeater.Init()` - Initializes script with validation
- `TSuperHeater.HasRequiredItems()` - Checks inventory for materials
- `TSuperHeater.SafeBankOpen()` - Opens bank safely
- `TSuperHeater.Terminate()` - Cleanup on script end

### 5. **actions.simba** - Action Methods
- `TSuperHeater.CastSpell()` - Executes spell casting
- `TSuperHeater.Deposit()` - Deposits bars and cleans inventory
- `TSuperHeater.WithdrawMaterial()` - Withdraws ores and runes
- `TSuperHeater.CollectRequiredItems()` - Handles collection box
- `TSuperHeater.CollectIfRequired()` - Manages collection box state

### 6. **statemachine.simba** - State Management
- `TSuperHeater.HandleActivity()` - Manages completion/level-ups
- `TSuperHeater.HandleBank()` - Determines bank actions
- `TSuperHeater.HandleCollects()` - Determines collection actions
- `TSuperHeater.GetState()` - Main state machine logic

### 7. **runner.simba** - Execution Loop
- `TSuperHeater.Run()` - Main loop that coordinates everything

### 8. **gui.simba** - User Interface
- `TSuperHeaterConfig.StartScript()` - Captures user settings
- `TSuperHeaterConfig.Run()` - Creates configuration GUI

## 🚀 How to Run

1. **Load the main file**: Open `superheater.simba` in Simba
2. **Configure settings**: The GUI will appear with options
3. **Select bar type**: Choose from dropdown (Bronze, Iron, etc.)
4. **Enable coal bag** (optional): For Steel/Mithril/Adamantite/Runite
5. **Click Start**: Script begins execution

## 🎯 Supported Bar Types

| Bar Type   | Primary Ore    | Secondary Ore | Coal Bag Benefit |
|------------|----------------|---------------|------------------|
| Bronze     | Tin (13)       | Copper (13)   | No               |
| Iron       | Iron (27)      | None          | No               |
| Silver     | Silver (27)    | None          | No               |
| Steel      | Iron (9/17)    | Coal (18/∞)   | **Yes**          |
| Gold       | Gold (27)      | None          | No               |
| Mithril    | Mithril (5/10) | Coal (20/∞)   | **Yes**          |
| Adamantite | Adam. (3/7)    | Coal (18/∞)   | **Yes**          |
| Runite     | Runite (3/5)   | Coal (24/∞)   | **Yes**          |

*Note: Numbers show (without coal bag / with coal bag)*

## ⚙️ Configuration Options

Edit `config.simba` to customize:

```pascal
CurrentTask: string = 'Iron';           // Default bar type
USE_COALBAG: Boolean = False;           // Enable coal bag
USE_GUI: Boolean = True;                // Show configuration GUI
MOUSEOVERRIDE: Int32 = 13;              // Mouse speed
CastAttemptReset: Integer = 3;          // Failed casts before banking
CastRune: String = 'Nature rune';       // Rune type for casting
```

## 📋 Requirements

- **Simba** with SRL-T and WaspLib installed
- **OSRS Client** in FIXED mode
- **Level 43 Magic** (Superheat Item spell unlocked)
- **Nature runes** (or Fire runes with Bryophyta staff)
- **Ores** in bank
- **Optional**: Coal bag for higher tier bars

## 🛠️ Extending the Script

The modular design makes it easy to:

### Add a new bar type:
Edit `core.simba` → `SetupItems()` method

### Modify state logic:
Edit `statemachine.simba` → `GetState()` method

### Add new actions:
Create methods in `actions.simba`

### Customize UI:
Edit `gui.simba` → `Run()` method

### Change configuration:
Edit `config.simba` constants

## 🔍 Troubleshooting

**Script won't start:**
- Ensure OSRS client is in FIXED mode
- Check brightness is at maximum (script auto-adjusts)

**Spell casting fails:**
- Verify you have sufficient runes
- Check you have the required Magic level (43)
- Ensure ores are visible in bank without scrolling

**Coal bag not working:**
- Enable the checkbox in GUI
- Only works for Steel/Mithril/Adamantite/Runite

## 📝 Developer Notes

### Why This Architecture?

**Separation of Concerns**: Each file has one clear responsibility
**Maintainability**: Easy to find and fix bugs
**Extensibility**: Simple to add new features
**Readability**: Well-documented with clear function names
**Testability**: Individual modules can be tested independently

### File Dependencies

```
superheater.simba (entry)
    ↓
    ├─ config.simba (no dependencies)
    ├─ types.simba (depends on: config)
    ├─ helpers.simba (depends on: types)
    ├─ core.simba (depends on: types, helpers, config)
    ├─ actions.simba (depends on: types, core, config)
    ├─ statemachine.simba (depends on: types, core)
    ├─ runner.simba (depends on: all above)
    └─ gui.simba (depends on: types, config)
```

## 📄 License

Original script by WaspScripts community. Refactored into modular architecture for improved maintainability.

---

**Version**: 8  
**Last Updated**: 2026  
**Architecture**: Master Architect Design Pattern
