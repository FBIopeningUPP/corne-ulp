# AERIX-ULP ZMK firmware

This ZMK configuration is for testing one keyboard half:

- 4 matrix rows
- 6 matrix columns
- Bluetooth advertising
- A single default keymap

The GPIO assignments in
[`config/boards/shields/aerix_ulp/aerix_ulp.overlay`](config/boards/shields/aerix_ulp/aerix_ulp.overlay)
are temporary. Replace them with the final E73 GPIO mapping after the
schematic is corrected.

The build targets Zephyr's `nrf52dk_nrf52832` board until the custom E73 board
definition is complete. Check the board target and GPIO map before flashing.

## Build with GitHub Actions

Push a commit or open a pull request. The workflow in
`.github/workflows/build-zmk.yml` builds the `aerix_ulp` shield and uploads the
firmware artifacts.

## Local build

Clone ZMK and initialize a west workspace, then point the build at
`firmware/config`:

```text
west init -m https://github.com/zmkfirmware/zmk.git
west update
west build -s app -d build/aerix_ulp -- \
  -DZMK_CONFIG=<path-to-corne-ulp>/firmware/config \
  -DBOARD=nrf52dk_nrf52832 \
  -DSHIELD=aerix_ulp
```

Flash the resulting `.hex` or `.uf2` over SWD using the procedure in the main
[README](../README.md).
