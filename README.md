#include <Servo.h>

#include <LiquidCrystal.h> //Incluyo la libreria para LCD
LiquidCrystal lcd(11,8,7,6,5,4); //Definimos los puertos para conectar la LCD


void setup() {
  lcd.begin(16,2);              //Configuramos para una pantalla LCD de 16x2
  lcd.print(" AutoFeed Camilo Torres");   //Imprimimos el mensaje en la pantalla
  delay(1000);                  //Insertamos un retardo de 1 segundo
}

void loop() {
  for(int posicion = 0; posicion <16; posicion++){//Ciclo para mover el mensaje a la izquierda en 16 posiciones
    lcd.scrollDisplayLeft();    //Funcion para el deslizamiento del mensaje por cada posicion
    delay(300);                 //Esperamos 0.3 segundos
    }
  for(int posicion =0;posicion<32;posicion++){//Ciclo para mover el mensaje a la derecha en 32 posiciones
    lcd.scrollDisplayRight();   //Funcion para el deslizamiento del mensaje por cada posicion
    delay(300);                //Esperamos 0.3 segundos  
    } 
  for(int posicion = 0; posicion<16;posicion++){//Ciclo para mover el mensaje a la izquierda en 16 posiciones (volvemos al centro de la pantalla)
    lcd.scrollDisplayLeft();    //Funcion para el deslizamiento del mensaje por cada posicion
    delay(300);                 //Esperamos 0.3 segundos
    }
    delay(2000);                //Esperamos 2 segundos para empezar a realizar todo el procedimiento anterior
}




#include <LiquidCrystal.h>

#include <Servo.h>

#include <SoftwareSerial.h>





Servo servo;

//Conexión de los pines de Transmisión (TX) y Recepción (RX) del Bluetooth
int pinBluetoothTX = 10;
int pinBluetoothRX = 11;

SoftwareSerial bluetooth(pinBluetoothTX, pinBluetoothRX);

int pinServo = 3; // Conexión del servo

char letra;

void setup() {
 Serial.begin(9600);
 servo.attach(pinServo); // Asociamos el servo con su pin
 servo.write(90);
 bluetooth.begin(9600);
}


void loop() {
// Comprobamos que este disponible el BT
if(bluetooth.available() > 0) {
  letra - bluetooth.read();
  Serial.println(letra);
}
// Controlamos si queremos mover el servo ("S")
if (letra == "0") {
  Serial.println("0 grados");
  servo.write(0);
}
if (letra == "1") {
  Serial.println("90 grados");
  servo.write(90);
}
if (letra == "2") {
  Serial.println("180 grados");
  servo.write(180);
}



}

