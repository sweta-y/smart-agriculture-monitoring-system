# Firmware Notes

The original creator's Arduino sketch for this build is **not open-sourced** and is not included in this repository. This file documents what the firmware needs to do, so it can be written or rewritten independently.

## Required Libraries

- `DHT sensor library` (Adafruit) — for reading the DHT11
- `LiquidCrystal` (built into Arduino IDE) — for driving the 16x2 LCD

## Expected Logic (Pseudocode)

```
setup():
    initialise LCD (columns=16, rows=2)
    initialise DHT11 on its data pin
    set analog pins for MQ135 and soil moisture sensor as inputs

loop():
    read temperature, humidity from DHT11
    read raw analog value from MQ135 (0–1023)
    read raw analog value from soil moisture sensor (0–1023)
    format all four values onto two 16-character LCD lines
    display on LCD
    wait briefly
    repeat
```

## Suggested Sketch Outline

```cpp
#include <DHT.h>
#include <LiquidCrystal.h>

#define DHTPIN 7
#define DHTTYPE DHT11

DHT dht(DHTPIN, DHTTYPE);
LiquidCrystal lcd(/* RS, E, D4, D5, D6, D7 pins */);

void setup() {
  lcd.begin(16, 2);
  dht.begin();
}

void loop() {
  float temp = dht.readTemperature();
  float hum  = dht.readHumidity();
  int airQuality   = analogRead(A0); // MQ135
  int soilMoisture = analogRead(A1); // Soil sensor

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("T:"); lcd.print(temp); lcd.print(" H:"); lcd.print(hum);
  lcd.setCursor(0, 1);
  lcd.print("AQ:"); lcd.print(airQuality); lcd.print(" SM:"); lcd.print(soilMoisture);

  delay(1000);
}
```

> This is a reference outline only — pin numbers, thresholds, and formatting should be adjusted to match your actual wiring and LCD library configuration.

## Calibration Notes

- The MQ135 gives a **relative** air-quality reading, not an absolute gas concentration, unless separately calibrated against a reference.
- The soil moisture sensor's dry/wet threshold should be calibrated by testing in known dry soil and in water, then picking a midpoint value.
- The DHT11 has limited accuracy (~±2°C, ±5% RH) — acceptable for this project's scope but not lab-grade.
