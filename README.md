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




1º PARTE - DESCRITIVO
#include <Arduino.h> //incluem as bibliotecas necessárias para o funcionamento do código.
#include <Arduino_FreeRTOS.h> //incluem as bibliotecas necessárias para o funcionamento do código.
#include <LiquidCrystal.h> // incluem as bibliotecas necessárias para o funcionamento do código.
#define LED_PIN_1 12 // Define constante para os pinos do LED
#define LED_PIN_2 4 // Define constante para os pinos do LED
#define LED_PIN_3 5 // Define constante para os pinos do LED
void TaskReadTemperature(void *pvParameters); // Essas linha é protótipo da função da tarefa, são declaradas aqui para que o compilador saiba que essas funções existem e possa usá-la posteriormente no código.
void TaskBlink2(void *pvParameters); // Essas linha é protótipo da função da tarefa, são declaradas aqui para que o compilador saiba que essas funções existem e possa usá-la posteriormente no código.
void TaskBlink3(void *pvParameters); // Essas linha é protótipo da função da tarefa, são declaradas aqui para que o compilador saiba que essas funções existem e possa usá-la posteriormente no código.

2º PARTE - DESCRITIVO
LiquidCrystal lcd(12,11,10,9,8,7);//Essa linha cria um objeto lcd do tipo LiquidCrystal para controlar o display LCD. Os números de 12, 11, 10, 9, 8 e 7 representam os pinos conectados ao display LCD para controlar as linhas e colunas.
void TaskReadTemperature(void *pvParameters); //Essa linha declara o protótipo da função TaskReadTemperature, que será responsável por ler a temperatura.
volatile float temperature = 0.0;//Essa linha declara uma variável temperature como um float e a define como volátil (volatile). A variável temperature será usada para armazenar o valor da temperatura lida.
volatile float Valor_para_acender = 26.0;//Essa linha declara uma variável Valor_para_acender como um float e a define como volátil (volatile). O valor dessa variável representa a temperatura em graus Celsius que, quando atingida, acenderá o LED correspondente.
void setup() { //A função setup() é uma função do Arduino que é chamada uma vez durante a inicialização do programa. Aqui estão algumas das ações realizadas:
pinMode(LED_PIN_1, OUTPUT);//INICIALIZAR OS PINOS DO LED'S COMO SAIDAS
pinMode(LED_PIN_2, OUTPUT);//INICIALIZAR OS PINOS DO LED'S COMO SAIDAS
pinMode(LED_PIN_3, OUTPUT);//INICIALIZAR OS PINOS DO LED'S COMO SAIDAS
 Serial.begin(9600); //inicia a comunicação serial com uma taxa de transmissão de 9600 bits por segundo. Isso permite a comunicação com o computador por meio da porta serial.
 lcd.begin(16,2); // inicia o display LCD com 16 colunas e 2 linhas. Isso configura o display para ser utilizado com essas dimensões.
 
3º PARTE - DESCRITIVO

 xTaskCreate( //Nesse bloco, a função xTaskCreate() é usada para criar a tarefa TaskReadTemperature
 TaskReadTemperature, //É o nome da função que será executada pela tarefa.
 "ReadTemperature", //É um nome descritivo para a tarefa.
 128, //É o tamanho da pilha em palavras (cada palavra geralmente tem 4 bytes).
 NULL, //É o parâmetro da tarefa (nesse caso, não é utilizado).
 3, //É a prioridade da tarefa (números maiores indicam prioridades mais altas).
 NULL ); //É o identificador da tarefa (nesse caso, não é utilizado).

xTaskCreate(//Nesse bloco, a função xTaskCreate() é usada para criar a tarefa TaskBlink2
  TaskBlink2, //É o nome da função que será executada pela tarefa.
  "Blink2", //É um nome descritivo para a tarefa.
  128, //É o tamanho da pilha em palavras (cada palavra geralmente tem 4 bytes).
  NULL, //É o parâmetro da tarefa (nesse caso, não é utilizado).
  5,  //É a prioridade da tarefa (números maiores indicam prioridades mais altas).
  NULL); //É o identificador da tarefa (nesse caso, não é utilizado).

xTaskCreate(//Nesse bloco, a função xTaskCreate() é usada para criar a tarefa TaskBlink3
  TaskBlink3, //É o nome da função que será executada pela tarefa.
  "Blink3", //É um nome descritivo para a tarefa.
  128, //É o tamanho da pilha em palavras (cada palavra geralmente tem 4 bytes).
  NULL, //É o parâmetro da tarefa (nesse caso, não é utilizado).
  6,  //É a prioridade da tarefa (números maiores indicam prioridades mais altas).
  NULL); //É o identificador da tarefa (nesse caso, não é utilizado).
  
 4º PARTE - DESCRITIVO
 void loop() {}
void TaskReadTemperature(void *pvParameters) { //Declaração da função TaskReadTemperature que recebe um ponteiro void como parâmetro.
  (void) pvParameters;
  float sensorValue = 0.0; //Declaração e inicialização da variável sensorValue como um número de ponto flutuante com valor inicial 0.0.
  for (;;) { //Início de um loop infinito.
    sensorValue = -10.0 + (rand() % 51); //Geração de um número aleatório entre -10 e 40 para simular a leitura de um sensor de temperatura.
    temperature = sensorValue; //Atribuição do valor de sensorValue à variável global temperature.
    vTaskDelay(2000 / portTICK_PERIOD_MS); //Atraso de 2 segundos usando a função vTaskDelay() do FreeRTOS.
    
    lcd.setCursor(0,0); //Define a posição do cursor do display LCD para a primeira coluna e primeira linha.
    lcd.print("Temp: "); //Imprime o texto "Temp: " no display LCD.
    lcd.print(temperature); //Imprime o valor da temperatura no display LCD.
    lcd.print(" C"); //Imprime a unidade de temperatura ("C") no display LCD.
  }
}
  
  
5º PARTE - DESCRITIVO
  void TaskBlink2(void *pvParameters){ //Declaração da função TaskBlink2 que recebe um ponteiro void como parâmetro.
  (void) pvParameters; //Ignora o parâmetro pvParameters e evita um aviso de variável não utilizada.
  for (;;){ //Início de um loop infinito.
    if (temperature == Valor_para_acender) { //Verifica se o valor da variável temperature é igual ao valor de Valor_para_acender. 
          digitalWrite(LED_PIN_2, HIGH); //Se for igual, acende o LED no pino LED_PIN_2
        } else {
          digitalWrite(LED_PIN_2, LOW); //caso contrário, apaga o LED.
        }
        vTaskDelay(3000 / portTICK_PERIOD_MS); //Aguarda um atraso de 3 segundos usando a função vTaskDelay() do FreeRTOS.
  }
}
    void TaskBlink3(void *pvParameters){ //Declaração da função TaskBlink3 que recebe um ponteiro void como parâmetro.
  (void) pvParameters; //Ignora o parâmetro pvParameters e evita um aviso de variável não utilizada.
  for (;;){ //Início de um loop infinito.
    digitalWrite(LED_PIN_3, HIGH); //Define o pino LED_PIN_3 como HIGH, acendendo o LED conectado a esse pino.
    vTaskDelay(500 / portTICK_PERIOD_MS); //Aguarda um atraso de 500 milissegundos usando a função vTaskDelay() do FreeRTOS.
    digitalWrite(LED_PIN_3, LOW); //Define o pino LED_PIN_3 como LOW, apagando o LED conectado a esse pino.
    vTaskDelay(500 / portTICK_PERIOD_MS); //Aguarda um atraso de 500 milissegundos usando a função vTaskDelay() do FreeRTOS.
  }
} //Fim do loop infinito.
  
