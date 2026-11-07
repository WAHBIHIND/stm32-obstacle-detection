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
