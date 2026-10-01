# Hardware Components

Full bill of materials for the Smart Agriculture Monitoring System.

| # | Component | Quantity | Purpose | Notes |
|---|---|---|---|---|
| 1 | Arduino UNO | 1 | Main controller — reads all sensors and drives the LCD | ATmega328P based |
| 2 | 16x2 LCD Display | 1 | Displays soil moisture, temperature, humidity, air quality | Wires pre-soldered for easy mounting |
| 3 | MQ135 Gas Sensor | 1 | Detects changes in air quality | Needs a brief warm-up time after power-on |
| 4 | DHT11 Sensor | 1 | Measures air temperature and relative humidity | Digital single-wire output |
| 5 | Soil Moisture Sensor | 1 | Detects whether soil is dry or wet | Probe extended outside enclosure on ~1m wire |
| 6 | 10k Preset (Potentiometer) | 1 | Adjusts LCD contrast | Connected to LCD's Vo pin |
| 7 | Male-to-Female Jumper Wires | Several | Sensor-to-Arduino connections | |
| 8 | Female-to-Female Jumper Wires | Several | LCD and sensor connections | |
| 9 | Power Jack | 1 | Connects battery supply to Arduino | |
| 10 | 9V Battery + Battery Cap | 1 | Main power source | |
| 11 | Switch | 1 | Power on/off control | |
| 12 | 3.7V Rechargeable Battery | 1 | Connected in series with the 9V battery to improve supply stability | |
| 13 | Wire (~1 metre) | 1 | Extends the soil moisture probe outside the enclosure | |
| 14 | Enclosure Box | 1 | Houses the circuit; vented to let air reach the MQ135 sensor | |

## Approximate Pin Mapping

| Component | Arduino Pin | Signal Type |
|---|---|---|
| DHT11 data pin | Digital Pin 7 | Digital |
| MQ135 analog out | Analog pin (A0–A5) | Analog (ADC) |
| Soil Moisture Sensor analog out | Analog pin (A0–A5) | Analog (ADC) |
| LCD (RS, E, D4–D7) | Digital pins | Digital (LiquidCrystal library) |
| LCD contrast (Vo) | 10k preset wiper | Analog voltage divider |

> Confirm exact analog pin assignments against your own wiring before flashing firmware — these are not hardcoded by any shared source code for this build.
