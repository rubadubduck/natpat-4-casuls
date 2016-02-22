# natpat-4-casuls
#CISCO IOS CONFIGURACION NAT: PAT. TUTORIAL RFC.
#hago esto con todo el cariño del mundo, esta parte es opcional a leer ya que lo importante es como te manejas con los comandos, 
lo importante lo remarcare con "[]".

El NAT: PAT nacio por la necesidad de 2 cosas
1. filtrar la capa de aplicacion a nivel de puertos (transporte)
2. Ahorrar dinero

El fundamento es simple, [una ip fija publica se combina con el num de puerto de aplicacion para generar una direcion de 
destino/envio], antes de empezar, quiero remarcar que es absolutamente necesario que la topologia este bien organizada o
tener una red simple (pero solo si no tienes ni idea de como hacer subredes o no conoces clases, en ese caso recomiendo vlsm-calc.net)

Al igual que con el resto de NATs, hay una parte interna, dividida en local y global, y una externa, dividida de la misma manera.
el proceso de traduccion es igual que en el resto de NATs

[COMO FUNCIONA:

NAT:PAT es coger el socket de la trama y utilizarla como direccion destino o de envio, lo primero que hay que configurar es
la lista de equipos que usaran la IP o IPs (normalmente suelen ser la red o subred), definir la bolsa de IPs publicas en caso de
que combinemos con dinamica y definir en las interfaces [LAS RAMAS DE INTERIOR (red local) Y EXTERIOR (internet)].

En caso de que no funcione:
1. Topologia de mierda
2. IPs y mascaras en los routers afectados con NAT mal configurados
3. La ACL de lista de uso esta mal definida o se ha configurado mal
4. La bolsa de IPs esta mal definida o se ha configurado mal
5. Las ramas interna y externa estan mal configuradas
6. Una configuracion antigual del router sobrepasa a la nueva configuracion
7. Estas haciendo mal ctrl+c ctrl+v a los apuntes de CCNA de Cisco

HERRAMIENTAS A USAR (en enable)

Debug ip nat: Muestra la lista de acciones en el proceso NAT para depuracion (En español: Aparece lo que hace el NAT para encontrar
lo que falla)
Show Ip nat translations: es un comando bastante util, ya que nos muestra toda la informacion de las ramas interior y exterior.
Show Ip nat stat: Estadisticas de fallo de paquetes, suele tener menos salero que los anteriores comandos.

HERRAMIENTAS A USAR (en cfg terminal)

no: es como el fairy, lo limpia todo, ponlo delante de los comandos que consideres que hay que borrar y lo borra

EJEMPLOS:
no ip nat inside source list 1 80.0.0.2 overload
no ip nat pool name piscina 80.0.0.2 80.0.0.5 netmask 255.255.255.0
no ip nat inside
no access-list 1

en caso de que esto no funcione, borra el startup-config (erase startup-config) y reinicia el router con reload
¡¡¡OJO, EXPORTA EL RUNNING-CONFIG A UN .txt PORQUE SI NO, ESTAS JODIDO!!!

En los archivos siguientes pondre lineas para configurar el NAT:PAT tanto en estatico como en dinamico
