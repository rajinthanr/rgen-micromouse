# 🐭 Open Source Micromouse Project

Welcome to the official repository of our **Open Source Micromouse** - a fast, intelligent, and compact maze-solving robot. This project aims to document every step of the design and development process, making it easy for students, hobbyists, and engineers to learn and contribute.

![Micromouse Design](Images/Final.jpg)

---

## 🚀 Project Goal

To design and develop a **four-wheel differential drive Micromouse robot** capable of solving mazes efficiently with smooth acceleration, encoder feedback, and intelligent path planning - while maintaining openness for community learning and contribution.

---

## 🧭 Table of Contents

- [🔍 Research & Reference Designs](#-research--reference-designs)
- [🧩 Component Selection](#-component-selection)
- [📐 Mechanical Design](#-mechanical-design)
- [⚙️ Drive System](#️-drive-system)
- [🔩 Drive System Assembly](#-drive-system-assembly)
- [🔌 Electronics & PCB Design](#-electronics--pcb-design)
- [📦 Firmware Development](#-firmware-development)
- [🖥️ Using the Mouse](#️-using-the-mouse)
- [🧠 Algorithms & Strategy](#-algorithms--strategy)
- [📸 Gallery](#-gallery)
- [📚 Resources](#-resources)
- [🤝 Contributing](#-contributing)
- [📜 License](#-license)
- [📬 Contact & Support](#-contact--support)

---

## 🔍 Research & Reference Designs

Before jumping into development, we explored multiple Micromouse designs, performance benchmarks, and open-source efforts.

- [Ukmars](https://ukmars.org/)
- [Greenye](https://youtube.com/@greenye?si=StKEDgfJgn1EC-rX) (Good YouTube channel)
- [Micromouse Online Handbook](https://micromouseonline.com/)
- [Speed Profile](https://micromouseonline.com/2017/08/03/micromouse-hard-acceleration/)

### 📄 Design Inspirations

- Green-Giant

*Reference images:*

| Reference Design 1 | Reference Design 2 |
|--------------------|--------------------|
| ![](Images/Green_Giant.png) | ![](Images/Green_Giant_V1.3.jpg) |

---

## 🧩 Component Selection

Every part was chosen with precision to balance performance, weight, and efficiency.

| Component | Description | Datasheet |
|----------|-------------|-----------|
| MCU | STM32F405 (ARM Cortex-M4) | [Datasheet](https://www.st.com/resource/en/datasheet/dm00037051.pdf) |
| Motors | Coreless Motor 1215 with quadrature magnetic encoders | [Buy](https://www.aliexpress.com/item/1005006009127311.html?spm=a2g0o.productlist.main.41.79802baa5jUvqW&algo_pvid=18bf682d-0367-49dd-b3c4-112c51e6d1a1&pdp_ext_f=%7B%22order%22%3A%229%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005006009127311%7C_p_origin_prod%3A) |
| Encoders | Built-in quadrature magnetic encoders | - |
| IMU | ICM-42688 | [Datasheet](https://invensense.tdk.com/download-pdf/icm-42688-p-datasheet/) |
| Sensors | TEFT4300 IR sensors with SFH4545 | [Datasheet](https://www.digikey.com/en/products/detail/vishay-semiconductor-opto-division/TEFT4300/1681175) |
| Power | 2S Li-Po 250mAh | [Buy](https://www.duino.lk/product/3-7v-220mah-25c-lipo-battery/) |

> 💡 *Includes datasheets for all components in the `Research/Datasheets` folder.*

---

## 📐 Mechanical Design

- Designed in [**Onshape**](https://www.onshape.com/)
- Lightweight 3D printable chassis
- Wheel size and placement optimized for turn radius

![Chassis render](Images/Design.png)

> 💡 *Includes STL files for all parts in the `Design/` folder.*

---

## ⚙️ Drive System

- **Differential drive** with PID-based velocity control
- Closed-loop motor control using encoders and gyro
- Acceleration curve implemented to avoid overshoot and wheel slippage

### Drive Tuning

- ✔️ Encoder and Gyro feedback integrated
- ✔️ PWM control through timer
- ✔️ Slew rate limiter for smooth turns

### Design Iterations

|V1|V2|V3|
|----|----|----|
|![](Images/Prototype_V1_2.jpg)|![](Images/PrototypeV2_3.jpg)|![](Images/PrototypeV3_3.jpg)|

### Drive System — Design Evolution

- Initial concept: single driven wheel per side - very simple and lightweight, but limited in traction, torque, and fault tolerance.  
- Iteration: switched to two wheels per side with proper gearing to share load, increase effective traction and torque, and add redundancy; gear ratio chosen for balanced acceleration and top speed.  
- Optimization: integrated motor mounts and trimmed mounting hardware to reduce space and mass; components repositioned to lower the center of gravity and simplify wiring and belt/gear routing.  
- Result: a compact, lightweight differential-drive assembly with improved performance, reliability, and manufacturability - documented trade-offs between complexity, weight, and available space.

---

## 🔩 Drive System Assembly

Tools required: screwdriver and some patience :)

### Components (extract)
1. Big gear and pins - harvested from an MG996R servo. You can either reuse the original gear pins or cut the servo screws and use those as compact pins (we need 4 of them).
2. Small gear - taken from an SG90 servo (we need 2 of them). 
3. O-Rings - find them at your local hardware shop.
4. All other structural parts - 3D printed (mounts, spacers).

### Step-by-step assembly
1. Prepare O-Rings, gears, and pins.  
2. Fit O-Ring into the 3D printed rim.  
3. Insert the pin/screw as shown in the figure.  
4. Install the small gear on its printed mount and verify axial alignment with the big gear. Adjust spacers as needed for proper backlash (~0.1–0.3 mm).  
5. Mount the motor.  
6. Assemble the two-wheel side: place the wheels with pins into the mount.  
7. Final check: rotate assembly by hand, verify smooth mesh, confirm no binding at extreme angles, and measure encoder counts while rotating to ensure correct coupling.

### Figures

<table>
   <tr>
      <td align="center"><img src="Images/Drive/MG996R_.jpg" alt="MG996R big gear & pins"/><br/><em>Fig 1 — Extracted MG996R big gear & pins</em></td>
      <td align="center"><img src="Images/Drive/SG90_.jpg" alt="Small gear from SG90"/><br/><em>Fig 2 — Small gear from SG90</em></td>
   </tr>
   <tr>
      <td align="center"><img src="Images/Drive/Gears.jpg" alt="Gear mounted in printed carrier"/><br/><em>Fig 3 — Gears, pins, rim, and O-Ring</em></td>
      <td align="center"><img src="Images/Drive/Assembly.jpg" alt="Pin inserted and secured"/><br/><em>Fig 4 — Pin inserted into the rim and spacer</em></td>
   </tr>
   <tr>
      <td align="center"><img src="Images/Drive/Drive_One_Side.jpg" alt="Side assembly with motor hub"/><br/><em>Fig 5 — Single side assembly</em></td>
      <td align="center"><img src="Images/Drive/Fully_Assembled.jpg" alt="Completed drive assembly (hand-checked)"/><br/><em>Fig 6 — Completed drive installation</em></td>
   </tr>
</table>

### Notes
- Keep gear mesh slightly loose to avoid binding under load.  
- If using servo screws as pins, file the screw heads flush and secure with a small dab of adhesive.  
- Document final spacer thicknesses for repeatable builds.

---

## 🔌 Electronics & PCB Design

Designed using [**EasyEDA**](https://easyeda.com) - a free tool for beginners. Our custom 2-layer PCB includes:

- STM32F405 MCU
- Power ICs
- Motor, encoder, and power connectors
- Motor drivers (DRV8833)
- Programming header (SWD)
- Debugging ports (UART)

| Design | Soldered |
|--------|----------|
| <img src="Images/PCB_1.png" height="600"/> | <img src="Images/PCB_2.jpeg" height="600"/> |

> 💡 *Includes relevant files in the `PCB/` folder.*
```bash
# PCB files and Gerbers:
PCB/
├── BOM.csv
├── micromouse.sch
└── gerbers/
```

---

## 📦 Firmware Development

### STM32CubeIDE Setup

#### 1. Prerequisites
- Download and install [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html) from STMicroelectronics.
- ST-Link USB debugger and drivers (or STMicro STM32CubeProgrammer for flashing).
- USB cable and target board powered.

#### 2. Locate the project
- Open the repository and find the Firmware folder (`Firmware/`).
- Confirm structure: `Core/` (Src, Inc), `Drivers/`, `.ioc`, `Debug/` or `Release/`.

#### 3. Import/open the project in STM32CubeIDE
- File → Import → General → Existing Projects into Workspace → select Firmware and finish.
- If there is a `.ioc` file, double-click it to open the CubeMX editor.

#### 4. Using the provided init code
- The project already contains generated init functions (`MX_GPIO_Init`, `MX_TIMx_Init`, `MX_USARTx_Init`, etc.) in `Core/Src` (`gpio.c`, `tim.c`, `usart.c`).
- `main.c` calls these `MX_*` functions. Do not delete them.
- If you need to change pin assignments: edit the `.ioc` in CubeMX, re-generate code (Project → Generate Code). Keep user code within the `USER CODE BEGIN/END` blocks to avoid overwrites.

##### 4.a Add Drivers include path

If you see missing headers from `Core/Drivers/Inc`, add the folder to the IDE include paths:

Project → Properties → C/C++ Build → Settings → Tool Settings → GCC C Compiler / GCC C++ Compiler → Includes

Add this include path (for both C and C++):
```bash
${workspace_loc:/${ProjName}/Core/Drivers/Inc}
```

#### 5. Build the project
- Project → Build All (or Ctrl+B).
- Fix any MCU mismatch by verifying the target MCU in the `.ioc` or project properties.

#### 6. Flashing and debugging
- Connect the board via ST-Link.
- Run → Debug As → STM32 Debugging (or Run As → STM32 C/C++ Application to run).
- Ensure target power and correct debug port (SWD).

#### 7. Common notes & troubleshooting
- Preserve `USER CODE BEGIN/END` regions when regenerating code.
- If HAL symbols are missing, re-generate CubeMX code or enable the required middleware/peripherals in the `.ioc`.
- If pins appear wrong at runtime, verify `.ioc` pinout matches the board silkscreen/labeling and that `MX_GPIO_Init` is being called from `main.c`.

#### 8. Quick checklist
- Firmware imported → `.ioc` verified → Generate (if changed) → Build → Connect ST-Link → Flash/Debug.

This will get the provided firmware building, pins initialized (via the generated `MX_*` init functions), and the code running on your STM32 target.

---

## 🖥️ Using the Mouse

### Basic Operation
- Once flashed, the mouse firmware will run automatically on power-up.
- The mouse should start tracking movement and button presses based on the configured sensors and GPIO pins.

### Debugging via UART
For runtime debugging and configuration, you can communicate with the mouse over UART:

#### 1. Hardware Setup
- Connect an HC-05 Bluetooth module to the UART TX/RX pins (refer to the PCB layout).
- Alternatively, use a USB-to-UART adapter directly connected to your PC.

#### 2. Serial Communication Settings
- Baud rate: **115200**
- Data bits: 8
- Parity: None
- Stop bits: 1

#### 3. Mobile Debugging (Recommended)
- Pair your phone with the HC-05 Bluetooth module.
- Use a Serial Bluetooth terminal app (e.g., "Serial Bluetooth Terminal" on Android).
- Connect to the HC-05 device.

#### 4. Available Commands
- Send `help` to display all available debug commands.
- Use the listed commands to inspect sensor values, test buttons, adjust sensitivity, or troubleshoot issues in real-time.

#### 5. Example Workflow
```
> help
[List of commands appears]
> info
[Current mouse state and sensor readings]
```

This allows you to tune and debug the mouse behavior without reflashing the firmware.

---

## 🤝 Contributing

We welcome contributions from the community! Whether you're fixing bugs, improving documentation, or adding new features:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 📬 Contact & Support

Have questions or need help? Feel free to reach out!

- **Issues**: Open an issue on this repository
- **Discussions**: Join our community discussions

Happy building! 🐭🚀

---

*Made with ❤️ by the Sri Lankan Open Source Micromouse Team*