# Project Vaayu 🌬️

**Open-source, affordable, accurate air quality monitoring for India**

*Vaayu (वायु) — Sanskrit for wind/air*

---

## The Problem

Air pollution is India's largest environmental health threat, reducing average life expectancy by over 5 years nationally and up to 10 years in cities like Delhi.

Yet there's a fundamental gap in how we measure and communicate air quality.

### The Hyperlocal Gap

When you check the AQI on your phone or a weather app, you're seeing a reading from a government CPCB (Central Pollution Control Board) monitoring station. These stations are sparse — a city like Bangalore with 13 million people has only a handful of monitors spread across the metropolitan area.

**The problem:** Air quality isn't uniform across a city. It varies dramatically within short distances:

| Location | Typical AQI Difference |
|----------|----------------------|
| Near construction site vs. 500m away | 50-100+ points |
| Busy intersection vs. residential lane | 30-60 points |
| Ground floor vs. 10th floor | 20-40 points |
| Morning rush hour vs. 2 AM | 50-150 points |

### A Real Example

Consider a mother living in Koramangala, Bangalore. She checks the AQI on her phone before taking her child to the park. The app shows **AQI 85 (Moderate)** — seems acceptable for outdoor play.

But that reading comes from the CPCB monitoring station in BTM Layout, approximately 4 kilometers away, positioned near a major road for traffic pollution monitoring.

The actual AQI at her neighborhood park — adjacent to an ongoing construction project — could be **AQI 160 (Unhealthy)**. Her child spends two hours breathing air that's nearly twice as polluted as she believed.

**She has no way to know. The infrastructure to tell her doesn't exist.**

This isn't a hypothetical edge case. It's the daily reality for hundreds of millions of Indians making health decisions based on air quality data that doesn't represent their actual environment.

---

## The Solution

**Project Vaayu** is an open-source hardware project to create an affordable, accurate, portable air quality monitor that enables true hyperlocal AQI measurement.

### Design Principles

1. **Accuracy over features** — ±10% accuracy target, validated against government reference stations
2. **Accessibility over complexity** — No app required, no technical knowledge needed
3. **Affordability over premium** — Target cost ≤₹5,000 (~$60 USD)
4. **Open over proprietary** — All designs, code, and documentation freely available

### Specifications

| Feature | Specification |
|---------|---------------|
| **Pollutants Measured** | PM2.5, PM10 |
| **Accuracy Target** | ±10% vs. CPCB reference stations |
| **Display** | 0.96" OLED — AQI value + category (Good/Moderate/Unhealthy/Severe) |
| **Power** | USB-C (5V) — works with any phone charger or power bank |
| **Connectivity** | WiFi (for initial calibration only) — then fully offline |
| **Enclosure** | Weather-resistant, designed for outdoor use |
| **Target Cost** | ≤₹5,000 BOM for single unit |

### What Makes Vaayu Different

Most affordable air quality sensors suffer from two accuracy problems:

**Problem 1: Environmental Sensitivity**

Humidity causes particles to absorb water and swell. A sensor calibrated in dry conditions will significantly over-read in humid environments (common during monsoon or coastal areas). Temperature also affects laser sensor behavior.

**Solution:** Vaayu includes a BME280 environmental sensor and applies peer-reviewed correction algorithms in real-time based on current humidity and temperature.

**Problem 2: Unit-to-Unit Variance**

Two identical sensors from the same manufacturing batch can read 10-20% differently due to slight variations in laser alignment and photodetector sensitivity.

**Solution:** Vaayu implements auto-calibration via the CPCB public API. During initial setup, the device compares its readings against the nearest government monitoring station over 24-48 hours and learns its specific bias correction factor. No need to physically visit a reference station.

---

## Technical Architecture

### Hardware Components

| Component | Model | Purpose | Est. Cost (INR) |
|-----------|-------|---------|-----------------|
| PM Sensor | Plantower PMS5003 | Laser light-scattering particle detection | ₹900-1,100 |
| Environmental Sensor | Bosch BME280 | Temperature, humidity, pressure for corrections | ₹250-350 |
| Microcontroller | ESP32-C3 SuperMini | Processing, WiFi, USB-C native | ₹350-450 |
| Display | 0.96" OLED (SSD1306) | AQI readout | ₹150-200 |
| Enclosure | 3D printed (PETG) | Weather-resistant housing | ₹300-500 |
| Miscellaneous | Wires, connectors, PCB | Integration | ₹200-400 |
| **Total BOM** | | | **₹2,150 - ₹3,000** |

### Software Stack

- **Firmware:** C/C++ (Arduino framework on ESP-IDF)
- **Correction Algorithms:** Based on peer-reviewed research on PMS5003 humidity response
- **Calibration:** CPCB API integration for reference data
- **Display:** Simple AQI number + category, no complex UI

### Data Flow

```
PMS5003 (raw PM2.5) ──┐
                      ├──▶ ESP32-C3 ──▶ Correction ──▶ Calibration ──▶ AQI ──▶ OLED
BME280 (temp/humidity)┘      │              Algorithm      Offset        Display
                             │
                             └──▶ WiFi ──▶ CPCB API (calibration phase only)
```

### AQI Calculation

Vaayu uses the India National Air Quality Index (NAQI) standard:

| AQI Range | Category | Health Implications |
|-----------|----------|---------------------|
| 0-50 | Good | Minimal impact |
| 51-100 | Satisfactory | Minor breathing discomfort to sensitive people |
| 101-200 | Moderate | Breathing discomfort to people with lung/heart disease |
| 201-300 | Poor | Breathing discomfort to most people on prolonged exposure |
| 301-400 | Very Poor | Respiratory illness on prolonged exposure |
| 401-500 | Severe | Affects healthy people, serious impact on those with existing diseases |

---

## Project Status

🚧 **Active Development**

### Completed
- [x] Problem definition and use case validation
- [x] Technical architecture design
- [x] Component selection and sourcing research
- [x] Correction algorithm research (literature review)

### In Progress
- [ ] Breadboard prototype assembly
- [ ] Basic firmware development

### Planned
- [ ] Environmental correction implementation
- [ ] CPCB API integration
- [ ] Auto-calibration system
- [ ] Enclosure design (3D printable)
- [ ] Field testing and validation
- [ ] Documentation and build guides

---

## Roadmap

| Phase | Timeline | Deliverables |
|-------|----------|--------------|
| **1. Prototype** | Month 1-2 | Working breadboard prototype, basic firmware, initial accuracy baseline |
| **2. Correction** | Month 2-3 | Humidity/temperature correction algorithms, validated accuracy improvement |
| **3. Calibration** | Month 3-4 | WiFi provisioning, CPCB API integration, auto-calibration system |
| **4. Enclosure** | Month 4-5 | 3D printed housing, thermal management, weather resistance validation |
| **5. Release** | Month 5-6 | Complete documentation, build guides, public release |

---

## Why Open Source?

### The Public Health Argument

Air pollution-related health costs in India are estimated at 1.4% of GDP annually. Access to accurate air quality information shouldn't be a privilege limited to those who can afford expensive monitoring equipment.

By open-sourcing Vaayu:
- **Individuals** can build their own monitor at component cost
- **Communities** can establish local monitoring networks
- **Schools** can use it as an educational platform for environmental science
- **Researchers** can improve algorithms and contribute corrections for different regions
- **Local makers** can adapt the design for specific use cases

### The Network Effect

The long-term vision: thousands of Vaayu devices across Indian cities, optionally contributing anonymized readings to create hyperlocal air quality maps with street-level resolution.

This is only possible with open-source — no single company or organization can deploy enough sensors to achieve this coverage. But a community can.

---

## Contributing

Contributions are welcome across all aspects of the project:

### Hardware
- PCB design optimization
- Alternative component suggestions (especially for local sourcing)
- Enclosure improvements for different manufacturing methods

### Firmware
- ESP32 sensor integration code
- Correction algorithm implementation and tuning
- Power optimization for battery operation (future)

### Data & Algorithms
- CPCB API integration
- Regional correction factor calibration
- Validation against reference instruments

### Documentation
- Build guides and tutorials
- Translations (Hindi, regional languages)
- Video assembly instructions

### Testing
- Field validation in different cities/conditions
- Long-term reliability testing
- Comparison against reference monitors

---

## Getting Started

*Detailed build instructions coming soon*

### Prerequisites
- Basic soldering skills (or access to pre-assembled modules)
- Arduino IDE or PlatformIO
- 3D printer access (for enclosure) or willingness to use alternative housing

### Quick Start
```bash
# Clone the repository
git clone https://github.com/61-Keys/vaayu.git
cd vaayu

# Firmware instructions (coming soon)
# Hardware assembly guide (coming soon)
```

---

## Repository Structure

```
vaayu/
├── firmware/           # ESP32 firmware source code
│   ├── src/
│   └── platformio.ini
├── hardware/           # Hardware design files
│   ├── schematic/
│   └── pcb/
├── enclosure/          # 3D printable enclosure files
│   └── stl/
├── docs/               # Documentation
│   ├── build-guide.md
│   ├── calibration.md
│   └── troubleshooting.md
├── research/           # Reference papers and data
├── funding.json        # Open source funding manifest
├── LICENSE
└── README.md
```

---

## License

**Software:** MIT License

**Hardware:** CERN Open Hardware License v2 - Permissive (CERN-OHL-P-2.0)

You are free to use, modify, and distribute both for personal and commercial purposes.

---

## Acknowledgments

This project builds on the work of the global air quality monitoring community:

- **[AQICN.org](https://aqicn.org/)** — Extensive research on PMS5003 sensor behavior and correction factors
- **[PurpleAir](https://www.purpleair.com/)** — Demonstrating that low-cost monitoring networks can provide valuable data
- **[AirGradient](https://www.airgradient.com/)** — Open-source air quality monitor designs
- **[CPCB](https://cpcb.nic.in/)** — India's Central Pollution Control Board for reference data access
- **Academic researchers** — Peer-reviewed studies on optical particle counter correction algorithms

---

## References

1. Zheng, T., et al. (2018). "Field evaluation of low-cost particulate matter sensors in high and low concentration environments." *Atmospheric Measurement Techniques*.

2. Barkjohn, K.K., et al. (2021). "Development and Application of a United States-wide correction for PM2.5 data collected with the PurpleAir sensor." *Atmospheric Measurement Techniques*.

3. Central Pollution Control Board. "National Air Quality Index." Ministry of Environment, Forest and Climate Change, Government of India.

---

## Contact

**Asutosh Rath**

- 📧 Email: asutoshrath26@gmail.com
- 🐙 GitHub: [github.com/61-Keys](https://github.com/61-Keys)
- 📍 Bengaluru, India

---

## Support This Project

Project Vaayu is seeking funding through open-source grant programs. See [funding.json](./funding.json) for details.

If you'd like to support this work:
- ⭐ Star this repository
- 🔄 Share with others who might benefit
- 🛠️ Contribute code, designs, or documentation
- 📣 Spread the word about hyperlocal air quality monitoring

---

<p align="center">
  <i>Breathe informed. Breathe better.</i>
</p>
