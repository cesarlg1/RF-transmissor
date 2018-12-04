// pinos que funcionam normalmente com as interupcoes externas do arduino due- sam3x8e-au      //
//     2-3-4-5-10-11-12-13-23-24-25-26-27-28-29-30-31-33-42-43-49-51  


#include <SPI.h>
#include <nRF24L01.h>
#include <RF24.h>
#include <DueTimer.h>

RF24 radio(50, 52); // CE, CSN

const byte addresses[][6] = {"00001", "00002"};

//*************  pinos de entrada dos sensores  *************************
  int interrupcao1 = 2;                                     // pino digital 2
  int interrupcao2 = 3;                                     // pino digital 3
  int interrupcao3 = 4;                                     // pino digital 4
  int interrupcao4 = 5;                                     // pino digital 5
  int interrupcao5 = 10;                                     // pino digital 10
  int interrupcao6 = 11;                                     // pino digital 11
  int interrupcao7 = 12;                                     // pino digital 12
  int interrupcao8 = 13;                                     // pino digital 13
  int interrupcao9 = 24;                                    // pino digital 24
   
//*************  Controle de Contagem  *************************
   int sensor1_rf = 0;
   int sensor2_rf = 0;
   int sensor3_rf = 0;
   int sensor4_rf = 0;
   int sensor5_rf = 0;
   int sensor6_rf = 0;
   int sensor7_rf = 0;
   int sensor8_rf = 0;
   int sensor9_rf = 0;
   

//*************** Controle do Projeto LOCAL ************

   int sensor1 = 0;
   int sensor2 = 0;
   int sensor3 = 0;
   int sensor4 = 0;
   int sensor5 = 0;
   int sensor6 = 0;
   int sensor7 = 0;
   int sensor8 = 0;
   int sensor9 = 0;
 
   //*************  Controle de estado dos pinos de contagem  *******************
   
int buttonState1;
int buttonState2;
int buttonState3;
int buttonState4;
int buttonState5;
int buttonState6;
int buttonState7;
int buttonState8;
int buttonState9;

void setup() {
  
  radio.begin();
  Serial.begin(115200);
  
  //*************** Controle do TEMPORIZACAO ***********************
  
  Timer3.attachInterrupt(myHandler);
  Timer3.start(3000000); // Calls every 3 s
 
  //*************** Controle do RF ***********************
  
  radio.openWritingPipe(addresses[1]); // 00001
  radio.openReadingPipe(1, addresses[0]); // 00002
  radio.setPALevel(RF24_PA_MIN);

  
  //*************** seta os pinos de entrada com pullup ************

for (int i = 2; i <= 28; i++)                          // Define pinMode INPUT e em PULLUP para os pinos utilizados como interrupcao
  {
    pinMode(i, INPUT_PULLUP);                            // seta pull up do pino 2 ao 26
  }
  attachInterrupt(interrupcao1, interrupcao_1, FALLING);    // seta a leitura de interrupcao para o pino 2
  attachInterrupt(interrupcao2, interrupcao_2, FALLING);    // seta a leitura de interrupcao para o pino 3
  attachInterrupt(interrupcao3, interrupcao_3, FALLING);    // seta a leitura de interrupcao para o pino 4
  attachInterrupt(interrupcao4, interrupcao_4, FALLING);    // seta a leitura de interrupcao para o pino 5
  attachInterrupt(interrupcao5, interrupcao_5, FALLING);    // seta a leitura de interrupcao para o pino 6
  attachInterrupt(interrupcao6, interrupcao_6, FALLING);    // seta a leitura de interrupcao para o pino 7
  attachInterrupt(interrupcao7, interrupcao_7, FALLING);    // seta a leitura de interrupcao para o pino 8
  attachInterrupt(interrupcao8, interrupcao_8, FALLING);    // seta a leitura de interrupcao para o pino 9
  attachInterrupt(interrupcao9, interrupcao_9, FALLING);    // seta a leitura de interrupcao para o pino 10
}

void loop() {
      
   //*************** Controle de Contagem ************

    Serial.print("sensor1 : ");                              //imprime
    Serial.println(sensor1);                                 //imprime variavel
    Serial.print("sensor2 : ");                              //imprime
    Serial.println(sensor2);                                 //imprime variavel
    Serial.print("sensor3 : ");                              //imprime
    Serial.println(sensor3);                                 //imprime variavel
    Serial.print("sensor4 : ");                              //imprime
    Serial.println(sensor4);                                 //imprime variavel
    Serial.print("sensor5 : ");                              //imprime
    Serial.println(sensor5);                                 //imprime variavel
    Serial.print("sensor6 : ");                              //imprime
    Serial.println(sensor6);                                 //imprime variavel
    Serial.print("sensor7 : ");                              //imprime
    Serial.println(sensor7);                                 //imprime variavel
    Serial.print("sensor8 : ");                              //imprime
    Serial.println(sensor8);                                 //imprime variavel
    Serial.print("sensor9 : ");                              //imprime
    Serial.println(sensor9);                                 //imprime variavel

    Serial.print("sensor1_rf : ");                              //imprime
    Serial.println(sensor1_rf);                                 //imprime variavel
    Serial.print("sensor2_rf : ");                              //imprime
    Serial.println(sensor2_rf);                                 //imprime variavel
    Serial.print("sensor3_rf : ");                              //imprime
    Serial.println(sensor3_rf);                                 //imprime variavel
    Serial.print("sensor4_rf : ");                              //imprime
    Serial.println(sensor4_rf);                                 //imprime variavel
    Serial.print("sensor5_rf : ");                              //imprime
    Serial.println(sensor5_rf);                                 //imprime variavel
    Serial.print("sensor6_rf : ");                              //imprime
    Serial.println(sensor6_rf);                                 //imprime variavel
    Serial.print("sensor7_rf : ");                              //imprime
    Serial.println(sensor7_rf);                                 //imprime variavel
    Serial.print("sensor8_rf : ");                              //imprime
    Serial.println(sensor8_rf);                                 //imprime variavel
    Serial.print("sensor9_rf : ");                              //imprime
    Serial.println(sensor9_rf);                                 //imprime variavel
        
    Serial.print("estado sensor1 : ");                              //imprime
    Serial.println(buttonState1);                                 //imprime variavel
    Serial.print("estado sensor2 : ");                              //imprime
    Serial.println(buttonState2);                                 //imprime variavel
    Serial.print("estado sensor3 : ");                              //imprime
    Serial.println(buttonState3);                                 //imprime variavel
    Serial.print("estado sensor4 : ");                              //imprime
    Serial.println(buttonState4);                                 //imprime variavel
    Serial.print("estado sensor5 : ");                              //imprime
    Serial.println(buttonState5);                                 //imprime variavel
    Serial.print("estado sensor6 : ");                              //imprime
    Serial.println(buttonState6);                                 //imprime variavel
    Serial.print("estado sensor7 : ");                              //imprime
    Serial.println(buttonState7);                                 //imprime variavel
    Serial.print("estado sensor8 : ");                              //imprime
    Serial.println(buttonState8);                                 //imprime variavel
    Serial.print("estado sensor9 : ");                              //imprime
    Serial.println(buttonState9);                                 //imprime variavel
    
  
  // ***********************    controle de estados dos pinos   ***********************

    buttonState1 = digitalRead(interrupcao1);
    buttonState2 = digitalRead(interrupcao2);
    buttonState3 = digitalRead(interrupcao3);
    buttonState4 = digitalRead(interrupcao4);
    buttonState5 = digitalRead(interrupcao5);
    buttonState6 = digitalRead(interrupcao6);
    buttonState7 = digitalRead(interrupcao7);
    buttonState8 = digitalRead(interrupcao8);
    buttonState9 = digitalRead(interrupcao9);
    
    radio.stopListening();
    radio.write(&sensor1_rf, sizeof(sensor1_rf));
    radio.write(&sensor2_rf, sizeof(sensor2_rf));
    radio.write(&sensor3_rf, sizeof(sensor3_rf));
    radio.write(&sensor4_rf, sizeof(sensor4_rf));
    radio.write(&sensor5_rf, sizeof(sensor5_rf));
    radio.write(&sensor6_rf, sizeof(sensor6_rf));
    radio.write(&sensor7_rf, sizeof(sensor7_rf));
    radio.write(&sensor8_rf, sizeof(sensor8_rf));
    radio.write(&sensor9_rf, sizeof(sensor9_rf));
}

void interrupcao_1() {                                    //chamada qd acontecer a interrupcao
  sensor1++;                                              //soma a variavel
}                                                          //repete todo conteudo do void loop com as outras entradas e variaveis
void interrupcao_2() {                                    //chamada qd acontecer a interrupcao
  sensor2++;                                              //soma a variavel
}                                                          //repete todo conteudo do void loop com as outras entradas e variaveis
void interrupcao_3() {                                    //chamada qd acontecer a interrupcao
  sensor3++;                                              //soma a variavel
}                                                          //repete todo conteudo do void loop com as outras entradas e variaveis
void interrupcao_4() {                                    //chamada qd acontecer a interrupcao
  sensor4++;                                              //soma a variavel
}                                                          //repete todo conteudo do void loop com as outras entradas e variaveis
void interrupcao_5() {                                    //chamada qd acontecer a interrupcao
  sensor5++;                                              //soma a variavel
}                                                          //repete todo conteudo do void loop com as outras entradas e variaveis
void interrupcao_6() {                                    //chamada qd acontecer a interrupcao
  sensor6++;                                              //soma a variavel
}                                                          //repete todo conteudo do void loop com as outras entradas e variaveis
void interrupcao_7() {                                    //chamada qd acontecer a interrupcao
  sensor7++;                                              //soma a variavel
}                                                          //repete todo conteudo do void loop com as outras entradas e variaveis
void interrupcao_8() {                                    //chamada qd acontecer a interrupcao
  sensor8++;                                              //soma a variavel
}                                                          //repete todo conteudo do void loop com as outras entradas e variaveis
void interrupcao_9() {                                    //chamada qd acontecer a interrupcao
  sensor9++;                                              //soma a variavel
}                                                          //repete todo conteudo do void loop com as outras entradas e variaveis

 //**************** tarefa apos estouro do timer (1 segundo)  ***********************
void myHandler(){
 sensor1_rf = sensor1/3;
 sensor1 = 0;
 
 sensor2_rf = sensor2/3;
 sensor2 = 0;
 
 sensor3_rf = sensor3/3;
 sensor3 = 0;
 
 sensor4_rf = sensor4/3;
 sensor4 = 0;
 
 sensor5_rf = sensor5/3;
 sensor5 = 0;
 
 sensor6_rf = sensor6/3;
 sensor6 = 0;
 
 sensor7_rf = sensor7/3;
 sensor7 = 0;
 
 sensor8_rf = sensor8/3;
 sensor8 = 0;
 
 sensor9_rf = sensor9/3;
 sensor9 = 0;
  
}
