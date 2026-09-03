# TOTEM - ZMK Firmware

ZMK firmware for the **TOTEM**, a 38-key split column-staggered keyboard,
with ZMK Studio for editing the keymap without reflashing.

## Specifications

| | |
|---|---|
| Layout | Split column-staggered 3×5 + 3 thumbs + 1 outer key per half (38 keys) |
| Switches | Kailh Choc (low profile) |
| Controller | Seeed XIAO nRF52840 (BLE) |
| Connection | Bluetooth LE or USB-C |
| Firmware | ZMK v0.3 |

## Layers

| Layer | How to reach it |
|---|---|
| **BASE** | default — QWERTY |
| **LOWER** | hold the left inner thumb — numbers, arrows, clipboard, media |
| **RAISE** | hold the right inner thumb — symbols |
| **ADJUST** | hold LOWER **and** RAISE — Bluetooth, F-keys, reset |

### Base layer

```
╭────┬────┬────┬────┬────╮   ╭────┬────┬────┬────┬────╮
│ Q  │ W  │ E  │ R  │ T  │   │ Y  │ U  │ I  │ O  │ P  │
├────┼────┼────┼────┼────┤   ├────┼────┼────┼────┼────┤
│ A  │ S  │ D  │ F  │ G  │   │ H  │ J  │ K  │ L  │ ;  │
├────┼────┼────┼────┼────┤   ├────┼────┼────┼────┼────┤
│ Z  │ X  │ C  │ V  │ B  │   │ N  │ M  │ ,  │ .  │ /  │
╰────┴────┴─┬──┴─┬──┴─┬──╯   ╰─┬──┴─┬──┴─┬──┴────┴────╯
            │TAB │LOWR│SPC│ RET │RAIS│BSPC│
            ╰────┴────┴───┴─────┴────┴────╯
```

ESC sits on the outer left key, `'` on the outer right.

## ZMK Studio

The keymap is editable live from [ZMK Studio](https://zmk.studio/) over
USB, with no rebuild.

**The board boots locked.** Connect the **left half** by USB, open Studio,
and then **hold LOWER and press Z** to unlock it. Until you do, Studio can
connect and show the layout but cannot change anything — so a stray
connection can't rewrite your keymap. The lock returns on the next reboot.

Only the left half runs Studio: it is the split central, and the one that
exposes the RPC.

## Installing

Download `TOTEM-<version>.zip` from
[Releases](https://github.com/codekeeb/totem-zmk/releases). It has one
`.uf2` per half plus `settings_reset`.

1. Connect one half over USB.
2. **Double-tap the reset button.** It mounts as a USB drive (`XIAO-SENSE`).
3. Copy the matching `.uf2` onto it:
   - Left half → `totem_left-seeeduino_xiao_ble-zmk.uf2`
   - Right half → `totem_right-seeeduino_xiao_ble-zmk.uf2`
4. The drive unmounts on its own and the half reboots.
5. Repeat for the other half.

**Flash both halves.** They talk to each other, so mismatched firmware on
the two sides causes connection problems.

### If something goes wrong

Flash `settings_reset-seeeduino_xiao_ble-zmk.uf2` onto **both** halves the
same way. That wipes saved settings, Bluetooth pairings included. Then
flash the normal firmware again and re-pair.

## References

- [TOTEM hardware](https://github.com/GEIGEIGEIST/TOTEM)
- [TOTEM ZMK shield module](https://github.com/BildermanKawasaki/zmk-keyboard-TOTEM)
