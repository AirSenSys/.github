<p align="center">
  <img src="https://cdn.abacus.ai/images/f1ffab09-701e-49f8-838e-e3fa28bdc5f3.png" alt="AirSenSys" width="100%">
</p>

# AirSenSys

Mobile air-quality sensor node for city-scale, crowdsourced particulate monitoring.

## Introduction

AirSenSys is a mobile air-quality sensing node built on the LilyGO T-SIM7000G, designed to generate dense spatiotemporal particulate matter (PM) datasets across a city. In the (fictional) deployment scenario, units are mounted on Vienna’s public bicycles. A small hub dynamo powers each node while riding, with an onboard battery buffering energy during stops and low-speed periods. As riders move through the city, the system continuously samples PM via the Sensirion SPS30, tags each reading with GNSS time and location, and transmits compact oneM2M-formatted data over LTE Cat-M (with 2G fallback). Temperature measurement is optional for added environmental context.

This project description captures the introductory quarter of the overall exposé, setting the scene before deeper sections on firmware state machine, oneM2M resource hierarchy, power budgeting, backend ingestion, and validation.

## What It Measures

- Mandatory: PM2.5, PM10 (via Sensirion SPS30)
- Optional: Temperature
- Context: GNSS timestamp and coordinates; basic network signal info (for diagnostics)

## oneM2M Alignment

- Resource model: An Application Entity (AE) publishes measurements as contentInstances under a container.
- Payload: JSON content with `cnf` (contentInfo) and `con` (content) fields.
- Transport: Uplink over LTE Cat-M with automatic 2G fallback; compact payloads to minimize power and cost.

### Example oneM2M contentInstance (request body)

```json
{
  "m2m:cin": {
    "cnf": "application/json",
    "con": {
      "ts": "2025-09-28T09:12:33Z",
      "loc": { "lat": 48.2082, "lon": 16.3738, "alt": 175 },
      "air": {
        "pm2_5_ugm3": 12.7,
        "pm10_ugm3": 21.4
      },
      "env": {
        "temp_c": 19.8
      },
      "dev": {
        "sensor": "SPS30",
        "fw": "0.3.1"
      },
      "net": {
        "rat": "LTE-M",
        "rssi_dbm": -87
      }
    }
  }
}
