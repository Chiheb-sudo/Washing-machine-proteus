================================================================================
  PROJET MACHINE À LAVER AUTOMATISÉE - SIMULATION PROTEUS
================================================================================

📋 CONTENU DU DOSSIER

  WashingMachine.pdsprj  → Fichier projet Proteus principal
  WashingMachine.dsn     → Schéma ISIS (schéma électrique)
  README.txt             → Ce fichier


🚀 DÉMARRAGE RAPIDE

  1. Installez Proteus 8.x ou supérieur
  2. Ouvrez "WashingMachine.pdsprj"
  3. Cliquez sur le bouton PLAY (F5)
  4. Utilisez les boutons virtuels pour contrôler la machine
  5. Observez l'affichage LCD pour les informations


🔧 CONFIGURATION SYSTÈME

  Proteus Version:  8.7+
  Arduino Model:    Mega 2560
  Simulation Mode:  Interactive
  Timestep:         Auto
  Frequency:        10 MHz (recommended)


🎮 CONTRÔLES DE SIMULATION

  Boutons virtuels (4):
    - Menu   : Naviguer entre menus
    - Haut   : Sélection précédente
    - Bas    : Sélection suivante
    - OK     : Confirmer/Démarrer

  Potentiomètres (4):
    - Niveau eau
    - Niveau savon
    - Niveau détergent
    - Niveau rinçage

  Signaux automatiques (4):
    - START : Démarrer cycle
    - STOP  : Arrêter cycle
    - MODE  : Changer mode
    - TEMP  : Changer température


📊 SPÉCIFICATIONS

  Affichage:       LCD 20x4 caractères (I²C @ 0x27)
  Microcontrôleur: Arduino Mega 2560 (16 MHz)
  Relais:          6 unités (Eau, Savon, Détergent, Rinçage, Vidange, Essorage)
  Capteurs:        4 niveaux (Eau, Savon, Détergent, Rinçage)
  Boutons:         4 commandes + 4 signaux machine
  Cycle complet:   ~17 secondes (simulation)


⏱️ PHASES DU CYCLE DE LAVAGE

  Phase 1 - Remplissage (3s)  : Électrovannes eau + savon
  Phase 2 - Lavage (5s)       : Électrovanne détergent + moteur
  Phase 3 - Rinçage (4s)      : Électrovanne rinçage
  Phase 4 - Vidange (2s)      : Pompe vidange
  Phase 5 - Essorage (3s)     : Moteur essorage à vitesse max
  → Fin et retour menu (< 1s)


🔌 ARCHITECTURE MATÉRIELLE

  Relais (Sorties 22-27):
    22 → Électrovanne eau
    23 → Électrovanne savon
    24 → Électrovanne détergent
    25 → Électrovanne rinçage
    26 → Pompe vidange
    27 → Moteur essorage

  Capteurs (Entrées A0-A3):
    A0 → Niveau eau
    A1 → Niveau savon
    A2 → Niveau détergent
    A3 → Niveau rinçage

  Boutons (Entrées 28-31):
    28 → Menu
    29 → Haut
    30 → Bas
    31 → OK

  LCD I²C (Pins 20-21):
    SDA → Pin 20
    SCL → Pin 21
    Addr → 0x27

  Signaux Machine (Entrées 32-35):
    32 → Signal START
    33 → Signal STOP
    34 → Signal MODE
    35 → Signal TEMP


💡 ASTUCES D'UTILISATION

  • Cliquez sur les boutons pour les actionner
  • Clic-droit sur potentiomètres pour ajuster manuellement
  • Observez les LEDs relais qui s'allument/éteignent
  • Vérifiez la console pour les messages de cycle
  • Utilisez le menu "Capteurs" pour voir les niveaux en temps réel


⚠️ DÉPANNAGE

  LCD vide?
    → Vérifier connexions SDA/SCL
    → Vérifier adresse I²C (0x27)
    → Vérifier alimentation 5V

  Boutons ne réagissent pas?
    → Cliquer directement sur le bouton virtuel
    → Vérifier pins 28-31 libres
    → Réinitialiser simulation (F5)

  Relais n'activent pas?
    → Vérifier pins sorties (22-27)
    → Vérifier alimentation relais
    → Attendre phase correspondante du cycle

  Simulation lente?
    → Réduire fréquence horloge
    → Fermer autres applications
    → Utiliser mode "Normal" au lieu de "Fastest"


📝 FICHIERS ASSOCIÉS

  Arduino/
    └─ WashingMachine.ino      Code source Arduino complet

  Documentation/
    ├─ PINOUT.md               Assignation détaillée des pins
    ├─ SCHEMA_DESCRIPTION.md   Description du schéma ISIS
    ├─ SIMULATION_GUIDE.md     Guide complet de simulation
    └─ COMPONENTS_LIST.md      Liste complète des composants


🔗 RESSOURCES

  Arduino Mega:   https://www.arduino.cc/en/Guide/ArduinoMega2560
  Proteus:        https://www.labcenter.com/
  LCD I²C Library: https://github.com/marcoschwartz/LiquidCrystal_I2C


✅ VÉRIFICATIONS

  Avant de lancer la simulation:
    ☐ Fichier .pdsprj présent
    ☐ Schéma .dsn chargé
    ☐ Arduino Mega visible en schéma
    ☐ Relais/Capteurs/Boutons connectés
    ☐ LCD I²C prêt

  Après démarrage simulation:
    ☐ LCD affiche l'accueil
    ☐ Boutons réagissent au clic
    ☐ Menus naviguent correctement
    ☐ Relais s'allument/s'éteignent
    ☐ Cycle s'exécute sans erreur


📞 SUPPORT

  Pour des questions ou problèmes:
  1. Consultez la documentation fournie
  2. Vérifiez les connexions schéma
  3. Testez chaque section individuellement
  4. Utilisez l'oscilloscope Proteus pour déboguer


================================================================================
Version: 1.0
Date: 2024
Statut: ✅ Fonctionnel et prêt pour simulation
================================================================================
