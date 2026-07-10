# ▶️ Guide Complet de Simulation Proteus

## 🚀 Démarrage rapide (5 minutes)

### Étape 1 : Ouvrir le projet
1. Lancez **Proteus 8.x** (ou supérieur)
2. Cliquez sur **File** → **Open Project**
3. Naviguez vers : `Proteus/WashingMachine.pdsprj`
4. Cliquez **Open**

### Étape 2 : Vérifier le schéma
1. Double-cliquez sur le fichier projet (ou cliquez sur l'onglet .dsn)
2. Vous devez voir le schéma ISIS complet avec :
   - Arduino Mega au centre
   - Relais à droite
   - Capteurs à gauche
   - Boutons en haut
   - LCD I²C en haut à droite

### Étape 3 : Démarrer la simulation
1. Cliquez sur le bouton **▶ PLAY** (barre d'outils)
   - Ou appuyez sur **F5**
   - Ou allez à **Simulate** → **Run**
2. La simulation démarre
3. L'écran LCD affiche l'écran d'accueil

### Étape 4 : Interagir
1. **Cliquez sur les boutons virtuels** :
   - [Menu] : Cycle entre les menus
   - [Haut] : Sélectionner option précédente
   - [Bas] : Sélectionner option suivante
   - [OK] : Confirmer/Démarrer
2. **Observez l'écran LCD** pour voir l'interface
3. **Les LED relais s'allument** quand les relais s'activent

---

## 📖 Guide détaillé de simulation

### Phase 1 : Démarrage et accueil

```
┌────────────────────────────┐
│    MACHINE A LAVER         │
│   Automatisee v1.0         │
└────────────────────────────┘
(Dure 2 secondes)
```

**Actions** :
- Attendez 2 secondes
- Puis vous verrez le menu principal

---

### Phase 2 : Menu principal

```
┌────────────────────────────┐
│ ==== MENU PRINCIPAL ====   │
│ Status: ARRET              │
│ Mode: Normal               │
│ Temp: Froid                │
└────────────────────────────┘
```

**Disponible** :
- Bouton [Menu] : Passe au menu Mode
- Bouton [OK] : Démarre le lavage immédiatement
- Boutons [Haut/Bas] : N'ont pas d'effet ici

---

### Phase 3 : Menu sélection Mode

```
┌────────────────────────────┐
│ ===== SELECTION MODE ====  │
│ > Normal                <--│
│ > Delicat               │
│ > Coton                 │
└────────────────────────────┘
```

**Actions** :
- Boutons [Haut/Bas] : Changent la sélection
- Bouton [OK] : Confirme et va au menu Température
- Bouton [Menu] : Retour au menu principal

**Modes disponibles** :
- Normal : 60°C, 1400 tr/min
- Délicat : 30°C, 800 tr/min
- Coton : 40°C, 1200 tr/min

---

### Phase 4 : Menu sélection Température

```
┌────────────────────────────┐
│ ==== SELECTION TEMP ====   │
│ > Froid                 <--│
│ > Tiede                 │
│ > Chaud                 │
└────────────────────────────┘
```

**Actions** :
- Boutons [Haut/Bas] : Changent la sélection
- Bouton [OK] : Confirme et démarre le cycle
- Bouton [Menu] : Retour au menu Mode

**Températures** :
- Froid : 15°C
- Tiède : 30°C
- Chaud : 60°C

---

### Phase 5 : Cycle de lavage

Une fois [OK] confirmé, le cycle démarre :

#### 🕐 Phase 1 : Remplissage (3 sec)
```
Action: Électrovannes EAU + SAVON activées
LEDs relais: RED (22, 23)
Capteurs: Niveau eau augmente
```

#### 🕑 Phase 2 : Lavage (5 sec)
```
Action: Électrovanne DÉTERGENT activée
LEDs relais: RED (24)
Moteur: Tourne (essorage ralenti)
```

#### 🕒 Phase 3 : Rinçage (4 sec)
```
Action: Électrovanne RINÇAGE activée
LEDs relais: RED (25)
Eau: Circule pour rincer
```

#### 🕓 Phase 4 : Vidange (2 sec)
```
Action: Pompe VIDANGE activée
LEDs relais: RED (26)
Eau: S'écoule
```

#### 🕔 Phase 5 : Essorage (3 sec)
```
Action: Moteur ESSORAGE à vitesse max
LEDs relais: RED (27)
Vibrations: Simulation essorage
```

#### ✅ Fin du cycle (< 1 sec)
```
Retour au menu principal
Message en console: "--- CYCLE TERMINÉ ---"
```

---

## 🎮 Commandes de simulation

### Boutons virtuels

| Bouton | Fonction | Accès |
|--------|----------|-------|
| [Menu] | Passe menu suivant | Toujours |
| [Haut] | Sélection précédente | Menu Mode/Temp |
| [Bas] | Sélection suivante | Menu Mode/Temp |
| [OK] | Confirme/Démarre | Toujours |

### Signaux automatiques

| Pin | Signal | Effet |
|-----|--------|-------|
| 32 | START | Démarre le cycle immédiatement |
| 33 | STOP | Arrête le cycle |
| 34 | MODE | Change mode (Normal→Délicat→Coton) |
| 35 | TEMP | Change température (Froid→Tiède→Chaud) |

---

## 📊 Observation des capteurs

### Menu Capteurs

```
┌────────────────────────────┐
│ ==== CAPTEURS ====         │
│ Eau:75% Savon:42%          │
│ Deterg:38% Rinc:65%        │
│ Relais actifs: 2           │
└────────────────────────────┘
```

**Comment modifier les niveaux** :
1. Cliquez droit sur un potentiomètre
2. Sélectionnez **Rotate** ou **Slider**
3. Ajustez la valeur (0-100%)
4. Observe le changement à l'écran LCD

**Interprétation** :
- 0% = Bidon vide
- 50% = Bidon à moitié
- 100% = Bidon plein

---

## 🔍 Vérifications de simulation

### Checklist de fonctionnement

- [ ] LCD affiche correctement (4 lignes)
- [ ] Boutons réagissent au clic
- [ ] Menus naviguent correctement
- [ ] Relais s'allument/s'éteignent en ordre
- [ ] Cycle dure ~17 secondes total
- [ ] Capteurs lisent les potentiomètres
- [ ] LEDs relais clignotent
- [ ] Console affiche messages cycle

### Tests détaillés

#### Test 1 : Affichage LCD
```
✓ Étape 1: Vérifier écran d'accueil (2 sec)
✓ Étape 2: Vérifier menu principal
✓ Étape 3: Vérifier menu modes
✓ Étape 4: Vérifier menu températures
✓ Étape 5: Vérifier menu capteurs
```

#### Test 2 : Navigation boutons
```
✓ Menu : Cycle entre écrans
✓ Haut : Change sélection (défile vers le haut)
✓ Bas : Change sélection (défile vers le bas)
✓ OK : Confirme action
```

#### Test 3 : Relais et séquençage
```
✓ Rel 1 (Eau) : S'allume phase 1
✓ Rel 2 (Savon) : S'allume phase 1
✓ Rel 3 (Détergent) : S'allume phase 2
✓ Rel 4 (Rinçage) : S'allume phase 3
✓ Rel 5 (Vidange) : S'allume phase 4
✓ Rel 6 (Essorage) : S'allume phase 5
✓ Tous s'éteignent après phase 5
```

#### Test 4 : Capteurs
```
✓ Modifier potentiomètre A0 → LCD change "Eau:%"
✓ Modifier potentiomètre A1 → LCD change "Savon:%"
✓ Modifier potentiomètre A2 → LCD change "Deterg:%"
✓ Modifier potentiomètre A3 → LCD change "Rinc:%"
```

---

## 🐛 Dépannage

### Problème 1 : L'écran LCD n'affiche rien

**Causes possibles** :
- Module I²C mal configuré
- Adresse I²C incorrecte (devrait être 0x27)
- Pas de rétro-éclairage

**Solutions** :
```
1. Vérifier connexions SDA/SCL
2. Vérifier alimentation LCD (5V)
3. Vérifier adresse I²C dans le code
   LiquidCrystal_I2C lcd(0x27, 20, 4);
4. Réinitialiser (F5 pour arrêter, puis Play)
```

### Problème 2 : Les boutons ne réagissent pas

**Causes possibles** :
- Boutons mal configurés
- Débounce trop long
- Pin incorrect

**Solutions** :
```
1. Vérifier pins (28-31)
2. Vérifier INPUT_PULLUP en setup
3. Réduire débounce si trop lent
4. Vérifier connexion GND
```

### Problème 3 : Les relais ne s'activent pas

**Causes possibles** :
- Pins sorties mal configurées
- Code de séquençage incorrect
- Alimentation insuffisante

**Solutions** :
```
1. Vérifier pinMode(RELAY_X, OUTPUT)
2. Vérifier digitalWrite(RELAY_X, HIGH/LOW)
3. Vérifier alimentation 5V
4. Vérifier courant disponible (2A min)
```

### Problème 4 : La simulation est lente

**Causes possibles** :
- Fréquence horloge trop haute
- Autres processus système
- RAM insuffisante

**Solutions** :
```
1. Réduire vitesse simulation (Settings)
2. Fermer autres programmes
3. Utiliser mode "Faster" au lieu de "Fastest"
4. Réduire timestep
```

---

## 📈 Statistiques de simulation

**Temps de cycle complet** : ~17 secondes  
**Nombre de relais** : 6  
**Nombre d'entrées analogiques** : 4  
**Nombre de boutons** : 4  
**Résolution LCD** : 20×4 caractères  
**Adresse I²C** : 0x27  

---

## 💡 Conseils d'optimisation

### Pour une meilleure simulation :

1. **Mode Full Screen**
   - Simulation → Settings → Simuler en plein écran

2. **Augmenter Performance**
   - Settings → Frequency = 20 MHz (max)
   - Timestep = Auto

3. **Afficher Graphiques**
   - Clic droit sur relais → Probe
   - Clic droit sur capteur → Probe Analog

4. **Enregistrer Données**
   - Tools → Generate Report
   - Exporte résultats en CSV

---

## 🎓 Exercices pratiques

### Exercice 1 : Test cycle complet
```
Durée : 5 minutes
Objectif : Faire tourner un cycle entier
Étapes :
1. Démarrer simulation
2. Sélectionner Mode = Normal
3. Sélectionner Temp = Chaud
4. Démarrer cycle
5. Observer toutes les phases
6. Vérifier fin cycle
```

### Exercice 2 : Test arrêt d'urgence
```
Durée : 3 minutes
Objectif : Tester arrêt en cours de cycle
Étapes :
1. Démarrer cycle
2. Attendre phase 3
3. Activer signal STOP (pin 33)
4. Vérifier tous relais s'éteignent
```

### Exercice 3 : Test capteurs limites
```
Durée : 5 minutes
Objectif : Vérifier lecture capteurs
Étapes :
1. Mettre pot A0 à 0%
2. Mettre pot A1 à 50%
3. Mettre pot A2 à 100%
4. Mettre pot A3 à 75%
5. Vérifier affichage LCD
```

---

## 📚 Ressources supplémentaires

- Documentation Proteus : `/Proteus/` folder
- Code Arduino : `/Arduino/WashingMachine.ino`
- Pinout : `Documentation/PINOUT.md`
- Schéma : `Documentation/SCHEMA_DESCRIPTION.md`

---

## ✅ Checklist avant déploiement réel

- [ ] Simulation fonctionne sans erreurs
- [ ] Tous les relais s'activent correctement
- [ ] LCD affiche correctement
- [ ] Capteurs lisent les bonnes valeurs
- [ ] Cycle complet fonctionne
- [ ] Arrêt d'urgence fonctionne
- [ ] Code commenté et documenté
- [ ] Pas d'avertissements à la compilation

---

**Bon test ! 🚀**
