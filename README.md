# ESP32CAM con MQTT.
Este proyecto incluye el código necesario para conectar el microcontrolador ESP32CAM a través de Internet, para poder conectarse a un broker de MQTT y, eventualmente, enviar y recibir mensajes utilizando dicho broker. Además, se incluye un _flow_ de NodeRed, para proveer una sencilla interfaz visual e implementar un _bot de Telegram_.
## Primeros pasos.
Para poder tener una copia de este proyecto funcionando, se requieren diferentes elementos de software y hardware, los cuales se describen a continuación.
### Hardware.
1. El microcontrolador ESP32 (para este proyecto se utilizó el ESP32-CAM, ya que incluye un LED flash soldado a su placa de desarrollo).
2. Modulo adaptador de USB a Serial para programar el microcontrolador. Alternativamente, se puede utilizar un Arduino para este propósito. 
### Software.
1. Broker Mosquitto corriendo de forma local.
2. La IDE de Arduino.
3. Biblioteca para programar el ESP32 desde la IDE de Arduino. 
4. Node-Red corriendo de forma local.
	* Nodo Dashboard.
	* Nodo de Telegram. 
5. Biblioteca PubSubClient para la IDE de Arduino. 
___Nota___: Los enlaces directos para las herramientas anteriores se encuentran en la sección de "Construido con".
## Configuración.
Antes de intentar cargar el código en su ESP32-CAM, debe realizar algunos ajustes al código.

1. En la línea 21 y 22, se deben colocar las credenciales de tu conexión a WiFi.
 ```
const char* ssid = "*****"; // Aquí debes poner el nombre de tu red
const char* password = "******"; // Aquí debes poner la contraseña de tu red
```
2.	En la línea 25 y 26, debes colocar el broker de MQTT que desees utilizar (ya sea publico o privado).
 ```
const char* mqtt_server = "x.x.x.x"; // Dirección IP del broker de MQTT
IPAddress server(x, x, x, x); // Dirección IP del broker de MQTT, separado por comas.
```
3. Si así lo desea, puede cambiar el tema donde se va a publicar, en la línea 101 (el programa por defecto publica en el tema  ___esp32/data___
 ```
client.publish("esp32/data", dataString);
```
4. Si así lo desea, puede cambiar el tema donde se va a suscribir, en las líneas 130 y 150.
 ```
130	if (String(topic) == "esp32/output") {
150	client.subscribe("esp32/output");
```
## Funcionamiento.
### Programa básico.
![Carga el archivo _flow.json_ en NodeRed y haz un _Deploy_.](https://github.com/Hugo-fv/ESP32CAM_MQTT-Basic/blob/main/Images/FLOW.png)
Verifica que el Broker está funcionando.
Compila y carga el archivo al ESP32-CAM (poner el microcontrolador en modo programación antes).
 ![En el _Monitor Serial_ de Arduino IDE, observarás el contador imprimiéndose cada 5 segundos.](https://github.com/Hugo-fv/ESP32CAM_MQTT-Basic/blob/main/Images/SERIAL.png)
![Despliega el Dashboard. Observarás el contador imprimiéndose y un switch](https://github.com/Hugo-fv/ESP32CAM_MQTT-Basic/blob/main/Images/SERIAL.png)
Con dicho switch puedes encender y apagar el Flash Led, el cual debería haber encendido si la conexión a Internet fue exitosa. 

### Nodos de Telegram.
Adicionalmente, he añadido la función de poder encender y apagar el Flash Led haciendo uso de un ![Bot de Telegram](t.me/AlertasAtencion_bot). Este bot fue creado utilizando el BotFather (información mas abajo).
Puedes encender el Flash Led del microcontrolador usando el comando _/on_ o la palabra clave _on_; del mismo modo, puedes apagar el Flash Led con el comando _/off_ o la palabra clave _off_. Ambos comandos devolverán el estado en el que quedó el Flash Led. 
![La conversación con el bot luce de la siguiente manera:](https://github.com/Hugo-fv/ESP32CAM_MQTT-Basic/blob/main/Images/TELEGRAM.png)
## Construido con:
![Eclipse Mosquitto](https://mosquitto.org/) como Broker de MQTT.
![Arduino IDE](https://www.arduino.cc/en/software) como IDE de desarrollo.
![Biblioteca de espressif](https://github.com/espressif/arduino-esp32) necesaria para programar el ESP32-CAM con la IDE de Arduino.
![Node-Red](https://nodered.org/) para cargar el _flow_.
![Nodos para Telegram](https://flows.nodered.org/node/node-red-contrib-telegrambot).
![Nodos de Dashboard](https://flows.nodered.org/node/node-red-dashboard).
![Biblioteca PubSubClient](https://github.com/knolleary/pubsubclient) para publicar y recibir mensajes con MQTT.
## Créditos. 
1. ![Hugo Vargas](https://github.com/hugoescalpelo) por proporcionar el código y por su labor de docente para su entendimiento.
2. ![Código IoT](https://github.com/codigo-iot) por gestionar el diplomado.
3. ![Victor Flores](https://github.com/Hugo-fv) por hacer esta documentación y la implementación del bot de Telegram. 

## Enlaces externos.
PONER LINK DEL VIDEO. 
