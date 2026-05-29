# BT60 V2 — ZMK Config

A clean ZMK config for the Polarity Works **BT60 V2**. It uses the board definition
straight from mainline ZMK, so there are **no board files to maintain here** — only
your keymap and settings.

## Files

```
config/
  west.yml      # tells the build to pull ZMK (which already contains the bt60 board)
  bt60.keymap   # your layout + where debounce goes
  bt60.conf     # firmware on/off settings (sleep, battery, RGB, backlight)
build.yaml      # says "build the bt60 board"
.github/workflows/build.yml   # runs the build on every push
```

## How to use

1. Create a **new, empty** GitHub repository.
2. Upload these files, keeping the folder structure exactly as above.
3. Go to the **Actions** tab and enable workflows if prompted.
4. Every push triggers a build. When it finishes, open the build run and download
   **`firmware`** from the **Artifacts** section at the bottom — that zip contains
   your `zmk.uf2`.
5. Put the keyboard in bootloader mode (double-tap reset) and drag `zmk.uf2` onto it.

## Common edits

- **Change the layout:** in `bt60.keymap`, uncomment one of `ANSI` / `ISO` / `ALL_1U` /
  `HHKB` at the top (ANSI is the default).
- **Change keys:** edit the `bindings` in `bt60.keymap`.
- **Debounce:** uncomment the `&kscan0 { ... }` block near the top of `bt60.keymap`
  (default is 5 ms; lower for snappier, higher if you get double-presses).
- **RGB / backlight:** uncomment the relevant lines in `bt60.conf`.

You never pick between the `1_0_0` and `2_0_0` revision files — those live upstream and
the build auto-selects V2 for you because that's the board's default revision.
