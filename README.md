# EV Savings Calculator for Home Assistant (Denmark)

Sammenligner udgifter for at køre din gamle Opel Astra på benzin vs. at oplade din Polestar 3.

## 📁 Mappestruktur

```
ev-savings-calculator/
├── packages/
│   └── ev-savings-calculator-package.yaml    ← Alle sensorer og logik
├── configuration.yaml                         ← Integrationsfil for din HA
├── README.md                                  ← Denne fil
└── DASHBOARD.yaml                             ← Dashboard-kode (kopi/paste til HA)
```

## 📋 Installation

### 1. I din Home Assistant config folder:

1. **Kopier** `packages/ev-savings-calculator-package.yaml` til din `config/packages/` folder
2. **Rediger** `configuration.yaml` og tilføj denne linje:

```yaml
homeassistant:
  packages:
    ev_savings_calculator: !include packages/ev-savings-calculator-package.yaml
```

3. **Rediger** din `configuration.yaml` og tilføj **OPTION A eller B**:

#### OPTION A: Automatiske benzinpriser (anbefalet)

Install [Fuelprices_DK](https://github.com/J-Lindvig/Fuelprices_DK) HACS integration, så tilføj:

```yaml
fuelprices_dk:
  companies:
    - ok
    - shell
    - circlek
  fueltypes:
    - oktan 95
```

#### OPTION B: Manuel benzinpris

Brug `input_number.benzinpris_manuel` (ingen integration nødvendig).
Sæt prisen manuelt i Home Assistant UI.

### 2. Restart Home Assistant

Gå til Developer Tools → YAML → Restart Home Assistant

### 3. Tilføj til dashboard

Kopier koden fra `DASHBOARD.yaml` til dit Home Assistant dashboard.

## 📊 Sensorer

### Priser
- `sensor.benzinpris_dk` - Aktuel benzinpris (DKK/L)
- `sensor.opel_astra_pris_per_km` - Opel Astra pris per km
- `sensor.polestar3_pris_per_km_uge` - Polestar 3 pris per km (denne uge)
- `sensor.polestar3_pris_per_km_maned` - Polestar 3 pris per km (denne måned)

### Benzin omkostninger
- `sensor.benzinomkostning_denne_uge` - Hvad Opel ville have kostet (denne uge)
- `sensor.benzinomkostning_denne_maned` - Hvad Opel ville have kostet (denne måned)

### EV ladning omkostninger
- `sensor.ev_charging_cost_weekly_net_only` - Polestar opladning (uge) efter solceller
- `sensor.ev_charging_monthly_cost` - Polestar opladning (måned) efter solceller
- `sensor.ev_ladningomkostning_denne_uge` - Polestar opladning (uge) total
- `sensor.ev_ladningomkostning_denne_maned` - Polestar opladning (måned) total

### Besparelser
- `sensor.ev_besparelse_denne_uge` - Besparelse denne uge
- `sensor.ev_besparelse_denne_maned` - Besparelse denne måned

## ⚙️ Indstillinger

To input_number sensorer kan justeres i Home Assistant UI:

- `input_number.benzin_forbrug_per_100km` - Opel Astra forbrug (default: 7.2 L/100 km)
- `input_number.benzinpris_manuel` - Benzinpris manuel (default: 13.50 DKK/L)

## 🚗 Tekniske specifikationer

**Opel Astra K Sports Tourer 1.4 Turbo (150 HP) 2016**
- NEDC: ~5.9 L/100 km
- Real-world: ~7.2 L/100 km

**Polestar 3 Long Range Dual Motor (489 HP)**
- WLTP: 19.0 - 23.1 kWh/100 km
- Real-world: ~21 kWh/100 km

## 📝 Noter

- Sensorer skal være tilgængelige i Home Assistant:
  - `sensor.korsel_denne_uge` - Din km kørt denne uge
  - `sensor.korsel_denne_maned` - Din km kørt denne måned

- Disse kan fx komme fra Google Calendar integration eller Tesla integration
