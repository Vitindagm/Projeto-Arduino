# Projeto-Arduino

Para programar um Arduino para detectar temperatura e umidade, você pode usar um sensor DHT11 ou DHT22, que são comumente utilizados para essas medições. Aqui está um exemplo básico de código usando a biblioteca DHT para Arduino:

Materiais Necessários:

Arduino (UNO, por exemplo)

Sensor DHT11 ou DHT22

Resistor 10kΩ (para o DHT22, opcional para o DHT11)

Fios Jumpers

Protoboard


Esquema de Ligação:

DHT11/DHT22:

VCC → 5V no Arduino

GND → GND no Arduino

DATA → Pino Digital 2 (ou outro pino digital à sua escolha no Arduino)



Código:

#include "DHT.h"

// Defina o tipo de sensor
#define DHTTYPE DHT11  // Se estiver usando o DHT22, troque por DHT22

// Defina o pino do sensor
#define DHTPIN 2

// Inicialize o sensor DHT
DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  Serial.println("Iniciando o sensor DHT");
  
  dht.begin();
}

void loop() {
  // Aguarde 2 segundos entre as leituras
  delay(2000);

  // Leitura da umidade
  float h = dht.readHumidity();
  // Leitura da temperatura em Celsius
  float t = dht.readTemperature();

  // Verifique se há erros de leitura
  if (isnan(h) || isnan(t)) {
    Serial.println("Erro ao ler o sensor DHT");
    return;
  }

  // Exiba os valores no Serial Monitor
  Serial.print("Umidade: ");
  Serial.print(h);
  Serial.print(" %\t");
  Serial.print("Temperatura: ");
  Serial.print(t);
  Serial.println(" °C");
}

Passos:

1. Instale a biblioteca DHT:

No Arduino IDE, vá em Sketch > Include Library > Manage Libraries.

Pesquise por "DHT" e instale a biblioteca "DHT sensor library for ESPx" por Adafruit.



2. Conecte o sensor ao Arduino de acordo com o esquema de ligação.


3. Copie e cole o código acima no Arduino IDE, selecione a placa correta e a porta, e carregue o código.



Agora o Arduino será capaz de ler a temperatura e a umidade e exibir esses valores no monitor serial.

