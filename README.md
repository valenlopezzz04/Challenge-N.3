# Sistema IoT para Detección de Incendios en los Cerros Orientales de Bogotá - Challenge 3

## Información del Proyecto
- **Universidad:** Universidad de La Sabana  
- **Facultad:** Facultad de Ingeniería  
- **Materia:** Internet de las Cosas  
- **Profesor:** Juan Manuel Aranda López King  

## Integrantes del Proyecto
| Nombre | Correo Electrónico |
|--------|-------------------|
| Valentina Alejandra López Romero | valentinalopro@unisabana.edu.co |
| Ana Lucía Quintero Vargas | anaquiva@unisabana.edu.co |
| Mariana Valle Moreno | marianavamo@unisabana.edu.co |

## Estructura de la Documentación
- [1. Introducción](#1-introducción)
- [2. Motivación y Justificación](#2-motivación-y-justificación)
- [3. Solución Propuesta](#3-solución-propuesta)
- [4. Configuración Experimental, Resultados y Análisis](#4-configuración-experimental-resultados-y-análisis)
- [5. Autoevaluación del Protocolo de Pruebas](#5-autoevaluación-del-protocolo-de-pruebas)
- [6. Conclusiones, Retos y Mejoras Futuras](#6-conclusiones-retos-y-mejoras-futuras)
- [7. Referencias](#7-referencias)
- [8. Anexos](#8-anexos)

---

## 1. Introducción
<p align="justify">
Los cerros orientales de Bogotá son fundamentales para la regulación climática y la conservación de la biodiversidad. Su presencia como barrera y protector natural constituye un regulador del clima, del cual depende en buena medida la disponibilidad de agua para la capital y municipios aledaños [1]. Además, son esenciales en la producción de oxígeno en una sabana donde la pérdida de vegetación es creciente, lo que los hace aún más vulnerables a incendios forestales agravados por sequías prolongadas, altas temperaturas y la acumulación de material seco, junto con actividades humanas como fogatas, quemas agrícolas y expansión urbana descontrolada [2].
</p>

<p align="justify">
Ante este panorama, es fundamental implementar sistemas inteligentes de monitoreo ambiental que permitan la detección temprana de incendios y habiliten una respuesta efectiva por parte de las autoridades. Este proyecto propone el desarrollo de un sistema IoT que integra sensores físicos con una arquitectura de comunicación basada en MQTT, diseñada para recolectar, analizar y transmitir en tiempo real datos sobre temperatura, presencia de gas y detección de llama en los cerros orientales de Bogotá.
</p>

<p align="justify">
La información capturada se visualiza localmente a través de un servidor web embebido en el ESP32 y, simultáneamente, se envía a una Raspberry Pi que actúa como IoT Gateway. Allí, los datos se almacenan en una base de datos SQLite y se reenvían a la plataforma IoT Ubidots. Esta plataforma permite la consulta remota desde cualquier navegador web, la recepción de alertas y la ejecución de acciones como el apagado de alarmas físicas mediante un botón interactivo. De esta forma, se garantiza un monitoreo constante, una trazabilidad confiable de los datos recolectados y una capacidad de respuesta rápida y descentralizada ante posibles emergencias ambientales; de esta manera, contribuyendo para optimizar los tiempos de respuesta, reducir el impacto ambiental de los incendios y fortalecer las estrategias de prevención.
</p>

---

## 2. Motivación y Justificación
<p align="justify">
Actualmente, la detección de incendios en los cerros orientales de Bogotá depende principalmente de vigilancia manual o reportes ciudadanos, lo que retrasa la respuesta de las autoridades y agrava los daños ecológicos, sociales y económicos. Ante este contexto, surge la necesidad de implementar soluciones tecnológicas que permitan un monitoreo constante, preciso y en tiempo real, capaces de generar alertas automáticas y accesibles desde cualquier punto del país.
</p>

<p align="justify">
Este proyecto propone una solución basada en Internet de las Cosas (IoT) que integra un sensor de temperatura (DS18B20), un sensor de llama y un sensor de gas (MQ-2), conectados a un ESP32 que recolecta los datos y activa alarmas visuales y sonoras, incluyendo un zumbador activo, un LED RGB y un módulo LCD I2C, para generar notificaciones en tiempo real en caso de riesgo. La información capturada se transmite mediante el protocolo de comunicación MQTT a una Raspberry Pi, que actúa como IoT Gateway, donde se almacenan los datos en una base de datos SQLite y se reenvían a la plataforma IoT Ubidots. Desde allí, las autoridades pueden visualizar remotamente los datos desde cualquier navegador web o dispositivo móvil, además, de recibir y desactivar las alertas fisicas automatizadas.
</p>

<p align="justify">
Gracias a su arquitectura modular, al uso de comunicación inalámbrica y a su capacidad de respuesta automática, esta solución mejora significativamente los tiempos de reacción ante emergencias, facilita el seguimiento preciso de las condiciones ambientales y contribuye al fortalecimiento de estrategias prevención y mitigación de incendios forestales en zonas vulnerables y de difícil acceso.
</p>

---

## 3. Solución Propuesta

### Restricciones de Diseño Identificadas

<p align="justify"> 
Al desarrollar el sistema IoT para detectar incendios en los cerros orientales de Bogotá, se identificaron varias restricciones que afectan su diseño, implementación y comunicación de datos:
</p> 

#### 1. Técnicas
- Se usa un **ESP32**, el cual tiene un límite en la memoria RAM y el procesamiento, lo que puede afectar la ejecución simultánea del servidor web local, la recolección de datos de sensores, la transmisión de datos mediante MQTT hacia el broker en la Raspberry Pi.
- Los sensores de **temperatura, gas (MQ-2) y llama** requieren una calibración precisa para minimizar falsas alarmas, además de que tienen determinados tiempos de respuesta que pueden influir en la detección temprana de incendios.
- Dependencia de una conexión estable de WiFi para enviar y visualizar los datos en la interfaz web local, mantener la conexión activa con el broker MQTT y permitir la actualización de estados en tiempo real hacia Ubidots.
- Para la gestión de múltiples tareas, se implementó un enfoque optimizado que permite la adquisición de datos sin afectar la estabilidad del sistema y la transmisión de datos por MQTT.
- El sistema debe gestionar reconexiones automáticas al broker MQTT para garantizar continuidad en la transmisión de datos ante caídas de red.
- La Raspberry Pi debe estar configurada de forma robusta para funcionar como un broker MQTT estable, lo que incluye la gestión de múltiples conexiones simultáneas si se escala el sistema.
- Dependencia de servicios en la nube (Ubidots), lo que introduce una nueva capa de posibles fallas externas (caídas del servicio, latencia en internet).

#### 2. Económicas
- Se sigue buscando minimizar costos, utilizando hardware como el ESP32, sensores económicos pero siendo lo suficientemente confiables y precisos para realizar apropiadamente las mediciones; y una Raspberry Pi como broker local en lugar de servicios en la nube de pago (por ejemplo, brokers MQTT comerciales).
- Utilización del Free Trial de Ubidots para el monitoreo en la nube.
- uso de tecnologías inalámbricas evita la necesidad de instalaciones físicas costosas (cableados extensivos, redes cableadas).
  
#### 3. Regulatorias
- Se debe cumplir con normativas ambientales y estándares de seguridad eléctrica para su instalación de equipos electrónicos en zonas protegidas y transmisión de datos desde dispositivos de monitoreo ambiental.
- Cualquier intervención en los cerros debe ajustarse a regulaciones locales.
- Debe revisarse el cumplimiento de normas sobre protección de datos y transmisión segura con plataformas externas (Ubidots).

#### 4. Espaciales
- El sistema debe ser compacto y resistente a condiciones climáticas adversas (lluvia, humedad y polvo).
- Los sensores deben estar ubicados estratégicamente para detectar cambios de temperatura y gases sin interferencias, maximizando su efectividad sin afectar el ecosistema.
- Para el montaje del sistema, la integración de la pantalla LCD, los LEDs y los sensores debe ser compacta y accesible.

#### 5. Escalabilidad
- Aunque es un prototipo, debe permitir mejoras o expansión en el futuro como agregar más nodos ESP32 reportando al mismo broker Raspberry Pi y hacer que Ubidots permite visualizar múltiples dispositivos o variables en un mismo tablero de control. 
- Si se desean conectar múltiples dispositivos a un mismo servidor, se debe optimizar la comunicación para no saturar la red.
- Si se requiere monitoreo en varias áreas, se debe considerar el crecimiento del número de conexiones simultáneas al broker local y el impacto en el desempeño de la red WiFi.

#### 6. Temporales
- El sistema debe operar en **tiempo real** para detectar incendios lo más rápido posible, donde se establece un intervalo adecuado entre lecturas en los sensores para evitar saturación del sistema sin comprometer la detección temprana (3 segundos), en este caso para la publicación de datos MQTT y que el servidor local y la nube muestren las actualizaciones casi inmediatamente después de cada lectura.
- El sistema ahora requiere mecanismos de reconexión automática para el broker MQTT y para el WiFi, minimizando la necesidad de intervención manual constante.
  
### Arquitectura Propuesta

<p align="justify"> 
A continuación, se presenta un Diagrama de Bloques que ilustra los elementos de hardware y software que conforman la solución IoT desarrollada.
</p> 

![Diagrama de la arquitectura de la solución](Diagramas/DiagramaBloques.png)
*Figura 1: Arquitectura IoT propuesta de la solución.*

<p align="justify"> 
El sistema está basado en un ESP32, que actúa como la unidad de procesamiento principal y se encarga de la adquisición y preprocesamiento de datos provenientes de los sensores de temperatura (DS18B20), gas (MQ-2) y llama. El módulo de sensado opera de forma continua en segundo plano, y la información recopilada es analizada localmente para actualizar el historial de temperaturas, detectar condiciones de riesgo y gestionar alertas en tiempo real. En caso de que se determine una situación de peligro, el módulo de actuadores entra en acción, activando un LED RGB y un buzzer para alertar sobre el estado del ambiente. Asimismo, el módulo de visualización local actualiza la pantalla LCD I2C, donde se muestra en tiempo real la temperatura y el estado general del entorno. </p>

<p align="justify">
De igual forma, con respecto a la visualización local, el ESP32 implementa un servidor web embebido (EWS), permitiendo a los usuarios monitorear el sistema en tiempo real a través de una interfaz web accesible desde cualquier dispositivo conectado a la misma red WiFi, la cual puede establecerse utilizando un punto de acceso externo (AP o router). La comunicación entre el ESP32 y los navegadores web se realiza mediante el protocolo TCP/IP. </p>

<p align="justify"> En cuanto a la comunicación externa, el ESP32 utiliza el protocolo MQTT para enviar periódicamente los datos adquiridos a una Raspberry Pi configurada como Gateway IoT. Esta Raspberry Pi alberga un broker Mosquitto y una base de datos SQLite que permite el almacenamiento local de la información, proporcionando una capa adicional de persistencia y respaldo de datos. </p>

<p align="justify"> Adicionalmente, la Raspberry Pi se encarga de reenviar los datos relevantes a la plataforma en la nube Ubidots, también utilizando el protocolo MQTT. Desde Ubidots, se habilita la supervisión remota del sistema y el control de alarmas, permitiendo el envío de comandos de respuesta hacia el ESP32 en situaciones de emergencia o condiciones anómalas. </p>

<p align="justify">
Cabe resaltar que toda la lógica de adquisición, procesamiento, comunicación y control ha sido desarrollada en C++ para el ESP32 y Python para la Raspberry Pi, garantizando una operación eficiente, autónoma y resiliente del sistema IoT propuesto. Esta integración de hardware y software permite monitorear el entorno de forma local y remota, maximizando la confiabilidad y accesibilidad de la solución. </p>


### Desarrollo Teórico Modular: Criterios de Diseño Establecidos
Para que el sistema sea eficiente y funcional, se definieron los siguientes criterios de diseño:

#### 1. Fiabilidad y Precisión
- Se seleccionaron sensores adecuados para la detección confiable sobre temperatura, gases y llamas.
- Se implementaron límites y filtros dentro del código para reducir errores y evitar falsas alarmas.
- Se optimizó la adquisición de datos mediante procesamiento concurrente, asegurando mediciones en tiempo real.

#### 2. Autonomía y Eficiencia
- El sistema es **autosuficiente**, operando sin necesidad de conexión a redes externas para su funcionamiento básico local.
- Su diseño es resistente a la intemperie, minimizando la necesidad de mantenimiento.
- Se implementaron mecanismos de gestión de tareas para evitar interrupciones en la adquisición de datos y la respuesta del sistema.
  - Se implementó **FreeRTOS**, lo que permitió la creación de un segundo y tercer hilo, mejorando la gestión del tiempo de ejecución de las tareas.
- **Concurrencia en FreeRTOS:** La concurrencia permite que varias tareas se ejecuten de manera que parecen realizarse simultáneamente.
  - Con **FreeRTOS**, se logró una gestión real de tareas en paralelo mediante múltiples hilos de ejecución.

#### 3. Interfaz de Usuario Intuitiva
- Se usa una **pantalla LCD** para mostrar datos en tiempo real localmente.
- Se integró un servidor web embebido (EWS) con HTML y JavaScript para la visualización remota a nivel de red local.
- Se incorporaron gráficos dinámicos con historial de mediciones recientes en la interfaz web.
- Se implementaron **alarmas visuales (LED RGB) y sonoras (zumbador)** para notificaciones inmediatas sobre condiciones de riesgo.
- Adicionalmente, se habilitó la monitorización remota a través de la nube utilizando la plataforma Ubidots, proporcionando acceso a la información desde cualquier lugar con conexión a Internet.

#### 4. Escalabilidad y Modularidad
- El sistema fue diseñado de forma **modular**, permitiendo agregar nuevos sensores o funciones en el futuro de manera sencilla.
- Se implementó el protocolo **MQTT** como capa de comunicación entre el dispositivo ESP32 y un Gateway IoT (Raspberry Pi).
- La Raspberry Pi no solo recibe y almacena datos localmente utilizando SQLite, sino que también actúa como puente para transmitir los datos a la nube (Ubidots) mediante MQTT.

#### 5. Persistencia de Datos y Resiliencia
- Se implementó un esquema de persistencia local mediante una base de datos SQLite en la Raspberry Pi, garantizando que los datos históricos estén disponibles incluso en caso de pérdida temporal de conexión a Internet.
- La duplicidad de almacenamiento (local en la Raspberry Pi y en la nube con Ubidots) asegura la disponibilidad continua de la información crítica.


### Diagrama UML

### Esquemático de Hardware

### Estándares de Ingeniería Aplicados

---

## 4. Configuración Experimental, Resultados y Análisis
<p align="justify">
  
</p>

---

## 5. Autoevaluación del Protocolo de Pruebas
<p align="justify">

</p>

### Mejoras Identificadas en el Proceso de Pruebas

### Comparación de Desempeño con Expectativas Iniciales
<p align="justify">

</p>

---

## 6. Conclusiones, Retos y Mejoras Futuras

### Conclusiones

### Retos Presentados Durante el Desarrollo del Proyecto

### Trabajo Futuro

---

## 7. Referencias

## 8. Anexos
