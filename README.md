# aka_walkman — ESP32-S3 Hi-Fi Audio Player

A portable, battery-powered hi-fi audio player built around the **ESP32-S3** and the
**Cirrus Logic CS43131** DAC/headphone amplifier, designed in **KiCad** on a custom PCB.
Firmware is planned with ESP-IDF / ESP-ADF and custom drivers.

## Features

- Stereo hi-fi playback to a 3.5 mm headphone jack (CS43131 DAC + integrated headphone amp, 24.576 MHz audio clock)
- Audio sources: microSD card, Bluetooth, (optionally) USB
- Single-cell (1S) Li-ion battery with USB-C charging and a fuel gauge
- Push-button power on/off with a hard power cut when off (LTC2954 controller)
- UI: Nokia 5110 LCD, rotary encoder with push switch, 4× Cherry MX keys + 2 tactile buttons
- USB-C with ESD protection and a CP2102N USB-UART bridge for flashing / debug

## Key components

| Function | Part |
|---|---|
| MCU | ESP32-S3-WROOM-2 (N32R16V: 32 MB flash / 16 MB PSRAM) |
| DAC / headphone amp | CS43131-CNZR |
| 1.8 V logic level translation (I²S / I²C) | TXU0204, PCA9306 |
| Battery charger | BQ25185 |
| Buck-boost 3.3 V rail | TPS63020 |
| 1.8 V LDOs (codec rails) | 3× LP5907MFX-1.8 |
| Fuel gauge | MAX17048G |
| Power on/off controller | LTC2954-1 |
| USB-UART | CP2102N |
| USB ESD | USBLC6-2SC6 |
| Display | Nokia 5110 (PCD8544) |
| Encoder | SIQ-02FVS3 |

Full BOM with LCSC part numbers: [`production/bom.csv`](production/bom.csv).

## Repository layout

```
aka_walkman.kicad_pro      KiCad project
aka_walkman.kicad_sch      Root schematic (MCU, USB, UI, SD card)
power.kicad_sch            Power sheet (charger, buck-boost, LDOs, fuel gauge, on/off)
Audio.kicad_sch            Audio sheet (CS43131, clock, level shifters)
aka_walkman.kicad_pcb      PCB layout
aka_walkman.kicad_dru      Custom design rules
libs/                      Project symbol / footprint / 3D libraries (easyeda)
datasheets/                Key datasheets
production/                Fabrication outputs (gerbers zip, BOM, CPL, IPC netlist)
```

## Opening the project

1. Open `aka_walkman.kicad_pro` in KiCad 9 or newer.
2. Project-local libraries are referenced from `libs/` via `sym-lib-table` / `fp-lib-table`.

## Manufacturing

Fabrication files in `production/` are generated with the KiCad *Fabrication Toolkit* plugin
(settings in `fabrication-toolkit-options.json`) for JLCPCB-style ordering.

## Status

Work in progress — hardware design stage.
