# rtty-arduino-beacon-audio

Implementacion de una baliza RTTY en Arduino, solo audio. Permite poner un texto que va a ser modulado en RTTY (default 45.5 Baudios) con un tono en un PIN del microcontrolador. Se puede conectar un parlante a este PIN y escuchar el audio.

Es un proyecto simple y basico para experimentar con Arduino en el ambito de la radioaficion. Es una adaptacion de otro proyecto mas simple [cw-arduino-beacon](https://github.com/lu1aat/cw-arduino-beacon/).

Si es lo primero que haces con Arduino, antes tenes que leer un tutorial de Arduino https://www.arduino.cc/en/Guide/HomePage y hacer los ejercicios basicos (titilar, leer un boton, etc). 


## Instrucciones

* Bajar este repositorio o el archivo `rtty-arduino-beacon-audio.ino`.
* Abrir el archivo con la IDE de Arduino (https://www.arduino.cc/en/main/software).
* Subir el programa al microcontrolador.
* Conectar el modulo Si5351 de la siguiente forma:
    * Arduino 3V    -   Si5351 VIN
    * Arduino GND   -   Si5351 GND
    * Arduino A4    -   Si5351 SDA
    * Arduino A5   -    Si5351 SCL

**Usar un filtro** acorde a la frecuencia donde se desea transmitir. Para hacer pruebas sin soldar el conector SMA se puede usar la salida _0_ del Si5351 y un cable como antena.

La baliza deberia comenzar a transmitir inmediatamente y hacer pausas de un minuto entre transmisiones.

<img src="https://github.com/lu1aat/rtty-arduino-beacon-si5351/raw/master/rtty-arduino-beacon-si5351-sketch_bb.svg">


## Configurando la baliza

Si no modificamos nada, la baliza comenzara a transmitir con los parametros por defecto. Para modificar estos parametros hay que usar la IDE de arduino, editar el codigo y subirlo nuevamente al microcontrolador.

### Mensaje

El mensaje por defecto esta definido en la linea, soporta solo letras en mayusculas y numeros:

```c++
char MESSAGE[] = "CQ CQ CQ DE N0CALL N0CALL N0CALL";
```

Cambiando el valor entre comillas se modifica el mensaje de la baliza. El mensaje por defecto demora en transmitirse 7 segundos aproximadamente.

### Tono

Algunos parametros de los tonos se pueden cambiar en:

```c++
const int markFreqHz = 2125;        // Frecuencia de la marca (MARK)
const int shiftFreqHz = 170;        // Variacion de frecuencia del espacio (SPACE) respecto de la marca (MARK)
const int spaceFreqHz = markFreqHz - shiftFreqHz;
const int toneDurationMs = 22;      // Duracion de los tonos, 22 hace que sean 45.5 baudios
```

Las frecuencias estan expresadas en Hz. La marca (MARK) es la frecuencia superior y espacio (SPACE) inferior. 


### Intervalo

El tiempo de espera en segundos, entre trasmision y transmision, puede ser cambiando desde:

```c++
const int SLEEP_SEC = 60;
```

### PIN de transmision

El PIN de salida de audio esta defindo en:

```c++
const int LED_PIN = LED_BUILTIN;
```

En el Arduino UNO ese PIN es el mismo que se utiliza para el LED que trae incorporado, esto facilita hacer pruebas.


## Ayuda

- LU1AAT, Andres
- lu1aat.andres @ gmail.com
