# SeismoLink: Off-Grid Seismic Alert System

SeismoLink is a solar-powered, internet-independent earthquake detection and alert system designed for underserved regions with unreliable infrastructure. Developed at Hack Without Borders (3rd Place Overall), the system utilizes edge computing on a Raspberry Pi to analyze satellite imagery and trigger accessible, localized alerts.

<img width="1541" height="717" alt="image" src="https://github.com/user-attachments/assets/aba73c67-2ef1-48f9-b2a7-916866b20980" />

*Figure 1: 3D CAD enclosure design housing the Raspberry Pi, SLA battery, and satellite modem, powered by a 10W solar panel.*

---

## Repository Structure
* `/src` - Core Python detection algorithms and image processing scripts.
* `/data` - GeoTIFF displacement data for seismic events.
* `/docs` - System flowcharts and the Hack Without Borders technical presentation.

---

## Software & Algorithmic Detection

The core detection logic relies on analyzing differential ground displacement using satellite GeoTIFF imagery captured before and after a seismic event.

* **Image Processing Pipeline:** Engineered in Python using `rasterio` to parse multi-band geospatial data.
* **Noise Reduction:** Implemented a `scipy.ndimage` median filter to smooth isolated sensor errors in the displacement data, ensuring true signal fidelity.
* **Displacement Calculation:** Performs pixel-wise subtraction between temporal datasets. The algorithm applies a strict 10mm physical change threshold.
* **Alert Trigger:** If a clustered risk zone exceeds 50 significantly displaced pixels, the system immediately logs the event and triggers the GPIO alarm state.

<img width="728" height="209" alt="image" src="https://github.com/user-attachments/assets/c5bf6f9b-5d3e-4826-be41-d224e25330a5" />

*Figure 2: Differential displacement map highlighting high-risk seismic zones using pixel-wise subtraction.*

---

## Hardware Architecture & Power Systems

Designed for continuous, autonomous operation without reliance on the traditional electrical grid or terrestrial internet.

* **Computing Edge:** Raspberry Pi executing the Python analysis script locally from a microSD card.
* **Communications:** FHB-AFV Satellite Modem for receiving automated GeoTIFF updates entirely off-grid.
* **Power Distribution:** 5-10W Solar Panel paired with a 12V 7Ah Sealed Lead Acid (SLA) battery, regulated by a 12V-to-5V buck converter to safely power the logic boards.
* **Output Interface:** High-decibel audio buzzer and high-visibility strobe LED wired to GPIO pins to ensure multi-sensory accessibility for the alerts.

---

## Authors
Ansh Shah · Eyad Ahmed · Eshaan Marocha · Omar Elmahdy

*Hack Without Borders — 3rd Place*
