# Representación de la Información

## Índice
1. [Fundamentos de la Información Digital](#1-fundamentos-de-la-información-digital)
2. [Sistemas de Numeración](#2-sistemas-de-numeración)
3. [Representación de Números Enteros](#3-representación-de-números-enteros)
4. [Representación de Números Reales (Coma Flotante)](#4-representación-de-números-reales-coma-flotante)
5. [Representación de Caracteres](#5-representación-de-caracteres)
6. [Aritmética Binaria (Ampliación)](#6-aritmética-binaria-ampliación)
7. [Bibliografía Recomendada](#bibliografía-recomendada)

---

## 1. Fundamentos de la Información Digital

### Naturaleza de la Información Digital
Desde una perspectiva técnica, la **información** se define como todo aquello capaz de reducir la incertidumbre o aportar conocimiento. En un sistema informático, esta información se materializa en forma de datos procesables.

En la arquitectura moderna de computadores (modelo **Von Neumann**), es fundamental comprender que la memoria principal almacena indistintamente dos categorías de entidades:

1.  **Instrucciones (Código):** La secuencia lógica de órdenes que dictan el comportamiento del procesador.
2.  **Datos:** La materia prima (números, caracteres, señales) sobre la que operan dichas instrucciones.

A bajo nivel, no existe diferencia física entre instrucciones y datos; ambos se representan universalmente mediante **patrones de bits** ($0$ y $1$), que en última instancia corresponden a estados físicos del hardware (niveles de voltaje, cargas eléctricas, magnetización...). Es el contexto de ejecución (cómo y cuándo accede el procesador a ellos) lo que determina su interpretación.

### Almacenamiento en el Ordenador: La Memoria
La memoria principal del ordenador se estructura como una **gran tabla lineal de celdas**. Cada celda es un espacio de almacenamiento direccionable individualmente.

En este esquema distinguimos dos conceptos clave:

1.  **Dirección (Address):** El número único que identifica la ubicación de la celda (como el número de un buzón).
2.  **Contenido:** El patrón de bits guardado en dicha celda.

#### Unidades de Medida
*   **Bit** (**Binary digit**): Unidad mínima de información ($0$ o $1$).
*   **Byte** (**Octeto**): Agrupación de **8 bits**. Es la **unidad mínima direccionable** de la memoria; el procesador lee o escribe bytes completos.



#### Visualización de la Memoria
Podemos imaginar la memoria como una tabla donde cada fila representa una celda y contiene un Byte:

| Contenido (Binario) | Interpretación Posible |
| :---: | :--- |
| `01000001` | Letra 'A' |
| `00010100` | Entero 20 |
| `11100011` | Instrucción CPU |

Esta naturaleza binaria se mantiene porque es la solución tecnológica más robusta: es más sencillo y seguro para un circuito distinguir entre dos estados extremos (On/Off) que intentar diferenciar 10 niveles de voltaje precisos para una supuesta aplicación de codificación adaptada al sistema decimal.

### Necesidad de la Codificación
Los humanos interactuamos con información simbólica (letras, números) o analógica (imágenes, sonido), mientras que el procesador trabaja internamente con estados binarios. Para salvar esta brecha es necesaria una transformación rigurosa:

$$ \text{Mundo Real} \xrightarrow{\text{Codificación}} \text{Mundo Digital} $$

Matemáticamente, la codificación debe ser una **transformación inyectiva**.
Esto significa que a cada elemento del conjunto original (ej. la letra 'A') le debe corresponder una secuencia de bits **única y exclusiva**. Si dos elementos distintos compartieran el mismo código, el proceso inverso (**decodificación**) sería ambiguo y no podríamos recuperar la información original sin errores.

#### Capacidad de Representación (Combinatoria)
Es un error común pensar que los bits suman capacidad linealmente. En realidad, la capacidad de diferenciar valores crece de forma **exponencial**: cada bit añadido **duplica** las posibilidades del anterior.

**Regla General:** Con $n$ bits podemos representar $m = 2^n$ valores diferentes.

| Nº Bits | Cálculo ($2^n$) | Cantidad de Valores | Ejemplo de uso |
| :---: | :---: | :---: | :--- |
| **1** | $2^1$ | **2** | Bombilla (Encendida/Apagada) |
| **2** | $2^2$ | **4** | Los 4 palos de la baraja |
| **3** | $2^3$ | **8** | Rosa de los Vientos (N, S, E, O ,NO, NE, SO, etc.) |
| ... | ... | ... | ... |
| **8** | $2^8$ | **256** | **1 Byte** (Podemos representar caracteres) |
| **10** | $2^{10}$ | **1.024** | Aprox. 1000 ($1K$ en Binario) |
| **32** | $2^{32}$ | **~4.000 Millones** | Direcciones IP (Internet) |


**Problema inverso:** Si necesito codificar $m$ valores, ¿cuál es el número mínimo $n$ de bits necesarios?

$$ n = \lceil \log_2 m \rceil \quad \longrightarrow \quad \text{Tomamos el entero más próximo por exceso} $$

!!! example "Ejemplo de cálculo de bits"
    Tenemos un almacén con **17524** contenedores y queremos identificarlos con una etiqueta binaria única.

    $$ \log_2 17524 \approx 14.097 $$
    
    **Solución:** Necesitamos **15 bits** (con 14 bits solo llegaríamos a 16.384 etiquetas).


## 2. Sistemas de Numeración

Antes de abordar cómo se almacenan en un sistema informático tipos de datos específicos (enteros, reales, texto), es imprescindible revisar la base matemática que lo sustenta. Aunque en la vida cotidiana operamos en base 10, el hardware impone el uso de bases potencias de 2.

El objetivo de este apartado no es convertirse en calculadoras humanas, sino entender la **lógica de traducción** entre el mundo humano y el de la máquina. Este conocimiento es vital para interpretar direcciones de memoria, entender los límites de capacidad de las variables o comprender cómo se representa internamente cualquier tipo de dato.

### Definición
Un sistema de numeración es una colección de símbolos y reglas para construir números válidos. Los sistemas usados en informática son **posicionales**: el valor de una cifra depende de su símbolo y de la posición que ocupa.

### Sistemas usuales en informática

| Sistema | Base ($b$) | Símbolos |
| :--- | :--- | :--- |
| **Decimal** | 10 | $\{0, 1, 2, 3, 4, 5, 6, 7, 8, 9\}$ |
| **Binario** | 2 | $\{0, 1\}$ |
| **Octal** | 8 ($2^3$) | $\{0, 1, 2, 3, 4, 5, 6, 7\}$ |
| **Hexadecimal** | 16 ($2^4$) | $\{0, ..., 9, A, B, C, D, E, F\}$ |

### Valor Posicional (Polinomio Equivalente)
El concepto fundamental de los sistemas numéricos modernos es el **valor posicional**. A diferencia de los números romanos, aquí el valor de cada dígito no es absoluto, sino que depende de la posición que ocupe respecto a la coma (o punto) decimal.

Cada posición $i$ tiene un **peso** asignado que es una potencia de la base ($b^i$):

*   Hacia la **izquierda** (parte entera), los pesos son potencias no negativas: $b^0$ (unidades), $b^1$, $b^2$...
*   Hacia la **derecha** (parte fraccionaria), los pesos son potencias negativas: $b^{-1}$, $b^{-2}$...

Para traducir cualquier número a nuestro sistema decimal, simplemente sumamos cada dígito multiplicado por su peso. Esto se formaliza mediante el **polinomio equivalente**:

$$ N = \sum_{i=-k}^{n-1} d_i \cdot b^i $$

$$ N = d_{n-1}b^{n-1} + \dots + d_1 b^1 + d_0 b^0 + d_{-1} b^{-1} + \dots + d_{-k} b^{-k} $$

donde:

*   $d_i$: Es el dígito en la posición $i$.
*   $b$: Es la base del sistema (2, 8, 16...).
*   $i$: Es el índice de la posición ($i=0$ es la primera posición entera).


!!! example Ejemplo: Hexadecimal a Decimal
    Valor del número $3F.D_{16}$:
    $$ 3 \cdot 16^1 + 15 \cdot 16^0 + 13 \cdot 16^{-1} = 48 + 15 + 0.8125 = 63.8125_{10} $$
    *(Nota: F=15, D=13)*

### Conversión de Decimal a Base $b$

Para convertir un número de nuestro sistema decimal a cualquier otra base (binario, octal, hexadecimal...), debemos procesar por separado la parte entera y la fraccionaria, ya que responden a lógicas matemáticas inversas.

El método general consiste en dividir la parte entera y multiplicar la parte fraccionaria.

#### 1. Parte Entera: Divisiones Sucesivas
El algoritmo consiste en **dividir sucesivamente** el número decimal entre la base destino ($b$) hasta que el cociente sea 0.

*   En cada paso, el **resto** de la división se convierte en un dígito del número convertido.
*   **Importante:** El primer resto obtenido corresponde al bit menos significativo (LSD o posición $b^0$). Por tanto, el número final se construye leyendo los restos en **orden inverso** (del último obtenido al primero).

#### 2. Parte Fraccionaria: Multiplicaciones Sucesivas
Tomamos la parte decimal pura (0.xxxx) y la **multiplicamos** por la base destino ($b$).

*   La **parte entera** del resultado será el siguiente dígito fraccionario (empezando por $b^{-1}$).
*   El proceso se repite tomando solo la parte decimal restante del resultado anterior.
*   En este caso, los dígitos se leen en **orden directo** (en el orden en que aparecen).

!!! example Ejemplo Completo: 35.625 a Binario
    **Paso 1: Parte Entera (35)**

    *   $35 / 2 = 17$, Resto **1** (Este es el último bit, LSB)
    *   $17 / 2 = 8$, Resto **1**
    *   $8 / 2 = 4$, Resto **0**
    *   $4 / 2 = 2$, Resto **0**
    *   $2 / 2 = 1$, Resto **0**
    *   $1 / 2 = 0$, Resto **1** (Este es el primer bit, MSB)
    
    $\rightarrow$ Leemos de abajo hacia arriba: **$100011_2$**

    **Paso 2: Parte Fraccionaria (0.625)**

    *   $0.625 \times 2 = \mathbf{1}.25 \rightarrow$ Guardo el **1**, me quedo con $0.25$
    *   $0.25 \times 2 = \mathbf{0}.5 \rightarrow$ Guardo el **0**, me quedo con $0.5$
    *   $0.5 \times 2 = \mathbf{1}.0 \rightarrow$ Guardo el **1**, me queda $0.0$ (Fin)
    
    $\rightarrow$ Leemos de arriba hacia abajo: **$.101_2$**

    **Resultado Final:** $35.625_{10} = 100011.101_2$

#### Error de Truncamiento y Precisión Finita
En la parte fraccionaria, la conversión a menudo no es exacta, resultando en números periódicos infinitos (al igual que $1/3$ es $0.333...$ en decimal).
    

!!! example Ejemplo con error de truncamiento
    Por ejemplo, el simple valor $0.1_{10}$ en binario es una fracción periódica: $0.0001100110011...$
    
    Dado que el ordenador tiene un número finito de bits para guardar el número, está obligado a **cortar (truncar)** la secuencia en algún punto. Esto implica que el ordenador casi nunca guarda *exactamente* el número real que escribimos, sino una aproximación muy cercana.

### Uso de Hexadecimal y Octal (Sistemas Compactos)

Aunque el ordenador trabaja estrictamente en binario, para los humanos leer secuencias largas como `101101011110` es lento, tedioso y muy propenso a errores visuales. 

Por esta razón, en informática se utilizan sistemas cuya base es una potencia exacta de 2 ($8=2^3$ y $16=2^4$). Estos sistemas funcionan como una **taquigrafía del binario**, permitiéndonos escribir la misma información de forma mucho más compacta sin tener que hacer divisiones o multiplicaciones complejas para la traducción.

*   **Hexadecimal (Base 16):** Es el estándar absoluto hoy en día. Se utiliza universalmente para representar **direcciones de memoria**, códigos de colores web (**#FFFFFF**), direcciones MAC o cualquier volcado de datos crudos (*raw data*). Un solo dígito hexadecimal representa **4 bits** (un *nibble*), por lo que dos dígitos hexadecimales representan exactamente **1 Byte**.
*   **Octal (Base 8):** Agrupa los bits de **3 en 3**. Fue muy popular en las primeras décadas de la informática (para palabras de 12, 24 o 36 bits), pero hoy su uso ha quedado relegado casi exclusivamente a la gestión de **permisos de ficheros en sistemas UNIX/Linux** (ej. `chmod 755`).

#### Método de Conversión por Agrupación
La conversión es directa y visual, ya que cada dígito en estas bases corresponde a un bloque fijo de bits.

1.  **Binario $\to$ Hexadecimal:** Agrupamos los bits de **4 en 4** partiendo desde la coma decimal hacia los extremos (izquierda para enteros, derecha para fracción). Si el último grupo queda incompleto, se rellena con ceros.
2.  **Binario $\to$ Octal:** El mismo proceso, pero haciendo grupos de **3 bits**.

!!! example "Ejemplo Completo con Decimales y Relleno"
    Convertir a Hexadecimal el binario: `111010.11011`
    
    El proceso exige agrupar de 4 en 4 **desde la coma hacia afuera**.
    
    **1. Parte Entera (`111010`):**
    *   Desde la coma a la izquierda: `1010` (grupo completo) $\to$ Quedan `11` sueltos.
    *   Rellenamos con ceros a la **izquierda**: `0011`.
    *   Grupos resultantes: `0011` | `1010` $\to$ **3** | **A**
    
    **2. Parte Fraccionaria (`.11011`):**
    *   Desde la coma a la derecha: `1101` (grupo completo) $\to$ Queda `1` suelto.
    *   Rellenamos con ceros a la **derecha**: `1000`.
    *   Grupos resultantes: `1101` | `1000` $\to$ **D** | **8**

    Resultado: **$3A.D8_{16}$**
    
    *(Nota: Los ceros de relleno son cruciales. Si en la parte fraccionaria hubiéramos tomado `1` como `0001` (1) en vez de `1000` (8), el error sería enorme)*

Convertir directamente de Octal a Hexadecimal o viceversa es simple si se usa como estrategia el **Binario como puente**:
    $$\text{Octal} \xrightarrow{\text{expandir a 3 bits}} \text{Binario} \xrightarrow{\text{agrupar de 4 bits}} \text{Hexadecimal}$$
    $$\text{Hexadecimal} \xrightarrow{\text{expandir a 4 bits}} \text{Binario} \xrightarrow{\text{agrupar de 3 bits}} \text{Octal}$$


## 3. Representación de Números Enteros

Los números enteros son la piedra angular de la aritmética computacional. No solo representan cantidades matemáticas, sino que constituyen el *lenguaje interno* del procesador: las direcciones de memoria, los punteros, los índices de arrays y los contadores de bucles son, estructuralmente, números enteros.

A diferencia de los números reales, la aritmética entera es **exacta**; no sufre de errores de precisión por redondeo. Sin embargo, se enfrenta a una limitación física ineludible: el **rango finito**. Al tener un número fijo de bits (ancho de palabra), existe un límite máximo y mínimo estricto que podemos representar, y superar ese límite tiene consecuencias drásticas.

### Enteros Sin Signo (Binario Puro)
Este formato se emplea para modelar problemas reales donde las magnitudes son siempre no negativas (el conjunto de los Naturales $\mathbb{N}$ más el cero).

**Usos típicos:**

*   Contadores de elementos (ej. número de alumnos).
*   Índices para acceder a listas o vectores.
*   Direcciones de memoria.

La representación interna coincide exactamente con el sistema numérico posicional base 2 visto anteriormente. Al no necesitar guardar información sobre el **signo**, utilizamos los $n$ bits completos para la magnitud.

*   **Rango Representable:** $[0, \quad 2^n - 1]$

#### Tabla de Valores (Ejemplo $n=8$ bits)
| Decimal | Patrón Binario ($b_7 \dots b_0$) | Lógica |
| :---: | :---: | :--- |
| **0** | `00000000` | Todos apagados |
| **1** | `00000001` | $2^0$ |
| **2** | `00000010` | $2^1$ |
| **3** | `00000011` | $2^1 + 2^0$ |
| ... | ... | ... |
| **254** | `11111110` | Todo $1$ menos el bit 0 |
| **255** | `11111111` | **Máximo** ($2^8 - 1$) |

#### Desbordamiento
Si a 255 (`11111111`) le sumamos 1, el resultado matemático sería 256 (`100000000`), pero como solo tenemos 8 bits, el bit superior se pierde y el resultado almacenado vuelve a ser **0** (`00000000`). Esto es el **desbordamiento** (*overflow*).

### Enteros Con Signo

#### 1. Signo y Magnitud
Es la forma más intuitiva para los humanos de representar números negativos. Consiste en utilizar el **bit más significativo (MSB)** exclusivamente para codificar el signo:

*   **Bit de Signo:** `0` para positivos, `1` para negativos.
*   **Magnitud:** Los $n-1$ bits restantes codifican el valor absoluto del número en binario puro.

**Rango de Representación:** $[-(2^{n-1} - 1), \quad +(2^{n-1} - 1)]$

!!! example Representar en *Signo y Magnitud* -47 con 8 bits
    Queremos codificar el número decimal **$-47_{10}$**.
    
    1.  **Bit de Signo:** Como es negativo, el bit más a la izquierda (MSB) es **`1`**.
    2.  **Magnitud (7 bits restantes):**
        *   Calculamos el valor absoluto: $|-47| = 47$.
        *   Descomponemos en potencias de 2: $47 = 32 + 8 + 4 + 2 + 1$.
        *   En binario puro es `101111` (6 bits).
        *   Rellenamos con ceros a la izquierda hasta completar los 7 bits reservados para la magnitud: **`0101111`**.
    
    **Resultado Final:** `1` (Signo) + `0101111` (Magnitud) = **`10101111`**

**Problemas y Desuso:**
Aunque conceptualmente sencilla, esta representación tiene graves defectos para el diseño de hardware:

1.  **Doble Cero:** Existen el $+0$ (`00000000`) y el $-0$ (`10000000`). Esto complica las comparaciones (`if x == 0`).
2.  **Aritmética Compleja:** La CPU necesitaría evaluar los signos antes de operar (como hacemos los humanos: *"si los signos son distintos, restamos"*). Esto es ineficiente; se prefiere un sistema donde la electrónica asociada a la suma funcione igual para positivos y negativos.

#### 2. Complemento a 2 (C2)
Es el sistema estándar utilizado por la aritmética de enteros en casi todos los procesadores modernos y el formato detrás del tipo entero en muchos de los lenguajes de programación.

**Definición Matemática:**
El complemento a la base $b$ de un número positivo $X$ codificado con $n$ cifras se define como $b^n - X$. En binario ($b=2$), esto es lo que llamamos Complemento a 2.

**Reglas de Representación:**

*   **Positivos y el 0:** Se representan idéntico a Signo-Magnitud (el MSB es `0`).
*   **Negativos:** Se representan calculando el complemento a 2 de su valor absoluto (el MSB es `1`).

**Interpretación del Peso Negativo (Polinomio Equivalente):**
Lo más interesante del C2 es que el bit de signo (MSB, posición $n-1$) no es solo una etiqueta, sino que tiene **valor matemático**. Su peso es igual a la potencia correspondiente pero con **signo negativo**.

$$ N = -d_{n-1} \cdot 2^{n-1} + \sum_{i=0}^{n-2} d_i \cdot 2^i $$
$$ N = \mathbf{-d_{n-1}2^{n-1}} + d_{n-2}2^{n-2} + \dots + d_1 2^1 + d_0 2^0 $$

*   **Rango:** $[-2^{n-1}, \quad 2^{n-1} - 1]$. (Es asimétrico: hay un valor negativo extra porque el 0 "gasta" una combinación de los positivos).


!!! example Ejemplo: Obtener el número negativo $-13$ en C2 con 6 bits
    
    Escribir el positivo: $13_{10} = 001101_2$ (Rellenamos con ceros hasta 6 bits)
    
    **Método 1: Inversión + 1 (Estándar)**

    *   Invertir todos los bits (cambiar 0s por 1s): `110010`
    *   Sumar 1 al resultado final: `110010` + `1` = **`110011`**
    
    **Método 2: Regla rápida (Visual)**

    *   Recorrer de derecha a izquierda hasta el primer '1' (inclusive), dejar esos bits igual e invertir el resto.
    *   `00110`**`1`** $\to$ Invertir parte izquierda $\to$ **`11001`**`1`

    **Método 3: Definición Matemática ($2^n - X$)**

    *   Aplicamos la fórmula estricta con $n=6$ y $X=13$.
    *   $2^6 - 13 = 64 - 13 = 51$
    *   Convertimos 51 a binario puro $\to$ **`110011`**

!!! example Ejemplo: Obtener el número negativo $-13$ en C2 con 10 bits
    
    Escribir el positivo: $13_{10} = 0000001101_2$ (Rellenamos con ceros hasta 10 bits)
    
    **Método 1: Inversión + 1 (Estándar)**
    *   Invertir todos los bits: `1111110010`
    *   Sumar 1: `1111110010` + `1` = **`1111110011`**
    
    **Método 2: Regla rápida (Visual)**
    *   `000000110`**`1`** $\to$ Invertir parte izquierda $\to$ **`111111001`**`1`

    **Método 3: Definición Matemática**
    *   $2^{10} - 13 = 1024 - 13 = 1011$
    *   $1011_{10}$ en binario es **`1111110011`**
    
    Resultado: **$1111110011_{C2}$**

!!! info "Curiosidad Histórica: El Complemento a 1"
    Existe otra representación llamada **Complemento a la base menos 1** (Complemento a 1 en binario), que se obtiene simplemente intercambiando 0s y 1s.
    
    Esta técnica fue utilizada en algunas series de computadoras pioneras descendientes de la **ENIAC**, como la serie **UNIVAC**. Actualmente está en desuso frente al Complemento a 2 porque, al igual que el Signo-Magnitud, sufre del problema del *doble cero*.

!!! tip La Analogía del Reloj
    El Complemento a 2 funciona exactamente igual que los minutos en un reloj analógico (aritmética modular).
    
    Si el reloj marca las `:00` y queremos restar 10 minutos:
    
    *   **Opción A (Resta):** Mover la aguja 10 minutos hacia atrás $\to$ Posición `:50`.
    *   **Opción B (Suma del Complemento):** Mover la aguja 50 minutos hacia adelante $\to$ Posición `:50`.
    
    En un sistema cíclico (limitado), **avanzar 50** pasos te deja en el mismo sitio que **retroceder 10**.
    
    El ordenador usa este truco para **no tener que implementar la resta** en hardware (que es costosa).
    Por ejemplo, en un sistema de 8 bits (donde la vuelta completa son 256 pasos), restar 1 es equivalente a sumar 255.
    
    Si calculamos $5 + 255$, la suma aritmética es $260$. Pero como solo tenemos 8 bits, se produce un **desbordamiento** (se pierde el bit que sobra al dar la vuelta) y el contador se queda en $4$.
    $$ 5 + 255 \equiv 4 \pmod{256} $$
    ¡Hemos conseguido el resultado correcto ($5-1=4$) usando solo la suma!

### Representación en Lenguajes de Programación


La representación interna de los números enteros depende drásticamente del lenguaje. Mientras que C++ ofrece control sobre el hardware (tamaños fijos), Python ofrece abstracción matemática (tamaños dinámicos).

#### C++
**Filosofía:** Eficiencia y cercanía al Hardware.

*   **Tamaños fijos:** C++ permite trabajar con enteros de 8, 16, 32 o 64 bits.
*   **Tipos:** Soporta `signed` (Complemento a 2) y `unsigned` (Binario Puro).

**Ejemplo: Representación en Memoria (32 bits)**
```cpp
int x = 23;  // Memoria: 00000000 ... 00010111
int x = -23; // Memoria: 11111111 ... 11101001 (Complemento a 2)
```

**Enteros sin Signo (`unsigned`)**
Eliminan el bit de signo para duplicar el rango positivo ($[0, 2^{32}-1]$ en 32 bits).

!!! warning Riesgo de Desbordamiento
    En C++, si sumas 1 al máximo entero representable, el valor *da la vuelta* y pasa a ser el mínimo negativo (en `signed`) o cero (en `unsigned`). **!El ejecutable no genera una excepción!**

#### Python
**Filosofía:** Comodidad y Abstracción.

*   **Precisión Arbitraria:** En Python 3, los enteros (`int`) crecen dinámicamente tanto como la RAM permita. ¡No existe *overflow* aritmético!
*   **Sin tipos `unsigned`:** Todos los enteros tienen signo.

**Estructura Interna (Precisión Arbitraria o *BigNum*)**
A diferencia de C++, donde un entero es una caja de tamaño fijo (si metes algo más grande, se rompe), en Python un entero es como un *acordeón* que se estira según se necesite.

Para lograr esto, Python no guarda el número tal cual lo hace el procesador. En su lugar, trocea el número grande en pequeños bloques de 30 bits y los trata como si fueran *dígitos* de una base numérica gigante (**Base $2^{30}$**).

Matemáticamente, funciona igual que nuestro sistema decimal (donde sumamos unidades, decenas, centenas...), pero usando potencias de $2^{30}$:
$$N = \sum_{i=0} d_i \cdot (2^{30})^i = d_0 + d_1 \cdot 2^{30} + d_2 \cdot 2^{60} + \dots$$

!!! example Ejemplo Práctico
    Imagina un número enorme como `123456789101112131415` (requiere unos 70 bits).
    1.  Como no cabe en un registro de CPU de 64 bits, Python lo descompone.
    2.  Calcula sus *dígitos* en base $2^{30}$ y obtiene tres bloques: `437976919`, `87719511` y `107`.
    3.  Guarda internamente una lista con la **magnitud**: `[437976919, 87719511, 107]`.
    
    Utiliza un campo extra para indicar la longitud y el signo: almacenará **3** si es positivo o **-3** si es negativo. Este valor se almacena en **Complemento a 2**. El signo de este campo es el signo del número original y su valor absoluto determina cuantos bloques (dígitos) tiene la lista.

    Si multiplicas este número por 1000 y el resultado necesita más espacio, Python simplemente añade un cuarto dígito a la lista.

!!! note El precio de la magia
    Mientras que en C++ sumar dos números es **una sola instrucción** eléctrica (nanosegundos), en Python implica ejecutar un pequeño programa que recorre estas listas, gestiona los acarreos y asigna memoria. Es mucho más cómodo, pero mucho más lento.


## 4. Representación de Números Reales (Coma Flotante)

La representación de números reales ($\mathbb{R}$) supone un reto mayúsculo para una máquina digital. Mientras que los enteros son discretos, los reales son continuos: entre $1.0$ y $1.1$ existen infinitos valores. Dado que tenemos una memoria finita, es **imposible** representar el conjunto de los números reales con total exactitud. 

La solución adoptada universalmente es la **Coma Flotante**, que permite cubrir un rango de valores gigantesco (desde lo subatómico hasta lo astronómico) sacrificando precisión absoluta en los decimales menos significativos.

!!! note Realidad Hardware: Todo son Enteros
    Estrictamente hablando, **un ordenador NO puede almacenar números reales**.
    
    A nivel de hardware, la memoria solo guarda patrones de bits (enteros). Lo que nosotros llamamos `float` o `double` no es más que una **apariencia**: tomamos un entero largo y acordamos dividir sus bits en *campos* (signo, exponente, mantisa) para aplicarles una fórmula matemática. Es una simulación numérica sobre un hardware discreto.

### Estándar IEEE 754
Prácticamente todos los computadores modernos siguen este estándar. Se basa en adaptar la **notación científica** al mundo binario:

$$ V = (-1)^s \cdot (1 + m) \cdot 2^{e - Bias} $$

*   **$s$ (Signo):** 1 bit ($0 \to +$, $1 \to -$).
*   **$m$ (Mantisa):** Parte fraccionaria normalizada ($1.xxxxx...$).
*   **$e$ (Exponente):** Entero representado en **exceso**.

### Estructura IEEE 754

| Precisión | Bits Totales | Signo | Exponente ($k$ bits) | Mantisa ($p$ bits) | Exceso (Bias) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Simple (`float`)** | 32 | 1 | 8 | 23 | 127 |
| **Doble (`double`)** | 64 | 1 | 11 | 52 | 1023 |

### Características Clave
1.  **Exponente en Exceso:** Se suma un sesgo ($Bias$) al exponente real.
    *   $E_{guardado} = E_{real} + Bias$.
    *   Permite comparar números reales como si fueran enteros (ordenación rápida).
2.  **Bit Implícito:** En la notación normalizada binaria, el número siempre empieza por `1.` (ej. `1.011...`). Para ahorrar espacio, ese `1` **no se guarda**.

!!! example "Ejemplo: Convertir 13.125 a IEEE 754 (Simple)"
    1.  **Binario:** $13.125_{10} = 1101.001_2$
    2.  **Normalizar:** $1.101001 \times 2^3$
    3.  **Componentes:**
        *   Signo: $0$ (+)
        *   Exponente Real: $3$. Exponente guardado: $3 + 127 = 130 \to 10000010_2$.
        *   Mantisa: $101001...$ (rellenar con ceros hasta 23 bits).
    4.  **Resultado Hex:** `0 10000010 1010010000...` $\to$ `41520000`

### Casos Especiales

| Exponente | Mantisa | Significado |
| :--- | :--- | :--- |
| Todo 0s | Todo 0s | Cero ($\pm 0$) |
| Todo 0s | $\neq 0$ | Números desnormalizados (muy pequeños) |
| Todo 1s | Todo 0s | Infinito ($\pm \infty$) |
| Todo 1s | $\neq 0$ | NaN (Not a Number) |

### Precisión y Problemas
Los números reales en el ordenador son un subconjunto discreto de los reales matemáticos.
*   **Densidad variable:** Hay más números representables cerca del cero que lejos de él.
*   **Errores de redondeo:** Números simples como $0.1_{10}$ tienen representación periódica infinita en binario, provocando errores de precisión.

!!! warning "Programación"
    Nunca compares números en coma flotante con igualdad estricta (`if x == y`). Usa un margen de tolerancia (épsilon): `if abs(x - y) < 0.00001`.

    *Ejemplo catastrófico:* Fallo del misil Patriot (error acumulado en el reloj del sistema).

---

## 5. Representación de Caracteres

### ASCII
*   Estándar original de 7 bits (128 caracteres).
*   Incluye letras inglesas, dígitos y control.
*   Las letras y números están ordenados consecutivamente (facilita la ordenación).
    *   `'0'` = 48, `'A'` = 65, `'a'` = 97.
    *   Diferencia entre mayúscula/minúscula es un solo bit.

### UNICODE
Estándar para representar todos los sistemas de escritura del mundo.
*   **UTF-8:** Codificación de longitud variable (1 a 4 bytes). Compatible con ASCII (los caracteres ASCII ocupan 1 byte en UTF-8). Es el estándar de la web y de **Python 3**.

### Cadenas (Strings)
*   **C++:**
    *   `char`: 1 byte (ASCII).
    *   Cadenas terminadas en `\0` o clase `std::string`.
*   **Python:**
    *   `str`: Unicode por defecto (UTF-8).

---

## 6. Aritmética Binaria (Ampliación)

### Álgebra de Boole
Operaciones a nivel de bit fundamentales para el hardware:
*   **NOT (`~`):** Inversión.
*   **AND (`&`):** Multiplicación lógica ($1$ si ambos son $1$).
*   **OR (`|`):** Suma lógica ($1$ si alguno es $1$).
*   **XOR (`^`):** O exclusival ($1$ si son diferentes).

### Suma Binaria
Se implementa mediante circuitos lógicos:
1.  **Semisumador:** Suma 2 bits. Produce *Suma* y *Acarreo*.
2.  **Sumador Completo:** Suma 2 bits más un acarreo de entrada.

!!! note "Desbordamiento (Overflow)"
    Al sumar enteros en C2, si sumamos dos números del mismo signo y el resultado tiene el signo opuesto, ha ocurrido un desbordamiento. El resultado no cabe en los bits disponibles.

### Resta Binaria
La resta se realiza sumando el complemento a 2 del sustraendo:
$$ A - B = A + (\text{C2}(B)) = A + (\sim B + 1) $$
Esto permite usar el mismo circuito sumador para restar.

---

## Bibliografía Recomendada

1.  **S. B. Lippman, J. Lajoie, B. E. Moo.** *C++ Primer*. Addison-Wesley.
2.  **R. E. Bryant, D. R. O’Hallaron.** *Computer Systems. A Programmer’s Perspective*. Pearson.
3.  [Estándar IEEE 754 (Wikipedia)](https://es.wikipedia.org/wiki/IEEE_754)
4.  [The Absolute Minimum Every Software Developer Must Know About Unicode](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/)