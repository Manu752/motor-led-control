# motor-led-control

> **Project Year: 2021**  
> Motor and LED control system with PWM speed control, motor states, battery monitoring and basic safety checks.

Small embedded C software for an automotive-style electronic control unit (ECU): it drives a brushless motor and an RGB LED, accepts only cryptographically signed commands, estimates a battery's state of charge, and proves with mutation testing that its tests catch bugs. All algorithms run on emulated Arm microcontrollers (QEMU).

---

## Architecture & Features

- **Motor & LED Middleware**: Portable C library with signed command verification (Zephyr + TrustZone TF-M, PSA Crypto).
- **Battery Management System (BMS)**: Extended Kalman Filter (EKF) State of Charge (SoC) estimation benchmarked against real LG HG2 cell datasets.
- **Mutation Testing Suite**: Proves test suite effectiveness by planting synthetic bugs across controller routines.
- **Interactive Dashboard**: Static web interface displaying size profiles, telemetry traces, and mutation scores.

---

## Quick Start & Execution

### 1. View the Web Dashboard
Serve the interactive report and results dashboard locally:
```bash
# Using Node / npm
npm install
npm start
# Opens at http://localhost:3000

# Or using Python 3
python3 -m http.server 3000
```

### 2. Embedded Build & Test
The C middleware and BMS routines can be compiled using `make`:
```bash
# Build the BMS library and run reference tests
make -C bms test

# Run Python-based SoC validation
pip install -r requirements.txt
python3 bms/tools/soc_eval.py
```

---

## Repository Structure

```
.
├── app/                  # Zephyr / TrustZone application and board overlays
├── bms/                  # Battery Management System (EKF SoC estimator & CAN frames)
├── mlmw/                 # Core motor & LED control middleware in C
├── results/              # Benchmark data, mutation scores, and size measurements
├── tools/                # Analysis scripts (mutation runner, node client, size check)
├── tests/                # Reference test suites
├── index.html            # Web dashboard entry point
├── style.css             # Dashboard styling
├── package.json          # Node server dependencies
├── requirements.txt      # Python dependencies
└── Makefile              # Build automation
```

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
