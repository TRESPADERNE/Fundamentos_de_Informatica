Aquí tienes el contenido reestructurado y ampliado en formato Markdown. He integrado el texto original de tus diapositivas con las explicaciones adicionales que diseñamos para enriquecer el temario.

He incluido marcadores como `[INSERTAR FIGURA X]` para que sepas dónde colocar tus imágenes originales.

---

# FI_2: Lenguajes de Programación
**Fundamentos de Informática**
*Departamento de Ingeniería de Sistemas y Automática. EII. Universidad de Valladolid*

---

## Índice
1. Introducción a los lenguajes de programación
2. Lenguaje Máquina
3. Lenguaje Ensamblador
4. Lenguajes de Alto Nivel
5. Compiladores (Enfoque C++)
6. Intérpretes y Máquinas Virtuales
7. Compiladores frente a Intérpretes

---

## 1. Introducción a los lenguajes de programación

### Concepto Básico
Los programadores escriben programas utilizando **lenguajes de programación** para que el ordenador ejecute una serie de instrucciones. Estos programas legibles por humanos se denominan **código fuente**.

Por otro lado, el ordenador (el hardware) trabaja internamente usando exclusivamente **código binario**, que resulta ininteligible a primera vista para las personas. El código binario ejecutable de un programa se denomina **código objeto** o **código máquina**.

> **Necesidad de traducción:** Es necesario utilizar programas "traductores" que conviertan el código fuente (alto nivel de abstracción) a código máquina (bajo nivel de abstracción).

### Definición y Componentes
Un Lenguaje de Programación es un conjunto de **símbolos y reglas** con los que expresar órdenes a un ordenador.

1.  **Léxico:** El conjunto de símbolos (palabras, signos de puntuación) que acepta el lenguaje.
2.  **Sintaxis:** Reglas que establecen qué construcciones son aceptables como instrucciones válidas (la "gramática").
3.  **Semántica:** Reglas que establecen el significado o comportamiento de dichas instrucciones.

**Diferencia clave entre Sintaxis y Semántica:**
*   *Ejemplo en lenguaje natural:* La frase "La silla come manzanas" es **sintácticamente correcta** (Sujeto + Verbo + Predicado), pero **semánticamente incorrecta** (carece de sentido lógico).
*   *Ejemplo en programación:* La instrucción `int resultado = "hola";` puede ser sintácticamente válida en la estructura de asignación, pero semánticamente errónea porque intentamos guardar texto en una variable numérica.

### Comparativa: Lenguaje Natural vs. Programación

| Característica | Lenguaje Natural (Humano) | Lenguaje de Programación |
| :--- | :--- | :--- |
| **Léxico** | Palabras y signos de puntuación. | Símbolos reservados del lenguaje (keywords, operadores). |
| **Sintaxis** | Oraciones gramaticalmente correctas. | Instrucciones bien formadas y válidas. |
| **Semántica** | Información o mensaje que transmite quien habla. | Qué acciones exactas debe ejecutar el hardware. |
| **Ambigüedad** | Alta (depende del contexto). | Nula (una instrucción debe tener una única interpretación). |

---

## 2. Niveles de los Lenguajes

Básicamente se pueden establecer tres niveles de abstracción:
1.  **Lenguaje máquina** (Bajo nivel)
2.  **Lenguaje ensamblador** (Bajo nivel)
3.  **Lenguajes de Alto nivel**

### Lenguaje Máquina
Es el lenguaje directamente comprensible por el procesador (CPU).
*   Consta de un **conjunto predefinido de instrucciones** y un sistema de codificación binaria (secuencias de 1's y 0's).
*   **Dependencia del Hardware:** Depende totalmente de la arquitectura. Es definido por el conjunto de instrucciones (**ISA**, *Instruction Set Architecture*) que soporta un procesador.
*   **Incompatibilidad:** Un código máquina para una CPU ARM (móvil) es incomprensible para una CPU Intel Core i7 (PC).
*   **Gestión:** A este nivel, el control de la memoria es manual y absoluto; no existen las "variables", solo direcciones de memoria física.

---

## 3. Lenguaje Ensamblador

Emplea palabras nemotécnicas (abreviaturas) para hacer referencia a las instrucciones del lenguaje de máquina, haciéndolo ligeramente más legible para el humano.

`[INSERTAR FIGURA: Tabla comparativa código máquina vs ensamblador]`

**Relación 1 a 1:**
Existe una correspondencia casi directa entre una instrucción de ensamblador y una instrucción de máquina.
*   *Ejemplo x86:* `MOV AL, 61h` (Mover el valor hexadecimal 61 al registro AL).
    *   Código máquina equivalente: `10110000 01100001`
*   El programa fuente en ensamblador debe ser traducido por un programa llamado **Ensamblador**.
*   Sigue siendo dependiente de la arquitectura (cada familia de CPU tiene su propio ensamblador).

---

## 4. Lenguajes de Alto Nivel

Estos lenguajes buscan acercarse a la forma de pensar humana y alejarse del detalle del hardware.

*   **Abstracción:** Definen su sintaxis y estructuras al margen del procesador. Son **portables** (a priori).
*   **Potencia:** Una sola sentencia de alto nivel genera muchas instrucciones de código máquina.
*   **Legibilidad:** Usan palabras en inglés (`if`, `while`, `print`) y expresiones matemáticas estándar.
*   **Tipado:**
    *   *Estático (C++, Java):* Tipos de datos definidos antes de compilar. Más seguro.
    *   *Dinámico (Python, JS):* Tipos deducidos durante la ejecución. Más flexible.

### Paradigmas de programación
Un paradigma describe la forma de estructurar y razonar sobre los cálculos.

1.  **Imperativo:** Describe **cómo** realizar los cálculos paso a paso, modificando el estado del programa. (Ej. C, Pascal).
2.  **Declarativo:** Describe **qué** cálculos deben realizarse, sin detallar el flujo de control explícito. (Ej. SQL, HTML).
3.  **Orientado a Objetos (POO):** Organiza el código en "clases" que encapsulan datos y comportamiento. (Ej. Java, C++, Python).
4.  **Funcional:** Trata la computación como la evaluación de funciones matemáticas y evita cambiar estados o datos mutables. (Ej. Haskell, Lisp).

`[INSERTAR FIGURA: Nube de palabras de lenguajes o gráfico de popularidad TIOBE/RedMonk]`

---

## 5. Compiladores (El modelo C/C++)

Un **compilador** es un programa que traduce todo el código fuente de una sola vez a un programa equivalente en otro lenguaje (normalmente código máquina) para su posterior ejecución.

> **Nota:** El compilador detecta errores en tiempo de compilación (sintaxis), pero no errores en tiempo de ejecución (lógica).

### Proceso de compilación en C++
1.  **Edición:** Se escribe el código fuente (`.cpp`, `.h`).
2.  **Preprocesamiento:** Antes de compilar, el **preprocesador** gestiona directivas (comenzadas por `#` como `#include`), expande macros y elimina comentarios.
3.  **Compilación:** Traduce el código preprocesado a **código objeto** (`.o` o `.obj`). Este código es binario pero aún no es ejecutable por sí mismo porque le faltan referencias.
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

## 6. Intérpretes y Máquinas Virtuales

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

## 7. Compiladores frente a Intérpretes (Resumen)

### Compilador nativo (Estilo C/C++)
*   **Proceso:** Fuente $\to$ Compilador $\to$ Código Máquina (Ejecutable).
*   **Distribución:** Debes recompilar y generar un ejecutable diferente para cada sistema operativo (uno para Windows, otro para Linux, etc.).
*   **Rendimiento:** Máximo (acceso directo al hardware).

### Intérprete con Máquina Virtual (Estilo Java/Python)
*   **Proceso:** Fuente $\to$ Compilador $\to$ Bytecode $\to$ VM (Ejecución).
*   **Distribución:** Distribuyes un único archivo de Bytecode.
*   **Ejecución:** Requiere que el usuario tenga instalada la Máquina Virtual específica para su sistema operativo.

`[INSERTAR FIGURA: Esquema árbol Compilación vs VM]`

### Bibliografía y Referencias
*   M. Franklin. *Computer Architecture and Organization. From Software to Hardware.* Pearson 2007.
*   Documentación oficial de C++ (cppreference.com) y Python (docs.python.org).
*   TIOBE Index & IEEE Spectrum (Rankings de lenguajes).