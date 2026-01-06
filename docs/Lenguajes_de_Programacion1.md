

# FI_2: Lenguajes de Programación
**Fundamentos de Informática**
*Departamento de Ingeniería de Sistemas y Automática. EII. Universidad de Valladolid*

---

## Índice
1. [Introducción a los lenguajes de programación](#1-introduccion-a-los-lenguajes-de-programacion)
2. [Clasificación](#2-clasificacion-niveles)
3. [Compiladores (Enfoque C++)](#3-compiladores-el-modelo-cc)
4. [Intérpretes y Máquinas Virtuales](#4-interpretes-y-maquinas-virtuales)
5. [Compiladores frente a Intérpretes](#5-compiladores-frente-a-interpretes-resumen)
6. [Ecosistema de Desarrollo (IDEs)](#6-ecosistema-de-desarrollo-ides)
7. [Futuro de la Programación](#7-futuro-de-la-programacion)

---

## 1. Introducción a los lenguajes de programación

### Concepto Básico
Los programadores escriben programas utilizando **lenguajes de programación** para que el ordenador ejecute una serie de instrucciones. Estos programas legibles por humanos se denominan **código fuente**.

Por otro lado, el ordenador (el hardware) trabaja internamente usando exclusivamente **código binario** (secuencias de 0s y 1s que representan estados físicos de voltaje), un formato que resulta ininteligible a primera vista para las personas. El código binario ejecutable de un programa se denomina **código objeto** o **código máquina**.

Por tanto, se deduce la necesidad de utilizar programas *traductores* que conviertan el código fuente (alto nivel de abstracción) a código máquina (bajo nivel de abstracción).

### Definición y Componentes
Un Lenguaje de Programación es un conjunto de **símbolos y reglas** con los que expresar órdenes a un ordenador.

1.  **Léxico:** El conjunto de símbolos (palabras, signos de puntuación) que acepta el lenguaje.
2.  **Sintaxis:** Reglas que establecen qué construcciones son aceptables como instrucciones válidas (la *gramática*).
3.  **Semántica:** Reglas que establecen el significado o comportamiento de dichas instrucciones.

**Diferencia clave entre Sintaxis y Semántica:**
*   *Ejemplo en lenguaje natural:* La frase **"La silla come manzanas"* es **sintácticamente correcta** (Sujeto + Verbo + Predicado), pero **semánticamente incorrecta** (carece de sentido lógico).
*   *Ejemplo en programación (Python):* La insltrucción `resultado = "Hola" / 2` es **sintácticamente correcta** (estructura válida: variable = valor / valor), pero **semánticamente errónea** (no tiene sentido lógico ni matemático dividir un texto (`"Hola"`) entre un número (`2`).

### Comparativa: Lenguaje Natural vs. Programación

| Característica | Lenguaje Natural (Humano) | Lenguaje de Programación |
| :--- | :--- | :--- |
| **Léxico** | Palabras y signos de puntuación. | Símbolos reservados del lenguaje (palabras clave, operadores). |
| **Sintaxis** | Oraciones gramaticalmente correctas. | Instrucciones bien formadas y válidas. |
| **Semántica** | Información o mensaje que transmite quien habla. | Qué acciones exactas debe ejecutar el hardware. |
| **Ambigüedad** | Alta (depende del contexto). | Nula (una instrucción debe tener una única interpretación). |

---

## 2. Clasificación: Niveles

### 2.1 Niveles de Abstracción

El concepto de **abstracción** en informática se refiere a la capacidad de ocultar la complejidad interna del hardware para facilitar la programación. Cuanto mayor es el nivel de abstracción de un lenguaje, más nos alejamos de los detalles físicos de la máquina (transistores, registros, direcciones de memoria) para centrarnos en la lógica del problema a resolver (fórmulas, objetos, datos).

Básicamente se pueden establecer tres niveles de abstracción:
1.  **Lenguaje máquina** (Bajo nivel)
2.  **Lenguaje ensamblador** (Bajo nivel)
3.  **Lenguajes de Alto nivel**


#### Lenguaje Máquina
Es el lenguaje directamente comprensible por el procesador (CPU). En el tema de **Arquitectura** estudiaremos cómo la CPU procesa estas órdenes; por ahora basta entender que es el componente hardware encargado de leer secuencialmente *unos y ceros* y actuar en consecuencia (sumar, guardar datos, etc.).

*   Utiliza un sistema de codificación binaria (secuencias de 1's y 0's) para definir un **conjunto predefinido de instrucciones**, (**ISA**, *Instruction Set Architecture*).
    > Una **instrucción** es la operación más elemental que el hardware puede realizar indivisiblemente, como *sumar dos valores*, *mover un dato de memoria al procesador*, etc.
*   Depende totalmente de la arquitectura: un código máquina para una CPU ARM (móvil) es incomprensible para una CPU Intel Core i7 (PC).
*   **Gestión:** A este nivel, el control de la **memoria** es manual y absoluto.
    > La memoria es el *casillero* gigante de celdas numeradas donde se almacenan los datos y el programa en ejecución. En código máquina no existen las *variables* con nombres (como `edad`), sino que el programador debe referirse a los datos por su **dirección física** (el número exacto de la celda, ej: `0x0045A`).


#### Lenguaje Ensamblador

Emplea palabras nemotécnicas (abreviaturas) para hacer referencia a las instrucciones del lenguaje de máquina, haciéndolo ligeramente más legible para el humano.

**Ejemplo de traducción y estructura (Familia x86/IA-32):**

| Lenguaje de máquina | Ensamblador |
| :--- | :--- |
| `10110000 01100001` | `MOV AL, 61h` |

En este ejemplo, la instrucción binaria se compone de 3 partes que el hardware decodifica:
1.  **Código de operación (5 primeros bits):** La secuencia `10110` ordena **mover** (*MOV*) un dato a un registro.
    > *Nota:* Un **registro** es una posición de memoria ultrarrápida situada *dentro* de la propia CPU.
2.  **Registro destino (3 siguientes bits):** El código `000` corresponde al registro interno denominado **AL**.
3.  **Dato (8 bits finales):** La secuencia `01100001` es el valor del dato (97 en decimal, 61 en hexadecimal).

El lenguaje ensamblador permite escribir `MOV AL, 61h` en lugar de la cadena de bits, resultando mucho más inteligible.

**Proceso de Traducción:**
El programa escrito en lenguaje ensamblador (**Programa Fuente**) debe ser traducido a lenguaje de máquina (**Programa Objeto**), ya que el procesador solo entiende 0s y 1s. Esta tarea la realiza una herramienta llamada **Ensamblador**.

`[Programa Fuente] --> [Ensamblador] --> [Programa Objeto]`

**Características clave:**
*   **Traducción directa:** Generalmente existe una correspondencia 1 a 1 entre instrucción ensamblador y máquina.
*   **Dependencia:** ¡Cada familia de CPU's tiene su propio lenguaje ensamblador!


#### Lenguajes de Alto Nivel

Estos lenguajes buscan acercarse a la forma de pensar humana y alejarse del detalle del hardware.

*   **Independencia y Portabilidad:** Definen su sintaxis y sus estructuras al margen del procesador que se utilice. Un mismo código fuente puede ejecutarse en diferentes máquinas (es **portable**), siempre que se traduzca adecuadamente.
*   **Correspondencia Compleja (1 a N):** A diferencia del ensamblador (1 a 1), una sola sentencia de alto nivel genera múltiples instrucciones de código máquina.
*   **Legibilidad y Edición:** Se escriben como **texto plano** (usando palabras en inglés como `if`, `while`) y permiten el uso de **comentarios** para explicar el código a otros humanos.
*   **Necesidad de Traducción:** Para poder ejecutarse, necesitan ser traducidos al lenguaje del procesador mediante **Compiladores** o **Intérpretes**.
*   **Tipado:**
    *   *Estático (C++, Java):* El tipo de dato debe definirse explícitamente antes de compilar.
        > Ejemplo: `int x = 3;` (El programador obliga a que `x` sea un número entero).
    *   *Dinámico (Python, JS):* El tipo se deduce automáticamente durante la ejecución.
        > Ejemplo: `x = 3` (Python infiere que `x` es un entero por el valor asignado, sin necesidad de declararlo).

##### Ejemplo Comparativo: "Hola Mundo"
Para visualizar la diferencia de abstracción, veamos cómo se imprime un mensaje en pantalla en distintos niveles:

| Nivel | Código Ejemplo |
| :--- | :--- |
| **Lenguaje Máquina** | `B8 21 0A 00 00 ...` (Secuencia binaria/hexadecimal ininteligible) |
| **Ensamblador (x86)** | `MOV EDX, len`<br>`MOV ECX, msg`<br>`MOV EBX, 1`<br>`MOV EAX, 4`<br>`INT 0x80` |
| **C++ (Alto Nivel)** | `std::cout << "Hola Mundo";` |
| **Python (Muy Alto Nivel)** | `print("Hola Mundo")` |

### Paradigmas de programación
Un paradigma de programación describe una forma de realizar los cálculos y la manera en que se deben estructurar y organizar las tareas que debe llevar a cabo un programa.

*   Los lenguajes de programación suelen implementar, a menudo de forma parcial, **varios paradigmas**.
*   Entre los diferentes tipos de paradigmas, una división básica es dividirlos en **imperativos** (se detalla *cómo* se realizan los cálculos) y **declarativos** (se indica *qué* cálculos deben realizarse).
*   Otros paradigmas se centran en la estructura y organización: programación **estructurada**, **modular**, **orientada a objetos**, genérica, orientada a eventos, concurrente...

> **Nota:** La mejor forma de entender un paradigma es aprender un lenguaje de programación que implemente ese paradigma, por lo que no entraremos por el momento en más detalles.

<p align="center">
  <img src="img/paradigmas.jpg" alt="Paradigmas de Programación">
  <br>
  <em>Clasificación de los paradigmas de programación.</em>
</p>

---

### La *jungla* de los lenguajes

A menudo, el panorama actual se percibe como una ***jungla* de lenguajes**.
*   Existen miles de lenguajes (se estima que hay más de 9.000 creados históricamente).
*   Para un alumno novel, enfrentarse a esta imagen provoca la parálisis de la elección: *¿Por cuál empiezo? ¿Cuál es el *mejor*?*
*   **La realidad:** No todos tienen la misma importancia. Muchos son académicos, otros están obsoletos (como el latín) y otros son de nicho muy específico.

En esa jungla encontraréis herramientas para todo. Python es una navaja suiza (sirve para casi todo, fácil de llevar), C++ es un bisturí láser industrial (muy potente, pero si no sabes usarlo te cortas un brazo), y otros son simplemente juguetes.



<p align="center">
  <img src="img/nube_lenguajes.jpg" alt="Nube de lenguajes">
  <br>
  <em>La jungla de lenguajes de programación.</em>
</p>

<p align="center">
  <img src="img/startcoding.jpg" alt="¿Qué lenguaje aprender primero?">
  <br>
  <em>¿Qué lenguaje aprender en primer lugar?</em>
</p>

<p align="center">
  <img src="img/redmonk.png" alt="Ranking Redmonk">
  <br>
  <em>Ranking Redmonk</em>

</p>

<p align="center">
  <img src="img/tiobe.jpg" alt="Ranking TIOBE">
  <br>
  <em>Ranking TIOBE</em>
</p>

### ¿Por qué Python como primer lenguaje en Ingeniería?

Dado que nuestra asignatura se orienta a titulaciones de ingeniería (Biomédica, Electrónica, Mecánica, Química...), la elección de Python como primer lenguaje no es arbitraria y se justifica por varios motivos técnicos y prácticos frente a opciones clásicas como C o C++:

1.  **Foco en la resolución del problema:** En ingeniería, la programación es una herramienta para resolver problemas (filtrar una señal fisiológica, simular una estructura mecánica, analizar datos químicos), no un fin en sí mismo. La sintaxis de Python es limpia y legible (cercana al pseudocódigo), lo que reduce la **carga cognitiva**: el alumno dedica su esfuerzo mental a entender el algoritmo, no a pelear con llaves, puntos y comas o gestión de memoria manual.

2.  **El estándar en Ciencia de Datos e IA:** Python posee el ecosistema de librerías científicas más robusto del mundo.
    *   **Biomédica:** Procesamiento de imágenes (*OpenCV*), señales médicas (*SciPy, MNE*).
    *   **Mecánica/Química:** Análisis de datos experimentales (*Pandas*), simulación numérica (*NumPy*).
    *   **Electrónica:** Control de instrumentos y automatización.

3.  **Productividad:** Un programa en Python suele requerir entre 3 y 5 veces menos líneas de código que su equivalente en C++ o Java. Esto permite prototipar soluciones funcionales en mucho menos tiempo.

4.  **Multiparadigma:** Permite empezar programando de forma imperativa (sencilla) y avanzar hacia la orientación a objetos o funcional progresivamente, sin imponer una estructura rígida desde la línea 1.

---

## 3. Compiladores (El modelo C/C++)

Un **compilador** es un programa que traduce todo el código fuente de una sola vez a un programa equivalente en otro lenguaje (normalmente código máquina) para su posterior ejecución.

> **Nota:** El compilador detecta errores en tiempo de compilación (sintaxis), pero no errores en tiempo de ejecución (lógica).

### Proceso de compilación en C++
1.  **Edición:** Se escribe el código fuente: las extensiones de los archivos típicos son `.cpp` y `.h`.
2.  **Preprocesamiento:** Es una fase previa de *preparación* del texto. El preprocesador limpia el código eliminando las notas del autor (comentarios) e incrusta el contenido de ficheros externos necesarios (como si hiciera un *copiar y pegar* automático de las bibliotecas), dejando el código listo para traducir.
3.  **Compilación:** Traduce el código preprocesado a **código objeto** (`.o` o `.obj`). Este código es binario pero aún no es ejecutable por sí mismo porque le faltan las conexiones con el resto del proyecto.
    > Un programa suele dividirse en **muchos archivos fuente**. En esta fase, cada archivo se traduce por separado, pero si uno necesita usar una función que está escrita en *otro* archivo, todavía no *sabe* dónde encontrarla. Esas *referencias* cruzadas están pendientes de resolver.
4.  **Enlazado (Linker):** Une todos los archivos objeto del programador con las **bibliotecas externas** (ej. funciones matemáticas) para crear un único fichero **ejecutable** binario (`.exe`).

`[INSERTAR FIGURA: Diagrama de flujo Preprocesador -> Compilador -> Enlazador]`

### Etapas internas del compilador
El compilador realiza la traducción típicamente en 2 grandes fases:

1.  **Fase de Análisis (Front-end):**
    *   **Léxico:** Verifica símbolos válidos.
    *   **Sintáctico:** Verifica la estructura gramatical.
    *   **Semántico:** Verifica la coherencia de tipos y significado.
2.  **Fase de Síntesis (Back-end):**
    *   Generación de código intermedio.
    *   **Optimización:** Fase crítica donde el compilador mejora el código (elimina código muerto, desenrolla bucles) para reducir tamaño o aumentar velocidad.
    *   Generación de código máquina específico para la arquitectura.

---

## 4. Intérpretes y Máquinas Virtuales

### Intérprete Puro
A diferencia del compilador, el **intérprete** lee, traduce y ejecuta el código fuente línea a línea (o bloque a bloque) en tiempo real.
*   No genera un ejecutable independiente.
*   **Ventaja:** Flexibilidad, depuración rápida, tipado dinámico.
*   **Desventaja:** Menor velocidad de ejecución (se traduce cada vez que se ejecuta).

### Modelo Híbrido: Máquinas Virtuales
Muchos lenguajes modernos (Java, Python, C#) utilizan un esquema intermedio.
1.  El código fuente se compila a un **Código Intermedio** o **Bytecode** (ej. `.class` en Java, `.pyc` en Python). Este código es universal y no depende de la CPU.
2.  Una **Máquina Virtual (VM)** instalada en el ordenador del usuario interpreta ese Bytecode y lo traduce a código máquina nativo.

`[INSERTAR FIGURA: Comparativa flujo Compilador vs Intérprete]`

**Ventajas de la Máquina Virtual:**
*   **Portabilidad (WORA):** "Write Once, Run Anywhere". El mismo bytecode corre en Windows, Linux o Mac, siempre que exista la VM correspondiente.
*   **Seguridad:** La VM actúa como una caja de arena (*sandbox*), aislando el código del hardware real.
*   **Gestión de Memoria:** La mayoría de VMs incluyen un **Recolector de Basura (Garbage Collector)** que libera memoria automáticamente, evitando fugas de memoria comunes en C++.

**Compilación JIT (Just-In-Time):**
Para mejorar el rendimiento, las VMs modernas (como la JVM de Java o V8 de JS) compilan trozos de bytecode a código nativo *mientras* el programa se ejecuta, combinando la velocidad de un compilado con la flexibilidad de un interpretado.

**Ejemplos:**
*   **Java:** Usa la JVM (Java Virtual Machine).
*   **Python:** Usa la PVM.
*   **.NET (C#):** Compila a CIL (Common Intermediate Language) y lo ejecuta el CLR (Common Language Runtime).

---

## 5. Compiladores frente a Intérpretes (Resumen)

A continuación, comparamos los enfoques principales: **Compilación Pura** (C++), **Interpretación Pura** (versiones antiguas de BASIC, Scripts de Shell) y **Enfoque Híbrido/VM** (Java, Python).

| Característica | Compilador Nativo (C++) | Intérprete Puro | Máquina Virtual (Java/Python) |
| :--- | :--- | :--- | :--- |
| **Proceso** | Fuente $\to$ Máquina (Ejecutable) | Fuente $\to$ Ejecución directa | Fuente $\to$ Bytecode $\to$ VM |
| **Cuándo se traduce** | Antes de ejecutar (tiempo de compilación). | Durante la ejecución (tiempo real). | Mixto (pre-compilación a bytecode + JIT). |
| **Rendimiento** | **Muy Alto.** Optimizado para el hardware específico. | **Bajo.** Sobrecarga por traducción constante. | **Medio/Alto.** Gracias a tecnologías JIT. |
| **Privacidad Código** | Alta (se entrega binario difícil de leer). | Nula (se entrega código fuente visible). | Media (se entrega bytecode, que es reversible). |
| **Portabilidad** | Baja. Requiere recompilar para cada SO. | Alta. Solo requiere el intérprete instalado. | **Muy Alta (WORA).** Bytecode universal. |
| **Detección Errores** | Todos los de sintaxis reportados antes de correr. | El programa se detiene al encontrar el primer error. | Errores de sintaxis al generar bytecode; lógica en ejecución. |

`[INSERTAR FIGURA: Esquema árbol Compilación vs VM]`

---

## 6. Ecosistema de Desarrollo (IDEs)

Programar en un simple editor de texto (como el Bloc de Notas) es posible, pero ineficiente. Los profesionales usan **IDEs (Integrated Development Environment)**, que combinan múltiples herramientas en una sola interfaz:

1.  **Editor de código:** Con resaltado de sintaxis y autocompletado automatizado.
2.  **Compilador/Intérprete integrado:** Para ejecutar el programa con un solo clic.
3.  **Depurador (Debugger):** Herramienta vital que permite detener la ejecución paso a paso para inspeccionar variables y encontrar errores lógicos.
4.  **Gestión de proyectos:** Organización de ficheros y control de versiones (Git).

*Ejemplos populares:* Visual Studio Code (ligero y multipropósito), Eclipse/IntelliJ (Java), Visual Studio (C++/C#), PyCharm (Python).

---

## 7. Futuro de la Programación

La forma en que programamos está en constante evolución:
*   **Asistentes de IA:** Herramientas como GitHub Copilot generan código automáticamente a partir de descripciones en lenguaje natural, cambiando el rol del programador de "escritor" a "supervisor".
*   **Low-Code / No-Code:** Plataformas visuales para crear aplicaciones sin escribir código manual, democratizando el desarrollo.
*   **Computación Cuántica:** Nuevos paradigmas y lenguajes (como Q# de Microsoft) diseñados para operar con qubits, resolviendo problemas inabordables para la informática clásica.

---

### Bibliografía y Referencias
*   M. Franklin. *Computer Architecture and Organization. From Software to Hardware.* Pearson 2007.
*   Documentación oficial de C++ (cppreference.com) y Python (docs.python.org).
*   TIOBE Index & IEEE Spectrum (Rankings de lenguajes).