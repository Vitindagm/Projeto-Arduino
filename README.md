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

DATA → Pino Digital 2 (ou outro pino digital à sua escolha no Arduino

Codigo:
#include <DHT.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

#define DHTPIN 2     // Pino digital sensor DHT
#define DHTTYPE DHT11 // DHT 11

DHT dht(DHTPIN, DHTTYPE);

// Definir o endereço do LCD para 0x27 para um display de 16 caracteres e 2 linhas
LiquidCrystal_I2C lcd(0x27, 16, 2);  // Endereço do LCD, número de colunas e linhas

void setup() {
  Serial.begin(9600);
  Serial.println(F("DHTxx teste!"));

  dht.begin();

  // Inicializar o LCD com 16 colunas e 2 linhas
  lcd.begin(16, 2);
}

void loop() {
  // Aguarde alguns segundos entre as medições.
  delay(2000);

  // A leitura da temperatura ou umidade leva cerca de 250 milissegundos!
  // O sensor pode ter um atraso de até 2 segundos para a leitura
  float h = dht.readHumidity();
  float t = dht.readTemperature();

  // Verifique se alguma leitura falhou e tenta novamente.
  if (isnan(h) || isnan(t)) {
    Serial.println(F("Falha de leitura do sensor DHT!"));
    return;
  }

  // Compute heat index in Celsius (isFahreheit = false)
  float hic = dht.computeHeatIndex(t, h, false);

  Serial.print(F("Umidade: "));
  Serial.print(h);
  Serial.print(F("%  Temperatura: "));
  Serial.print(t);
  Serial.print(F("°C "));

  lcd.setBacklight(HIGH);

  lcd.setCursor(0, 0);
  lcd.print(F("Humidade: "));
  lcd.setCursor(10, 0);
  lcd.print(round(h));
  lcd.setCursor(12, 0);
  lcd.print(F(" %"));
  delay(3000);

  lcd.setCursor(0, 1);
  lcd.print(F("Tempo: "));
  lcd.setCursor(7, 1);
  lcd.print(round(t));
  lcd.setCursor(9, 1);
  lcd.write(32);  // Caracter espaço
  lcd.write(223); // Caracter °
  lcd.print(F("C"));
  delay(3000);
}

Passos:

1. Instale a biblioteca DHT:

No Arduino IDE, vá em Sketch > Include Library > Manage Libraries.

Pesquise por "DHT" e instale a biblioteca "DHT sensor library for ESPx" por Adafruit.



2. Conecte o sensor ao Arduino de acordo com o esquema de ligação.


3. Copie e cole o código acima no Arduino IDE, selecione a placa correta e a porta, e carregue o código.

4. Não esqueça de instalar bibliotecas necessarias caso precise.



Agora o Arduino será capaz de ler a temperatura e a umidade e exibir esses valores no monitor serial.

