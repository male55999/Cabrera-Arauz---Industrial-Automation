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
Para su implementación, se creo paralelamente el HMI y el diagram de escalera con el fin de que se vincularan al final. Lo primer que se hizo fue crear la visualización (HMI) en POU y por medio de las diferente herraminetes de CODESYS se fue creando el HMI que se puede observar en la imagen2. Cuando inicia la simulación el nivel comienza a aumentar tanto en el manometro como en el tanque y a medida que esto pasa se van mostrando los niveles con las diferentes lamparas, en caso de que exista una fuga se enciende la alarma y se pausa aumento de nivel al igual que el funcionamiento de la bomba.
<img width="706" height="367" alt="Captura de pantalla 2025-09-24 184922" src="https://github.com/user-attachments/assets/809e7102-03c0-43f6-978a-bf0bb63ed404" />
Imagen2 (Diseño en CODESYS de la HMI)

Paralelamente como se mencionó anteriormente, se creo el diagrama en escalera que se puede observar en la imagen3, en el primer Rung podemos observar el ingreso de la señal de los dos sensores (bajo y alto) a la bomba de control que por medio de un SR (Set/Reset) prende o apaga la bomba, es decir, cuando el sensor_nivel_bajo manda la señal se activa y cuando entra la señal del sensor_nivel_alto se apaga, además, en este Rung tambien entra el sensor_fuga que lo que hace por medio de un contacto negado es pausar el funcionamiento de la bomba en caso de fuga. Para el Rung 2, tenemos el sumador de nivel, es decir que el nivel se va sumando de uno en uno. Finalmente, los Rungs 3, 4 y 5 funcionan de forma similar y estos tienen como función mas que todo generar la visualización del HMI, en el Rung 3 se ve el nivel alto es decir cuando es igual a 999, en el Rung 4 cuando es mayor a 100 pero menor de 999 y en el Rung 5 cuando es menor o igual a 100. Todo esto resulto en una simulación satisfactoria donde el diagrama de escalera muestra de forma positiva su ejecución con el HMI.
<img width="1105" height="827" alt="Captura de pantalla 2025-09-24 184908" src="https://github.com/user-attachments/assets/cdbedc15-ba58-46be-9961-12d7ad927841" />
Imagen3 (Diagrama en escalera en CODESYS)
## OPENPLC
### Lógica del Sistema:
Para validar de manera independiente la lógica de control, se replicó el diagrama de escalera en OpenPLC. Esta herramienta fue fundamental para simular el comportamiento de un PLC real. La lógica se configuró para mapear las entradas y salidas virtuales de la simulación a los pines físicos de una placa de hardware, preparando el sistema para las pruebas de campo.
### Implementación y Resultados:
Para este paso, se generaron los mismos 5 Rungs que ya mencioné anteriormente pero en esta ocasión en OPENPLC, acá se tuvieron que declarar las variables con mayor detalle como se muestra en la imagen4, posteriormente, ya con las variables creadas se implemento el diagrama de escalera mencionado anteriormente como se puede ver en la imagen5 y finalmente se compilo lo realizado para así poderlo llevar a un Arduino Uno como se ve en la imagen6. Como resultado, se compilo y se genero el formato Arduino Uno exitosamente.
<img width="576" height="274" alt="Captura de pantalla 2025-09-24 200340" src="https://github.com/user-attachments/assets/ae2dbc73-9f4b-4cec-872a-aadf3cffaad6" />
Imagen4 (Declaración de variables en OPENPLC)
<img width="1145" height="641" alt="image" src="https://github.com/user-attachments/assets/7c8c3721-f23a-426a-a0f2-80340161668c" />
Imagen5 (Diagrama en escalera en OPENPLC)
<img width="1232" height="773" alt="image" src="https://github.com/user-attachments/assets/91243138-e332-48e4-9f4d-0ee9cbfb1172" />
Imagen6 (Compilación funcionando en OPENPLC)
## HARDWARE
### Lógica del Sistema:
El circuito de hardware fue diseñado para simular los componentes industriales del sistema. Los sensores de nivel se representaron con interruptores, y los actuadores (indicadores de estado y bombas) se simularon con LEDs. Todo esto sale de la placa que ejecuta el código de OpenPLC y que se transformo en Arduino Uno.
### Implementación y Resultados:
El hardware se construyó físicamente en un protoboard. Las pruebas de cableado no fueron exitosas, lo que representó un desafío significativo. Los cables y conexiones presentaban fallos intermitentes y no lograban replicar la lógica de control de manera confiable. Pero quedó el cableado como se ve en la imagen7.
![Imagen de WhatsApp 2025-09-25 a las 22 17 20_d63cabb0](https://github.com/user-attachments/assets/f287ec05-843a-4764-b6d0-939a63933724)
Imagen7 (Cableo de la simulación del Hardware)
## CONCLUSIÓN
### Resumen de Resultados:
En síntesis, este proyecto demostró con éxito la viabilidad de utilizar un flujo de trabajo que combina simulación y validación con hardware real. El proyecto alcanzó sus objetivos de diseño e implementación de un sistema de automatización funcional aunque no fue posible su ejecución en un entorno físico. La integración de CODESYS y OpenPLC fue exitosa, confirmando la robustez de la lógica combinacional de control.

### Aprendizajes y Desafíos:
Durante el proceso, se obtuvieron lecciones aprendidas sobre la resolución de problemas y se superaron desafíos técnicos en la integración de software. El proyecto subraya la importancia de la validación como un paso crítico para garantizar la fiabilidad de un sistema antes de su despliegue final. Adicionalmente y personalmente, aprendí mucho y me sentí bien ejecutandolo.
