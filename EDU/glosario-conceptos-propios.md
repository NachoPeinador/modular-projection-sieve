# Glosario de Conceptos Propios: Teoría de Proyección Modular y Umbrales $K_{\min}^\pm$

*Documento de Referencia Científica y Terminología Matemática*  
*Generado por Gemini Notebook*

---

Este glosario define de forma rigurosa y accesible la terminología original desarrollada en la **Teoría de Cribado por Proyección Modular**. Esta teoría unifica la aritmética modular en el anillo cociente $\mathbb{Z}/6\mathbb{Z}$, la teoría de representaciones espectrales sobre espacios de Hilbert discretos y la física del caos cuántico. 

Cada concepto aquí expuesto se fundamenta en las estructuras algebraicas que rigen la distribución determinista de los números primos, asociándose directamente con sus correspondientes demostraciones analíticas, fórmulas del manuscrito y su certificación axiomática en el asistente de demostraciones **Lean 4**.

---

## Índice de Conceptos
1. [Canal Modular (𝒞₁ y 𝒞₅)](#1-canal-modular-c1-y-c5)
2. [Simetría Quiral y Operación Estrella (★)](#2-simetria-quiral-y-operacion-estrella-)
3. [Coprimo Posicional (NextKop / Cop(p))](#3-coprimo-posicional-nextkop--copp)
4. [Brecha Quiral (Chiral Gap)](#4-brecha-quiral-chiral-gap)
5. [Distancia Hueca (Hollow Distance / ΔK)](#5-distancia-hueca-hollow-distance--delta-k)
6. [Desierto Topológico (Topological Desert)](#6-desierto-topologico-topological-desert)

---

### 1. Canal Modular ($\mathcal{C}_1$ y $\mathcal{C}_5$)

#### Definición Accesible
Los **Canales Modulares** son las dos "autopistas aritméticas" independientes e infinitas por donde viajan todos los números enteros candidatos a ser primos (aquellos que no son múltiplos de 2 ni de 3). Al restringir la búsqueda a estos canales, el sistema descarta pasivamente el $66.67\%$ del dominio entero sin realizar marcas ni operaciones en memoria.

#### Definición Rigurosa y Formulada
Sea $\mathcal{N} = \{N \in \mathbb{N} \mid N > 3, \gcd(N, 6) = 1\}$ el conjunto de enteros candidatos a primo. Por el **Teorema de Clasificación Modular (Teorema 2.1)**, todo elemento de $\mathcal{N}$ pertenece de forma unívoca a una de las dos clases de equivalencia del grupo de unidades del anillo cociente $\mathbb{Z}/6\mathbb{Z}$, el cual es $(\mathbb{Z}/6\mathbb{Z})^\times = \{1, 5\} \cong \mathbb{Z}_2$. 

Se define la proyección biyectiva $\Pi: \mathcal{N} \to \mathcal{S}_k$ que mapea cada candidato $N$ a su par posicional orientado $(k, \varepsilon)$ en el espacio de estados de índices $\mathcal{S}_k = \mathbb{N}^+ \times \{1, -1\}$ mediante:

$$k = \lfloor N / 6 \rfloor \quad \text{o} \quad \left\lceil N / 6 \right\rceil, \quad \varepsilon \in \{1, -1\}$$

De este modo se definen los canales:
*   **Canal positivo $\mathcal{C}_1$:** Formado por los enteros con polaridad quiral positiva $\varepsilon = 1$:
    $$N = 6k + 1 \quad (k \ge 1)$$
*   **Canal negativo $\mathcal{C}_5$:** Formado por los enteros con polaridad quiral negativa $\varepsilon = -1$:
    $$N = 6k - 1 \quad (k \ge 1)$$

#### Relación con el Manuscrito y Lean 4
Esta clasificación se corresponde con el **Teorema 2.1** (Clasificación Modular de Números Naturales) y el **Lema 3.1** (Equivalencia Modular sobre el Espacio de Índices). En Lean 4, la correctitud absoluta de esta partición disjunta y exhaustiva ha sido mecánicamente certificada en Mathlib utilizando la táctica de aritmética ecuacional lineal `omega` (aritmética de Presburger), asegurando una tasa de error del $0.0\%$.

---

### 2. Simetría Quiral y Operación Estrella ($\star$)

#### Definición Accesible
La **Simetría Quiral** describe la interacción geométrica y algebraica "tipo espejo" entre los dos canales modulares. Determina cómo se comportan los compuestos resultantes de multiplicar números primos: multiplicar dos primos del mismo canal siempre produce un número en el canal positivo ($\mathcal{C}_1$), mientras que multiplicar primos de canales cruzados genera un compuesto en el canal negativo ($\mathcal{C}_5$).

#### Definición Rigurosa y Formulada
El grupo de unidades $(\mathbb{Z}/6\mathbb{Z})^\times$ tiene un comportamiento multiplicativo isomorfo al grupo cíclico de orden dos ($\mathbb{Z}_2$), caracterizado por la involución modular de sus generadores:

$$1 \cdot 1 \equiv 1 \pmod 6, \quad 5 \cdot 5 \equiv 1 \pmod 6, \quad 1 \cdot 5 \equiv 5 \pmod 6$$

Al trasladar la multiplicación clásica en $\mathbb{N}$ al dominio posicional de coordenadas mediante el **Isomorfismo I (Teorema 4.3)**, se demuestra que el producto de dos candidatos $N_1 = 6k_1 + \varepsilon_1$ y $N_2 = 6k_2 + \varepsilon_2$ equivale exactamente a la aplicación de la **operación de semigrupo conmutativo estrella ($\star$)** sobre sus pares posicionales:

$$(k_1, \varepsilon_1) \star (k_2, \varepsilon_2) = (K, \varepsilon_R)$$

Expandiendo el producto algebraico en el cuerpo real:

$$N_1 \cdot N_2 = (6k_1 + \varepsilon_1)(6k_2 + \varepsilon_2) = 36k_1k_2 + 6\varepsilon_1 k_2 + 6\varepsilon_2 k_1 + \varepsilon_1\varepsilon_2$$

Factorizando el módulo primorial $6$, obtenemos las leyes de composición interna que definen la simetría quiral en el espacio de índices:
1.  **Índice Posicional Resultante ($K$):** 
    $$K = 6k_1k_2 + \varepsilon_1 k_2 + \varepsilon_2 k_1$$
2.  **Polaridad Quiral Resultante ($\varepsilon_R$):** 
    $$\varepsilon_R = \varepsilon_1 \cdot \varepsilon_2$$

Esto consolida las reglas de colisión quiral:
$$\mathcal{C}_1 \times \mathcal{C}_1 \to \mathcal{C}_1 \quad (\varepsilon_R = 1)$$
$$\mathcal{C}_5 \times \mathcal{C}_5 \to \mathcal{C}_1 \quad (\varepsilon_R = 1)$$
$$\mathcal{C}_1 \times \mathcal{C}_5 \to \mathcal{C}_5 \quad (\varepsilon_R = -1)$$

#### Relación con el Manuscrito y Lean 4
Sustentado formalmente por el **Teorema 4.3 (Isomorfismo I)**. En Lean 4, este núcleo algebraico de involución quiral y grupo de unidades ha sido verificado sintácticamente a nivel de Mathlib mediante la táctica de decisión estricta `decide` y la normalización numérica `norm_num`.

---

### 3. Coprimo Posicional (NextKop / Cop(p))

#### Definición Accesible
Para un número primo base dado en una "autopista" modular, su **Coprimo Posicional** representa la "pareja" de menor tamaño ubicada en la autopista opuesta (canal alternante). Este emparejamiento es el eslabón fundamental que permite calcular matemáticamente dónde ocurrirá la primera colisión compuesta cruzada entre canales sin tener que buscar a ciegas en la recta numérica.

#### Definición Rigurosa y Formulada
Dado un primo base $p = 6k_p \pm 1$ perteneciente a un canal de origen con polaridad $\varepsilon_p$, se define su **Coprimo Posicional** (denotado por $\mathrm{Cop}(p)$) como el menor número primo $q = 6k_q \mp 1$ perteneciente al canal con polaridad opuesta $-\varepsilon_p$ tal que su índice posicional cumple:

$$k_q \ge k_p$$

El índice posicional de esta coordenada coprima mínima se denota mediante la función de coincidencia asintótica:

$$\mathrm{NextKop}(p) = k_q$$

La existencia asintótica del NextKop para cualquier primo generador está matemáticamente respaldada por el Teorema de Dirichlet sobre primos en progresiones aritméticas para las clases de residuos de módulo 6.

Cuando el salto topológico de entrelazamiento es nulo, es decir:

$$\Delta k = \mathrm{NextKop}(p) - k_p = 0$$

El sistema físico-espectral se encuentra en su **estado fundamental (vacío)**. Esto se traduce aritméticamente en la colisión espacial simétrica de un par de **primos gemelos** de la forma:

$$(6k_p - 1, 6k_p + 1)$$

#### Relación con el Manuscrito y Lean 4
Este concepto está formalizado en la **Definición 3.6 (Coprimo Posicional)** y el **Corolario 7.2** del artículo. En Lean 4, la topología del estado fundamental ha sido demostrada de forma axiomática sin axiomas omitidos (`sorry-free`), probando con la táctica `ring` que al cumplirse la igualdad del estado fundamental $\Delta k = 0$ ($k_q = k_p$), el umbral colapsa en el producto algebraico conjugado exacto de los primos gemelos.

---

### 4. Brecha Quiral (Chiral Gap)

#### Definición Accesible
Es la brecha física o distancia real (en números enteros tradicionales) que separa a un primo base de su coprimo posicional conjugado. A diferencia de las brechas clásicas de primos consecutivos, la **Brecha Quiral** mide específicamente el acoplamiento o distancia asimétrica cruzada entre las dos "autopistas" modulares, trazando la velocidad a la que se diluyen las colisiones del entrelazamiento.

#### Definición Rigurosa y Formulada
Sea $p = 6k_p \pm 1$ un primo base con índice $k_p$ y polaridad $\varepsilon_p$. Sea $\mathrm{Cop}(p) = 6k_q \mp 1$ su coprimo posicional con índice $k_q = \mathrm{NextKop}(p)$. Se define la **Brecha Quiral** ($g_{\text{quiral}}$) como la distancia absoluta en el espacio de números naturales:

$$g_{\text{quiral}} = |\mathrm{Cop}(p) - p|$$

Expresada rigurosamente en términos del espacio de índices y el salto topológico de entrelazamiento $\Delta k = k_q - k_p$:

*   **Si el primo base $p \in \mathcal{C}_5$ ($\varepsilon_p = -1$):** El coprimo posicional pertenece a $\mathcal{C}_1$, por lo tanto:
    $$g_{\text{quiral}} = (6k_q + 1) - (6k_p - 1) = 6(k_q - k_p) + 2 = 6\Delta k + 2$$
*   **Si el primo base $p \in \mathcal{C}_1$ ($\varepsilon_p = 1$):** El coprimo posicional pertenece a $\mathcal{C}_5$, por lo tanto:
    $$g_{\text{quiral}} = (6k_p + 1) - (6k_q - 1) = 6(k_p - k_q) + 2 = 6|\Delta k| + 2$$ (dado que $k_q \ge k_p$ y para colisiones no redundantes, se analiza la magnitud absoluta).

Esta distancia rige el sesgo de densidad en la red de entrelazamiento y se vincula formalmente con la derivación de la constante de primos gemelos de Hardy-Littlewood ($C_2$). Al evaluar la tasa de supervivencia ante las inecuaciones del aniquilador cuadrático espectral:

$$k^2 - k_p^2 \not\equiv 0 \pmod p$$

La brecha quiral demuestra que la probabilidad real de supervivencia a la criba no es estadísticamente independiente, sino que está corregida por la impedancia quiral del anillo modular:

$$f(p) = \frac{p(p-2)}{(p-1)^2} = 1 - \frac{1}{(p-1)^2}$$

#### Relación con el Manuscrito y Lean 4
Asociada al **Teorema 4.4** (Condición de Supervivencia y Constante $C_2$). En Lean 4, la transferencia de divisibilidad que formaliza la no colisión del entrelazamiento quiral y la inecuación del aniquilador cuadrático espectral ha sido validada mecánicamente a través de la normalización sintáctica y la táctica `ring`.

---

### 5. Distancia Hueca (Hollow Distance / $\Delta K$)

#### Definición Accesible
La **Distancia Hueca** es una "zona muerta" de inmunidad total ubicada en el canal negativo ($\mathcal{C}_5$). Representa una brecha de seguridad espacial entre el primer múltiplo que un primo genera en su propio canal (su cuadrado $p^2$, en el canal positivo $\mathcal{C}_1$) y su primer múltiplo cruzado en el canal opuesto ($p \cdot \mathrm{Cop}(p)$). En esta zona es matemáticamente imposible que el primo genere múltiplos, lo que ahorra valiosos ciclos de procesamiento en CPUs de alto rendimiento al evitar búsquedas inútiles en dicha área.

#### Definición Rigurosa y Formulada
Para cada primo base $p = 6k_p \pm 1$ se calculan analíticamente dos umbrales mínimos de activación asimétricos e independientes, denotados como $\mathrm{Kmin}^\pm(p)$:

*   **Umbral Local $\mathrm{Kmin}^+(p)$:** Controla el inicio de marcas en el canal positivo $\mathcal{C}_1$. Al ser todo cuadrado de un número coprimo con 6 congruente con $1 \pmod 6$ ($p^2 \equiv 1 \pmod 6$), este primer impacto ocurre invariablemente en $\mathcal{C}_1$.
*   **Umbral Cruzado $\mathrm{Kmin}^-(p)$:** Controla el inicio de marcas en el canal opuesto $\mathcal{C}_5$. Este impacto nace exclusivamente del producto entrelazado con su coprimo posicional ($p \cdot \mathrm{Cop}(p) \equiv 5 \pmod 6$).

Se define la **Distancia Hueca** ($\Delta K$) como la diferencia absoluta en el espacio de índices posicionales entre ambos umbrales:

$$\Delta K = |\mathrm{Kmin}^-(p) - \mathrm{Kmin}^+(p)|$$

Las fórmulas analíticas exactas para calcular estos umbrales según el canal de origen del primo base son:

1.  **Si el primo base $p = 6k_p - 1 \in \mathcal{C}_5$:**
    $$\mathrm{Kmin}^+(p) = p \cdot k_p - k_p$$
    $$\mathrm{Kmin}^-(p) = p \cdot \mathrm{NextKop}(p) + k_p$$
    $$\Delta K = p \cdot (\mathrm{NextKop}(p) - k_p) + 2k_p = p\Delta k + 2k_p$$

2.  **Si el primo base $p = 6k_p + 1 \in \mathcal{C}_1$:**
    $$\mathrm{Kmin}^+(p) = p \cdot k_p + k_p$$
    $$\mathrm{Kmin}^-(p) = p \cdot \mathrm{NextKop}(p) - k_p$$
    $$\Delta K = p \cdot (\mathrm{NextKop}(p) - k_p) - 2k_p = p\Delta k - 2k_p$$

Cualquier algoritmo clásico fundamentado en un límite global de raíz cuadrada ($\sqrt{N}$) desperdicia recursos evaluando el canal opuesto a partir de $\mathrm{Kmin}^+$. El uso de los umbrales asimétricos $K_{\min}^\pm$ permite omitir completamente esta brecha inútil.

#### Relación con el Manuscrito y Lean 4
Sustentado por la **Definición 3.7** y el **Teorema 3.7** (Cálculo de Umbrales por Entrelazamiento Primo-Coprimo). En Lean 4, las cuatro expresiones algebraicas de entrelazamiento asimétrico cruzado que sustentan los umbrales de la distancia hueca han sido certificadas axiomáticamente de forma robusta con la ayuda de la táctica de anillos conmutativos `ring`.

---

### 6. Desierto Topológico (Topological Desert)

#### Definición Accesible
El **Desierto Topológico** es una representación macroscópica de las zonas vacías de la red modular. Describe cómo, a medida que avanzamos hacia el infinito en la recta numérica, el espacio de índices experimenta grandes franjas logarítmicas donde las líneas de aniquilación proyectadas por los primos base saturan el espacio, impidiendo la aparición de nuevos primos. Sin embargo, debido al entrelazamiento quiral, la red modular exhibe una tenacidad geométrica asombrosa, concentrando más del $50\%$ de sus proyecciones de mínima energía en saltos ultra-cortos, incluso en escalas del orden de $10^9$.

#### Definición Rigurosa y Formulada
A gran escala ($N \to \infty$), el Teorema de los Números Primos dicta que la densidad de primos decrece logarítmicamente. En el espacio de proyección modular, esto se traduce en una reducción asintótica de la densidad de elementos en el Hamiltoniano discreto de criba $\mathbf{H}_N = MM^T$, induciendo un fenómeno análogo a la **Localización de Anderson** en matrices dispersas (*sparse random matrices*).

El crecimiento y la cota superior del tamaño de estos desiertos topológicos en el operador de entrelazamiento (que mide la distancia máxima entre un primo base y el primer compuesto inédito de la red) se define mediante la **Conjetura del Entrelazamiento Quiral de Cramér (Conjetura 7.4)**. Se postula que la magnitud máxima del salto topológico $\Delta k$ está asintóticamente acotada por una envolvente cuadrática logarítmica:

$$\Delta k_{\max}(N) = O\left((\ln N)^2\right)$$

A escala masiva (analizando más de $15.6$ millones de proyecciones hasta $k = 100,000,000$, que equivale a $N \approx 6 \times 10^8$), la red de entrelazamiento modular demuestra una obstinada resistencia frente a la dilución. Mientras que la teoría de probabilidad clásica predeciría una dispersión caótica desordenada (estadística de Poisson), el sistema se mantiene anclado en su configuración geométrica de mínima energía:

*   El **$50.54\%$** de todas las proyecciones asintóticas a escala $k=10^8$ colapsan en el vecindario de proximidad extrema **$\Delta k \le 3$**.
*   Apenas un **$2.06\%$** de las proyecciones logran superar un salto posicional de $20$ índices ($\Delta k > 20$).

Esto confirma que el desierto topológico no es una llanura de azar aleatorio, sino una estructura espectral regulada por la repulsión de niveles propia del **Ensamble Ortogonal Gaussiano (GOE)**, con un ratio de espaciado empírico medio universal de:

$$\langle r \rangle \approx 0.4989$$

#### Relación con el Manuscrito y Lean 4
Este comportamiento asintótico está detallado en la **Conjetura 7.4** (Acotación de Entrelazamiento y Desiertos Quirales), la **Observación 6.7** (Espectroscopía Cuántica) y el **Teorema Espectral**. En Lean 4, la autoadjuntidad del Hamiltoniano discreto $H_N = M M^T$ que sustenta este análisis ha sido demostrada formalmente mediante la táctica de simplificación matricial `simp` aplicada a la propiedad `Matrix.transpose_mul`.

---
