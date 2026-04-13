# LibBazWidget-1.0

Standalone widget registry library for World of Warcraft addons. Provides a publish/subscribe contract between **widget publishers** (any addon that creates a dockable widget) and **widget consumers** (any addon that hosts/displays widgets).

Think of it like LibDataBroker, but for dockable UI widgets instead of data feeds.

## Usage

### Publishers

```lua
local LBW = LibStub("LibBazWidget-1.0")

local myWidget = {
    id           = "myaddon_coolwidget",
    label        = "Cool Widget",
    frame        = myWidgetFrame,
    designWidth  = 200,
    designHeight = 80,
}

LBW:RegisterWidget(myWidget)
```

### Consumers (Hosts)

```lua
local LBW = LibStub("LibBazWidget-1.0")

-- Get all registered widgets
local widgets = LBW:GetWidgets()

-- Get a specific widget
local w = LBW:GetWidget("myaddon_coolwidget")

-- Listen for registry changes
LBW:RegisterCallback(function()
    -- A widget was added, removed, or re-registered
    MyHost:Reflow()
end)
```

## Widget Contract

| Field | Required | Description |
|-------|----------|-------------|
| `id` | Yes | Unique string identifier |
| `frame` | Yes | The Frame to parent into a host slot |
| `label` | No | Display label for title bars |
| `icon` | No | Texture path or atlas name |
| `designWidth` | No | Native width in pixels (host scales to fit) |
| `designHeight` | No | Native height in pixels (initial hint) |

### Optional Callbacks

| Method | Description |
|--------|-------------|
| `GetDesiredHeight()` | Host asks how tall the widget wants to be |
| `GetStatusText()` | Returns `text, r, g, b` for the title bar |
| `GetOptionsArgs()` | Returns AceConfig-style args table |
| `OnDock(host)` | Called when parented into a host slot |
| `OnUndock()` | Called when removed from a host slot |

## Installation

Install as a standalone addon, or embed in your addon's `Libs/` folder (standard LibStub pattern).

## License

GPL v2
