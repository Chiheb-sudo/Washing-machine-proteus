# 📦 Liste complète des composants Proteus

## 🎯 Récapitulatif

```
Microcontrôleur    : 1
Modules relay      : 1 (6 relais intégrés)
LCD I²C            : 1
Potentiomètres     : 4
Boutons poussoirs  : 4 + 4 (signaux)
LEDs              : 14
Résistances       : Variées
Condensateurs     : Variés
Diodes            : 6
```

---

## 📋 Microcontrôleur

| Composant | Référence | Qté | Description |
|-----------|-----------|-----|-------------|
| Arduino Mega 2560 | MEGA2560 | 1 | Processeur principal 16MHz, 256KB Flash |

**Caractéristiques** :
- 54 pins I/O numériques
- 16 entrées analogiques 10-bit
- 4 UARTs (ports série)
- 1 I²C, 1 SPI
- Alimentation : 5V, ~50mA

---

## 🔌 Relais et électrovannes

| Composant | Référence | Qté | Description |
|-----------|-----------|-----|-------------|
| Module relais 6 voies | RELAY6CH-5V | 1 | 6 relais 5V 5A |
| Électrovanne 1 | SOL1 | 1 | Entrée eau |
| Électrovanne 2 | SOL2 | 1 | Savon |
| Électrovanne 3 | SOL3 | 1 | Détergent |
| Électrovanne 4 | SOL4 | 1 | Rinçage |
| Pompe vidange | PUMP1 | 1 | Évacuation eau |
| Moteur essorage | MOTOR1 | 1 | Essorage/Centrifugation |

**Caractéristiques relais** :
- Tension bobine : 5V
- Courant bobine : 50-100mA
- Contacts : SPDT (NO/NC)
- Courant contact : Max 5A
- Tension contact : 250V AC / 30V DC

**Protection** :
- Diode 1N4007 en antiparallèle (roue libre)
- Résistance de pulldown 10kΩ

---

## 📺 Affichage LCD

| Composant | Référence | Qté | Description |
|-----------|-----------|-----|-------------|
| LCD 20×4 I²C | LCD20X4_I2C | 1 | Écran caractères 20 col × 4 lig |
| Module I²C PCF8574 | PCF8574 | 1 | Intégré au LCD (adresse 0x27) |

**Spécifications LCD** :
- Résolution : 20 colonnes × 4 lignes
- Type : Caractères (5×7 pixels)
- Adresse I²C : 0x27 (configurable)
- Alimentation : 5V, ~30mA
- Rétro-éclairage : LED bleu

**Connexions** :
- SDA → Arduino Pin 20
- SCL → Arduino Pin 21
- Vcc → +5V
- GND → GND

---

## 🎛️ Capteurs de niveau (Potentiomètres)

| Composant | Référence | Qté | Description |
|-----------|-----------|-----|-------------|
| Potentiomètre 10kΩ | POT10K | 4 | Simulation capteurs niveau |
| Condensateur 100nF | C100N | 4 | Filtrage analogique |

**Configuration** :
```
     +5V
      │
      R (10kΩ potentiomètre)
      │
      └─── Pin A0/A1/A2/A3 (Arduino)
      │
     GND
```

**Affectation** :
- POT1 → A0 (Niveau eau)
- POT2 → A1 (Niveau savon)
- POT3 → A2 (Niveau détergent)
- POT4 → A3 (Niveau rinçage)

---

## 🔘 Boutons de commande

| Composant | Référence | Qté | Description |
|-----------|-----------|-----|-------------|
| Bouton poussoir 12mm | SW_PUSH | 4 | Commandes menu |
| Condensateur 100nF | C100N | 4 | Débounce analogique |
| Résistance 10kΩ | R10K | 4 | Protection entrée |
| LED rouge 3mm | LED_RED | 4 | Indication appui |
| Résistance 470Ω | R470 | 4 | Limitation courant LED |

**Affectation** :
- SW1 → Pin 28 (Bouton Menu)
- SW2 → Pin 29 (Bouton Haut ↑)
- SW3 → Pin 30 (Bouton Bas ↓)
- SW4 → Pin 31 (Bouton OK)

**Configuration** :
```
Bouton
  │
  └─ GND (Pull-up interne Arduino)
  │
  └─ Arduino Pin (INPUT_PULLUP)

LED d'indication :
  Anode (+) ──470Ω── Arduino Pin (HIGH = allumé)
  Cathode (-) ─── GND
```

---

## 🚨 Signaux de simulation machine

| Composant | Référence | Qté | Description |
|-----------|-----------|-----|-------------|
| Bouton poussoir 12mm | SW_SIGNAL | 4 | Signaux auto |
| LED bleu 3mm | LED_BLUE | 4 | Indication signal |
| Résistance 470Ω | R470 | 4 | Limitation courant |

**Affectation** :
- SIGNAL1 → Pin 32 (START automatique)
- SIGNAL2 → Pin 33 (STOP automatique)
- SIGNAL3 → Pin 34 (MODE automatique)
- SIGNAL4 → Pin 35 (TEMP automatique)

---

## 💾 Mémoire et Alimentation

| Composant | Référence | Qté | Description |
|-----------|-----------|-----|-------------|
| Crystal 16MHz | XTAL16 | 1 | Horloge Arduino |
| Condensateur 22pF | C22P | 2 | Stabilisation crystal |
| Condensateur 10µF | C10U | 1 | Reset circuit |
| Résistance 10kΩ | R10K | 1 | Pull-up reset |
| Condensateur 100µF | C100U | 2 | Filtrage alimentation |
| Condensateur 10µF | C10U | 4 | Découplage +5V |

**Schéma de puissance** :
```
         USB/Adaptateur
            │
            ↓
         Régulateur 5V
            │
         +5V ─────────────────┐
            │                 │
         [C100µ]           [C10µ]
            │                 │
            ├─────[Masse]─────┤
            │
    Distribué à tous les circuits
```

---

## 🔌 Résistances

| Valeur | Qté | Fonction |
|--------|-----|----------|
| 470Ω | 12 | Limitation courant LED (12 LEDs) |
| 10kΩ | 10 | Pull-up, protection, debounce |
| 1kΩ | 4 | Pull-down optionnel |
| 100Ω | 2 | Protection sorties |

**Tolérance** : 5% (standard)

---

## 🔋 Condensateurs

| Valeur | Qté | Fonction |
|--------|-----|----------|
| 100nF (0.1µF) | 12 | Filtrage, debounce |
| 10µF | 6 | Découplage, filtrage |
| 100µF | 2 | Filtrage alimentation |
| 22pF | 2 | Crystal circuit |

**Tension** : 25V minimum

---

## ⚡ Diodes

| Composant | Référence | Qté | Description |
|-----------|-----------|-----|-------------|
| Diode silicium 1N4007 | D1N4007 | 6 | Roue libre relais |
| Diode zener 5.1V | DZ5V1 | 2 | Protection opcional |

**Caractéristiques diodes de protection** :
- Type : Silicium rapide
- Tension inverse max : 1000V
- Courant max : 1A
- Temps recouvrement : <75ns

**Installation** :
```
Bobine relais :
    ↑ Vcc
    │
   ╱│ Diode (cathode vers Vcc)
   ─┤
    │ Bobine
    │
    ↓ Vers Arduino Pin
```

---

## 🎨 LEDs d'indication

| Type | Couleur | Qté | Fonction |
|------|---------|-----|----------|
| LED 3mm | Rouge | 6 | Indication relais actif |
| LED 3mm | Rouge | 4 | Indication bouton menu |
| LED 3mm | Bleu | 4 | Indication signaux auto |
| LED 3mm | Vert | 0 | Réservé future |

**Caractéristiques LED** :
- Tension nominale : 2V rouge, 3V bleu
- Courant nominal : 20mA
- Puissance : 0.1W
- Limite courant : Résistance 470Ω

---

## 📊 Tableau de distribution

| Section | Vcc | GND | Qté pins |
|---------|-----|-----|----------|
| Arduino Mega | 2 | 4 | 6 pins |
| Relais | 1 | 1 | 2 pins |
| LCD I²C | 1 | 1 | 2 pins |
| Capteurs | 4 | 0 | 4 pins A |
| Boutons | 0 | 4 | 4 pins + GND |
| Signaux | 0 | 4 | 4 pins + GND |

**Total** :
- Pins numériques utilisées : 14 (28-35) + 6 (22-27) = 20
- Pins analogiques utilisées : 4 (A0-A3)
- Pins I²C utilisées : 2 (SDA/SCL)

---

## 🛠️ Outils de simulation Proteus

| Outil | Fonction |
|------|----------|
| Voltmeter | Mesurer tension |
| Ammeter | Mesurer courant |
| Oscilloscope | Visualiser signaux |
| Power Probe | Points de test |
| Logic Analyzer | Signaux numériques |

---

## 📝 Notes de composants

1. **Arduino Mega** : Clonage acceptable (Elegoo, etc)
2. **Relais** : Module 6 canaux 5V standard
3. **LCD I²C** : Adresse peut varier (0x26, 0x27, 0x3F)
4. **LEDs** : 3mm ou 5mm selon préférence
5. **Résistances** : Tolérance 5% suffisante
6. **Alimentation** : 2A @ 5V minimum

---

## 💰 Coût approximatif (€)

| Composant | Coût unitaire | Qté | Total |
|-----------|--------------|-----|-------|
| Arduino Mega | 8-15 | 1 | 15 |
| Module relais 6 voies | 5-10 | 1 | 8 |
| LCD 20×4 I²C | 4-8 | 1 | 6 |
| Potentiomètres | 0.5 | 4 | 2 |
| Boutons | 0.5 | 8 | 4 |
| LEDs | 0.1 | 14 | 1.4 |
| Résistances | 0.05 | 30 | 1.5 |
| Condensateurs | 0.1 | 20 | 2 |
| Câbles/Connecteurs | - | - | 5 |
| Divers | - | - | 5 |
| **TOTAL** | | | **~50€** |

---

## ✅ Checklist de vérification

- [ ] Tous les composants présents
- [ ] Aucun composant défectueux
- [ ] Connexions correctes
- [ ] Polarités respectées (LEDs, diodes)
- [ ] Valeurs résistances/condensateurs vérifiées
- [ ] Tension d'alimentation correcte (5V)
- [ ] Courant disponible suffisant (2A)
- [ ] Simulation démarre sans erreurs

---

**Dernière mise à jour** : 2024
