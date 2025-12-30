# Project Vaayu 🌬️

**Open-source, affordable, accurate air quality monitoring for India**

*Vaayu (वायु) — Sanskrit for wind/air*

---

## The Problem

When you check the AQI on your phone, you're seeing a reading from a government monitoring station — often 5-10 kilometers away from where you actually are. 

Air quality isn't uniform across a city. It varies dramatically:
- Near a construction site vs. a park
- At a busy intersection vs. a residential lane  
- During morning traffic vs. late night

**You don't know what you're actually breathing.**

A mother in Koramangala sees AQI 85 on her phone and decides to take her child to the park. But that reading is from BTM Layout, 4km away. The actual AQI at the park, next to ongoing construction, might be 160.

She has no way to know. The infrastructure to tell her doesn't exist.

---

## The Solution

**Vaayu** is a portable air quality monitor that tells you the AQI right where you are, right now.

| Feature | Specification |
|---------|---------------|
| **Accuracy** | ±10% (with environmental correction + auto-calibration) |
| **Cost** | ~₹5,000 (~$60 USD) |
| **Power** | USB-C (phone charger / power bank) |
| **Display** | OLED screen — AQI number + category |
| **Connectivity** | WiFi for one-time calibration, then works offline |
| **Portability** | Pocket-sized, weather-resistant |

**No app required. No technical knowledge needed. Just a number you can trust.**

---

## How It Works

### Hardware
- **PMS5003** — Laser particle sensor (PM2.5 / PM10)
- **BME280** — Temperature, humidity, pressure sensor
- **ESP32-C3** — Microcontroller with WiFi and native USB-C
- **0.96" OLED** — Clear display readable at a glance

### The Secret Sauce: Calibration

Most cheap air quality sensors are inaccurate because:
1. They don't correct for humidity (particles swell in humid air, causing over-reading)
2. Each sensor unit has manufacturing variance

**Vaayu solves both:**

1. **Environmental Correction** — Uses BME280 readings to apply peer-reviewed humidity/temperature correction formulas in real-time

2. **Auto-Calibration** — On first setup, connects to WiFi and compares readings against the nearest CPCB government station via public API. Learns the sensor's bias and corrects for it. No need to physically visit a reference station.

---

## Project Status

🚧 **Currently in development**

- [x] Technical architecture defined
- [x] Component selection finalized  
- [ ] Breadboard prototype
- [ ] Correction algorithm implementation
- [ ] Auto-calibration system
- [ ] Enclosure design
- [ ] Documentation & release

---

## Bill of Materials (Estimated)

| Component | Purpose | Est. Cost (INR) |
|-----------|---------|-----------------|
| Plantower PMS5003 | PM2.5/PM10 sensing | ₹900-1100 |
| ESP32-C3 SuperMini | MCU + WiFi | ₹350-450 |
| BME280 module | Temp/humidity/pressure | ₹250-350 |
| 0.96" OLED (SSD1306) | Display | ₹150-200 |
| USB-C breakout/cable | Power | ₹100-150 |
| Enclosure (3D printed) | Housing | ₹300-500 |
| PCB + misc | Integration | ₹300-500 |
| **Total** | | **₹2,350 - ₹3,250** |

*Final retail target: ≤₹5,000 including assembly margin*

---

## Why Open Source?

Air pollution reduces average life expectancy in India by **5+ years**. In Delhi, it's closer to 10 years.

This isn't a problem that should be solved by expensive proprietary devices accessible only to the wealthy. Accurate air quality information is a public health necessity.

By open-sourcing Vaayu:
- Anyone can build one for themselves
- Communities can set up local monitoring networks
- Researchers can improve the correction algorithms
- Local makers can adapt it for their specific needs
- Eventually: crowdsourced hyperlocal AQI maps across Indian cities

---

## Contributing

This project is just getting started. Contributions welcome:

- **Hardware**: PCB design, enclosure optimization
- **Firmware**: ESP32 code, calibration algorithms
- **Data Science**: Correction factor tuning, CPCB API integration
- **Documentation**: Build guides, translations
- **Testing**: Real-world validation across different conditions

---

## Roadmap

**Phase 1: Prototype** (Month 1-2)
- Breadboard assembly
- Basic firmware
- Initial accuracy testing

**Phase 2: Correction** (Month 2-3)  
- Humidity correction implementation
- Temperature correction
- Validation against CPCB

**Phase 3: Calibration** (Month 3-4)
- WiFi provisioning
- CPCB API integration
- Auto-calibration system

**Phase 4: Enclosure** (Month 4-5)
- 3D printed housing design
- Thermal management
- Weather resistance testing

**Phase 5: Release** (Month 5-6)
- Complete documentation
- Build guides with photos
- Public release

---

## License

MIT License — use it, modify it, share it.

Hardware designs: [CERN-OHL-P-2.0](https://ohwr.org/cern_ohl_p_v2.txt) (Permissive)

---

## Acknowledgments

This project is inspired by the citizen science air quality movement and builds on the work of:
- [PurpleAir](https://www.purpleair.com/) — proving low-cost monitoring can work
- [AirGradient](https://www.airgradient.com/) — open-source air quality kits
- [AQICN](https://aqicn.org/) — global air quality data and sensor research
- [CPCB](https://cpcb.nic.in/) — India's Central Pollution Control Board

---

## Contact

**Asutosh Rath**  
📧 asutoshrath26@gmail.com  
🐙 [github.com/61-Keys](https://github.com/61-Keys)

---

*Breathe informed. Breathe better.*
