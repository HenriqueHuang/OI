/\*\*

- @file ESP32_DHT22_Send_MQTT.ino
- @author Saulo Aislan
- @brief Firmware que ler o sensor de temperatura, envia os dados via MQTT.
- @version 0.1
-
- @copyright Copyright (c) 2022
- \*/

#include "EspMQTTClient.h"
#include "DHTesp.h"

EspMQTTClient client(
"Wokwi-GUEST", // SSID WiFi
"", // Password WiFi
"broker.hivemq.com", // MQTT Broker
"mqtt-mack-pub-sub", // Client
1883 // MQTT port
);

const int DHT_PIN = 15;

DHTesp dhtSensor;

void setup()
{
Serial.begin(115200);

dhtSensor.setup(DHT_PIN, DHTesp::DHT22);

client.enableDebuggingMessages();
client.enableLastWillMessage("TestClient/lastwill", "Vou ficar offline");
}

void lerEnviarDados() {
TempAndHumidity data = dhtSensor.getTempAndHumidity();
client.publish("PokemonGo/Temperatura", String(data.temperature, 2) + "°C");
client.publish("PokemonGo/Umidade", String(data.humidity, 1) + "%");
}

/\*\*

- @brief Esta função é chamada quando tudo estiver conectado (Wifi e MQTT),
- para utilizá-la deve-se implemtentar o struct EspMQTTClient
  \*/
  void onConnectionEstablished()
  {
  client.subscribe("PokemonGo/#", [](const String & topic, const String & payload) {
  Serial.println("Mensagem recebida no topico: " + topic + ", payload: " + payload);
  });
  }

void loop()
{
client.loop(); // Executa em loop
lerEnviarDados();
delay(2000);
}
