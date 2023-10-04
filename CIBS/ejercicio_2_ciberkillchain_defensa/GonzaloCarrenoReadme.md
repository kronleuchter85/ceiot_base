# Ejercicio CiberKillChain - Defensa

Hacer una copia de este documento para utilizar com plantilla para el ejercicio

## Alumno

Gonzalo Carreno

## Enunciado

El proyecto es un sistema de IoT compuesto por un sistema robotico de exploracion ambiental que envia los datos sensados en tiempo real a un sistma backend de procesamiento big data en la nube que los procesa y entrega informacion de valor. El stack tecnologico del sistema, del lado backend, se compone de un endpoint MQTT encargado de recibir los eventos en tiempo real publicado por medio de AWS IoT Core y pasarlos al resto del pipeline.El siguiente componente es AWS Kinesis Data Streams que toma los mensajes de AWS IoT Core y los procesa utilizando endpoints AWS Lambda. Los mismos luego del procesamiento parcial de los eventos almacenan en AWS Dynamo los resultados. Finalmente existe un servidor Node.js que accede a estos resultados y los publica via API REST a traves de los correspondientes endpoints.

## Resolución

### Objetivo
El objetivo es definir un plan de defenza contra la denegacion de servicios para el sistema propuesto.

### Reconnaissance
Se debe evitar la provision de informacion al maximo posible. En lugar de usar endpoints en la internet publica para el backend, establecer un enlace hyperconnect con el proveedor cloud a traves de una colocation facility. En el sistema edge se deben usar conexiones cifradas.

### Weaponization
Se toma como medida ocultar el SSID de la red para minimizar fugas de informacion. Ademas la red esta configurada con IP estatica, DHCP desabilitado y se especifican los MAC address que se pueden conectar.

### Delivery
Desde el punto de vista backend se implementan balanceadores de carga y AWS Shield como mecanismo para mitigar el ataque de DDoS.

### Exploit

### Instalation

### Command and Control

### Actions on Objectives
