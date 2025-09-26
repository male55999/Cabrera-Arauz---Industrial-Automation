# INDUSTRIAL AUTOMATION
MARIA ALEJANDRA CABRERA ARAUZ
### Descripción General:
### Introducción:
En este informe se expondrá la construcción de un sistema de automatización que tiene como fin hacer monitorización de niveles, en este caso de tanques de líquidos químicos. Por medio de una metodología que incluye el diseño de una interfaz HMI en CODESYS, la validación de la lógica con OpenPLC y la integración con hardware, para este ultimo punto usamos Arduino Uno. El enfoque principal del sistema es la lógica combinacional, asegurando un control preciso y fiable en un entorno simulado, plantando las bases para su aplicación en un contexto industrial real.
### Objetivo:
Diseñar e implementar una solución de control, con su respectiva validación, y la documentación de todo el proceso. Se buscó desarrollar una lógica combinacional robusta para garantizar un control seguro del sistema dentro de un entorno industrial simulado.
### Estructura del Informe:
La metodología de este informe sigue las fases del proyecto dadas: primero el diseño lógico y la simulación en CODESYS, seguido de la implementación de software en OpenPLC y, finalmente, la validación con hardware físico (Arduino Uno).
## CODESYS
### Lógica del Sistema:
La base del control en CODESYS es un circuito de lógica combinacional diseñado para gestionar y visualizar los niveles del tanque, además, se implemento un sensor de fuga que detra el proceso hasta que este sea solucionado. Esta lógica se implementó mediante un diagrama de escalera (Ladder Diagram) como se puede observar en la imagen1 que define las relaciones entre los sensores de nivel (alto y bajo), los indicadores visuales de estado (bajo, cargando, alto y el medidor), el funcionamiento de la bomba y el sensor de fuga.
<img width="669" height="375" alt="Captura de pantalla 2025-09-23 213045" src="https://github.com/user-attachments/assets/5893857c-9dfa-4f35-99e7-0730b88ae732" />
imagen 1 (creación de archivo LD en CODESYS)
### Implementación y Resultados:
Para su implementación, se creo paralelamente el HMI y el diagram de escalera con el fin de que se vincularan al final. Lo primer que se hizo fue crear la visualización (HMI) en POU y por medio de las diferente herraminetes de CODESYS se fue creando el HMI que se puede observar en la imagen2.
<img width="706" height="367" alt="Captura de pantalla 2025-09-24 184922" src="https://github.com/user-attachments/assets/809e7102-03c0-43f6-978a-bf0bb63ed404" />
Imagen2 (Diseño en CODESYS de la HMI)

Paralelamente como se mencionó anteriormente, se creo el diagrama en escalera que se puede observar en la imagen3,
<img width="1105" height="827" alt="Captura de pantalla 2025-09-24 184908" src="https://github.com/user-attachments/assets/cdbedc15-ba58-46be-9961-12d7ad927841" />
Imagen3 (Diagrama en escalera en CODESYS)
## OPENPLC
### Lógica del Sistema:
### Implementación y Resultados:
## HARDWARE
### Lógica del Sistema:
### Implementación y Resultados:
## CONCLUSIÓN
