# Real-Time Obstacle Detection & Non-Intrusive Debugging (STM32F411RE)

## Overview
Ce projet implémente un système d'alerte et de détection d'obstacles en temps réel basé sur un microcontrôleur ARM Cortex-M4 (STM32F411RE). L'objectif principal est de valider le comportement temporel du système à l'aide d'une méthodologie de débogage non-intrusif.

## Key Features
* **Firmware C / Timers :** Développement en bare-metal/HAL pour la gestion des périphériques (HC-SR04, buzzer et LED Heartbeat).
* **Gestion Matérielle :** Configuration précise de la PWM et de l'Input Capture (génération d'impulsion Trig 10 µs et mesure du temps de vol Echo).
* **Débogage Non-Intrusif :** Qualification temporelle via analyseur logique USB (**Saleae Logic 2** à 12 MS/s) évitant les breakpoints bloquants pour préserver le temps réel.
* **Validation :** Vérification des signaux (temps de réponse, largeur d'impulsion) et déclenchement d'alerte sur seuil critique (< 15 cm).

## Tech Stack & Tools
* **Microcontrôleur :** STM32F411RE (ARM Cortex-M4)
* **Capteurs/Actuateurs :** Ultrason (HC-SR04), Buzzer, LED
* **Langage & IDE :** C, STM32CubeIDE
* **Outils d'Analyse :** Saleae Logic 2, WinUSB / Zadig
# Real-Time Obstacle Detection & Non-Intrusive Debugging (STM32F411RE)

## Overview
Ce projet implémente un système d'alerte et de détection d'obstacles en temps réel basé sur un microcontrôleur ARM Cortex-M4 (STM32F411RE). L'objectif principal est de mesurer précisément la distance via capteur ultrason et de valider le comportement temporel du système à l'aide d'une méthodologie de débogage non-intrusif.

---

## Hardware Connection Diagram

```text
  +-------------------+              +----------------------+
  |    STM32F411RE    |              |   HC-SR04 Ultrasonic |
  |     (Nucleo)      |              +----------------------+
  |                   |              | VCC  ----> +5V       |
  |  PA8 (TIM1_CH1) --+------------->| TRIG                 |
  |  PA0 (TIM2_CH1) <-+--------------| ECHO                 |
  |  GND -------------+------------->| GND                  |
  |                   |              +----------------------+
  |                   |
  |  PA5 (Heartbeat) -+----> [ LED / Debug GPIO ]
  |  PB10 (PWM Out) --+----> [ Buzzer Alarm ]
  +-------------------+
            |
            | Debug Signals
            v
  +-------------------+
  |  Saleae Logic 2   |
  +-------------------+
  | CH0 <--- PA8 (Trig)
  | CH1 <--- PA0 (Echo)
  | CH3 <--- PA5 (Heartbeat GPIO)
  +-------------------+
## Project Structure
```text
├── Core/
│   ├── Inc/       # En-têtes (.h) pour timers, HC-SR04 et GPIO
│   └── Src/       # Fichiers sources (.c) et boucle principale
├── Docs/          # Captures d'écran Saleae Logic 2 (signaux Trig/Echo)
└── README.md
