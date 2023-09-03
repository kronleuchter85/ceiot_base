# Universidad de Buenos Aires
# Especializacion en Internet de las Cosas
# Cyberseguridad en IoT

## Alumno: Gonzalo Carreno

Enunciado del TP: (leer el archivo Readme.md)

Descripcion del proyecto target:
El proyecto target es un sistema de IoT compuesto por un sistema robotico de exploracion ambiental que envia los datos sensados en tiempo real a un sistma backend de procesamiento big data en la nube que los procesa y entrega informacion de valor.

El stack tecnologico del sistema, del lado backend, se compone de un endpoint MQTT encargado de recibir los eventos en tiempo real publicado por medio de AWS IoT Core y pasarlos al resto del pipeline.El siguiente componente es AWS Kinesis Data Streams que toma los mensajes de AWS IoT Core y los procesa utilizando endpoints AWS Lambda. Los mismos luego del procesamiento parcial de los eventos almacenan en AWS Dynamo los resultados. Finalmente existe un servidor Node.js que accede a estos resultados y los publica via API REST a traves de los correspondientes endpoints.

Pensando como el atacante, los puntos de vulnerabilidad accesibles mas simplemente serian desde el punto de vista de los endpoints open source utilizados: MQTT en la ingesta de datos y HTTP en el servidor Node.js.
Buscando las vulnerabilidades de Node.js:
- https://www.cvedetails.com/vulnerability-list/vendor_id-12113/Nodejs.html

Y en MQTT:
- https://www.cvedetails.com/vulnerability-list/vendor_id-10410/product_id-45945/Eclipse-Mosquitto.html
- https://www.electropages.com/blog/2022/02/researchers-find-mqtt-have-33-vulnerabilities


