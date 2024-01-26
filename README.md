# PRACTICA ESP32 CON ULTRASONICO Y LCD
Este repositorio muestra como podemos programar una ESP32 con el sensor ULTRASONICO y un display LCD.

## Introducción

### Descripción
La ```ESP32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor ultrasonico (```HC-SR04```) para adquirir la distancia del entorno, asi como tambien un display (```LCD16x2(I2C)```) donde podremos visualizar los medidas en cm y mi nombre con la carrera que cursé; cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).

## Material Necesario
Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP32
- Sensor HC-SR04
- Display LCD16x2(I2C)
## Instrucciones
### Requisitos previos
Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).

### Instrucciones de preparación de entorno 
1. Abrir la terminal de programación y colocar la siguente programación:
```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);
void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms
  
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) +"cm  ");
  delay(1000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Daniel Armenta");
  lcd.setCursor(0, 1);
  lcd.print("Ing. Electrico");
  delay(2000);

}
```
2. Instalar la libreria de **DHT sensor library for ESPx** como se muestra en la siguente imagen.

![](https://github.com/DanielX834/PRACTICA-N4/blob/main/1Libreria.jpg?raw=true)

3. Instalar la libreria de **LiquidCrystal I2C** como se muestra en la siguente imagen.

![](https://github.com/DanielX834/PRACTICA-N4/blob/main/2LibreriaL2C.jpg?raw=true)

4. Hacer la conexion de **HC-SR04** con la **ESP32** como se muestra en la siguente imagen.

![](![image](https://github.com/DanielX834/PRACTICA-N4/assets/154008369/2fb96e8d-bc3a-40ae-a53b-8e5a73298573)


5. Hacer la conexion de **LCD16x2(I2C)** con la **ESP32** como se muestra en la siguente imagen.

![](https://github.com/DanielX834/PRACTICA-N4/blob/main/3ConexionL2C.jpg?raw=true)

### Instrucciónes de operación
1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la distancia dando *doble click* al sensor **HC-SR04** 

## Resultados
Cuando haya funcionado, verás los valores dentro del monitor serial y el display como se muestra en la siguente imagen.

