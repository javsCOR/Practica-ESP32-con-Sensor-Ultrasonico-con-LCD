# Practica ESP32 con  Sensor Ultrasonico con LCD
Este repositorio muestra como podemos programar una ESP32 con el sensor  y nos muestra  las distancias  en cm y mandar los resultados a una una pantalla LCD y mandando otros comandos.


## Introducción

### Descripción

La ```Esp32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```DTH11```) para adquirir la distancia y mandar las señales o resultados a una pantalla LCD; Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- Sensor ultrasonico
- pantalla LCD 12 X2


## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:

```
##include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4


const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
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

 lcd.setCursor(0, 0);
  lcd.print("distancia: " + String(d) +"cm ");
  lcd.setCursor(0, 1);
  
 
  lcd.setCursor(0,1);
  lcd.print("JAVIER CORTES");
   delay(1000);

}


```
2. Instalar la libreria de **liquidCrystal I2C** como se muestra en la siguente imagen.

![](https://github.com/javsCOR/Practica-ESP32-con-Sensor-Ultrasonico-con-LCD/blob/main/LIBRERIA%20LIQUID.png?raw=true)

3. Hacer la conexion de **DHT11** a **Sensor Ultrasonico**  y conectar ala pantalla **LCD32**como se muestra en la siguente imagen.

![](https://github.com/javsCOR/Practica-ESP32-con-Sensor-Ultrasonico-con-LCD/blob/main/coneccion.png?raw=true)

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la distancia dando *doble click* al sensor **DHT11** 
4. tambien  agregamos comandos diferentes a los resultados en la pantalla **LCD32** COMO SE MUESTRA EN LA SIGUIENTE  IMAGEN 

![](https://github.com/javsCOR/Practica-ESP32-con-Sensor-Ultrasonico-con-LCD/blob/main/interpretacion.png?raw=true)


## Resultados

Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en la siguente imagen.

![](https://github.com/javsCOR/Practica-ESP32-con-Sensor-Ultrasonico-con-LCD/blob/main/DIAGRAMA.png?raw=true)







# Créditos

creado por ING javier cortes rojas
