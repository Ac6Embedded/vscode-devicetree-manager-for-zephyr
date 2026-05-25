# Change Log

All notable changes to the "devicetree-manager-for-zephyr" extension will be
documented in this file.

Check [Keep a Changelog](http://keepachangelog.com/) for recommendations on how
to structure this file.

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
