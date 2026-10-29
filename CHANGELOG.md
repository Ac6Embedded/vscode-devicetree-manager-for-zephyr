# Change Log

All notable changes to the "devicetree-manager-for-zephyr" extension will be
documented in this file.

Check [Keep a Changelog](http://keepachangelog.com/) for recommendations on how
to structure this file.

## [1.3.2]
- Added the Clocks view: the **Pins | Clocks** toggle at the top of the chip card shows the clock
  tree, every clock with its frequency and the peripherals that run on it. Dividers, multipliers and
  clock sources are changed in place, and the frequency Zephyr reads (`clock-frequency`) is kept in
  step. Frequencies are checked against the chip's datasheet limits and the vendor's rules. Covered:
  STM32 (most series), Renesas RA and RA0, Silicon Labs Series 2 and 3, NXP Kinetis KE1x.
- Added NXP Kinetis, S32K1 and LPC (LPC51U68, LPC54114, LPC55), and Microchip SAM and PIC32C boards
  to the pin configurator.
- Added ADC and DAC channels (DAC from Zephyr 4.4): a channel is added by picking its pin, with
  settings the driver accepts, and **Use in app** lists it in `/zephyr,user` `io-channels`.
- Added PWM outputs: a `pwms` property opens as a table (the pin by name, the period, the
  polarity), and each PWM controller gets an **Outputs** tab.
- The Functions panel is now part of the Pins view: it opens when a pad is clicked and folds to a
  rail. The Chip / List toggle moved to the chip card's search row.
- An application that is not built yet now says "Build the application first", and opens by itself
  once the build is done.
- A custom board now finds its pin file from its SoC (an ESP32 board named after another variant no
  longer gets the wrong chip).
- Overlay changes that are already built no longer show as "unbuilt".
- The IRQ line in the interrupts table is now read only, as the hardware sets it. The raw view still
  edits every cell.

## [1.3.1]
- Added Infineon boards to the pin configurator: PSoC 6, PSoC 4, PSoC Control C3, CYW20829,
  XMC7000 / TRAVEO T2G and PSoC Edge, plus XMC4500 and XMC4700. A function Zephyr does not
  predefine gets a pin node in the overlay, with Infineon's default drive mode; an XMC4 input also
  sets its peripheral's input selector.
- Added GPIO handling: pins used through `*-gpios` properties (LEDs, buttons, chip selects, reset
  lines) show on the chip in violet, with a warning when a pin also goes to a peripheral or to
  another GPIO.
- Each GPIO property opens as a table in the node editor: the pin by name, the active level, pull
  and drive. A GPIO property that is not set takes a pin from its table (**Pick a pin…**) or from
  the pin (**GPIO** in the Functions card). The overlay includes Zephyr's GPIO flags header.
- NXP MCX A boards (FRDM-MCXA156 and others) now show their pins.

## [1.3.0]
- Added Renesas RA and RA0 boards to the pin configurator: chip view, pin functions and overlay
  generation, written with Zephyr's own `RA_PSEL(...)` macros.
- Renesas pin data is installed once from the chip area (**Install**, about 14 MB, from
  [pinmapping-renesas](https://github.com/Ac6Embedded/pinmapping-renesas), which follows Renesas FSP
  releases). Newer versions are offered with **Update** when a chip is missing, and at most once a
  week in a notification.
- Board pin settings that a Renesas chip does not offer are shown as "not offered" functions with a
  warning, so they can be found and removed.
- Requires VS Code 1.88 or newer.

## [1.2.0]
- Added Zephyr Sysbuild support: the manager now opens a sysbuild build directory by resolving its
  default (or MAIN) image, with an **Image** selector to inspect other images such as mcuboot on
  multi-image builds.
- Overlay writes now target the file the build actually consumed instead of always composing
  `boards/<board>.overlay`, fixing qualified/multicore board targets and no longer unhooking
  `app.overlay`-based projects.

## [1.0.14]
- Renamed the **Export Custom Build as Task** action and added a `tasks.json` hint on hover.

## [1.0.13]
- Added a custom build-directory source mode with task automation, so the panel can open directly on
  a build directory.
- Added property-gated UART pinctrl validation (single-wire, hardware flow control).
- UI copy cleanup.

## [1.0.12]
- Maintenance release (packaging/republish); no functional changes.

## [1.0.11]
- Internal tooling and documentation only; no user-facing changes.

## [1.0.10]
- Editable resolved-interrupts table and a raw/resolve toggle in the Node Detail / reg editors.
- Phandle values shown as navigable node chips, with inline editing and autocomplete for raw phandles.
- "Pads" button on pinctrl rows even without an auto-match; Silabs timer/letimer pinctrl linked to the
  pwm child node; assorted fixes.

## [1.0.9]
- Help tooltip with full property and node descriptions; always-available `/zephyr,user` node with
  free-form properties.
- Resolved-node view for single-phandle properties; group-style pinctrl cell edits now reflected in
  the views.
- Not-okay nodes tinted red in the status row; load/perf fixes.

## [1.0.8]
- Assign and surface pins on unconfigured and disabled peripherals.
- Function-card breadcrumb lists every bound signal; pin-configurator search highlights matching
  function chips.

## [1.0.7]
- Overlay reads/writes confined to a managed comment region.
- Single recursive merge engine that preserves a node's other properties.
- No default pad selection; click empty space to deselect.

## [1.0.6]
- Beta notice banner with a feedback link.
- Unbuilt overlay changes reflected in the views, with smarter overlay deletes and label-less node
  generation.

## [1.0.5]
- Decoupled ADC child-naming from the pinctrl architecture.
- Fixed the Functions card auto-opening on pad right-click.

## [1.0.4]
- Added the Silicon Labs Series 2 (DBUS) pinctrl backend.
- Multi-group staging, cross-vendor validation, and visible Generate errors.
- Structural `&pinctrl` child-node merges and overlay-drift fixes.

## [1.0.3]
- Resolve the devicetree adapter's Python from the build's own `WEST_PYTHON`.

## [1.0.2]
- Depth-aware overlay-drift detection against the full child tree.
- Auto-stage parent `#address-cells` / `#size-cells` when adding reg-bearing children.
- Centralised devicetree property formatting.

## [1.0.1]
- First Marketplace-ready packaging: proprietary EULA, marketplace logo and screenshot, and the
  **Issues** link routed to the Zephyr Workbench tracker.

## [0.1.0]

Initial release. Companion to the Zephyr Workbench extension.

### Devicetree Manager
- Visual editor for the devicetree of the application + build configuration selected in the Workbench. Open it from the Zephyr Workbench shortcut tree under **Devicetree Manager**, or from the command palette with **Devicetree Manager: Open**.
- Vendor-themed chip canvas with every pad and every alternate function it can carry. Click a pin to stage an assignment; the panel writes the right pinctrl edit for your vendor.
- Devicetree node list grouped by binding category, with status toggles, binding-typed property editors, `/chosen` and `/aliases` support, and per-node detail tabs (Channels, Groups, Pin Groups, Regions).
- Staged changes and detected issues live in one bar. A **Generate** action writes (or per-property merges into) `boards/<board>.overlay`, preserving any hand-edited block, and reminds you to rebuild when the overlay carries changes the current build has not picked up yet.

### Requirements
- The Zephyr Workbench extension (`Ac6.zephyr-workbench`), version 3.1.0 or later. The Workbench supplies the Zephyr application list, single-application lookup, and the configured Zephyr venv.
- A Python interpreter with `edtlib` available (typically the same venv the Workbench is configured against).
