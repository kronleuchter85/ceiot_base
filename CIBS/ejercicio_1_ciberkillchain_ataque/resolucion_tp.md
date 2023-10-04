# Universidad de Buenos Aires
# Especializacion en Internet de las Cosas
# Cyberseguridad en IoT

## Alumno 
Gonzalo Carreno

Enunciado del TP: No disponible. Leer Descripcion del Trabajo

## Descripcion del trabajo:
El proyecto es un sistema de IoT compuesto por un sistema robotico de exploracion ambiental que envia los datos sensados en tiempo real a un sistma backend de procesamiento big data en la nube que los procesa y entrega informacion de valor.
El stack tecnologico del sistema, del lado backend, se compone de un endpoint MQTT encargado de recibir los eventos en tiempo real publicado por medio de AWS IoT Core y pasarlos al resto del pipeline.El siguiente componente es AWS Kinesis Data Streams que toma los mensajes de AWS IoT Core y los procesa utilizando endpoints AWS Lambda. Los mismos luego del procesamiento parcial de los eventos almacenan en AWS Dynamo los resultados. Finalmente existe un servidor Node.js que accede a estos resultados y los publica via API REST a traves de los correspondientes endpoints.

## Resolucion

### Objetivo:
No hay objetivos de ganancia economica en el ataque. El objetivo en una primera instancia es denegacion de servicio. Cualquier tecnica que pueda comprometer la disponibilidad y funcionamiento del sistema sera valida. Adicionalmente se aprecia el almacenamiento de los datos originales con el fin de explotar cualquier otro valor que se pueda extraer del ataque.
Para el backend se considera una alternativa de denegacion de servicio distribuida.

### Reconnaissance
Se reconocen los puertos expuetos por el sistema backend. Se averigua la arquitectura de hardware utilizada en el componente edge. Se reconoce el proveedor cloud utilizado y servicios accedidos.Se realiza discovery (https://attack.mitre.org/tactics/TA0007/ y https://attack.mitre.org/techniques/T1595/002/).
Buscando vulnerabilidades en las herramientas tecnologicas utilizadas:
- https://www.cvedetails.com/vulnerability-list/vendor_id-12113/Nodejs.html
- https://www.cvedetails.com/vulnerability-list/vendor_id-10410/product_id-45945/Eclipse-Mosquitto.html
- https://www.electropages.com/blog/2022/02/researchers-find-mqtt-have-33-vulnerabilities

### Weaponization
Si me logro acercar al alcance de la red edge y logro acceso a la misma, podria ver si la comunicaion con el servicio backend esta siendo cifrada. En caso de que no lo este podria sniffear paquetes (https://attack.mitre.org/techniques/T1040/) y explorar la posibilidad de hacer adversary-in-the-middle (https://attack.mitre.org/techniques/T1557/). Ademas si logro acceso a la red podria cambiar la configuracion para denegar el servicio en la parte edge. 

### Delivery
Me acerco con un vehiculo hasta el alcance de la red Wifi con el equipamiento necesario para poder conectarme a la red y sniffear paquetes.
Para la conexcion con la red Wifi sera necesario crackear la autenticacion WPA2 (por ejemplo usando fuerza bruta https://attack.mitre.org/techniques/T1110/) o conseguir mediante algun otro metodo (ingenieria humana por ejemplo) las credenciales.

### Exploit
Una vez se ha realizado ingeneria social o el ataque de fuerza bruta se cuenta con las credenciales de la red.

### Installation
Con las credenciales de la red se conecta el dispositivo de captura de trafico y se comienza a sniffear los paquetes. En caso de no estar cifrado se pueden apreciar todos los campos de los paquetes, la informacion que contiene. En caso de estar cifrado se procede a escanear los puertos abiertos del dispositivo emisor de eventos y del servicio cloud accedido.

### Command & Control
Conociendo el servicio cloud accedido se puede ejecutar un ataque de DDoS.

### Actions on Objectives



