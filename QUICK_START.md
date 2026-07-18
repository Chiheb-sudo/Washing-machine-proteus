# 📋 GUIDE D'INSTALLATION ET DE DÉMARRAGE RAPIDE
## Machine à Laver Automatisée - Simulation Proteus

---

## 📦 CONTENU DU PROJET TÉLÉCHARGÉ

Votre dossier `Washing-machine-proteus` contient :

```
Washing-machine-proteus/
│
├── 📂 Arduino/
│   └── WashingMachine.ino              ← Code Arduino complet (450 lignes)
│
├── 📂 Proteus/
│   ├── WashingMachine.pdsprj           ← FICHIER PRINCIPAL A OUVRIR ⭐
│   ├── WashingMachine.dsn              ← Schéma ISIS
│   ├── WashingMachine.net              ← Netlist ISIS
│   └── README.txt                      ← Notes simulation
│
├── 📂 Documentation/
│   ├── PINOUT.md                       ← Assignation des pins détaillée
│   ├── SCHEMA_DESCRIPTION.md           ← Description complète du schéma
│   ├── SIMULATION_GUIDE.md             ← Guide pas à pas de simulation
│   ├── COMPONENTS_LIST.md              ← Liste de tous les composants
│   └── SCHEMATIC_ASCII.txt             ← Diagramme ASCII du système
│
└── README.md                           ← Vue d'ensemble du projet
```

---

## 🚀 DÉMARRAGE EN 3 ÉTAPES

### ✅ Étape 1 : Installation de Proteus
```
1. Téléchargez Proteus 8.7 ou supérieur
   https://www.labcenter.com/downloads/
2. Installez le logiciel
3. Assurez-vous que la licence est valide
```

### ✅ Étape 2 : Ouvrir le projet
```
1. Lancez Proteus
2. Allez à File → Open Project
3. Naviguez vers: Proteus/WashingMachine.pdsprj
4. Cliquez "Open"
```

### ✅ Étape 3 : Lancer la simulation
```
1. Cliquez sur le bouton ▶ PLAY (ou F5)
2. La simulation démarre
3. L'écran LCD affiche l'accueil
4. Commencez à tester !
```

---

## 🎮 CONTRÔLES DE BASE

### Les 4 Boutons principaux
```
┌─────────────────────────────────────────┐
│  [MENU]        [HAUT ↑]                 │
│                                         │
│  [BAS ↓]       [OK]                     │
└─────────────────────────────────────────┘

Fonctions:
- MENU  : Navigue entre les écrans (Normal → Mode → Temp → Capteurs)
- HAUT  : Change sélection vers le haut
- BAS   : Change sélection vers le bas
- OK    : Confirme et démarre le cycle
```

### Les 4 Signaux automatiques
```
Boutons supplémentaires:
- START : Démarre le cycle automatiquement
- STOP  : Arrête le cycle
- MODE  : Change mode (Normal/Délicat/Coton)
- TEMP  : Change température (Froid/Tiède/Chaud)
```

### Les 4 Potentiomètres (Capteurs)
```
Sliders à ajuster avec la souris:
- Niveau eau        (A0)
- Niveau savon      (A1)
- Niveau détergent  (A2)
- Niveau rinçage    (A3)
```

---

## 📊 CYCLE DE LAVAGE COMPLET

La simulation exécute automatiquement ce cycle:

```
PHASE 1: REMPLISSAGE (3 secondes)
├─ Électrovanne EAU        → ACTIVE (LED K1 rouge)
├─ Électrovanne SAVON      → ACTIVE (LED K2 rouge)
└─ LCD affiche: "Remplissage en cours..."

PHASE 2: LAVAGE (5 secondes)
├─ Électrovanne DÉTERGENT  → ACTIVE (LED K3 rouge)
├─ Moteur ESSORAGE         → ACTIF (LED K6 rouge)
└─ LCD affiche: "Lavage en cours..."

PHASE 3: RINÇAGE (4 secondes)
├─ Électrovanne RINÇAGE    → ACTIVE (LED K4 rouge)
└─ LCD affiche: "Rinçage en cours..."

PHASE 4: VIDANGE (2 secondes)
├─ Pompe VIDANGE           → ACTIVE (LED K5 rouge)
└─ LCD affiche: "Vidange en cours..."

PHASE 5: ESSORAGE (3 secondes)
├─ Moteur ESSORAGE         → VITESSE MAX (LED K6 rouge)
└─ LCD affiche: "Essorage en cours..."

PHASE 6: FIN (< 1 seconde)
├─ Tous les relais OFF
└─ Retour au menu principal
```

**Durée totale: ~17 secondes**

---

## 💡 EXEMPLES D'UTILISATION

### Exemple 1 : Démarrer un cycle Normal à Froid

```
1. Appuyez sur [MENU]
2. Sélectionnez "Normal" (déjà sélectionné)
3. Appuyez sur [OK]
4. Sélectionnez "Froid" (déjà sélectionné)
5. Appuyez sur [OK]
6. Le cycle démarre !
```

### Exemple 2 : Tester les capteurs

```
1. Appuyez sur [MENU] 3 fois pour aller au menu Capteurs
2. Vous voyez: "Eau:XX% Savon:XX% Deterg:XX% Rinc:XX%"
3. Déplacez les potentiomètres avec la souris
4. Les valeurs LCD changent en temps réel
```

### Exemple 3 : Arrêter le cycle en cours

```
1. Pendant un cycle en cours
2. Cliquez sur le bouton [STOP] (signal)
3. Tous les relais s'éteignent immédiatement
4. La machine revient au menu
```

---

## 🔌 ARCHITECTURE MATÉRIELLE RÉSUMÉE

### Microcontrôleur
- **Arduino Mega 2560** : Processeur 16MHz, 256KB Flash

### Commandes
- **6 Relais** : Eau, Savon, Détergent, Rinçage, Vidange, Essorage
- **4 Boutons** : Menu, Haut, Bas, OK
- **4 Signaux** : Start, Stop, Mode, Temp

### Affichage
- **LCD 20×4 I²C** : Adresse 0x27, interface I²C

### Capteurs
- **4 Potentiomètres** : Simulation des niveaux des bidons

### Protection
- **6 Diodes** : Protection des relais (1N4007)
- **14 LEDs** : Indication des états
- **Alimentation** : 5V 2A minimum

---

## ⚙️ CONFIGURATION LOGICIELLE

### Arduino IDE (si vous modifiez le code)
```
1. Ouvrez Arduino/WashingMachine.ino
2. Sélectionnez Board: Arduino Mega 2560
3. Port: COM3 (ou le port de votre Arduino)
4. Téléversez le code
```

### Bibliothèques requises
```
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
```

### Adresse LCD I²C
```
LCD initialisée à: 0x27
Si l'écran ne s'affiche pas, testez: 0x26, 0x3F, etc.
```

---

## 🧪 POINTS DE TEST

### Test 1 : Affichage LCD
- [ ] Écran d'accueil visible (2 sec)
- [ ] Menu principal visible
- [ ] Tous les menus naviguent correctement

### Test 2 : Boutons
- [ ] [MENU] change d'écran
- [ ] [HAUT] et [BAS] changent sélection
- [ ] [OK] confirme
- [ ] Les LEDs s'allument quand appuyé

### Test 3 : Relais
- [ ] K1 s'allume phase 1 (EAU)
- [ ] K2 s'allume phase 1 (SAVON)
- [ ] K3 s'allume phase 2 (DÉTERGENT)
- [ ] K4 s'allume phase 3 (RINÇAGE)
- [ ] K5 s'allume phase 4 (VIDANGE)
- [ ] K6 s'allume phase 5 (ESSORAGE)

### Test 4 : Capteurs
- [ ] Potentiomètre A0 change niveau eau
- [ ] Potentiomètre A1 change niveau savon
- [ ] Potentiomètre A2 change niveau détergent
- [ ] Potentiomètre A3 change niveau rinçage

### Test 5 : Signaux automatiques
- [ ] START démarre le cycle
- [ ] STOP arrête le cycle
- [ ] MODE change le mode
- [ ] TEMP change la température

---

## 🐛 DÉPANNAGE COURANT

### Problème: "L'écran LCD est vide"
```
Solution:
1. Vérifier les connexions SDA/SCL
2. Vérifier l'adresse I²C (devrait être 0x27)
3. Redémarrer la simulation (F5)
4. Vérifier l'alimentation 5V
```

### Problème: "Les boutons ne réagissent pas"
```
Solution:
1. Cliquer directement sur le bouton dans Proteus
2. Vérifier les pins 28-31 ne sont pas en conflit
3. Vérifier la connexion GND
```

### Problème: "Les relais ne s'activent pas"
```
Solution:
1. Vérifier les pins sorties 22-27
2. Vérifier l'alimentation 5V des relais
3. Vérifier que le cycle est en cours
4. Consulter la console pour les erreurs
```

### Problème: "La simulation est lente"
```
Solution:
1. Réduire la fréquence d'horloge
2. Fermer les autres applications
3. Utiliser le mode "Normal" au lieu de "Fastest"
```

---

## 📚 FICHIERS IMPORTANTS

| Fichier | Fonction |
|---------|----------|
| `WashingMachine.pdsprj` | Fichier principal Proteus (OUVRIR CELUI-CI) |
| `WashingMachine.dsn` | Schéma ISIS complet |
| `WashingMachine.ino` | Code Arduino source |
| `PINOUT.md` | Détail des connexions |
| `SIMULATION_GUIDE.md` | Guide complet de simulation |

---

## 🎓 PROCHAINES ÉTAPES

### Pour approfondir:
1. Lisez `SIMULATION_GUIDE.md` pour guide détaillé
2. Consultez `SCHEMA_DESCRIPTION.md` pour architecture
3. Examinez `COMPONENTS_LIST.md` pour tous les composants

### Pour modifier:
1. Éditez `Arduino/WashingMachine.ino`
2. Recompilez avec Arduino IDE
3. Générez le fichier HEX
4. Rechargez dans Proteus

### Pour améliorer:
- Ajouter capteur de température
- Ajouter WiFi (ESP8266)
- Ajouter écran graphique
- Ajouter alarme sonore

---

## ✅ VÉRIFICATION FINALE

Avant d'utiliser le projet:

```
☐ Proteus 8.7+ installé
☐ Fichier WashingMachine.pdsprj accessible
☐ Arduino IDE optionnellement installé
☐ Tous les fichiers décompressés
☐ Pas d'erreurs d'accès
```

---

## 📞 SUPPORT ET RESSOURCES

### Documentation officielle
- Proteus: https://www.labcenter.com/
- Arduino: https://www.arduino.cc/
- LCD I²C: https://github.com/marcoschwartz/LiquidCrystal_I2C

### Dans ce projet
- Consultez les fichiers MD pour documentation
- Lisez les commentaires du code Arduino
- Utilisez SCHEMATIC_ASCII.txt pour comprendre

---

## 🎉 BON COURAGE !

Vous avez maintenant un projet Proteus complet et fonctionnel !

**Prochaines actions:**
1. ✅ Téléchargez les fichiers
2. ✅ Installez Proteus
3. ✅ Ouvrez WashingMachine.pdsprj
4. ✅ Appuyez sur F5
5. ✅ Profitez de la simulation ! 🚀

---

**Version**: 1.0  
**Date**: 2024  
**Statut**: ✅ Prêt pour simulation
