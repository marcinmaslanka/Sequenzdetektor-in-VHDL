# 🔁 Sequence Detector (VHDL) – Simulation and Verilog Conversion

This project implements a **BCD-based sequence detector** in VHDL. Upon detecting the specific input sequence:

"0011" → "0010" → "0001" → "0000"

it triggers a **12-bit serial output pattern**: `110010001010`.

The design features:
- Finite State Machine (FSM)
- Timer-based control
- Bit-serial output

---

## 🧠 Entity: `sd`

### 📌 Ports

| Name         | Direction | Width  | Description                       |
|--------------|-----------|--------|-----------------------------------|
| `clk`        | in        | 1 bit  | Clock input                       |
| `reset`      | in        | 1 bit  | Asynchronous reset                |
| `bcd_in`     | in        | 4 bits | BCD input for sequence detection  |
| `detected`   | out       | 1 bit  | High when sequence is detected    |
| `serial_out` | out       | 1 bit  | 12-bit pattern output (serial)    |

### 🧩 Design Highlights

- **FSM** with 5 states: `S0` → `S4`
- **Sequence Detection Logic** based on BCD input
- **12-bit Serial Output**: `110010001010`
- **Timer** to control output duration

---

## 🧪 Simulation with GHDL & GTKWave

### 🌀 1. Analyze and Elaborate the Design

```bash
ghdl -s sd.vhdl
ghdl -s sd_tb.vhdl
ghdl -a sd.vhdl
ghdl -a sd_tb.vhdl
ghdl -e sd_tb
```

### ▶️ 2. Run the Simulation
```
ghdl -r sd_tb --vcd=sd.vcd --stop-time=1ms
```

### 📈 3. View the Waveform in GTKWave
```
gtkwave sd.vcd
```

## 🔀 Convert VHDL to Verilog using GHDL + Yosys
🚀 1. Launch Yosys
```
yosys
```

### 🧙‍♂️ 2. In the Yosys shell, enter:
```
ghdl -a sd.vhdl
ghdl synth --out=verilog sd > sd.v
```

This creates a Verilog equivalent of the VHDL module in sd.v.

💡 I recommend creating a new directory for the Verilog files, for example:
/foss/designs/SKY/sd/verilog
Place your converted file and Verilog testbench in that folder.

✅ Verify the Converted Verilog Code
```bash
iverilog -o sd_tb.vvp sd_tb.v sd.v
vvp sd_tb.vvp
gtkwave sd_tb.vcd
```
This allows you to check for any ambiguity between the VHDL and Verilog versions.

🏗️ Synthesis and Layout with OpenLane2
1. Create Project Directory
bash
Kopieren
Bearbeiten
mkdir -p /headless/OpenLane/designs/sd
Copy the following files into the new directory:

sd.v

config.json

2. Run the Flow
From your project directory:

bash
Kopieren
Bearbeiten
openlane config.json
After ~2 minutes, the flow will be completed.

🔍 How to View Results
🔌 Power Report
bash
Kopieren
Bearbeiten
/headless/OpenLane/designs/sd/runs/RUN_2025-04-13_08-27-15/54-openroad-stapostpnr/nom_tt_025C_1v80/power.rpt
⏱️ Static Timing Analysis (STA)
bash
Kopieren
Bearbeiten
/headless/OpenLane/designs/sd/runs/RUN_2025-04-16_20-31-21/54-openroad-stapostpnr/nom_tt_025C_1v80/sta.log
📐 Core and Die Area
bash
Kopieren
Bearbeiten
/headless/OpenLane/designs/sd/runs/RUN_2025-04-13_08-27-15/13-openroad-floorplan/openroad-floorplan.log
🧱 Layout (GDS File)
bash
Kopieren
Bearbeiten
cd /headless/OpenLane/designs/sd/runs/RUN_2025-04-13_08-27-15/final/gds
klayout sd.gds
🔥 Heatmap (GUI)
bash
Kopieren
Bearbeiten
cd /headless/OpenLane/designs/sd/runs/RUN_2025-04-13_08-27-15/final/odb
openroad -gui


---

Feel free to use, modify, and share.
