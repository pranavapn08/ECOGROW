#define BLYNK_TEMPLATE_ID "TMPL3eEMfNwDR"
#define BLYNK_TEMPLATE_NAME "EcoGrow"
#define BLYNK_AUTH_TOKEN "TOKEN"

#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include <OneWire.h>
#include <DallasTemperature.h>

// WiFi Credentials
char ssid[] = "WiFi_Name";
char pass[] = "WiFi_Password";

// Pin Definitions
#define SOIL_SENSOR_DO D5
#define WATER_SENSOR_AO A0
#define TEMP_SENSOR_PIN D8
#define RELAY_PIN D6

// Temperature Sensor Setup
OneWire oneWire(TEMP_SENSOR_PIN);
DallasTemperature sensors(&oneWire);

// Blynk Virtual Pins
#define VPIN_SOIL V0
#define VPIN_WATER V1
#define VPIN_TEMP V2
#define VPIN_RELAY V3

void setup() {
  Serial.begin(9600);

  pinMode(SOIL_SENSOR_DO, INPUT);
  pinMode(WATER_SENSOR_AO, INPUT);
  pinMode(RELAY_PIN, OUTPUT);
  digitalWrite(RELAY_PIN, LOW); // motor OFF by default

  sensors.begin();  // Start temp sensor

  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);
}

void loop() {
  Blynk.run();

  // Read values
  int soilMoisture = digitalRead(SOIL_SENSOR_DO); // 0 = wet, 1 = dry
  int waterLevel = analogRead(WATER_SENSOR_AO);   // 0–1023
  sensors.requestTemperatures();
  float tempC = sensors.getTempCByIndex(0);

  // Send to Blynk
  Blynk.virtualWrite(VPIN_SOIL, soilMoisture);
  Blynk.virtualWrite(VPIN_WATER, waterLevel);
  Blynk.virtualWrite(VPIN_TEMP, tempC);

  delay(2000);  // Read every 2 seconds
}

// Control motor via Blynk button
BLYNK_WRITE(VPIN_RELAY) {
  int value = param.asInt();
  digitalWrite(RELAY_PIN, value);
}
