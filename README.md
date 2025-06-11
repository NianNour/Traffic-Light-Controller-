# 🚦 VHDL Traffic Light Controller

This project implements a **traffic light controller** using VHDL for a highway and a farm road intersection. The system reacts to a vehicle sensor on the farm road and manages light transitions using a finite state machine (FSM).

---

## 🧠 Overview

- ✅ Designed for use in FPGA or CPLD environments.
- 🕒 Uses a clocked process to handle light changes over time.
- 🚗 Prioritizes **highway traffic** unless a car is detected on the **farm road**.
- 📟 Simple FSM with three states: `Green`, `Yellow`, and `Red`.

---

## 🔧 Inputs & Outputs

### 🔁 Inputs:
- `clock`: System clock (used for timing)
- `reset`: Asynchronous reset signal
- `sensor`: High when a vehicle is detected on the farm road

### 🔀 Outputs:
- `highway_light`: Controls the light for the highway (1 = Green/Yellow, 0 = Red)
- `farm_light`: Controls the light for the farm road (1 = Green, 0 = Red)

---

## ⚙️ How It Works

### FSM States:
- **Green**:
  - `highway_light` is green (`'1'`)
  - `farm_light` is red (`'0'`)
  - If `sensor = '1'`, transitions to `Yellow`

- **Yellow**:
  - Highway light stays yellow for 3 clock cycles (`yellow_duration`)
  - Prepares to transition to `Red`

- **Red**:
  - `farm_light` turns green for 10 clock cycles (`red_duration`)
  - Afterward, transitions back to `Green` state

### Reset Behavior:
- On `reset = '1'`, the controller resets to `Green` state with `counter = 0`

---

## 🧪 Simulation/Test Ideas

To test this design in simulation:
- Provide a clock with a known frequency
- Toggle the `sensor` signal and observe state transitions
- Test `reset` to verify the controller returns to initial state

---

## 📁 File Structure

- `TrafficLightController.vhdl` – Main VHDL module implementing the FSM-based controller

---

## 🛠️ Tools You Can Use

- **ModelSim** / **GHDL** – For simulation
- **Quartus** / **Vivado** – For synthesis on FPGA boards

---

## 🧱 Future Improvements

- Add `Yellow` state output as a separate signal
- Parameterize durations using generics
- Add timer resolution scaling for real-world timing

