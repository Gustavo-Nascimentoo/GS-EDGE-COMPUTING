# OrbitFlood — Sistema Inteligente de Monitoramento de Enchentes

## Integrantes

- Gustavo Almeida Lopes do Nascimento — RM: 571070
- João Gabriel Mosqueti Agra Cunha — RM: 572017
- Rafael Yuta Nischida — RM: 570552
- Leonardo Teodoro Leitão - RM: 569724

---

## Descrição

O **OrbitFlood** é um sistema inteligente de alerta de enchentes inspirado em tecnologias de monitoramento climático, sistemas embarcados e soluções utilizadas em cidades inteligentes.

O projeto utiliza sensores para simular a análise do ambiente, monitorando o **nível da água** e a **intensidade da chuva**, gerando alertas automáticos conforme o risco identificado.

---

## Objetivo

Monitorar o nível da água e detectar condições de risco de enchente, emitindo alertas preventivos através de sinais visuais e sonoros.

---

## Aplicação Real e Conceitos Utilizados

As enchentes urbanas representam um dos principais desafios ambientais e sociais das grandes cidades, causando alagamentos, prejuízos materiais, interrupção de serviços e riscos à população.

Atualmente, sistemas modernos de monitoramento utilizam sensores, automação e processamento de dados para prever situações críticas e permitir respostas mais rápidas. Inspirado nessas tecnologias, o **OrbitFlood** simula um sistema preventivo capaz de monitorar condições ambientais através do **nível da água** e da **intensidade da chuva**, gerando alertas automáticos conforme as condições detectadas.

O projeto aplica conceitos fundamentais de **Edge Computing**, realizando o processamento local dos dados diretamente no **Arduino**, sem depender de servidores externos ou processamento em nuvem.

Além disso, incorpora conceitos de **IoT (Internet of Things)**, **sensoriamento**, **monitoramento em tempo real** e **automação embarcada**, utilizando sensores para coleta de dados ambientais, análise das leituras obtidas e acionamento automático de LEDs e buzzer conforme o nível de risco identificado.

A lógica do sistema simula aplicações presentes em soluções de monitoramento climático, prevenção de desastres e infraestrutura de cidades inteligentes.

---

## Tecnologias Utilizadas

- Arduino
- C++
- Wokwi
- GitHub

---

## Componentes Utilizados

- Arduino Uno
- Sensor ultrassônico HC-SR04
- Sensor de chuva / umidade
- LED Verde
- LED Amarelo
- LED Vermelho
- Buzzer
- Resistores
- Jumpers

---

## Funcionamento

O sistema realiza duas leituras simultâneas:

### Sensor Ultrassônico (HC-SR04)

Mede a distância simulando o nível da água.

### Sensor de Chuva / Umidade

Simula a intensidade da chuva através de leitura analógica.

Com base nos valores detectados, o sistema classifica o ambiente em níveis de alerta.

### Estados do Sistema

### Seguro
- Água baixa
- Pouca chuva
- LED Verde ligado

### Atenção
- Água alta **OU** chuva intensa
- LED Amarelo ligado

### Risco Crítico
- Água alta **E** chuva intensa
- LED Vermelho ligado
- Buzzer acionado

---

## Ideia do Código Arduino

### Lógica Utilizada

```cpp
Se distância >= 20cm E chuva <= 700:
    LED Verde → SEGURO

Se distância < 20cm OU chuva > 700:
    LED Amarelo → ATENÇÃO

Se distância < 20cm E chuva > 700:
    LED Vermelho + Buzzer → RISCO CRÍTICO
```

---

## Código Arduino (C++)

```cpp
#define TRIG 9
#define ECHO 10

#define LED_VERDE 2
#define LED_AMARELO 3
#define LED_VERMELHO 4

#define BUZZER 5
#define SENSOR_CHUVA A0

void setup() {

  pinMode(TRIG, OUTPUT);
  pinMode(ECHO, INPUT);

  pinMode(LED_VERDE, OUTPUT);
  pinMode(LED_AMARELO, OUTPUT);
  pinMode(LED_VERMELHO, OUTPUT);

  pinMode(BUZZER, OUTPUT);

  Serial.begin(9600);
}

void loop() {

  digitalWrite(TRIG, LOW);
  delayMicroseconds(2);

  digitalWrite(TRIG, HIGH);
  delayMicroseconds(10);

  digitalWrite(TRIG, LOW);

  long duracao = pulseIn(ECHO, HIGH);

  float distancia = duracao * 0.034 / 2;

  int chuva = analogRead(SENSOR_CHUVA);

  Serial.print("Nivel da agua: ");
  Serial.print(distancia);
  Serial.println(" cm");

  Serial.print("Intensidade da chuva: ");
  Serial.println(chuva);

  if (distancia >= 20 && chuva <= 700) {

    digitalWrite(LED_VERDE, HIGH);
    digitalWrite(LED_AMARELO, LOW);
    digitalWrite(LED_VERMELHO, LOW);

    noTone(BUZZER);

    Serial.println("STATUS: SEGURO");
  }

  else if ((distancia < 20 && chuva <= 700) ||
           (distancia >= 20 && chuva > 700)) {

    digitalWrite(LED_VERDE, LOW);
    digitalWrite(LED_AMARELO, HIGH);
    digitalWrite(LED_VERMELHO, LOW);

    noTone(BUZZER);

    Serial.println("STATUS: ATENCAO");
  }

  else {

    digitalWrite(LED_VERDE, LOW);
    digitalWrite(LED_AMARELO, LOW);
    digitalWrite(LED_VERMELHO, HIGH);

    tone(BUZZER, 1000);

    Serial.println("STATUS: RISCO CRITICO");
  }

  Serial.println("---------------------------");

  delay(1000);
}
```

---

## Link do Projeto Wokwi

Adicionar link aqui:

```md
https://wokwi.com/projects/465209777453508609
```

---

## Entregáveis — Edge Computing

✅ Repositório GitHub

✅ README completo

✅ Código Arduino/C++

✅ Link do Wokwi

✅ Mesmo vídeo do Pitch
