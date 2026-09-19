

Yes. Since **October 3, 2026 is your hardware deadline**, I would make the combined project a single system with **two physical subsystems**, but build it in a way that lets you demonstrate the complete pipeline even if the AI/cloud side is still being developed.

Sri Lanka has a strong justification for this direction: FAO identifies climate-resilient agrifood systems as an important need, and Sri Lanka's climate-related agricultural challenges include drought, flooding and water-management problems. Sri Lanka's climate commitments also explicitly include reducing post-harvest losses. ([FAOHome][1])

# 🌾 Combined Project

## **AgriShield**

### An Intelligent Climate-Resilient Farming and Post-Harvest Management System

The complete system:

```text
                         AGRISHIELD
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
       SMART FARM FIELD              SMART STORAGE
              │                             │
      ┌───────┼────────┐             ┌──────┼───────┐
      │       │        │             │      │       │
    Water   Weather   Soil         Temp  Humidity Camera
      │       │        │             │      │       │
      └───────┼────────┘             └──────┼───────┘
              │                             │
              ▼                             ▼
        ESP32 CONTROL                 ESP32 CONTROL
              │                             │
        ┌─────┴──────┐                ┌─────┴─────┐
        │            │                │           │
      PUMP        DRAINAGE          FAN       COOLING
        │            │                │           │
        └────────────┴────────────────┴───────────┘
                             │
                             ▼
                       BACKEND + AI
                             │
                             ▼
                        DASHBOARD
```

The important thing is that **both sides physically do something**.

---

# 1. What exactly are we building?

### Module 1 — Smart Field

It monitors:

* Soil moisture
* Field water level
* Rainfall
* Temperature
* Humidity
* Water flow

Then controls:

* Irrigation pump
* Irrigation valve
* Drainage mechanism

Example:

```text
Soil dry
+
No rain
+
Water available

        ↓

IRRIGATE
```

But:

```text
Heavy rain
+
Water level rising
+
Soil already saturated

        ↓

STOP IRRIGATION
        ↓
OPEN DRAINAGE
```

That is the **climate-resilience part**.

Sri Lanka's recent agricultural situation makes this particularly relevant: FAO reports that Cyclone Ditwah affected more than 129,000 hectares of agricultural land and over 227,000 farming households, with damaged irrigation infrastructure among the problems reported. ([FAOHome][2])

---

# 2. Smart Storage

After harvesting:

```text
Farm
 ↓
Harvest
 ↓
AgriShield Storage
 ↓
Market
```

Inside the storage chamber:

```text
Temperature
Humidity
CO₂ / air quality
Camera
Weight
```

The controller monitors conditions.

Then:

```text
Temperature ↑
Humidity ↑
Visual quality ↓

        ↓

SPOILAGE RISK ↑

        ↓

Fan / ventilation
        +
Cooling
        +
Farmer alert
```

Sri Lanka's national climate commitments specifically identify reduction of post-harvest losses as an agricultural priority. ([FAOLEX][3])

---

# 🧠 3. AI layer

Don't start with complicated AI.

Build it in stages.

### Level 1 — Rule engine

```text
IF soil_moisture < threshold
AND rain = false
THEN irrigation = ON
```

### Level 2 — Prediction

Use historical sensor data:

```text
Temperature
Humidity
Soil moisture
Rainfall
Water level
        ↓
      ML model
        ↓
Irrigation requirement
```

### Level 3 — Storage prediction

```text
Temperature
Humidity
CO₂
Image
Storage duration
        ↓
      AI model
        ↓
Spoilage risk
```

### Level 4 — Computer vision

```text
Camera
  ↓
Crop image
  ↓
CNN / lightweight vision model
  ↓
Quality classification
```

Don't make AI the first thing you build. **Get the hardware working first.**

---

# 🛒 What you need to buy from Tronic

If by "Tronic shop" you mean TRONIC.LK in Nugegoda, it is listed as an electronics store at Sunethradevi Road. There are also electronic-parts suppliers around Colombo such as Unitech Trading (Pvt) Ltd - Colombo 11 if something is unavailable.

## 🔴 MUST BUY

### Controllers

| Item                              |   Quantity |
| --------------------------------- | ---------: |
| ESP32 development board           |      **2** |
| ESP32-CAM / ESP32-S3 camera board |      **1** |
| Breadboard                        |    **2–3** |
| Jumper wire set                   | **2 sets** |
| USB cables                        |      **3** |
| 5V power supply                   |      **2** |

I recommend **two ESP32s**:

```text
ESP32 #1 → Field
ESP32 #2 → Storage
```

This keeps the systems independent.

---

# 🌱 FIELD MODULE

### Sensors

| Component                                         | Qty | Purpose                |
| ------------------------------------------------- | --: | ---------------------- |
| Capacitive soil-moisture sensor                   |   2 | Soil condition         |
| Waterproof water-level sensor / ultrasonic sensor |   1 | Field water level      |
| DHT22 / SHT31                                     |   1 | Temperature + humidity |
| Rain sensor                                       |   1 | Rain detection         |
| Water-flow sensor                                 |   1 | Irrigation measurement |

I'd buy **two soil sensors**, because one can fail during testing.

### Actuators

| Component           |    Qty |
| ------------------- | -----: |
| DC water pump       |      1 |
| Relay/MOSFET module |    1–2 |
| Solenoid valve      |      1 |
| Small DC motor      |      1 |
| Motor driver        |      1 |
| Tubing              | enough |
| Water container     |      1 |

The **solenoid valve** controls water entering the field.

The **motor** can operate your miniature drainage gate.

---

# 🍅 STORAGE MODULE

### Sensors

| Component                   | Qty |
| --------------------------- | --: |
| Temperature/humidity sensor |   1 |
| CO₂ sensor                  |   1 |
| Air-quality/VOC sensor      |   1 |
| Load cell                   |   1 |
| HX711 module                |   1 |
| Camera                      |   1 |

The load cell is actually useful because:

```text
Initial weight = 5 kg

After storage = 4.7 kg
```

You can quantify weight loss.

That gives you a proper experimental measurement.

---

# 🌬️ Storage actuators

| Component                   |      Qty |
| --------------------------- | -------: |
| 5V/12V fan                  |      1–2 |
| MOSFET/relay module         |        1 |
| Small cooling/Peltier setup | Optional |
| LED lighting                |        1 |
| Buzzer                      |        1 |

### Don't buy an expensive refrigeration system yet.

For your first prototype:

**fan + ventilation + controlled temperature experiment**

is enough.

You can add Peltier cooling if the basic system works.

---

# ⚡ Power

Get:

* 12V adapter
* 5V buck converter
* 12V → 5V converter
* terminal blocks
* fuse
* switches
* wires
* connectors

For the final field version:

```text
Solar panel
     ↓
Charge controller
     ↓
Battery
     ↓
12V / 5V
     ↓
ESP32 + sensors + pump
```

But **solar is Phase 2**.

Don't let solar power delay the October prototype.

---

# 🧰 Mechanical materials

Don't forget these.

You need:

* PVC pipe
* water container
* small transparent box/container
* acrylic sheets
* cardboard/foam board for prototype
* screws
* nuts/bolts
* brackets
* tubing
* hose connectors
* waterproof enclosure

The storage chamber can be made from a transparent plastic/acrylic box.

The farm can be a miniature model:

```text
          RAIN
           ↓↓↓
 ┌───────────────────────┐
 │       FARM            │
 │                       │
 │   🌱 🌱 🌱 🌱        │
 │                       │
 │ ────────────────────  │
 │       WATER           │
 │                       │
 └──────────┬────────────┘
            │
       Drainage gate
            │
            ▼
        Reservoir
```

---

# 📦 Your October 3 shopping checklist

Take this list to the shop.

### Electronics

```text
[ ] ESP32 × 2
[ ] ESP32-CAM / ESP32-S3 camera × 1
[ ] Breadboard × 2
[ ] Jumper wires
[ ] USB cables
[ ] Resistors
[ ] LEDs
[ ] Push buttons
[ ] Buzzers
[ ] 5V power supplies
[ ] 12V power supply
[ ] Buck converters
[ ] Relay modules
[ ] MOSFET modules
```

### Sensors

```text
[ ] Capacitive soil moisture × 2
[ ] DHT22/SHT31 × 2
[ ] Water level sensor × 1
[ ] Rain sensor × 1
[ ] Water flow sensor × 1
[ ] CO₂ sensor × 1
[ ] Air quality/VOC sensor × 1
[ ] Load cell × 1
[ ] HX711 × 1
```

### Actuators

```text
[ ] DC water pump
[ ] Solenoid valve
[ ] DC motor
[ ] Motor driver
[ ] 12V/5V fans × 2
[ ] Optional Peltier module
```

### Mechanical

```text
[ ] PVC pipes
[ ] Silicone tubing
[ ] Water container
[ ] Transparent storage box
[ ] Acrylic/foam board
[ ] Screws
[ ] Nuts + bolts
[ ] Wire terminals
[ ] Cable ties
[ ] Waterproof enclosure
```

---

# 📅 Timeline to October 3

Assuming **today is September 19**, you have roughly two weeks.

Don't try to finish everything.

## September 19–20

### Architecture + requirements

Finish:

```text
Problem statement
       ↓
System architecture
       ↓
Hardware list
       ↓
Data flow
       ↓
Prototype design
```

Also choose **one crop for the storage experiment**.

I would choose something easy to observe visually, rather than trying to support many crops.

---

# September 21

## Buy hardware

Go to the electronics shop and get the complete **MUST BUY** list.

Then inventory everything.

Don't start assembling randomly.

Create:

```text
/components
    sensors
    actuators
    controllers
    power

/docs
    architecture
    circuit
    BOM

/software
    field
    storage
    backend
```

---

# September 22–23

## Sensor testing

Test each sensor independently.

### Day 1

```text
ESP32
 ↓
Soil moisture
 ↓
Serial Monitor
```

Then:

```text
ESP32
 ↓
Temperature
 ↓
Serial Monitor
```

Then:

```text
ESP32
 ↓
Water level
```

Do this for every sensor.

**Don't connect everything at once.**

---

# September 24

## Field prototype

Build:

```text
ESP32
 │
 ├── Soil moisture
 ├── Water level
 ├── Rain sensor
 ├── Temperature
 │
 └── Relay
       │
       └── Pump
```

Get this working first.

---

# September 25

## Automated irrigation

Implement:

```text
IF soil dry
AND water available
AND no heavy rain

→ Pump ON
```

Then:

```text
IF soil wet
OR water level high

→ Pump OFF
```

---

# September 26

## Flood control

Build the miniature drainage mechanism.

```text
Water level LOW
      ↓
Gate closed

Water level HIGH
      ↓
Gate OPEN
```

Now you have your first **physical autonomous agricultural system**.

---

# September 27

## Storage prototype

Build the storage box.

```text
┌─────────────────────┐
│      CAMERA         │
│                     │
│   🍅 🍅 🍅 🍅       │
│                     │
│ Sensor              │
│                     │
│ Fan →→→→→           │
└─────────────────────┘
```

Connect:

```text
Temperature
Humidity
CO₂
Camera
Weight
Fan
```

---

# September 28

## Storage automation

Implement:

```text
Humidity HIGH
     ↓
Fan ON
```

and:

```text
Temperature HIGH
     ↓
Cooling / ventilation ON
```

Don't worry about sophisticated AI yet.

---

# September 29–30

## Backend

Now connect everything.

```text
ESP32
   ↓
HTTP / MQTT
   ↓
Spring Boot
   ↓
PostgreSQL
   ↓
React dashboard
```

Store:

```text
timestamp
device_id
temperature
humidity
soil_moisture
water_level
rain
flow_rate
storage_weight
```

---

# October 1

## Dashboard

Build only the important screens.

### Farm

```text
🌱 FARM

Soil Moisture     31%
Water Level       22%
Temperature       28°C

Irrigation        OFF
Drainage          OFF

Flood Risk        LOW
```

### Storage

```text
🍅 STORAGE

Temperature       24°C
Humidity          76%
Weight            4.82 kg

Spoilage Risk     LOW
Fan               ON
```

---

# October 2

## Integration + testing

This is **NOT** the day to add new features.

Test scenarios.

### Scenario 1

Dry soil:

```text
Dry soil
 ↓
Pump ON
```

### Scenario 2

Heavy water:

```text
Water level HIGH
 ↓
Pump OFF
 ↓
Drainage ON
```

### Scenario 3

Storage humidity high:

```text
Humidity HIGH
 ↓
Fan ON
```

### Scenario 4

Storage temperature high:

```text
Temperature HIGH
 ↓
Cooling/ventilation ON
```

---

# 🚨 October 3 — DEMO DAY

Your demonstration should be something like this:

### Step 1

Show dry field.

```text
SOIL: DRY
```

System automatically starts irrigation.

### Step 2

Add water to the field.

Water level increases.

System detects:

```text
FLOOD RISK
```

Pump stops.

Drainage activates.

### Step 3

Move to storage.

Show:

```text
Temperature
Humidity
Weight
Camera
```

Create an artificially unfavorable storage condition.

System detects the change.

Fan activates.

### Step 4

Dashboard

Show everything remotely:

```text
             AGRISHIELD

FIELD                 STORAGE

Soil 31%              Temp 24°C
Water 18%             Humidity 76%
Pump OFF              Fan ON
Flood LOW             Risk LOW
```

That's a **very demonstrable project**.

---

# ⚠️ One thing I would change from the original idea

Don't promise:

> "Our AI will predict crop spoilage with 95% accuracy."

You won't have enough real-world data in two weeks.

Instead, structure it:

### Phase 1

**Sensor-based decision engine**

### Phase 2

**Collect real data**

### Phase 3

**Train ML model**

### Phase 4

**Deploy ML prediction**

That is scientifically much more defensible.

---

# 🎯 What you absolutely need working by October 3

If time becomes tight, prioritize this order:

```text
                    PRIORITY

                       1
                ESP32 + sensors
                       ↓
                       2
              Automated irrigation
                       ↓
                       3
                Flood detection
                       ↓
                       4
                Storage monitoring
                       ↓
                       5
              Automatic ventilation
                       ↓
                       6
                   Dashboard
                       ↓
                       7
                     AI
```

**Do not sacrifice the physical hardware to build a fancy dashboard.**

The heart of your project should be:

> **Sense → Decide → Act → Measure**

That's what turns AgriShield from a normal IoT agriculture project into an actual **agricultural automation and climate-resilience system**.

### Where to buy

For the October 3 shopping trip, the search returned TRONIC.LK in Nugegoda, plus Unitech Trading (Pvt) Ltd - Colombo 11 and Lankatronics (Pvt) Ltd. as other local electronics options. Availability of each exact sensor should be confirmed before travelling.

[1]: https://www.fao.org/climate-change/news/news-detail/transparent-data--stronger-agrifood-action--colombo-workshop-sets-direction-for-cop31/en?utm_source=chatgpt.com "News detail | Climate change | Food and Agriculture Organization of the United Nations"
[2]: https://www.fao.org/srilanka/news/detail/fao-appeals-for-usd-16.5-million-to-restore-livelihoods-after-cyclone-ditwah-devastates-sri-lanka-s-agrifood-sector/en?utm_source=chatgpt.com "FAO in Chile| News detail"
[3]: https://faolex.fao.org/docs/pdf/srl239976.pdf?utm_source=chatgpt.com "<table id=\"e1\">"
