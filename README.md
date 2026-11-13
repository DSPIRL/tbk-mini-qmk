# Preface
- You will most likely want/need to build the QMK firmware at least once to flash the keyboard if you want to enable configuration through the web browser vs always building the firmware locally.
- This keymap is built with [Argos](https://docs.bastardkb.com/fw/argos.html), so after flashing it the keyboard can be configured in the browser at https://argos.bastardkb.com (Chromium based browsers are best for this) without rebuilding.
- A prebuilt firmware is included: `bastardkb_tbkmini_splinktegrated_rev1_argos.uf2`. Rebuild it after changing any of the files below.
- Before flashing the firmware see below...
> https://docs.bastardkb.com/fw/flashing.html

# Flashing
- The **right** half is the one plugged into USB (`MASTER_RIGHT`). Plugging in the left half on its own makes both halves think they are the other side.
- Flash both halves with the same `.uf2`, each plugged in on its own: double-tap the reset button (or press `QK_BOOT`) so the `RPI-RP2` drive appears, then drag the `.uf2` onto it.
- To clear the saved settings (EEPROM), hold **Del** (top outer key of the right half) while plugging in the right half. For the left half, hold **Tab** while plugging the USB cable into the right half.

# File descriptions
- `config.h` is where you can set various QMK variables.
> https://docs.qmk.fm/config_options#the-config-h-file
- `rules.mk` holds variables like the `VIA_ENABLE` variable that can enable support for flashing keyboard firmware through the VIA QMK configuration website. This is currently enabled with `VIA_ENABLE = yes`, which Argos also requires.
> https://caniusevia.com/
> https://docs.qmk.fm/getting_started_make_guide#rules-mk-options
- `keymap.c` is the where you create macros and keyboard layers.
> https://docs.qmk.fm/newbs_building_firmware#open-keymap-c-in-your-favorite-text-editor
- `keymap.json` enables the `bastardkb/argos` community module. It only lists modules; the layers stay in `keymap.c`.
- Argos sets 8 layers and manages combos, tap dances and tapping terms itself, so settings made in Argos can override `TAPPING_TERM` in `config.h`.

# More useful resources.
For checking keycodes:
- https://www.toptal.com/developers/keycode

For seeing the default keymap (this isn't the current keymap):
- https://docs.bastardkb.com/fw/default-keymaps.html#tbk-mini

The default `keymap.c`:
- https://github.com/Bastardkb/qmk_userspace/blob/main/keyboards/bastardkb/tbkmini/keymaps/vendor/keymap.c

Web configuration:
- https://docs.bastardkb.com/fw/argos.html#what-is-argos






# Building
(if you build your own firmware this is good to know, it's also covered in the docs somewhere)
Argos is a QMK community module, so the firmware is built with the Bastard Keyboards QMK fork and their QMK userspace.
1. Clone the fork with its submodules: `git clone --recurse-submodules https://github.com/Bastardkb/bastardkb-qmk.git`
2. Clone the userspace with its submodules (this brings in the Argos module): `git clone --recurse-submodules https://github.com/Bastardkb/qmk_userspace.git`
3. Point QMK at the userspace: `qmk config user.overlay_dir="$(realpath qmk_userspace)"`
4. Copy `config.h`, `keymap.c`, `keymap.json` and `rules.mk` from this repo into `qmk_userspace/keyboards/bastardkb/tbkmini/keymaps/argos/`
5. From inside the `bastardkb-qmk` folder, build: `qmk compile -kb bastardkb/tbkmini/splinktegrated_rev1 -km argos`
- The fork maps `bastardkb/tbkmini/v2/splinky_3` to `bastardkb/tbkmini/splinktegrated_rev1`, which is why the firmware has that name.

