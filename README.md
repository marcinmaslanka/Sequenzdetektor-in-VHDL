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

### 📁 Files
File | Description
- sd.vhdl | Main sequence detector (VHDL)
- sd_tb.vhdl | Testbench for simulation (user-provided)
- sd.vcd | Simulation waveform for GTKWave
- sd.v | Generated Verilog file

### 📜 License
MIT License – Feel free to use, modify, and share.
