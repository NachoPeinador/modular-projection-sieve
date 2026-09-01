Esta sección de **Preguntas Frecuentes (FAQ) y Mitos Comunes** está diseñada especialmente para estudiantes e ingenieros que se adentran en la **Teoría de Proyección Modular**. Su objetivo es disipar las dudas conceptuales más recurrentes y tender un puente comprensible entre la rigidez del álgebra abstracta y la intuición física de la red modular.

---

### ❓ FAQ 1: Si el Módulo 30 descarta más números, ¿por qué nos limitamos al Módulo 6?
*   **El Mito:** *"En las cribas basadas en 'ruedas de factorización', cuanto más grande es el módulo base (módulo 30, 210, etc.), más eficiente es el algoritmo porque tachamos más candidatos de entrada."*
*   **La Realidad Matemática:** En la optimización computacional real, existe un compromiso o **"trilema"** entre el ahorro de candidatos y el costo de gestionar la memoria en la CPU. 
    Al pasar del módulo 2 al módulo 6 (transición primorial $2 \to 6$), reducimos la densidad de números supervivientes del $50\%$ al $33.3\%$, requiriendo vigilar solo **2 canales activos** ($\mathcal{C}\_1$ y $\mathcal{C}\_5$). Esto representa el **Punto Crítico de Pareto** con un Retorno de Inversión Informacional de $\mathrm{ROI}\_{2\to6} \approx 0.105155$.
    Si intentáramos escalar al módulo 30 (transición $6 \to 30$), la densidad de candidatos supervivientes apenas bajaría del $33.3\%$ al $26.7\%$, pero el número de canales que la CPU tendría que rastrear en paralelo **se cuadruplicaría de 2 a 8 canales** ($\phi(30) = 8$). Esta explosión combinatoria destruye por completo la localidad de caché L1/L2 de la CPU, satura los registros de cálculo y desploma el ROI informacional en más de un **350%** ($\mathrm{ROI}\_{6\to30} \approx 0.029885$). El módulo 6 es, por lo tanto, el único **canal sin ruido** espectral que maximiza la eficiencia termodinámica de la información.

---

### ❓ FAQ 2: ¿Por qué se dice que los primos gemelos representan el "estado fundamental" (vacío) del sistema?
*   **El Mito:** *"Los primos gemelos son simplemente una fluctuación estadística o una feliz coincidencia aritmética en la recta numérica."*
*   **La Realidad Matemática:** Bajo la óptica de la teoría de operadores y entrelazamiento, los primos gemelos son una consecuencia geométrica determinista y natural. 
    Cuando un primo del canal negativo $p \in \mathcal{C}\_5$ busca activamente a su "pareja" o coprimo posicional $\mathrm{Cop}(p)$ en el canal positivo $\mathcal{C}\_1$, la distancia o "brecha" que separa sus índices posicionales en la red modular se conoce como el **salto topológico de entrelazamiento**:
    
    $$\Delta k = \mathrm{NextKop}(p) - k\_p \ge 0$$
    
    *   Si $\Delta k > 0$, el sistema se encuentra en un **estado excitado** (el coprimo está más adelante en la red).
    *   Si **$\Delta k = 0$**, el salto topológico es nulo. Esto significa que el primo y su coprimo posicional comparten exactamente la misma coordenada o índice espacial $k$, colapsando simétricamente en las formas conjugadas $6k-1$ y $6k+1$.
    
    Este colapso representa el **estado fundamental o de mínima energía geométrica** del operador de entrelazamiento. Lejos de ser una anomalía caótica, el análisis espectral revela que la configuración de primos gemelos es el estado más denso del sistema, concentrando de manera natural el $21.69\%$ de todas las interacciones de acoplamiento en la red.

---

### ❓ FAQ 3: ¿Por qué el algoritmo no necesita calcular raíces cuadradas para operar?
*   **El Mito:** *"Dado que todo algoritmo de criba debe detenerse en "* $\sqrt{N}$ *" para no calcular múltiplos redundantes, es obligatorio calcular raíces cuadradas flotantes para cada primo."*
*   **La Realidad Matemática:** El cálculo tradicional de raíces cuadradas flotantes (operaciones de hardware costosas como `sqrt()`) se evita traduciendo algebraicamente el límite global del espacio entero al espacio de índices posicionales $k$.
    En lugar de evaluar la cota general $p \le \sqrt{N}$ en cada paso de manera iterativa, el algoritmo de proyección modular calcula analíticamente, una sola vez al descubrir el primo, su **Umbral Mínimo de Activación** $k\_{\min}(p)$. Mediante simples multiplicaciones de enteros en el dominio de índices, sabemos con precisión absoluta y sin margen de error dónde ocurrirá el primer múltiplo inédito del primo en cada canal:
    *   **Umbral Local** $K\_{\min}^+$ (derivado del cuadrado $p^2$ en el canal $\mathcal{C}\_1$).
    *   **Umbral Cruzado** $K\_{\min}^-$ (derivado del producto cruzado $p \cdot \mathrm{Cop}(p)$ en el canal $\mathcal{C}\_5$).
    
    Al estructurar estas balizas de entrada directas, el flujo de control sabe de antemano que para cualquier índice $k < K\_{\min}^\pm$, es matemáticamente imposible que el primo $p$ genere una colisión. El algoritmo simplemente "despierta" al primo base cuando el índice $k$ alcanza sus umbrales, omitiendo por completo el cálculo de raíces o divisiones continuas sobre zonas vacías (la **distancia hueca**).
---

