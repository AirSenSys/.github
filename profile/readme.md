<p align="center">
  <img src="https://cdn.abacus.ai/images/f1ffab09-701e-49f8-838e-e3fa28bdc5f3.png" alt="AirSenSys" width="100%">
</p>

# AirSenSys

Mobile air-quality sensor node for city-scale, crowdsourced particulate monitoring.

## Introduction

AirSenSys is a mobile air-quality sensing node built on the LilyGO T-SIM7000G platform, designed to generate dense spatiotemporal particulate matter (PM) datasets across a city.  The system combines low-power cellular connectivity, precision air quality sensors, and GPS tracking to create a comprehensive environmental monitoring solution.

**Current Status: Prototype**  
For detailed information about each component, please refer to the README in each repository.

## What It Measures

- **Mandatory**: PM2.5, PM10 (via Sensirion SPS30)
- **Optional**: Temperature
- **Context**:  GNSS timestamp and coordinates; basic network signal info (for diagnostics)

## System Architecture

The AirSenSys project consists of several integrated components:

### Hardware & Firmware
- **[LillyGO_Firmware](https://github.com/AirSenSys/LillyGO_Firmware)** - C++ firmware for the ESP32-based sensor nodes
  - Handles sensor data collection from the SPS30
  - Manages GPS positioning and timestamping
  - Controls LTE Cat-M cellular communication with 2G fallback
  - Implements power management for mobile deployment
  - *Status: Active development*

### Data Infrastructure
- **[Cloud](https://github.com/AirSenSys/Cloud)** - Cloud infrastructure and database setup (PLpgSQL)
  - Database schema and management scripts
  - Data storage and retrieval systems
  - Backend infrastructure configuration
  - *Status: In development*

- **[NodeRED](https://github.com/AirSenSys/NodeRED)** - Data processing and workflow automation
  - Real-time data ingestion pipelines
  - Data transformation and validation
  - Integration with storage and visualization systems
  - *Status: In development*

- **[Thingsboard](https://github.com/AirSenSys/Thingsboard)** - IoT platform integration
  - Data visualization dashboards
  - Device management and monitoring
  - Real-time analytics and alerts
  - *Status:  In development*
