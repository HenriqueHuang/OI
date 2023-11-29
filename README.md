Objetos Inteligentes Conectados
Projeto para conectar um sensor de Temperatura, Umidade

EC2
Influxdb
MQTT
NodeRED
A instância EC2 serve para hospedar o NodeRED, que recebe os dados do sensor para poder armazenar no banco de dados. 
O dispositivo IoT é conectado ao EC2 através do protocolo MQTT.
Conforme os dados são gerados no sensor, eles são transmitidos ao NodeRED, e o InfluxDB os armazena.
