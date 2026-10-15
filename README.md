# Reverse engineering - Statistics

### No elijas una cuenta de fondeo por su tamaño. Analiza lo que sus reglas permiten ganar en promedio.

**Trader Estadistico** es una calculadora de probabilidades y esperanza matemática para analizar cuentas de fondeo de **prop firms**. Su enfoque es hacer **ingeniería inversa de la estructura de cada cuenta**: convertir objetivos, límites de pérdida, drawdown, costes y condiciones de retiro en un modelo que permita comparar su atractivo estadístico.

La pregunta central no es únicamente «¿puedo aprobar?», sino:

> **¿Qué cuenta ofrece la mejor esperanza matemática entre las alternativas analizadas, después de considerar la probabilidad de llegar a los retiros y el precio de intentarlo?**

Una cuenta más grande, un examen más barato o una probabilidad de aprobación más alta no garantizan, por sí solos, una mejor oportunidad. Importa cómo se combinan las reglas de evaluación, supervivencia y cobro.

## Qué significa hacer reverse engineering de una cuenta

La calculadora descompone el recorrido en cuatro fases:

1. **Aprobar la evaluación.** Alcanzar el objetivo antes de agotar el margen de pérdida.
2. **Llegar al primer retiro.** Analizar la fase fondeada y el objetivo configurado.
3. **Conseguir el segundo retiro.** Evaluar la supervivencia con el colchón disponible.
4. **Conseguir el tercer retiro.** Incorporar otra oportunidad de cobro a la cascada de probabilidades.

A partir de esa estructura estima probabilidades, retiros esperados, valor esperado neto por examen y ROI esperado. Permite explorar cómo cambian los resultados al modificar las condiciones, en lugar de depender solamente de la publicidad de una firma.

## ¿También sirve para trades aleatorios?

**Sí: el modelo permite estudiar la estructura de una cuenta incluso sin suponer una ventaja predictiva al elegir la dirección del mercado.** Utiliza un marco de juego justo y paseos aleatorios para aislar el efecto de las reglas de fondeo.

Eso permite formular una pregunta especialmente útil:

> **Si no atribuyo ninguna ventaja a mi entrada, ¿qué resultado esperado produce la estructura de esta cuenta bajo estos supuestos?**

No significa que todos los trades tengan un 50% de probabilidad de alcanzar su objetivo. Con barreras distintas de beneficio y pérdida, la estimación orientativa por fila es:

**P(objetivo antes del stop) = riesgo / (objetivo + riesgo)**

| Objetivo | Riesgo | Probabilidad modelada |
|---:|---:|---:|
| $600 | $600 | 50,0% |
| $625 | $600 | 49,0% |
| $100 | $600 | 85,7% |

La probabilidad por fila **no es una tasa de acierto histórica**. Tampoco debe multiplicarse automáticamente para obtener la probabilidad de la fase: si se puede recuperar después de un día perdedor, o si el drawdown persigue los máximos, el análisis es diferente.

**Operar al azar no garantiza rentabilidad.** Las conclusiones dependen del modelo y pueden cambiar con comisiones, spread, slippage, restricciones operativas y ejecución real.

## Qué puedes explorar

- **Cuentas y parámetros editables:** precio de evaluación, objetivo, drawdown, importe de retiro, split y condiciones configurables.
- **Distintos tipos de drawdown:** estático, trailing al cierre del día y trailing intradía.
- **Límite de pérdida diaria (DLL)** y riesgo automático o manual.
- **Planes de objetivos diarios:** distribución automática, patrones o edición manual.
- **Probabilidad visible en cada fila**, actualizada al cambiar objetivo o riesgo.
- **Simulaciones de supervivencia** para contrastar la estrategia configurada.
- **Esperanza matemática y ROI**, combinando las probabilidades de las fases.
- **Análisis de cobertura con capital real**, como herramienta exploratoria sujeta a las reglas y riesgos aplicables.

## Cómo se calcula la esperanza matemática

En la configuración que incluye aprobar la evaluación, las probabilidades acumuladas de cobro son:

- Primer retiro: P(evaluación) × P(primer retiro).
- Segundo retiro: probabilidad acumulada anterior × P(segundo retiro).
- Tercer retiro: probabilidad acumulada anterior × P(tercer retiro).

La calculadora pondera cada retiro por su probabilidad acumulada y aplica el split configurado:

**EV bruto = suma de los tres retiros ponderados por su probabilidad**

**EV neto = EV bruto − precio del examen**

**ROI esperado = EV neto / precio del examen × 100**, cuando el precio es mayor que cero.

También permite analizar los retiros condicionados a estar ya fondeado, sin multiplicar por la probabilidad de aprobación.

Un EV positivo es un **resultado teórico del modelo**, no una promesa de cobro. Esta versión considera hasta tres retiros y descuenta el precio del examen; no debe interpretarse como una contabilidad completa de suscripciones, activaciones, resets, comisiones o todos los costes de operar.

## Cómo buscar la mejor cuenta para tu análisis

1. Selecciona un preset o adapta sus parámetros a la cuenta que quieras estudiar.
2. Verifica las reglas y precios actuales directamente con la prop firm.
3. Ajusta el objetivo, el riesgo, los retiros y el plan diario.
4. Revisa tanto la probabilidad de aprobación como la de llegar a cobrar.
5. Compara la esperanza neta y el ROI usando supuestos equivalentes.
6. Cambia los parámetros para comprobar qué tan sensible es el resultado.

**La mejor cuenta es la que ofrece la mejor combinación de esperanza matemática, riesgo y condiciones entre las que hayas modelado.** El proyecto no consulta automáticamente todas las firmas del mercado ni mantiene un ranking actualizado en tiempo real. Los presets son puntos de partida, no una certificación de las reglas vigentes de cada empresa; algunas condiciones específicas pueden quedar fuera del modelo.

## Empezar a usarla

Descarga o clona el repositorio, conserva los archivos en la misma carpeta y abre **index.html** en tu navegador.

- No requiere instalación, servidor ni claves API.
- Los cálculos se ejecutan en el navegador.
- Las fuentes de Google requieren conexión; sin ella se utilizan fuentes alternativas.
- El enlace **Presentacion** abre la presentación en otra pestaña.

## Archivos

| Archivo | Contenido |
|---|---|
| index.html | Calculadora, estilos y lógica de análisis. |
| presentacion.html | Presentación explicativa original. Sus cifras son ilustrativas y no se sincronizan con la calculadora. |
| trader-estadistico-logo.png | Identidad visual de Trader Estadistico. |

Este repositorio es una copia independiente de la calculadora. Los cambios posteriores en la aplicación de origen no se sincronizan automáticamente.

## Alcance y responsabilidad

Herramienta educativa y de análisis estadístico. **No ofrece asesoramiento financiero, señales de entrada ni garantías de rentabilidad.** Un resultado esperado favorable no elimina las pérdidas, la variabilidad, el riesgo de ruina ni el riesgo de contraparte. Verifica siempre las condiciones de cada firma y si la estrategia o cobertura considerada está permitida.

---

**Menos intuición sobre la oferta. Más análisis de la estructura, las probabilidades y el valor esperado.**
