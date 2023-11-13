# Sprint04-Edge


Hardware necessário:

Arduino Uno
Módulo leitor de QR code
Servomotor
Jumpers e uma placa de prototipagem
Instalar bibliotecas necessárias:

Conectar os componentes:
Conecte o módulo leitor de QR code e o servomotor ao Arduino Uno usando jumpers.

Código do Arduino:
Aqui está um exemplo básico de como o código pode ser estruturado. Certifique-se de ajustar conforme necessário para atender às especificações exatas dos seus componentes.

---------------------------------------------------------------------------------

#include <Servo.h>
#include <ZXing.h>

Servo meuServo;
ZXing barcodeReader;

void setup() {
  meuServo.attach(9); // Conecte o pino do servomotor ao pino 9
  Serial.begin(9600);
}

void loop() {
  // Leitura do QR code
  String resultadoQR = barcodeReader.read();
  
  // Verifica se o QR code é autorizado
  if (resultadoQR.equals("SEU_QR_CODE_AUTORIZADO")) {
    // Gira o servomotor
    meuServo.write(90); // Ajuste o ângulo conforme necessário
    delay(1000); // Aguarda um segundo
    meuServo.write(0); // Retorna à posição inicial
  }

  delay(1000); // Aguarda um segundo antes de ler o próximo QR code
}




// Defina os pinos do sensor ultrassônico
const int triggerPin = 4;
const int echoPin = 2;

// Defina os pinos dos LEDs
const int redLedPin = 7;
const int greenLedPin = 8;

// Variáveis para armazenar as leituras do sensor
long duration;
int distance;

#include <Servo.h>

int posicao = 0;
Servo servo;

#define bt1 13
#define bt2 12


void setup() {
  pinMode(triggerPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(redLedPin, OUTPUT);
  pinMode(greenLedPin, OUTPUT);

  // Inicialmente, os LEDs estão apagados (verde para livre)
  digitalWrite(redLedPin, LOW);
  digitalWrite(greenLedPin, HIGH);
  // Inicia o servoMotor
  Serial.begin(9600);
  servo.attach(11);
  servo.write(0);//INICIA O MOTOR NA POSIÇÃO 0º
  pinMode(bt1, INPUT);
  pinMode(bt2, INPUT);
}


void loop() {
  // Gere um pulso no pino Trigger do sensor
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);

  // Meça o tempo de resposta no pino Echo
  duration = pulseIn(echoPin, HIGH);

  // Converta o tempo em distância (cm)
  distance = duration / 29 / 2;

  // Verifique a distância
  if (distance < 10) {
    // Se a distância for menor que 10 cm, o sensor detectou algo
    // Acenda o LED vermelho (indicando ocupado) e apague o LED verde
    digitalWrite(redLedPin, HIGH);
    digitalWrite(greenLedPin, LOW);
  } else {
    // Caso contrário, o sensor não detectou nada
    // Acenda o LED verde (indicando livre) e apague o LED vermelho
    digitalWrite(greenLedPin, HIGH);
    digitalWrite(redLedPin, LOW);
  }

  delay(1000); // Aguarde 1 segundo antes de fazer outra medição


Serial.println(digitalRead(bt1));
Serial.println(digitalRead(bt2));
  
  if(digitalRead(bt1) == HIGH && posicao <=180){
    
    posicao = posicao + 20;
    servo.write(posicao);
    delay(10);
  }
  
  if(digitalRead(bt2) == HIGH && posicao >= 0){
    
    posicao = posicao - 20;
    servo.write(posicao);
    delay(5);
  }
}


-----------------------------------------------------------------

OBS: Para o projeto do servomotor que seria feito com QrCode, infelizmente não foi possivel pois não tem no maker.
Foi então adaptado o projeto para ser usado com um botão que simula a leitura do QrCOde, girando o servomotor que atua como uma catraca.

-----------------------------------------------------------------

Link do video de apresentação


https://youtube.com/shorts/v-ihSnq5-sM?feature=share




Integrantes:

RM98765 - Filipe Prado Menezes
RM93445 - Gabriel Gomes Catanzaro
RM88166 - pedro Henrique Salvitti
RM98766 - Lucas Gomes Alcantara

