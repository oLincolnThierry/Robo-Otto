# Robo-Otto 🤖
**Descrição:**
Este projeto demonstra como construir um robô Arduino. O código implementa um comportamento de evitação de obstáculos básico para o robô Otto, utilizando um sensor ultrassônico e uma lógica de controle simples para modificar a trajetória do robô em resposta a estímulos do ambiente.

![Robo-otto](https://github.com/user-attachments/assets/d68e4de0-ed10-415c-a4ff-d3917893058e)
# Projeto Robô Seguidor de Linha

**Instalação:**
1. Clone este repositório.
2. Instale as bibliotecas necessárias.
3. Carregue o código `sketch.ino` no Arduino.

**Código:**

```c++
//Projeto: Robô Otto com Arduino Nano
//Materiais Utilizados:

//1x Placa Nano V3.0 ATmega328P + Cabo USB (Compatível com Arduino)

//1x Módulo Adaptador para Expansão do Arduino Nano

//6x Micro Servo 9g SG90 TowerPro

//1x Campainha Ativo 5V 12mm

//1x Sensor Ultrassônico – HC-SR04

//1x Jumpers Fêmea/Fêmea 20 Vias – 20cm

Código:
cpp

Copiar
#include <Otto.h>

Otto Otto;

#define PernaEsq 2
#define PernaDir 3
#define PeEsq 4
#define PeDir 5
#define Buzzer 13
#define Trigger 8 // Pino trigger do sensor ultrassônico
#define Echo 9    // Pino echo do sensor ultrassônico

/**
 * @brief Emite uma onda ultrassônica para medir a distância
 * @return long distância
 */
long ultrasound() {
    long duration, distance;
    digitalWrite(Trigger, LOW);
    delayMicroseconds(2);
    digitalWrite(Trigger, HIGH);
    delayMicroseconds(10);
    digitalWrite(Trigger, LOW);
    duration = pulseIn(Echo, HIGH); // Duração do pulso(ms) do pino Echo.
    distance = duration / 58;       // Tempo em microssegundos dividido pelo dobro da
                                    // distância que o som percorre por microssegundo(cm)
    return distance;
}

/**
 * @brief setup
 */
void setup() {
    Otto.init(PernaEsq, PernaDir, PeEsq, PeDir, true, Buzzer); // Inicializa os pinos dos
                                                               // servos e Buzzer
    pinMode(Trigger, OUTPUT);
    pinMode(Echo, INPUT);
    Otto.swing(2, 1000, 20);       // Balançando de um lado para o outro
    Otto.shakeLeg(1, 2000, -1);    // Chacoalhar a perna direita
}

/**
 * @brief loop
 */
void loop() {
    if (ultrasound() <= 15) {       // Se a distância for menor ou igual a 15cm
        Otto.sing(S_surprise);      // Emite um som de surpresa
        Otto.walk(2, 1000, -1);     // Volta dois passos
        Otto.turn(4, 1000, 1);      // Faz uma curva pela esquerda em 3 passos
    }
    Otto.walk(1, 1000, 1);          // Anda um passo para frente
}
```
**Descrição de Funções**💻

 Função setup():

- Otto.init(PernaEsq, PernaDir, PeEsq, PeDir, true, Buzzer): Inicializa os pinos dos servos e do Buzzer.
- PernaEsq: Pino do servo da perna esquerda
- PernaDir: Pino do servo da perna direita
- PeEsq: Pino do servo do pé esquerdo
- PeDir: Pino do servo do pé direito
- true: Indica que o robô está usando um sensor ultrassônico
- Buzzer: Pino do Buzzer
- pinMode(Trigger, OUTPUT): Define o pino Trigger como saída.
- pinMode(Echo, INPUT): Define o pino Echo como entrada.
- Otto.swing(2, 1000, 20): Faz o robô balançar de um lado para o outro.
- 2: Número de vezes que o movimento deve ser executado
- 1000: Tempo de duração de cada movimento, em milissegundos
- 20: Ângulo de orientação do robô, em graus
- Otto.shakeLeg(1, 2000, -1): Faz o robô chacoalhar a perna direita.
- 1: Número de vezes que o movimento deve ser executado
- 2000: Tempo de duração de cada movimento, em milissegundos
- -1: Ângulo de inclinação da perna, em graus
- Função loop():
- if (ultrasound() <= 15): Verifica se a distância medida pelo sensor ultrassônico é menor ou igual a 15 cm.
- Otto.sing(S_surprise): Emite um som de surpresa.
- Otto.walk(2, 1000, -1): Dá dois passos para trás.
- 2: Número de passos
- 1000: Tempo de duração de cada passo, em milissegundos
- -1: Direção do movimento (1 para frente, -1 para trás)
- Otto.turn(4, 1000, 1): Faz uma curva pela esquerda em três passos.
- 4: Número de passos
- 1000: Tempo de duração de cada passo, em milissegundos
- 1: Direção do movimento (1 para frente, -1 para trás)

 Por fim, Otto.walk(1, 1000, 1) faz o robô andar um passo para frente.
