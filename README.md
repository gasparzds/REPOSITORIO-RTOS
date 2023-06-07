CODIGO:


#include <Arduino.h>

#include <Arduino_FreeRTOS.h>

#include <LiquidCrystal.h>

#define LED_PIN_1 12

#define LED_PIN_2 4

#define LED_PIN_3 5

void TaskReadTemperature(void *pvParameters);

void TaskBlink2(void *pvParameters);

void TaskBlink3(void *pvParameters);

LiquidCrystal lcd(12,11,10,9,8,7);

void TaskReadTemperature(void *pvParameters);

volatile float temperature = 0.0;

volatile float Valor_para_acender = 26.0;

void setup() {

pinMode(LED_PIN_1, OUTPUT);

pinMode(LED_PIN_2, OUTPUT);

pinMode(LED_PIN_3, OUTPUT);

 Serial.begin(9600);
 
 lcd.begin(16,2);


![image](https://github.com/gasparzds/REPOSITORIO-RTOS/assets/61299557/f87174fa-3bf6-4184-a1f3-3d47f0a52d0f)
