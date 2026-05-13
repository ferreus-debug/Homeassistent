# 🚀 Quick Start - Installation

## Hurtig Installation (5 minutter)

### 1️⃣ Kopier Package-filen

```
Din HA config folder:
config/
└── packages/
    └── ev-savings-calculator-package.yaml     ← Kopier fra: packages/
```

### 2️⃣ Rediger `configuration.yaml`

Tilføj denne blok øverst:

```yaml
homeassistant:
  packages:
    ev_savings_calculator: !include packages/ev-savings-calculator-package.yaml
```

### 3️⃣ Vælg benzinpris-metode

**Vælg EN af disse:**

#### A) Automatisk (anbefalet)
Installer [Fuelprices_DK HACS](https://github.com/J-Lindvig/Fuelprices_DK) og tilføj:

```yaml
fuelprices_dk:
  companies:
    - ok
    - shell
    - circlek
  fueltypes:
    - oktan 95
```

#### B) Manuel
Lad `input_number.benzinpris_manuel` være som standard. Du sætter prisen i HA UI.

### 4️⃣ Restart Home Assistant

- Gå til: **Developer Tools** → **YAML** → **Restart Home Assistant**
- Vent 2-3 minutter

### 5️⃣ Tilføj Dashboard

1. Åbn Home Assistant dashboard
2. Klik **✎ Edit** (øverst højre)
3. Klik **+ Create New Card**
4. Vælg **Manual** og kopier koden fra `DASHBOARD.yaml`

## ✅ Verifikation

Går til **Developer Tools** → **States** og søg efter:
- `sensor.benzinpris_dk`
- `sensor.ev_besparelse_denne_uge`
- `input_number.benzinpris_manuel`

Hvis disse vises → Det virker! 🎉

## 🆘 Troubleshooting

**Sensorer vises ikke:**
- Check Home Assistant logs: `tail -f /config/home-assistant.log`
- Sikr at YAML er gyldig: `yamllint packages/ev-savings-calculator-package.yaml`

**Benzinpris vises ikke:**
- Hvis du bruger OPTION A: Check om Fuelprices_DK integration er installeret
- Hvis du bruger OPTION B: Indstil `input_number.benzinpris_manuel` manuelt i UI

**Dashboard viser "not available":**
- Sensorer skal have data. Check at disse sensorer findes i Home Assistant:
  - `sensor.korsel_denne_uge`
  - `sensor.korsel_denne_maned`
  - `sensor.ev_charging_cost_weekly_net_only`
  - `sensor.ev_charging_cost_monthly_net_only`
