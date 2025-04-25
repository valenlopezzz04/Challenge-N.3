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

### Arquitectura Propuesta

### Desarrollo Teórico Modular: Criterios de Diseño Establecidos

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
