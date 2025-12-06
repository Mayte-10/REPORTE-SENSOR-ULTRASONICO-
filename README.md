# REPORTE-SENSOR-ULTRASONICO-
# REPORTE-DHT22-LCD-ULTRASONICO
## USO DEL SENSOR ULTRASONICO
### Reporte: Sensor utrasónico con LCD-Tarjeta ESP32

- Introducción

Utilizar ESP32
Medir temperatura y humedad (DHT22).
Medir distancia mediante ultrasonido (HC-SR04).
Mostrar la información en una pantalla LCD 16x2.

- Materiales Utilizados

  1. Sensor DHT22
  2. Tarjeta ESP32
  3. LCD 
  4. WOKWI SIMULATOR (https://wokwi.com)
![](https://github.com/Mayte-10/-DHT22-CON-LCD/blob/main/WhatsApp%20Image%202025-11-30%20at%2019.54.34.jpeg)

- PROCEDIMIENTO 

- Ingresar a  WOKWI SIMULATOR y seleccionar el microcontrolador ESP32

  ![](https://github.com/Mayte-10/REPORTE-SENSOR-DTH22/blob/main/WhatsApp%20Image%202025-11-23%20at%2021.14.00%20(1).jpeg)
  ![](https://github.com/Mayte-10/REPORTE-SENSOR-DTH22/blob/main/WhatsApp%20Image%202025-11-23%20at%2020.50.01.jpeg)

- Colocar el sensor DHT22, el sensor ultrasonico y la LCD
- Realizar la conexión correspondiente
  
  ![](https://github.com/Mayte-10/REPORTE-DHT22-LCD-ULTRASONICO/blob/main/CONEXIONES%20Y%20MATERIAL.PNG)

- Colocar el siguiente código
  
```
#include <LiquidCrystal_I2C.h>
#include "DHTesp.h"
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
const int DHT_PIN = 13;
DHTesp dhtSensor;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200); //iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros
TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
    lcd.clear();

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
      lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("BIENVENIDOS");
  lcd.setCursor(0, 1);
  lcd.print("MODULO 5");

delay(1500);
 lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("MAYTE TORRES");
  lcd.setCursor(0, 1);
  lcd.print("ING.INDUSTRIAL");
 
delay(1500);
lcd.clear();
lcd.setCursor(0, 1);
  lcd.print("DISTANCIA: ");
  lcd.print(d);      //Enviamos serialmente el valor de la distancia
  lcd.print("cm");
  delay(1000);          //Hacemos una pausa de 100ms

delay(1500);
lcd.clear();
lcd.setCursor(0, 0);
  lcd.print("  TEMP: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" HUMIDITY: " + String(data.humidity, 1) + "% ");
delay(2000);
}
```
ADJUNTAR LAS LIBRERÍAS CORRESPONDIENTES 
![](https://github.com/Mayte-10/REPORTE-DHT22-LCD-ULTRASONICO/blob/main/LIBRERIAS.PNG)
- COMPILAR
![](        )
  
- FUNCIONAMIENTO 
En la simulación de Wokwi se observa:
La pantalla LCD actualiza la temperatura, humedad y distancia.
El sensor ultrasónico responde correctamente cuando se modifica la distancia en el simulador.
El DHT22 genera valores de temperatura y humedad típicos.
  ![](https://github.com/Mayte-10/REPORTE-DHT22-LCD-ULTRASONICO/blob/main/COMPILACION%201.PNG)
   ![](https://github.com/Mayte-10/REPORTE-DHT22-LCD-ULTRASONICO/blob/main/COMPILACION%202.PNG)
   ![](https://github.com/Mayte-10/REPORTE-DHT22-LCD-ULTRASONICO/blob/main/COMPILACION%203.PNG)
   ![]( )


Realizó
Mayte Torres 
