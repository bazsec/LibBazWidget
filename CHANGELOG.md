# LibBazWidget-1.0 Changelog

## 001 - Initial Release
- Standalone widget registry library using LibStub
- Publisher API: `RegisterWidget(widget)`, `UnregisterWidget(id)`
- Consumer API: `GetWidgets()`, `GetWidget(id)`, `RegisterCallback(fn)`
- Enables two-sided ecosystem: any addon can publish widgets, any addon can host/display them
- No WoW frames, events, or saved variables — pure data registry
- LibStub handles version negotiation when multiple addons embed the library
