# Modular LED Lighting Tiles

Modular decorative LED tiles in multiple shapes (hex, square, triangle...) sharing one PCB design. Tiles connect edge-to-edge to share power and sync lighting effects across a network.

## Overview

Each tile is an independent, battery-powered LED node built around an ESP32-C3, with USB-C charging and a shared power/data bus that lets tiles connect edge to edge. Tiles can pull power from and push power to their neighbors, so a single plugged-in tile can charge several unpowered neighbors at once. The same PCB design drops into enclosures of different shapes (hexagon, square, triangle, pentagon, circular), so the electronics are built once and reused across every form factor.

**Key design points:**
- **Priority power management:** a hardware power mux automatically prefers wired USB power over battery, with no firmware involvement, so LEDs always run off wired power when it's available and switch to battery seamlessly when it's not.
- **LiFePO4 battery charging:** a dedicated charger IC handles battery charging independently of the tile's own power draw, so charging doesn't compete with LED brightness for current budget.
- **Tile-to-tile mesh network:** tiles discover their neighbors automatically over a UART mesh, elect a master per connected group ("island"), and stream synchronized lighting effects across the whole group enabling smooth cross-tile animations like spirals and waves that flow across tile boundaries.
- **Multi-island coordination:** each island's master connects over WiFi to a central coordinator, so multiple physically separate groups of tiles can be synced together.
- **Shape-agnostic PCB:** the same board and firmware work across every enclosure shape; only the physical tile body changes.

## Status

Schematic and PCB layout are complete (4-layer board, DRC clean). Not yet fabricated or bench-tested — feedback and review are very welcome before I send this off for manufacturing.

## Repo Structure
- **Electronics:**          KiCad project files for the shared PCB (schematic, layout, plots)
- **Enclosures:**           Mechanical designs for each tile shape (hexagon, square, triangle, etc.)
- **Docs:**                 Design notes, shared dimensions reference, process history

## View the PCB

The full schematic and PCB layout can be explored interactively (pan, zoom, toggle layers, click any trace to see its net) via KiCanvas:
PLACEHOLDERS
- [Schematic](https://kicanvas.org/?repo=https%3A%2F%2Fgithub.com%2FOA-Designs%2FLED-TILE%2Fblob%2Fa3d1c1e77a491de677230b5438bf334c2ac30740%2Felectronics%2Flighting-tile-pcb%2FLighting%2520Tile%2520Circuit%2520V3.kicad_sch)
- [PCB Layout](https://kicanvas.org/?repo=https%3A%2F%2Fgithub.com%2FOA-Designs%2FLED-TILE%2Fblob%2Fa3d1c1e77a491de677230b5438bf334c2ac30740%2Felectronics%2Flighting-tile-pcb%2FLighting%2520Tile%2520Circuit%2520V3.kicad_pcb)

## Design Process

This design went through several rounds of community feedback before reaching its current state — including a full rework of the power/charging circuit, switching to an external-antenna module for layout flexibility, and a move from 2 to 4 layers to resolve routing density. If you're curious about the reasoning behind specific decisions, feel free to open an issue or start a discussion.

## License

Licensed under [GNU GPL v3.0](LICENSE). Modifications and derivatives must remain open source under the same license.
