# ESP12-WeatherStation-I2C-12864-WeatherApi-zh

ESP-12 (ESP8266) weather station: shows local outside weather + a 5-day
forecast on a 128x64 SPI LCD, plus an internal DHT temperature/humidity
sensor reading and a smoke-alarm buzzer/LED. Optionally also cycles through
two additional world cities' current conditions.

<img src="WeatherStation1.jpg" alt="Weather Station" width="400"><br/>
<img src="WeatherStation2.jpg" alt="Weather Station" width="400"><br/>
<img src="WeatherStation3.jpg" alt="Weather Station" width="400"><br/>
<img src="WeatherStation4.jpg" alt="Weather Station" width="400">

## Setup

1. Install dependencies: `U8g2`, `WiFiManager`, `DHT sensor library` (+
   `Adafruit Unified Sensor`), `Timezone`, `JsonStreamingParser`.
2. This sketch vendors its shared dependencies directly so it builds
   standalone - **replace their placeholder credentials/locations before
   flashing**:
   - `WeatherApiWeather.h`/`.cpp` ([source](https://github.com/bobhuang1/esp8266-weather-WeatherApi)) -
     set `WEATHERAPI_LOCATION` (and `WEATHERAPI_LOCATION1`/`WEATHERAPI_LOCATION2`
     if you enable `SHOW_US_CITIES`) below the `#include`s to real city names,
     and set `WEATHERAPI_APP_ID` (also below the `#include`s) to your
     [WeatherAPI.com](https://www.weatherapi.com/) key.
   - `StringHelpers`, `AlarmBeeper`, `WiFiMultiConnect`, `WeatherDisplayHelpers`,
     `BootSplashBitmap` ([source](https://github.com/bobhuang1/ESP8266-Functions-Common)) -
     set `WIFI_SSIDS`/`WIFI_PASSWORDS` to your own network(s), or enable
     `USE_WIFI_MANAGER` instead of hardcoding credentials at all.
   - If you update any shared library, re-copy its `src/` files here.
3. `#define SHOW_US_CITIES` (disabled by default) also cycles through two
   more cities' current conditions between the local weather and forecast
   pages.
4. `#define USE_LED` / `USE_HIGH_ALARM` / `USE_OLD_LED` select the
   smoke-detector alarm wiring variant for a particular built unit - see the
   comments next to each `#define` at the top of the .ino.

## Notes

- Weather data comes from [WeatherAPI.com](https://www.weatherapi.com/)
  (see [esp8266-weather-WeatherApi](https://github.com/bobhuang1/esp8266-weather-WeatherApi)).
  Current conditions and the forecast are returned in a single request, so
  this sketch refreshes both together on the same interval
  (`UPDATE_INTERVAL_SECS`).
- The daily forecast has one overall condition per day (not a separate
  day/night pair) and a peak wind speed with no direction - see
  esp8266-weather-WeatherApi's README for details.
- `#define LANGUAGE_CN` / comment it out to switch the on-screen text between
  Chinese and English.


## License

This project is free software, released under the **GNU General Public License v3.0**. You may redistribute and/or modify it under those terms; see [LICENSE.md](LICENSE.md) for the full text.
