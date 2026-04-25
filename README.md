# Microgrid Hardware Description

![Microgrid Hardware Overview](Pics/Image.jpg)

A collection of power electronics PCB designs built to form a modular, sensor-rich microgrid testbed. Each converter module is designed with galvanic isolation for its power supply, onboard current sensing, and a communication interface (I2C / SPI) to stream real-time sensor data to an external MCU controller via an external ADC.

---

## Repository Structure

```
Microgrid_hardware_description/
├── Buck Converter/              # Isolated DC-DC step-down converter
├── Four Leg Inverter/           # 4-leg 3-phase + neutral-leg VSC
├── Line Commutated Converter/   # Thyristor-based AC-DC converter (LCC)
├── Neutral Point Clamp/
│   ├── Gate Driver Module/      # Isolated gate driver board for NPC
│   └── NPC/                     # 3-phase Neutral Point Clamped inverter
└── Three Leg Inverter/          # 3-phase 2-level Voltage Source Converter (VSC)
```

Each sub-project is a self-contained **Altium Designer** project (`.PrjPcb`) and contains:
| File type | Description |
|---|---|
| `.SchDoc` | Schematic sheet(s) |
| `.PcbDoc` | PCB layout |
| `.PrjPcbStructure` | Altium project panel structure |

---

## Modules

### Buck Converter
A DC-DC step-down converter providing isolated auxiliary power to the converter boards. Includes a current sensor sub-schematic for output current monitoring.

### Three Leg Inverter (VSC)
A standard 3-phase, 2-level Voltage Source Converter. Contains dedicated schematics for:
- Gate driver circuitry (`GateDriver.SchDoc`)
- Phase current sensing (`Current_Sensor.SchDoc`)
- PWM pulse generation interface (`Pulse_Generator.SchDoc`)

### Four Leg Inverter
Extension of the 3-leg VSC with an additional neutral leg for unbalanced or single-phase load support. Same modular sub-schematic structure.

### Line Commutated Converter (LCC)
A thyristor-based (phase-controlled) AC-DC rectifier. Includes gate driver and pulse generator schematics for firing-angle control.

### Neutral Point Clamp (NPC)
A 3-phase, 3-level NPC inverter split across two sub-projects:
- **Gate Driver Module** — isolated gate drive board designed to interface with the NPC switches.
- **NPC** — main inverter board with current sensing and pulse generator.

---

## Key Design Features

- **Isolated gate driver supply** — galvanic isolation is achieved by running a 100 kHz half-bridge inverter on the control side to generate a high-frequency AC pulse, passing it through a small transformer, and then rectifying the output to produce an isolated DC rail for each gate driver. This keeps the high-voltage power stage fully isolated from the control circuitry, improving noise immunity and safety.
- **Sensor-rich** — onboard current sensors and voltage sensors on every converter allow real-time monitoring of all the important variables on each board.
- **External ADC interface** — sensor signals are connected to an external ADC and the data then is sent to the MCU over **I2C / SPI** connection, enabling high-resolution, synchronised data acquisition.
- **Modular architecture** — gate driver, current sensor, and pulse generator circuits are implemented as reusable schematic sheets across all projects.

---

## Tools & Requirements

| Tool | Version |
|---|---|
| Altium Designer | 20 or later (recommended) |

---

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/Rasoolpey/Microgrid_hardware_description.git
   ```
2. Open the desired sub-project by opening its `.PrjPcb` file in Altium Designer.
3. All schematic sheets and the PCB layout will load automatically via the project panel.

---

## License

This project is currently unlicensed. Contact the author before using or redistributing any design files.

