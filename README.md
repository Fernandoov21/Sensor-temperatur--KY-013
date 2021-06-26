# Sensor-KY-013

# **¿Que es el modeulo KY-013?**

El módulo ky-013 es un sensor de temperatura analógico para Arduino.

El sensor de temperatura analógica KY-013 para Arduino mide la temperatura ambiente en función de la resistencia del termistor.

Este sensor de temperatura analógica KY-013 consta de un termistor NTC y una resistencia de 10 kΩ  (Coeficiente de temperatura negativo), que significa que la resistencia disminuye al aumentar la temperatura. La resistencia del termistor varía con la temperatura ambiente,usaremos la ecuación de Steinhart-Hart para obtener la temperatura precisa del termistor.

[![ky013.jpg](https://i.postimg.cc/BbbwCHGn/ky013.jpg)](https://postimg.cc/0Kgfk6QT)


**Modo de conexion arduino**

[![k13-arduino.png](https://i.postimg.cc/GtDgNr9W/k13-arduino.png)](https://postimg.cc/kRny60Qs)

**Especificaciones:**
- Voltaje de funcionamiento:  5 Volts
- Rango de medición de temperatura:   -55 °C a 125 °C  [ -67  °F  a 257 °F]
- Exactitud de medición:  ± 0.5  °C
- Dimensiones:  2.2 x 1.5 x 0.9 cm
- Peso: 1 gr

**Codigo para practica basica**
El codigo  derivará la temperatura del termistor utilizando la  ecuación de Steinhart-Hart . El código devolverá la temperatura en grados Celsius, descomente la línea 17 para obtener la temperatura en grados Farenheit.
´´´´
int ThermistorPin = A0;
int Vo;
float R1 = 10000; // value of R1 on board
float logR2, R2, T;
float c1 = 0.001129148, c2 = 0.000234125, c3 = 0.0000000876741; //steinhart-hart coeficients for thermistor

void setup() {
  Serial.begin(9600);
}

void loop() {
  Vo = analogRead(ThermistorPin);
  R2 = R1 * (1023.0 / (float)Vo - 1.0); //calculate resistance on thermistor
  logR2 = log(R2);
  T = (1.0 / (c1 + c2*logR2 + c3*logR2*logR2*logR2)); // temperature in Kelvin
  T = T - 273.15; //convert Kelvin to Celcius
 // T = (T * 9.0)/ 5.0 + 32.0; //convert Celcius to Farenheit

  Serial.print("Temperature: "); 
  Serial.print(T);
  Serial.println(" C"); 

  delay(500);
}

´´´´
