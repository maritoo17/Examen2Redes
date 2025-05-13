# Examen2Redes

# Misión 1: Reconexión en la Base Eco (Hoth) – Direccionamiento IP y Subredes

## Requisitos de la misión:
- **Comando Central**: ~50 hosts
- **Defensa Perimetral**: ~30 hosts
- **Centro Médico**: ~20 hosts
- **Hangar y Taller**: ~14 hosts
- **Enlace Troncal**: Conexión con la antena de comunicaciones (1 subred)

## Red Asignada:
- **Red inicial**: 172.16.0.0/24 (256 direcciones disponibles)

## Subnetting

### 1. **Comando Central**: ~50 hosts
- Para 50 hosts necesitamos al menos una subred que soporte 64 direcciones (para cubrir la máscara de subred más pequeña que dé soporte).
- **Subred requerida**: /26 (64 direcciones)
  - **Dirección de red**: 172.16.0.0/26
  - **Rango de Hosts**: 172.16.0.1 - 172.16.0.62
  - **Dirección de broadcast**: 172.16.0.63

### 2. **Defensa Perimetral**: ~30 hosts
- Para 30 hosts necesitamos una subred con al menos 32 direcciones.
- **Subred requerida**: /26 (64 direcciones)
  - **Dirección de red**: 172.16.0.64/26
  - **Rango de Hosts**: 172.16.0.65 - 172.16.0.126
  - **Dirección de broadcast**: 172.16.0.127

### 3. **Centro Médico**: ~20 hosts
- Para 20 hosts necesitamos una subred con al menos 32 direcciones.
- **Subred requerida**: /27 (32 direcciones)
  - **Dirección de red**: 172.16.0.128/27
  - **Rango de Hosts**: 172.16.0.129 - 172.16.0.158
  - **Dirección de broadcast**: 172.16.0.159

### 4. **Hangar y Taller**: ~14 hosts
- Para 14 hosts necesitamos una subred con al menos 16 direcciones.
- **Subred requerida**: /28 (16 direcciones)
  - **Dirección de red**: 172.16.0.160/28
  - **Rango de Hosts**: 172.16.0.161 - 172.16.0.174
  - **Dirección de broadcast**: 172.16.0.175

### 5. **Enlace Troncal (Antena de Comunicaciones)**: Conexión interplanetaria
- Para este enlace, se puede utilizar una subred pequeña, dado que solo se necesita 1 enlace.
- **Subred requerida**: /30 (4 direcciones)
  - **Dirección de red**: 172.16.0.176/30
  - **Rango de Hosts**: 172.16.0.177 - 172.16.0.178
  - **Dirección de broadcast**: 172.16.0.179

## Resumen de Subredes

| **Subred**                | **Máscara** | **Dirección de Red** | **Rango de Hosts**          | **Broadcast**           | **Hosts útiles** |
|---------------------------|-------------|----------------------|----------------------------|-------------------------|------------------|
| **Comando Central**        | /26         | 172.16.0.0           | 172.16.0.1 - 172.16.0.62   | 172.16.0.63             | 62               |
| **Defensa Perimetral**     | /26         | 172.16.0.64          | 172.16.0.65 - 172.16.0.126 | 172.16.0.127            | 62               |
| **Centro Médico**          | /27         | 172.16.0.128         | 172.16.0.129 - 172.16.0.158| 172.16.0.159            | 30               |
| **Hangar y Taller**        | /28         | 172.16.0.160         | 172.16.0.161 - 172.16.0.174| 172.16.0.175            | 14               |
| **Enlace Troncal**         | /30         | 172.16.0.176         | 172.16.0.177 - 172.16.0.178| 172.16.0.179            | 2                |

# Misión 2: Sabiduría de Yoda – Algoritmos de Enrutamiento y Rutas

 # Comparativa entre Enrutamiento Estático y Dinámico

En la vastedad de la galaxia, los datos fluyen a través de rutas que pueden ser configuradas de forma estática o dinámica. Ambos métodos tienen sus ventajas y desventajas, y elegir el adecuado depende de las circunstancias específicas de la red.

## Enrutamiento Estático

El enrutamiento estático implica que un administrador de red configure manualmente las rutas entre los nodos. Estas rutas son fijas y no cambian a menos que se intervenga manualmente.

### Ventajas:
1. **Simplicidad y control:** El administrador tiene control total sobre la ruta que toma cada paquete. Las rutas son predecibles y no dependen de decisiones automáticas de los routers.
2. **Bajo uso de recursos:** Al ser configurado manualmente, no consume recursos adicionales en los routers, lo que puede ser útil en redes pequeñas o simples.
3. **Seguridad:** Al no depender de protocolos de enrutamiento externos, el enrutamiento estático puede ser más seguro, ya que no se exponen las rutas a cambios no deseados por protocolos dinámicos.

### Inconvenientes:
1. **Escalabilidad limitada:** En redes grandes, gestionar las rutas de forma estática se vuelve muy complejo. Cada vez que un nodo cambia de estado o se añaden nuevos routers, hay que reconfigurar manualmente las rutas.
2. **Falta de adaptabilidad:** Si un nodo o enlace falla, las rutas estáticas no se adaptan automáticamente. El administrador debe intervenir para ajustar las rutas, lo que puede generar tiempos de inactividad.
3. **Propenso a errores humanos:** La configuración manual aumenta el riesgo de errores, especialmente en redes grandes.

## Enrutamiento Dinámico

El enrutamiento dinámico utiliza protocolos que permiten a los routers intercambiar información entre sí para determinar automáticamente las rutas más eficientes. Existen diferentes tipos de protocolos, tales como **RIP** (Routing Information Protocol) y **OSPF** (Open Shortest Path First).

### Ventajas:
1. **Adaptabilidad:** Los protocolos dinámicos se ajustan automáticamente a los cambios en la red. Si un enlace o nodo falla, el protocolo recalcula las rutas y redirige el tráfico de manera eficiente.
2. **Escalabilidad:** A medida que la red crece, el enrutamiento dinámico puede adaptarse sin necesidad de intervención manual. Ideal para redes grandes o en expansión.
3. **Reducción de errores humanos:** Al automatizar la gestión de rutas, el enrutamiento dinámico minimiza los errores humanos que pueden surgir al configurar manualmente rutas estáticas.

### Inconvenientes:
1. **Uso de recursos:** Los protocolos dinámicos requieren más recursos de CPU y memoria en los routers, ya que deben mantener tablas de enrutamiento actualizadas y realizar cálculos continuos.
2. **Complejidad:** Los protocolos dinámicos son más complejos de configurar y mantener, especialmente cuando se usan en grandes redes. La elección del protocolo adecuado (RIP, OSPF, BGP, etc.) depende de las necesidades específicas de la red.
3. **Posibles bucles de enrutamiento:** Si no se configuran adecuadamente, los protocolos de enrutamiento dinámico pueden generar bucles de enrutamiento, lo que provoca un tráfico innecesario y ralentiza la red.

## Protocolo de Enrutamiento Dinámico: RIP vs. OSPF

### RIP (Routing Information Protocol)

- **Tipo de protocolo:** Protocolo de vector de distancia.
- **Funcionamiento:** Los routers con RIP comparten información de distancia a otras redes y seleccionan las rutas basadas en la menor cantidad de saltos. Sin embargo, no tiene en cuenta la latencia o el ancho de banda de los enlaces, lo que lo hace menos eficiente en redes grandes.
- **Ventajas:** Es sencillo de configurar y adecuado para redes pequeñas.
- **Desventajas:** Tiene limitaciones en términos de escalabilidad y convergencia, ya que los cambios de red pueden tardar más en propagarse.

### OSPF (Open Shortest Path First)

- **Tipo de protocolo:** Protocolo de estado de enlace.
- **Funcionamiento:** OSPF utiliza el algoritmo de Dijkstra para calcular las rutas más cortas, teniendo en cuenta el estado completo del enlace. Cada router mantiene una visión completa de la red y comparte esta información con los demás.
- **Ventajas:** Ofrece un rendimiento mucho mejor que RIP en redes grandes debido a su capacidad para elegir rutas basadas en métricas más completas (como la latencia y el ancho de banda).
- **Desventajas:** Es más complejo de configurar y consumir más recursos que RIP.

## Diferencias en Términos de Rendimiento y Complejidad

1. **Rendimiento:**  
   - **RIP**, al ser un protocolo de vector de distancia, tiene un enfoque más simple, pero es menos eficiente en redes grandes. Tiene una convergencia más lenta, lo que significa que los cambios en la red pueden tardar más en ser reflejados en las tablas de enrutamiento de los routers. Además, RIP solo utiliza la cantidad de saltos como métrica, lo que no siempre refleja el rendimiento real de la red.
   - **OSPF**, al ser un protocolo de estado de enlace, ofrece una convergencia más rápida y una mayor eficiencia en la elección de rutas, ya que tiene en cuenta métricas más complejas. Esto es especialmente útil en redes grandes o complejas, donde se necesita tomar decisiones de enrutamiento basadas en factores como el ancho de banda y la latencia.

2. **Complejidad:**  
   - **RIP** es más fácil de configurar y administrar, pero su simplicidad se traduce en limitaciones de escalabilidad y rendimiento.
   - **OSPF** es más complejo, pero su capacidad de manejar redes más grandes y complejas lo convierte en una opción más robusta, aunque requiere más recursos.

## ¿Cómo reaccionarían estos enfoques ante la caída repentina de un nodo?

- **Enrutamiento Estático:** Si un nodo o enlace falla, el enrutamiento estático no podrá adaptarse automáticamente. El administrador debe intervenir manualmente para ajustar las rutas y restablecer la conectividad.
- **Enrutamiento Dinámico:** Si un nodo o enlace falla, los protocolos dinámicos como RIP u OSPF recalcularán las rutas disponibles y encontrarán un nuevo camino para los paquetes. Este ajuste es automático y mucho más rápido que en el caso del enrutamiento estático.

# Misión 3: Los Nombres del Holonet – DNS y Resolución de Nombres

## Introducción

En la galaxia de las redes, la comunicación eficiente depende de la correcta resolución de nombres de dominio a direcciones IP. Esto es lo que hace posible que podamos acceder a sitios web, servidores y sistemas de forma rápida y sencilla utilizando nombres simbólicos en lugar de memorizar complejas direcciones numéricas.

### **¿Qué es DNS?**

El **Sistema de Nombres de Dominio (DNS)** es un sistema jerárquico y distribuido que se utiliza para traducir los nombres de dominio legibles por humanos (como "holonet.rebelion.org") a direcciones IP que las computadoras pueden entender (como "192.168.1.1"). Este sistema es esencial para la navegación y la comunicación dentro de redes como el Holonet o cualquier red TCP/IP.

### **Funcionamiento Básico del Sistema DNS**

Cuando un dispositivo (ya sea una computadora, un router o una nave rebelde) necesita conectarse a un servidor, lo primero que hace es intentar resolver un nombre de dominio en una dirección IP. Esto se logra mediante una serie de pasos:

1. **Solicitud de Resolución**: El dispositivo solicita al sistema DNS que resuelva un nombre de dominio (por ejemplo, "holonet.rebelion.org").
   
2. **Consulta Recursiva**: Si el servidor DNS local no tiene la dirección IP en su caché, la solicitud se envía a otros servidores DNS de la red hasta que se encuentra la dirección IP correcta.

3. **Respuesta**: Una vez que el servidor DNS encuentra la dirección IP correspondiente al nombre de dominio, la devuelve al dispositivo solicitante.

Este proceso de traducción es fundamental para la correcta comunicación entre dispositivos en la red, permitiendo que nombres simbólicos sean utilizados de manera efectiva en lugar de direcciones numéricas difíciles de recordar.

### **Servidor DNS y Registros**

Un **servidor DNS** es un servicio que maneja las solicitudes de resolución de nombres de dominio. Estos servidores almacenan información sobre los nombres de dominio y sus direcciones IP en lo que se conoce como **registros DNS**.

#### **Tipos de Registros DNS:**
- **Registro A**: Traduce un nombre de dominio a una dirección IPv4. Este es el tipo de registro más común para la resolución de nombres a direcciones IP.
  
  Ejemplo:
  - Si queremos resolver "holonet.rebelion.org", el servidor DNS buscaría en su base de datos un registro A para este dominio, que podría ser algo como:
    - **Nombre de dominio**: holonet.rebelion.org
    - **Dirección IP**: 192.168.1.10
  
  Esto significa que, al realizar una solicitud para "holonet.rebelion.org", el servidor DNS devolvería la dirección IP "192.168.1.10" al dispositivo solicitante, permitiendo que se establezca la conexión.

- **Otros Registros**: Además del registro A, existen otros tipos de registros DNS, como el **registro MX** (para servidores de correo) o **registro CNAME** (para alias de nombres de dominio), que son utilizados en diferentes contextos de la red.

### **Ejemplo de Resolución de Nombres**

Imaginemos que la red rebelde necesita acceder a un sistema clave en el Holonet, y la dirección de destino es "holonet.rebelion.org". El proceso de resolución sería el siguiente:

1. El dispositivo realiza una consulta DNS para resolver "holonet.rebelion.org".
2. El servidor DNS revisa si tiene la dirección IP asociada en su caché.
   - Si no la tiene, consulta otros servidores DNS hasta encontrar la información.
3. El servidor DNS devuelve la dirección IP asociada, por ejemplo, **192.168.1.10**.
4. El dispositivo puede ahora usar esa dirección IP para establecer la conexión con el servidor o dispositivo al que pertenece "holonet.rebelion.org".

### **Importancia del DNS en la Comunicación de Redes**

El **DNS** es vital porque permite que los usuarios y sistemas de la Alianza (y de cualquier red TCP/IP) utilicen nombres fáciles de recordar en lugar de direcciones IP. Esto hace que la administración de las redes sea mucho más sencilla y que los usuarios puedan acceder a recursos de la red sin tener que memorizar largas cadenas numéricas.

Sin un sistema DNS, la comunicación sería extremadamente difícil. Para cada conexión, los usuarios tendrían que conocer y escribir la dirección IP exacta del servidor, lo cual es poco práctico, especialmente en redes grandes y dinámicas como la que necesita la Alianza Rebelde.

### **¿Qué Sucede si el Servidor DNS No Está Disponible?**

Si el servidor DNS no está disponible, la red rebelde (o cualquier red TCP/IP) no podrá resolver los nombres de dominio en direcciones IP. Esto tendría un gran impacto en las comunicaciones, ya que:

1. **No se podrá acceder a sitios web ni servidores:** Las direcciones de destino, como "holonet.rebelion.org", no se traducirán a las direcciones IP necesarias para establecer conexiones.
2. **Interrupción en los servicios:** Cualquier servicio que dependa de la resolución de nombres de dominio, como el correo electrónico, el acceso a bases de datos remotas, y la navegación en la HoloRed, se vería afectado.
3. **Falta de conectividad:** Sin DNS, los dispositivos solo podrían comunicarse mediante direcciones IP directas, lo que sería poco práctico y propenso a errores.

Este escenario sería catastrófico para la Alianza, ya que sus sistemas de comunicación y coordinación con la flota rebelde se verían severamente interrumpidos.

## **Conclusión**

El sistema **DNS** es fundamental para la operación de redes modernas, como la HoloRed utilizada por la Alianza Rebelde. Permite que los nombres de dominio sean traducidos a direcciones IP, lo que facilita la comunicación en redes grandes y complejas. Sin un servidor DNS disponible, las comunicaciones de la Alianza estarían gravemente comprometidas, como demostraría el ejemplo de "Unknown host" que observamos a bordo de la nave Home One. La fiabilidad y disponibilidad de los servidores DNS son cruciales para mantener la red operativa y garantizar el éxito de las misiones de la Alianza.

# Misión 4: “Es una trampa… de protocolos!” – TCP vs UDP en las transmisiones

# Comparativa entre TCP y UDP en la Transmisión de Datos

Durante la batalla espacial sobre Endor, Luke Skywalker nota que algunas de sus transmisiones son rápidas, pero con pérdidas ocasionales de datos, mientras que otras son más lentas, pero seguras y ordenadas. Esto se debe al uso de distintos protocolos de transporte: **TCP (Transmission Control Protocol)** y **UDP (User Datagram Protocol)**. Ambos protocolos tienen características y comportamientos distintos en cuanto a la transmisión de datos. Vamos a comparar ambos en este contexto galáctico.

## **TCP (Transmission Control Protocol)**

### **Características:**

1. **Orientado a conexión:** TCP establece una conexión confiable entre el emisor y el receptor antes de que los datos sean enviados. Este proceso de "handshake" asegura que ambas partes estén listas para recibir y enviar datos de manera segura.

2. **Fiabilidad:** TCP garantiza la entrega correcta y ordenada de los datos. Si los paquetes se pierden o llegan de manera desordenada, TCP los detectará y solicitará su reenvío. Esto asegura que los datos lleguen completos y sin errores.

3. **Control de flujo y congestión:** TCP implementa mecanismos para controlar la cantidad de datos enviados y evitar sobrecargar la red. Si hay congestión, TCP reduce la velocidad de transmisión hasta que la red esté libre.

4. **Mayor latencia:** Debido a sus mecanismos de control y verificación, TCP introduce un retraso adicional, lo que lo hace más lento que UDP.

### **Ventajas:**
- **Confiabilidad:** Ideal para aplicaciones donde la integridad y el orden de los datos son cruciales.
- **Ideal para datos críticos:** Garantiza que todos los datos lleguen de manera completa, sin errores y en el orden correcto.

### **Desventajas:**
- **Mayor latencia:** El control de flujo, la verificación de errores y la retransmisión de paquetes perdidos pueden ralentizar la transmisión de datos.

### **Ejemplo Galáctico:**
- **Comunicaciones rutinarias** (por ejemplo, la transferencia de los **planos de la Estrella de la Muerte**): Estos datos deben llegar de manera completa y en el orden correcto, ya que un solo error podría comprometer una misión. En este caso, TCP es la elección correcta porque garantiza la entrega sin pérdidas y ordenada.

## **UDP (User Datagram Protocol)**

### **Características:**

1. **No orientado a conexión:** UDP no establece una conexión antes de enviar los datos. Los paquetes se envían sin verificar si el receptor está listo o si los paquetes llegarán correctamente.

2. **No confiable:** UDP no realiza comprobaciones de error ni garantiza la entrega de los datos. Si un paquete se pierde en el camino, no se solicita su reenvío. Los paquetes pueden llegar en un orden diferente al que fueron enviados.

3. **Sin control de flujo ni congestión:** UDP no realiza ningún control sobre el flujo de datos ni sobre la congestión de la red. Esto lo hace más rápido, pero también menos seguro.

4. **Baja latencia:** Dado que UDP no tiene mecanismos de control, los datos se envían más rápidamente y con menor latencia que TCP.

### **Ventajas:**
- **Rapidez:** La ausencia de verificación y control de errores permite una transmisión de datos mucho más rápida.
- **Ideal para aplicaciones en tiempo real:** Perfecto para situaciones donde la velocidad es más importante que la integridad completa de los datos.

### **Desventajas:**
- **No garantiza la entrega:** Si los paquetes se pierden o llegan fuera de orden, no hay ninguna manera de recuperarlos. Esto puede ser un problema en aplicaciones que necesitan datos completos y en orden.

### **Ejemplo Galáctico:**
- **Transmisión de datos en tiempo real** (por ejemplo, las **coordenadas de combate de un X-Wing**): En una misión crítica, las coordenadas deben enviarse rápidamente para evitar que la nave rebelde se pierda en el combate. En este caso, una pequeña pérdida de datos no es un gran problema, ya que la prioridad es la rapidez en la transmisión. UDP es ideal para esta situación porque minimiza los retrasos, lo cual es más importante que asegurar la integridad de cada paquete.

## **Comparación de Rendimiento y Uso**

| **Característica**      | **TCP**                                      | **UDP**                                       |
|-------------------------|----------------------------------------------|-----------------------------------------------|
| **Confiabilidad**        | Alta, garantiza la entrega de datos completos y ordenados | Baja, no garantiza la entrega ni el orden de los datos |
| **Latencia**             | Alta, debido a los controles y verificaciones | Baja, transmite rápidamente sin controles     |
| **Ideal para**           | Datos que requieren integridad, como la transferencia de archivos o comunicaciones cruciales | Datos que requieren velocidad, como transmisiones en vivo o comunicaciones en tiempo real |
| **Ejemplo Galáctico**    | Transferencia de planos de la Estrella de la Muerte | Transmisión de coordenadas de combate de un X-Wing |
| **Control de Congestión**| Sí, reduce la velocidad en caso de congestión | No, no hay control sobre la congestión         |

## **Conclusión**

La diferencia entre **TCP** y **UDP** radica en cómo gestionan la confiabilidad, la latencia y el control de los datos. **TCP** es perfecto para comunicaciones donde la integridad de los datos es esencial, como en la transferencia de los planos de la Estrella de la Muerte, ya que garantiza que los datos lleguen completos y en orden. Por otro lado, **UDP** es ideal para situaciones donde la velocidad es crucial y se pueden tolerar algunas pérdidas, como la transmisión de las coordenadas de combate de un X-Wing, donde la rapidez es más importante que la perfección de cada paquete.

La elección del protocolo adecuado depende del tipo de aplicación y de las necesidades específicas de cada misión en la galaxia, ya sea una operación secreta que depende de datos completos y ordenados o una batalla en tiempo real donde la velocidad lo es todo.


# Misión 5: Comunicación Segura o lado oscuro – Criptografía y Seguridad de la Red

# Protocolo de Comunicación Cifrada para la Alianza Rebelde

## Introducción

La seguridad de las comunicaciones es fundamental para la Alianza Rebelde. El Imperio, con su vasto alcance de vigilancia, intercepta cualquier señal para obtener inteligencia sobre las operaciones de la Rebelión. Para mantener la confidencialidad de los mensajes, es esencial cifrar las transmisiones, utilizando técnicas de cifrado que impidan que los enemigos, incluidos los espías imperiales, puedan descifrar la información.

## **Cifrado Simétrico vs. Cifrado Asimétrico**

Existen dos métodos principales para cifrar las comunicaciones: **cifrado simétrico** y **cifrado asimétrico**. Ambos métodos sirven para proteger los mensajes, pero funcionan de maneras diferentes y tienen ventajas específicas según la situación.

### **Cifrado Simétrico**

**¿Cómo Funciona?**
- En el **cifrado simétrico**, se utiliza una **misma clave secreta** para cifrar y descifrar el mensaje. Tanto el remitente como el receptor deben conocer esta clave secreta para que la comunicación sea segura.
- **Ejemplo**: Si **Leia** y **Luke** comparten una clave secreta, como una **frase clave** secreta, pueden usarla para cifrar sus **holomensajes**. El proceso sería el siguiente:
  1. **Leia** utiliza la clave secreta para cifrar su mensaje.
  2. **Luke**, quien también tiene la misma clave secreta, usa la misma clave para descifrar el mensaje.

**Ventajas:**
- **Rápido y eficiente**: El cifrado simétrico es generalmente más rápido que el asimétrico, lo que lo hace ideal para cifrar grandes volúmenes de datos.
- **Menos recursos computacionales**: Requiere menos poder de procesamiento en comparación con el cifrado asimétrico.

**Desventajas:**
- **Distribución de claves**: El mayor problema con el cifrado simétrico es la necesidad de compartir la clave secreta de manera segura antes de que las comunicaciones puedan comenzar. Si un espía intercepta esta clave, podrá descifrar todos los mensajes.
- **Riesgo si la clave se ve comprometida**: Si la clave secreta es interceptada o descubierta por el enemigo, toda la comunicación queda en riesgo.

**Ejemplo Galáctico**: 
- **Leia y Luke comparten una clave secreta para cifrar sus comunicaciones.** Este tipo de cifrado sería **simétrico**, ya que ambos necesitan la misma clave para acceder a los mensajes cifrados.

---

### **Cifrado Asimétrico (Criptografía de Clave Pública y Privada)**

**¿Cómo Funciona?**
- El **cifrado asimétrico** utiliza dos claves diferentes: una **clave pública** para cifrar el mensaje y una **clave privada** para descifrarlo. Las claves pública y privada están relacionadas matemáticamente, pero no se pueden derivar una de otra.
- **Ejemplo**: Si la **Alianza** quiere enviar un mensaje a un nuevo aliado sin haber intercambiado una clave secreta previamente, el proceso sería el siguiente:
  1. La **Alianza** obtiene la **clave pública** del aliado (que puede ser obtenida a través de un directorio público).
  2. La Alianza cifra el mensaje con esta clave pública.
  3. El **nuevo aliado**, quien posee la **clave privada** correspondiente, puede descifrar el mensaje con su clave privada.

**Ventajas:**
- **Seguridad sin necesidad de compartir claves secretas**: No es necesario compartir claves antes de la comunicación. Cualquier persona puede cifrar un mensaje con la clave pública de otra, pero solo el titular de la clave privada correspondiente puede descifrarlo.
- **Ideal para comunicaciones iniciales**: Permite a la Alianza enviar mensajes seguros a nuevos aliados sin tener que intercambiar claves secretas previamente.

**Desventajas:**
- **Lento y requiere más recursos**: El cifrado asimétrico es más lento y consume más recursos computacionales que el cifrado simétrico. Esto lo hace menos adecuado para cifrar grandes volúmenes de datos.

**Ejemplo Galáctico**: 
- Si la **Alianza Rebelde** quiere enviar un mensaje seguro a un nuevo aliado, puede cifrarlo usando la **clave pública** del aliado. El aliado podrá descifrarlo solo con su **clave privada**. Este tipo de cifrado sería **asimétrico**.

---

## **Autenticación y No Repudio**

En el contexto de las comunicaciones de la Alianza, es esencial no solo garantizar la **confidencialidad** de los mensajes, sino también asegurar que:
1. **El mensaje proviene de quien dice ser**: Esto se logra mediante un proceso de **autenticación**, que puede hacerse usando firmas digitales. Una **firma digital** es un tipo de cifrado que permite al receptor verificar que el mensaje proviene de una fuente legítima.
   
2. **El mensaje no ha sido alterado**: Al usar **hashes criptográficos** junto con firmas digitales, podemos asegurarnos de que los mensajes no hayan sido modificados durante el tránsito.

3. **No repudio**: El **no repudio** se refiere a garantizar que el remitente no pueda negar haber enviado el mensaje. Si un mensaje está firmado digitalmente por el remitente, no podrá alegar que no lo envió.

---

## **Uso de Protocolos Seguros: SSH vs. Telnet**

Cuando los rebeldes administran de forma remota los sistemas y servidores de la red, es crucial utilizar un protocolo seguro como **SSH (Secure Shell)** en lugar de **Telnet**. ¿Por qué?

- **SSH** cifra toda la comunicación entre el cliente y el servidor, protegiendo así las credenciales y los datos transmitidos de cualquier posible interceptación por parte del Imperio.
- **Telnet**, por otro lado, envía la información en texto plano, lo que significa que cualquier espía imperial podría interceptar fácilmente las credenciales de acceso, comprometiendo la seguridad de la red rebelde.

Por lo tanto, al administrar remotamente los equipos, **SSH** asegura que las credenciales y las acciones de administración estén protegidas contra interceptaciones, mientras que **Telnet** representa un grave riesgo para la seguridad.

---

## **Conclusión**

Para garantizar la confidencialidad, autenticidad y seguridad de las comunicaciones de la Alianza Rebelde:
- **Cifrado Simétrico** es útil para comunicaciones rápidas y entre miembros confiables que ya tienen una clave compartida, como en el caso de **Leia y Luke**.
- **Cifrado Asimétrico** es esencial para comunicaciones seguras con nuevos aliados sin haber intercambiado previamente una clave secreta.
- La **autenticación** y el **no repudio** son necesarios para garantizar que los mensajes no sean alterados y provengan de una fuente confiable.
- **Protocolos seguros como SSH** son imprescindibles para la administración remota de la red rebelde, evitando que las credenciales sean interceptadas.

La clave para la seguridad de la Alianza radica en emplear estas técnicas de cifrado y autenticación en todas las comunicaciones, garantizando que los planes de batalla y las misiones críticas no caigan en manos del Imperio.

