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
Nota: Los enlaces directos para las herramientas anteriores se encuentran en la sección de "Construido con".
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
* ![Carga el archivo _flow.json_ en NodeRed y haz un _Deploy_.](https://drive.google.com/file/d/1qOgwqFJZRpUiI8tTKXNtBoc1bU7igSJb/view?usp=sharing "San Juan Mountains")
* Verifica que el Broker está funcionando.
* Compila y carga el archivo al ESP32-CAM (poner el microcontrolador en modo programación antes).
* ![En el _Monitor Serial_ de Arduino IDE, observarás el contador imprimiéndose cada 5 segundos.](https://drive.google.com/file/d/1ULW-w-OrAQwJuX-oDu8WCPKfkv6eqDUi/view?usp=sharing "Monotiro Serial")
* ![Despliega el Dashboard. Observarás el contador imprimiéndose y un switch](https://drive.google.com/file/d/13_V0KV-2xeHxr8XjT7UerhPa-ogm3uKi/view?usp=sharing "Dashboard")
	* Con dicho switch puedes encender y apagar el Flash Led, el cual debería haber encendido si la conexión a Internet fue exitosa. ambiar información.
