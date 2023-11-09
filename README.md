# Sprint04-Edge


Hardware necessário:

Arduino Uno
Módulo leitor de QR code (por exemplo, um módulo de câmera com capacidade de processamento, como o OV7670)
Servomotor
Jumpers e uma placa de prototipagem
Instalar bibliotecas necessárias:
Certifique-se de ter as bibliotecas necessárias instaladas. Para o leitor de QR code, você pode usar uma biblioteca como a ZXing e para controlar o servomotor, a biblioteca Servo.

Para instalar a biblioteca ZXing, vá até o Arduino IDE, clique em "Sketch" -> "Incluir Biblioteca" -> "Gerenciar Bibliotecas". Procure por ZXing e instale a biblioteca.

Para a biblioteca Servo, vá para o mesmo local e procure por Servo.

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
