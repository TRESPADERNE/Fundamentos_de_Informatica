# Introducción a la Arquitectura de Computadores


## Índice
1. [Introducción](#1-introducción)
2. [Estructura de un computador: enfoque multinivel](#2-estructura-de-un-computador-enfoque-multinivel)
3. [Organización y funcionamiento de la CPU](#3-organización-y-funcionamiento-de-la-cpu)
4. [El repertorio de instrucciones (ISA)](#4-el-repertorio-de-instrucciones-isa)
5. [El rendimiento de un computador](#5-el-rendimiento-de-un-computador)
6. [La memoria](#6-la-memoria)
7. [Interrupciones](#7-interrupciones)
8. [Dispositivos de Entrada/Salida](#8-dispositivos-de-entradasalida)
9. [Bibliografía](#bibliografía)



## 1. Introducción
En 1945 John Von Neumann publicó un modelo de arquitectura de computador que sigue hoy en día siendo la base de la mayor parte de las arquitecturas de computador actuales.

La **arquitectura Von Neumann** distingue tres bloques funcionales fundamentales:
*   **El procesador o CPU (Central Processing Unit)**
Ejecuta los programas.
*   **La memoria**
Contiene **datos** e **instrucciones**, que pueden ser leídos y escritos.
    *   **valores**, como peso, volumen, sueldo, velocidad, cantidades, nombres, fechas, etc. y **direcciones de memoria**.
    *  **instrucciones** para procesar esos valores.
*   **Dispositivos de entrada/salida**
Suministran al computador los datos que debe procesar y reciben los resultados.

Estos bloques funcionales se interconectan a través del **bus del sistema**, conjunto de conductores eléctricos que transmiten:
* las **direcciones** de memoria para acceder a los datos,
* los propios **datos** (instrucciones y valores) y
* las **señales de control**.

![Bus del Sistema](img/AC/bus_sistema.jpg){: style="display: block; margin: 0 auto" }
<center><em>Figura 1.1 - Bloques funcionales de la arquitectura Von Neumann.<br><small>(Fuente: <a href="https://es.wikipedia.org/wiki/Arquitectura_de_Von_Neumann">https://es.wikipedia.org/wiki/Arquitectura_de_Von_Neumann</a>)</small></em></center>

<br>

Las características fundamentales de la **arquitectura Von Neumann** son:
1.	Valores e instrucciones se almacenan en la misma memoria (**programa almacenado**). 
2.	El contenido de la memoria se organiza en **celdas**, que son accesibles (lectura y escritura) proporcionando una **dirección**.
3.	La **ejecución** de los programas se realiza por defecto de forma **secuencial**, una lista consecutiva de **instrucciones** que se ejecutan una tras otra.

!!! note "El *cuello de botella* de Von Neumann"
    Valores e instrucciones comparten el **bus de datos** para ser transferidos a la CPU. Como consecuencia, el procesador no puede acceder simultáneamente a las instrucciones y a los datos, lo que genera una restricción en el rendimiento conocida como el **cuello de botella de Von Neumann**. En la práctica, esto significa que la velocidad del sistema está limitada por el ancho de banda del bus de memoria, que suele ser mucho más lento que la velocidad de procesamiento de la CPU.
### 1.1 Programación cableada frente a programación software
*   **Programa cableado**
Mediante la combinación de componentes lógicos es factible recrear funciones que, a partir de unos datos de entrada, permitan obtener las salidas correspondientes. El proceso de diseño y posterior interconexión de estos componentes para lograr efectuar un cálculo **determinado** es de hecho una forma de programación, es un **programa cableado**.
*   **Programa software**
Para dotar de un **propósito general** a un dispositivo, la alternativa es utilizar una combinación de componentes que implementen diversas **operaciones básicas** lógico/aritméticas. Esto permite ejecutar diferentes funciones según se apliquen diferentes señales de control sobre los datos de entrada.
Se asocia a cada operación básica un **código** y se añade un hardware que, en función del código recibido, genera las señales de control asociadas. Para recrear un cálculo o **algoritmo** determinado, basta determinar la **secuencia de códigos** adecuada. Esta secuencia de códigos o **instrucciones** es el **programa software**.


![Programa Hardware vs Software](img/AC/programa_hard_vs_soft.jpg){: style="display: block; margin: 0 auto" }
<center><em>Figura 1.2 - Programación cableada frente a programación software.<br><small>(Fuente: W. Stallings. Organización y arquitectura de computadores, pág. 59)</small></em></center>
<br>

Las dos cajas mostradas en la figura 1.2.b se corresponden con la **CPU**: bloque funcional formado por el intérprete de instrucciones, la **Unidad de Control** (**CU**), y el módulo de uso general que implementa las funciones aritméticas y lógicas, la **Unidad Aritmético Lógica** (**ALU**).

Faltan dos elementos esenciales para que el sistema software pueda funcionar:
* **Módulo de Entrada/Salida**: los datos e instrucciones deben introducirse en el sistema con algún componente que transforme los formatos de entrada a los formatos que utilice el sistema. Del mismo modo, los resultados deben poder ser accesibles desde el exterior.
* **La memoria principal**: es un componente que en la arquitectura Von Neumann sirve de almacén tanto de las instrucciones como de los datos durante la ejecución del programa. Aunque, a priori, sería factible para cálculos simples proporcionar secuencialmente las instrucciones y datos según se vayan ejecutando (es lo que se hace formalmente con una calculadora de bolsillo), de forma general, un cálculo complejo no siempre ejecutará las instrucciones siguiendo la secuencia predeterminada, pudiendo hacer **saltos** hacia adelante y hacia atrás. Además, durante el proceso pueden generarse operandos intermedios que se utilizarán más adelante y que, por tanto, necesitan ser almacenados temporalmente. 

 

---

## 2. Estructura de un computador: enfoque multinivel


![Enfoque multinivel](img/AC/enfoque_multinivel.jpg){: style="display: block; margin: 0 auto" }
<center><em>Figura 2.1 – Enfoque multinivel de un computador<br><small>(Fuente: A. Tanembaum. Organización de computadoras. Un enfoque estructurado, pág. 5)</small></em></center>
<br>

El enfoque multinivel considera al computador estructurado en niveles.

### 2.1 Nivel 0: Lógica digital
Es el hardware de la máquina, donde encontramos **compuertas lógicas** formadas por transistores y las líneas eléctricas que las conectan. Las compuertas lógicas son circuitos digitales que implementan funciones booleanas, es decir, funciones con entradas y salidas en el conjunto de valores {0, 1}. Ejemplos básicos son las compuertas que implementan las operaciones AND y OR.

**Tablas de verdad**
El funcionamiento de un tipo de compuerta se modela por su **tabla de verdad**: nos muestra la salida de la compuerta para cada combinación de entradas posible. En general, para una función booleana de $n$ entradas tenemos una tabla de $2^n$ filas.


![Compuerta lógica](img/AC/compuerta_logica.jpg){: style="display: block; margin: 0 auto" }
<center><em>Figura 2.2 – Compuerta lógica AND formada por transistores<br><small>(Fuente: <a>https://es.wikipedia.org/wiki/Puerta_lógica)</a></small></em></center>
<br>

### 2.2 Nivel 1: Microarquitectura
Detalla cómo están conectados e interactúan entre sí los dispositivos del nivel 0 y como se organizan formando unidades funcionales. Aquí se decide qué señales de control se utilizarán, las interfaces con los dispositivos de E/S, las tecnologías de memoria utilizadas, etc.

Desde el punto de vista de un programador, la organización **no es visible**.
> Una instrucción de multiplicar puede llevarse a cabo en el nivel de microarquitectura con un circuito integrado (chip) especializado o con un microprograma interno que realiza de forma iterada sumas.


![Microarquitectura](img/AC/microarquitectura.jpg){: style="display: block; margin: 0 auto" }
<center><em>Figura 2.3 - Microarquitectura del Intel 80286<br><small>(Fuente: <a>hhttps://en.wikipedia.org/wiki/Microarchitecture)</a></small></em></center>
<br>

### 2.3 Nivel 2: Arquitectura del Conjunto de instrucciones (ISA)
El acrónimo **ISA**: **I**nstruction **S**et **A**rchitecture es una **especificación** que define el **conjunto** o **repertorio** de todas las **instrucciones** disponibles para una familia de diseños de microarquitecturas compatibles.

Aunque depende de la bibliografía, el conjunto formado por la ISA y la microarquitectura se conoce como la **arquitectura de un computador**. Como es lógico, el diseño del repertorio de instrucciones y la microarquitectura asociada están íntimamente ligados.

### 2.4 Nivel 3: Sistema Operativo
Un **Sistema Operativo** actúa como interfaz entre el usuario y el hardware del computador.
El sistema operativo es un **conjunto de programas** que **interpretan** complejas **instrucciones** que:
* **asignan** y **gestionan** los recursos del computador
* **controlan** los programas de los usuarios y las operaciones de E/S. 

Las instrucciones ISA también son accesibles desde este nivel.

El S.O. **extiende** el repertorio de instrucciones de la ISA con **llamadas al sistema** (**System Calls**). Para un programador de nivel 3, una instrucción para escribir en un archivo es tan *básica* como una suma, aunque por debajo implique miles de operaciones.


![Logos S.O.](img/AC/logos_so.jpg){: style="display: block; margin: 0 auto" }
<center><em>Figura 2.4 – Logos de algunos Sistemas Operativos actuales</em></center>
<br>

### 2.5 Niveles 4 y 5: Lenguajes ensamblador y alto nivel
Ya hemos hablado de ellos en temas anteriores. Los niveles 1 al 3 son utilizados por los **programadores de sistemas**, es decir, los encargados de **diseñar** y/o **implementar** programas tales como **Sistemas Operativos**, **Compiladores**, **Controladores de Dispositivos**, etc.

Los niveles 4 y particularmente el 5 son utilizados por los **programadores de aplicaciones**, tales como procesadores de texto, aplicaciones de contabilidad, páginas web, etc.


---

## 3. Organización y funcionamiento de la CPU

### 3.1 Introducción
Un procesador debe realizar 5 tareas: captar instrucciones, interpretarlas, captar datos, procesar datos y escribir datos.

> **[Figura 3.1 - El procesador (Esquema interno)]**

Componentes básicos:
1.  **Unidad de Control (CU):** Decodifica, secuencia transferencias y controla la ALU.
2.  **Unidad Aritmético Lógica (ALU):** Realiza operaciones aritmético-lógicas.
3.  **Registros:** Almacenamiento temporal interno.
4.  **Buses:** Canales de comunicación interna.

> **[Figura 3.2 – Representación esquemática de la ALU]**

#### Los Registros
*   **Visibles por el usuario:** Permiten minimizar accesos a memoria (generalmente 32 o 64 bits).
*   **De control y de estado:**
    *   **PC (Program Counter):** Dirección de la siguiente instrucción.
    *   **IR (Instruction Register):** Instrucción captada más recientemente.
    *   **PSW (Program Status Word):** Bits indicadores (Signo, Cero, Acarreo, etc.).

#### Los Buses
Agrupación de conductores para intercambio de información. El bus del sistema incluye: bus de direcciones, bus de datos y bus de control.

### 3.2 El ciclo de instrucción
Pasos básicos:
1.  **Captación (fetch):** Se obtiene la instrucción de memoria (usando el PC) y se guarda en el IR. Se incrementa el PC.
2.  **Decodificación (decode):** La UC interpreta el código binario.
3.  **Ejecución (execute):** Se leen operandos, se opera y se almacenan resultados.

> **[Figura 3.3 – El ciclo de instrucción (Diagrama)]**

---

## 4. El repertorio de instrucciones (ISA)
Describe los aspectos del procesador visibles para el programador de sistemas: tipos de formatos, tipos de datos y número de registros.

### 4.1 Tipos de instrucciones
*   **Transformación:** Operaciones sobre datos.
*   **Transferencia:** Copia de datos (Memoria $\leftrightarrow$ Registros, etc.).
*   **Control del flujo:** Saltos en la ejecución.
*   **Control del procesador:** Cambio de modo de funcionamiento.

### 4.2 Codificación y formatos
Un formato de instrucción incluye el **opcode** (operación) y los campos de **direccionamiento** (operandos).

> **[Figura 4.1 – Formato de una instrucción]**

### 4.3 Clasificación de arquitecturas
Según el almacenamiento de operandos:
1.  **Pila:** Operandos implícitos.
2.  **Acumulador:** Un operando es siempre el registro acumulador.
3.  **GPR (Registros de propósito general):**
    *   **Memoria-Registro:** Un operando puede estar en memoria.
    *   **Registro-Registro (RISC):** Operandos solo en registros. Solo `LOAD` y `STORE` acceden a memoria.

> **[Figura 4.2 – Situación de los operandos para cuatro tipos de arquitecturas]**

---

## 5. El rendimiento de un computador
Se define como la capacidad para ejecutar programas en el menor tiempo posible.

### 5.1 El reloj
Sincroniza las operaciones. La frecuencia (Hz) es la referencia de rendimiento.

> **[Figura 5.1 – Oscilador de cristal y generador de reloj]**
> **[Figura 5.2 – Señal de onda rectangular]**

**Fórmula de tiempo de CPU:**
$$\text{Tiempo de CPU} = \text{Número de instrucciones} \times \text{CPI} \times \text{Tiempo de ciclo}$$

### 5.2 Paralelismo: procesadores multinucleo
Varios núcleos en un mismo chip para ejecutar procesos o hilos (threads) concurrentemente.

> **[Figura 5.3 – Frecuencia y Potencia de procesadores Intel x86 (30 años)]**
> **[Figura 5.4 – Sistema de refrigeración de una CPU]**

### 5.3 Segmentación de instrucciones (Pipelining)
Divide la ejecución en etapas (ej. IF, ID, EX, MEM, WB) para procesar varias instrucciones a la vez.

> **[Figura 5.5 – Tiempos de ejecución de las etapas para diferentes tipos de instrucción]**
> **[Figura 5.6 – Comparación de ciclo simple frente a segmentación]**

---

## 6. La memoria
Organizada jerárquicamente para equilibrar coste, capacidad y velocidad.

### 6.1 Tipos de memorias
*   **Volátiles:** SRAM (caché, rápida) y DRAM (memoria principal, lenta pero densa).
*   **No volátiles:** ROM, PROM, EPROM, EEPROM y Memoria Flash.
*   **Secundaria:** Discos duros, SSD, etc.

> **[Figura 6.1 – Tecnología de almacenamiento secundario obsoleta]**

### 6.2 La jerarquía de memoria
Basada en los principios de **localidad temporal** (reuso de datos) y **localidad espacial** (datos cercanos en memoria).

> **[Figura 6.2 – Fragmentos de código con buena/mala localidad espacial]**
> **[Figura 6.3 – La pirámide de la jerarquía de memoria]**
> **[Figura 6.4 – Intercambios de datos entre niveles (palabras, bloques, páginas)]**

### 6.3 La memoria caché
Memoria pequeña y rápida entre la CPU y la RAM.
*   **Conceptos:** Hit (acierto), Miss (fallo), Ancho de banda y Latencia.
*   **Políticas de ubicación:** Directa, Asociativa y Asociativa por conjuntos.

> **[Figura 6.5 – Principio de funcionamiento de una caché]**
> **[Figura 6.6 – Jerarquía caché en un Intel Core i7]**

### 6.4 La arquitectura Harvard
Usa memorias y buses físicamente separados para instrucciones y datos. Ventaja: acceso simultáneo.

> **[Figura 6.7 – Comparativa Von Neumann vs Harvard]**
> **[Figura 6.8 – Arquitectura Harvard en microcontrolador Arduino]**

---

## 7. Interrupciones
Alteración forzada del flujo de ejecución ante un evento. Incluye un número de interrupción (IRQ) y una rutina de servicio (ISR).

> **[Figura 7.1 – Ciclo de instrucción con interrupciones]**

*   **Tipos:** Hardware (asíncronas), Llamadas al sistema (traps) y Excepciones (errores).

---

## 8. Dispositivos de Entrada/Salida

### 8.1 Módulos de E/S
Actúan como interfaz para gestionar la diversidad de periféricos y velocidades.

> **[Figura 8.1 – Diagrama de bloques de un módulo de E/S]**

### 8.2 Buses de E/S
Estándares actuales: **USB** (propósito general), **PCIe** (alta velocidad/tarjetas), **SPI** (baja velocidad/sensores) y **SATA** (almacenamiento).

> **[Figura 8.2 – Componentes de una placa base]**
> **[Figura 8.3 – Diagrama de bloques del chipset Intel Z690]**

### 8.4 Técnicas de sincronización
1.  **Sondeo (Polling):** La CPU consulta periódicamente el estado.
2.  **Interrupción:** El dispositivo avisa a la CPU cuando está listo.

> **[Figura 8.4 – Diagramas de flujo de sondeo continuo y periódico]**
> **[Figura 8.5 – Sincronización mediante interrupciones]**

### 8.5 Transferencia de datos
*   **Por programa:** La CPU mueve los datos uno a uno.
*   **DMA (Direct Memory Access):** Un controlador especializado mueve bloques de datos entre periférico y memoria sin usar la CPU.

> **[Figura 8.6 – Transferencias de datos entre disco y memoria: PIO vs DMA]**

---

## Bibliografía
*(Listado de referencias del documento original)*