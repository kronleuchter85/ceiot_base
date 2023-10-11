# Ejercicio CiberKillChain - Defensa

Hacer una copia de este documento para utilizar com plantilla para el ejercicio

## Alumno

Gonzalo Carreno

## Enunciado

El proyecto es un sistema de IoT compuesto por un sistema robotico de exploracion ambiental que envia los datos sensados en tiempo real a un sistma backend de procesamiento big data en la nube que los procesa y entrega informacion de valor. El stack tecnologico del sistema, del lado backend, se compone de un endpoint MQTT encargado de recibir los eventos en tiempo real publicado por medio de AWS IoT Core y pasarlos al resto del pipeline.El siguiente componente es AWS Kinesis Data Streams que toma los mensajes de AWS IoT Core y los procesa utilizando endpoints AWS Lambda. Luego del procesamiento parcial se almacenan en AWS Dynamo los resultados. Finalmente existe un servidor Node.js que accede a estos resultados y los publica via API REST a traves de los correspondientes endpoints.

## Resolución

### Objetivo
El objetivo es tener un plan de defenza contra un ataque de denegacion de servicio.

### Reconnaissance
Se debe evitar la provision de informacion al maximo posible. En lugar de usar endpoints en internet publica para el backend, establecer un enlace AWS Direct Connect (https://aws.amazon.com/directconnect/) con el proveedor cloud a traves de una colocation facility. En el sistema edge se deben usar conexiones cifradas. El SSID de la red debe estar oculto.

### Weaponization
La red edge esta configurada aceptando IPs estaticas, DHCP desabilitado y se especifican los MAC address que se pueden conectar.

### Delivery
Para proteger el backend se activa el servicio AWS Shield (https://aws.amazon.com/shield/) para permitir el escalamiento horizontal de los balanceadores de carga cuando se detecta un DDoS y de esta forma absorber las solicitudes y bloquear IPs de origen.

### Exploit
Para evitar las vulnerabilidades en el backend 
- se activa el servicio AWS Secrets Manager
- se implementa la rotacion de secretos para reducir el tiempo de vida de API keys y demas secretos y facilitar la rotacion de los mismas, con reducir el tiempo en el cual -en caso de ser filtradas al atacante- puedan ser utilizadas.
- se implementa MFA para los principals que pueden configurar el sistema, generando una barrera mas para una autenticacion/autorizacion no permitida, como resultado de filtracion de credenciales.
- se activan los servicios AWS IoT Device Defender (https://aws.amazon.com/iot-device-defender/) y AWS IoT Device Manager (https://aws.amazon.com/iot-device-management) con el fin de mejorar la gestion y reducir los puntos de ataques en la parte edge.

### Instalation
N/A - no se instala nada en el ataque

### Command and Control
Se evita el control del servidor al evitar las vulnerabilidades mencionadas que permitieron el acceso al mismo.

### Actions on Objectives
El sistema de defenza compuesto por AWS Shield y los ELBs escala horizontalmente absorbiendo las peticiones, bloqueando las IPs desde donde provienen las peticiones y evitando asi la denegacion de servicio.
Ademas no se detectaron accesos no autorizados al sistema ni interrupcion del servicio en ningun punto de la arquitectura.
