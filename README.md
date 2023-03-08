<p align="center">
<img src="Imagenes/logos.PNG">
</p>
<h1 align="center">Instituto Tecnológico de Tijuana</h1>
<h3 align="center">Depto de Sistemas y Computación</h3>
<h3 align="center">Ing. En Sistemas Computacionales</h3>
<h3 align="center">DHT22:  sensor de temperatura y humedad </h3>
<h3 align="center">Autor : Millán Guízar Arely Vanessa</h3>
<h3 align="center">Repositorio: DHT22</h3>
<h3 align="center">Fecha de revisión:   00/00/00</h3>

<h1 align="center">DHT22:  sensor de temperatura y humedad</h1>

El DHT22 es un sensor de temperatura y humedad con unas prestaciones que lo acercan mucho a los de alta precisión. Lo puedes encontrar fácilmente en tiendas especializadas o grandes superficies, donde No products found.. Eso te permite no tener que depender de un sensor de temperatura y otro de humedad por separado, sino tenerlo todo integrado en un mismo dispositivo.

<p align="center">
<img width="400" src="Imagenes/DHT22.jpg" alt="DHT22">
</p>

Sus principales características generales son:
- Alimentación: 3.3v – 5.5v, tomando como valor recomendado 5v.
- Resolución decimal, es decir, los valores tanto para  humedad como para temperatura serán números con una cifra decimal.
- Tiempo de muestreo: 2 segundos, es decir, sólo nos puede ofrecer datos cada 2 segundos.

En cuanto a sus prestaciones leyendo temperatura:
- Rango de valores desde -40ºC hasta 80ºC de temperatura.
- Precisión: ±0.5ºC, ±1ºC como máximo en condiciones adversas.
- Tiempo de respuesta: <10 segundos, es decir, de media, tarda menos de 10 segundos en reflejar un cambio de temperatura real en el entorno.

Si hablamos de sus prestaciones leyendo humedad relativa:
- Rango de valores desde 0% hasta 99.9% de Humedad Relativa.
- Precisión: ±2%RH, a una temperatura de 25ºC.
- Tiempo de respuesta: <5 segundos, es decir, de media, tarda menos de 5 segundos en reflejar un cambio de humedad relativa real en el entorno. Además, para darse esta afirmación, los tests indicaron que la velocidad del aire debe ser de 1 m/s.

<h2 align="center">Interfaz con Raspberry Pi Pico</h2>

El diagrama de conexión se muestra en la imagen de abajo.

<p align="center">
<img width="400" src="Imagenes/Raspberry%20pi%20pico.PNG" alt="Raspberry">
</p>

- El primer pin para ambos sensores es un pin de fuente de alimentación (Vcc). Conéctelo con el pin de 3,3 voltios de Raspberry Pi Pico.
- Los datos de salida son el pin a través del cual obtenemos muestras de temperatura y humedad del sensor DHT. Conecte este pin con GPIO2 de Raspberry Pi Pico y también conecte el pin de datos con una resistencia pull-up de 10k. Pero también puede usar cualquier pin digital de Raspberry Pi Pico. Se utiliza una resistencia Pull-up para mantener el pin de datos alto para una comunicación adecuada entre el microcontrolador y el sensor.
- El tercer pin no se utiliza
- Conecte el cuarto pin (GND) al pin de tierra de la placa

<h2 align="center">Código de MicroPython</h2>

```python
from machine import Pin
from time import sleep
import dht
 
sensor = dht.DHT22(Pin(2)) 
 
while True:
    sensor.measure()
    temp = sensor.temperature()
    hum = sensor.humidity()
    print("Temperature: {}°C   Humidity: {:.0f}% ".format(temp, hum))
    sleep(2)
```

<h2 align="center">Función del código</h2>

En primer lugar, importamos Pin, dht y módulo de suspensión para que podamos acceder a sus métodos a través de sus clases definidas.

```python
from machine import Pin
from time import sleep
import dht
```

A continuación, definiremos un objeto dht llamado 'sensor' y le asignaremos el pin de datos. Aquí estamos utilizando el sensor DHT22 con pin de datos conectado en GPIO2.

```python
sensor = dht.DHT22(Pin(2))
```

Dentro del bucle infinito, obtendremos la lectura de temperatura y humedad y la guardaremos en 'temp' y 'hum' respectivamente. Estos se imprimirán en la consola de shell después de un retraso de 2 segundos.

```python
while True:
    sensor.measure()
    temp = sensor.temperature()
    hum = sensor.humidity()
    print("Temperature: {}°C   Humidity: {:.0f}% ".format(temp, hum))
    sleep(2)
 ```
    
Nos mostrará el siguiente resultado
 
<p align="center">
<img width="400" src="Imagenes/Resultado.PNG" alt="Resultado">
</p>

https://wokwi.com/projects/358588113192635393
