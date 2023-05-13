***Desarrollado para la materia Administración de Redes instituida por el profesor Juan Manuel Aranda Lopez King por Juan Camilo Adames, Nicolás Vargas Wilches y Santiago Contreras del programa de ingeniería informática de la Universidad de La Sabana.***

# PRESENTACIÓN DEL LABORATORIO

En este proyecto se retomará el uso de una topología semiempresarial previamente modificada para ser compatible con IPv6, y se modificará una vez más con el fin de integrar un sistema de soporte y gestión , además de comunicación segura entre Intranets usando diferentes herramientas.

##INTRODUCCIÓN:

El Protocolo Simple de Administración de Red (SNMP) es fundamental para permitir la coexistencia de los protocolos IPv4 e IPv6 en una topología de red. La diferencia en la estructura de las direcciones IP entre ambos protocolos requiere que los administradores comprendan cómo integrar SNMP en una topología mixta. Esto implica configurar los dispositivos de red de manera adecuada y adaptarse a los cambios necesarios para garantizar un funcionamiento eficiente en ambas versiones del protocolo IP. La correcta implementación de SNMP en esta configuración mixta asegura una gestión efectiva de la red y facilita el monitoreo y la administración de los dispositivos.

## Desarrollo
Paso 1: Agregar un enrutador a la topología
Dado a que la guía nos recomienda cambiar los routers 2811 R1Bog y R1Mad a routers 2911, notando la principal diferencia en los la cantidad de puertos Gigabit Ethernet (Ge) y la inexistencia de puertos FastEthernet (Fe).

Paso 2: Configurar las interfaces de los enrutadores
Procedemos a asignar direcciones Ip de los routers y volvemos a configurar tal como teníamos configurados los routers 2811 anteriormente reemplazados.

Paso 3: Habilitar y configurar SNMP para su funcionamiento en las VLAN 100 (tech) y 25 (vice)
Para realizar la configuración debemos ingresar a la consola CLI de cada uno de los routers 2911 y efectuar la siguiente lista de comandos:

  -> configuracion snmp-server community <nombre_comunidad> RO
El argumento <nombre_comunidad> es el nombre de la comunidad de SNMP que se va a utilizar para el acceso de solo lectura (RO).

  -> configuracion snmp-server version <version>
El argumento <version> es el número de versión de SNMP que se va a utilizar, en este caso la versión 3.
  
  -> configuracion snmp-server host <direccion_ip> version <version> <nombre_comunidad>
El argumento <direccion_ip> es la dirección IP del host de administración de SNMP (PC 2-3 & PC 6-8). El argumento <version> es la versión de SNMP que se va a utilizar. El argumento <nombre_comunidad> es el nombre de la comunidad de SNMP que se va a utilizar.
  
  -> configuracion snmp-server enable traps
Este comando activa las notificaciones de SNMP, es útil cuando como equipo de TI queremos que algún equipo configurado como agente SNMP nos notifique alguna irregularidad presente en el equipo.
  
  -> configuracion interface <interface>
  -> snmp-server community <nombre_comunidad> RO
El argumento <interface> es la interfaz que se utilizará para la administración de SNMP. El argumento <nombre_comunidad> es el nombre de la comunidad de SNMP que se va a utilizar.
  
Una vez configurado el protocolo SNMP en los routers, veremos las funcionalidades que este permite mediante el acceso al MIB Browser, estos son:
  ## Operación Get
La operación Get se utiliza para recuperar información de un dispositivo de red. Un cliente SNMP envía una solicitud de Get a un dispositivo de red gestionado, y el dispositivo de red gestionado responde con el valor solicitado. La solicitud de Get incluye el identificador de objeto (OID) del valor solicitado. Por ejemplo, si un administrador de red quiere conocer el estado de la interfaz FastEthernet0/0 de un enrutador Cisco, puede enviar una solicitud de Get al OID correspondiente para recuperar el valor actual de la interfaz, el dispositivo de red gestionado responderá con el valor actual de la interfaz, pero si la interfaz está activa, el valor de retorno será "up" y si está inactiva, el valor de retorno será "down".

  ## Operación Get-Bulk
La operación Get-Bulk se utiliza para recuperar grandes cantidades de información de un dispositivo de red. La solicitud de Get-Bulk incluye el OID de inicio y el número máximo de objetos que se pueden recuperar.Por ejemplo, si un administrador de red quiere conocer el estado de todas las interfaces de 
un enrutador Cisco, puede enviar una solicitud de Get-Bulk al OID correspondiente para recuperar el valor actual de todas las interfaces.
El dispositivo de red gestionado responderá con los valores actuales de todas las interfaces en una sola respuesta, esto es más eficiente que enviar múltiples solicitudes de Get individuales para cada interfaz.

 ## Operación Set
La operación Set se utiliza para configurar o modificar un valor en un dispositivo de red. Un cliente SNMP envía una solicitud de Set a un dispositivo de red gestionado, y el dispositivo de red gestionado cambia el valor especificado.Por ejemplo, si un administrador de red quiere cambiar la configuración 
de una interfaz en un enrutador Cisco, puede enviar una solicitud de Set al OID correspondiente para cambiar la configuración de la interfaz.
El dispositivo de red gestionado cambiará la configuración de la interfaz según lo especificado en la solicitud de Set, es importante destacar que la operación Set requiere permisos de escritura y autenticación adecuados para evitar cambios no autorizados en la configuración de los dispositivos de red.
  
  ## CONCLUSIÓN 
  Wilches.
