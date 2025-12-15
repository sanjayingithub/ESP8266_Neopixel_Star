# Custom Christmas Star with ESP8266 & WLED
<img width="1280" height="1280" alt="image" src="https://github.com/user-attachments/assets/43e53b29-75f2-488a-9c90-ac37f21e5c4d" />

A fully customizable, open‑source Christmas star built using an ESP8266 and addressable LEDs. This project reimagines traditional Christmas decorations by combining low‑cost hardware with powerful, flexible software (WLED), enabling animations, scheduling, wireless control, and long‑term repairability.

---

## Features

* **Fully customizable lighting effects** using WLED
* **Independent LED grouping** (non‑continuous LEDs supported)
* **Sunrise & sunset based automation** (location aware)
* **Different presets for different days of the week**
* **Wireless control** via web UI, mobile app, or HTTP API
* **Bare ESP8266 support** (no dev board required)
* **Low‑cost and easily available components**

---

## Why this project?

Earlier, people used paper stars for Christmas decoration. With time and the reduction in LED costs, LED stars became popular. However, most commercially available LED stars are:

* Expensive for what they offer
* Built using low‑quality materials
* Poorly customizable or completely closed

This project aims to provide an **affordable, high‑quality, and customizable alternative**, while remaining fully open‑source and easy to replicate.

---

##  Components Required

### Electronics

* **ESP8266 module** (ESP‑12 / ESP‑12F recommended)
* **ESP8266 dev board** (for flashing WLED)
* **Addressable LED strip** (WS2812B 90 leds 60leds/meter)
* **MP2307 buck module** (5V → 3.3V, capable of ≥600 mA)
* **Capacitors**:

  * 0.1 µF ceramic (decoupling) for ESP
  * 10–22 µF ceramic or electrolytic (bulk) for ESP
  * 470 µF electrolytic capacitor for LED strip
* **2 10 kΩ resistors** (for EN / GPIO boot strapping)
* **5V power supply** 
* Wire using **20 AWG** for connecting between **psu and led strip**. 
  Use **24-22 AWG** wire for **esp buck modue**.
* **Frame** I am using a frame from an old star. You could also create our own. 
<img width="919" height="1280" alt="image" src="https://github.com/user-attachments/assets/77a81c9b-2407-4b81-8432-944753c8c5bb" />
<img width="921" height="1280" alt="image" src="https://github.com/user-attachments/assets/6af6255f-e82b-43f2-8bd8-8c72d6151ccd" />
<img width="1280" height="1280" alt="image" src="https://github.com/user-attachments/assets/bebd35d4-d2d0-41d7-be1f-19ed0a60445c" />

These are the dimensions.

---

## Power Considerations

* I am using a **Computer PSU.** As its cheap, safe (if you know what you are doing) and can provide plenty of power. You can use a 5v 4-6 amp supply if you are unsure
<img width="959" height="1280" alt="image" src="https://github.com/user-attachments/assets/62288413-2d37-41c3-b73b-ea3480233364" />

These were my observations test ours before connecting no guarantees.
* LEDs run on **5V**.
* ESP8266 runs on **3.3V** (do NOT power directly from 5V)
* Ensure a **common ground** between ESP8266 and LEDs
* Place capacitors **close to the ESP8266 VCC pin** to avoid Wi‑Fi brownouts

---

##  How to Build Your Own

### 1️⃣ Prepare the ESP8266

Connection for Flashing

* [explains different approaches to program the module ](https://youtu.be/_iX67plFeLs?t=264&si=rprZcbhLp1iBNAGA)
* <img width="1122" height="674" alt="image" src="https://github.com/user-attachments/assets/00fc5e66-14ec-4071-a756-66f1eaf3856a" />
<img width="1280" height="1280" alt="image" src="https://github.com/user-attachments/assets/01180668-9392-460b-8437-7b151b00d0fe" />



Flash **WLED (ESP8266 build)** using:

* esptool.py [The webflasher doesn't seem to work so using this method](https://www.youtube.com/watch?v=l8OMi7SMpqs)

---

### 2️⃣ Configure WLED

1. Connect to the WLED access point
2. Configure Wi‑Fi
3. Set [star.local](http://www.star.local) instead of wled.local
4. Set:
<img width="1918" height="856" alt="wifi" src="https://github.com/user-attachments/assets/3ecbc5fd-b5a3-4a04-b724-cf561c54fb78" />

   * Set current to 500 if you are testing and not sure of the capability of your power supply. Increase to 4000-6000 if you are using a dedicated supply with 4-6amps.
   * LED count 90 in this case
   * GPIO pin 4 default is 2
   * LED type WS2812B
5. Define **segments** for independent LED groups
![The order for address the leds the colours represents the regions where the strip was cut and squares represents the 3 segements](https://github.com/user-attachments/assets/03c860f8-a189-458d-a759-f79937b4196a)
The order for address the leds the colours represents the regions where the strip was cut and squares represents the 3 segements
6. Create **presets** for different animations remember to save them and remember their IDs for setting timers.
7. I have pasted pasted the preset and ledmap json file for getting started. Feel free to modify it.
8. You will have to paste them by going to **star.local/edit** 
<img width="1918" height="865" alt="edit" src="https://github.com/user-attachments/assets/2637cdbe-f5d3-48b2-8a56-106edc614021" />

   Remember naming is important for the file.

<img width="1918" height="867" alt="Colors" src="https://github.com/user-attachments/assets/7c7bf0de-bfe6-44d4-a046-1af111bbbb99" />
This is how it looks with the segments and presents

---

### 3️⃣ Set Up Automation

* Enable NTP time sync its available in timesetup window
* Enter latitude & longitude for calculation of sun rise and sun set time. **This will only work on the computer version**
* Configure **sunrise and sunset timers** remember to click the blue tick to enable it. And save. 
* Assign different presets to different weekdays if you want. For it to work you should create the presets and not down their ids. Which is pasted in the table.
<img width="1893" height="805" alt="timesetup" src="https://github.com/user-attachments/assets/a12d3cd5-b7ee-45ec-bd4e-d6498425d1cf" />
<img width="351" height="770" alt="timersetup" src="https://github.com/user-attachments/assets/9d00b238-8de0-4d6d-8cbd-67afea1330b4" />


Example:

* Weekdays → calm glow
* Friday → party mode
* Sunrise → LEDs OFF

---

### 4️⃣ Assemble the Star

* Mount LEDs along the star edges using the adhesives tape.
* <img width="1280" height="1280" alt="image" src="https://github.com/user-attachments/assets/a879f8d3-57c3-4865-b970-412d639721dc" />

* The wiring diagram
![circuit star](https://github.com/user-attachments/assets/85cebf6a-668f-4288-9c43-2ba47196b356)


* Route wires cleanly
* Secure ESP8266 and power modules
* <img width="1280" height="1280" alt="image" src="https://github.com/user-attachments/assets/bd77a117-966b-476c-a11b-198c0942a6d4" />

* Ensure ventilation and strain relief

---

## Control Options

* Web UI (browser)
* WLED mobile app
* Automation via timers

---

## Tested Configuration

* ESP8266 (bare module) using blink sketch before starting.
* 90 WS2812B LEDs setting to white and going through each led. As I had encountered 1 defected led.
* WLED firmware
* Segmented LED mapping
* Sunrise/sunset scheduling

---

## 🙌 Acknowledgements

* **WLED** by Aircoookie [https://github.com/wled/WLED](https://github.com/wled/WLED)
* Open‑source hardware community

---

If you build your own version, feel free to fork this repository and share your design!
