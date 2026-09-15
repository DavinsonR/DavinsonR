## Davirson Novoa Ramírez

*[Read in English](README.md)*

**Economista y consultor FP&A que construye la infraestructura de datos él mismo.
Leo un P&L y construyo el pipeline que lo alimenta.**

Tres años dentro de finanzas corporativas —tesorería, facturación y FP&A— para
operaciones en más de 15 países de América. Maestría en Economía en la Pontificia
Universidad Javeriana: tesis radicada en agosto de 2026, grado previsto para
noviembre de 2026.

Bogotá · GMT-5 · solapamiento completo con horario de EE. UU. · abierto a roles remotos

**[proyecto-davirson-git.vercel.app](https://proyecto-davirson-git.vercel.app)**

---

### Riesgo de crédito con gobierno de modelos
[`credit-risk-mlops`](https://github.com/DavinsonR/credit-risk-mlops)

Un sistema de decisión crediticia sobre datos públicos reales de EE. UU. —1,96
millones de préstamos SBA 7(a) y 62,4 millones de solicitudes HMDA—. El modelo no
es el punto. El punto es que sobrevive una auditoría, y que la auditoría la corrí
primero contra mí mismo.

**Mi primer número honesto fue uno que borré.** El chequeo de señal devolvió AUC
0,9461, que no es un modelo de crédito: es una fuga. `TermInMonths` se sobrescribe
cuando el préstamo se liquida, así que el campo cargaba el resultado. Quitarlo
baja la ablación a 0,6621. Producción queda en **0,7005**, +0,0311 sobre un
scorecard WoE interpretable, con error de calibración 0,0107.

**Diez gates de promoción, y uno de ellos bloquea mi propio modelo.** El modelo de
acceso tiene una razón de impacto dispar de **0,7639** contra un umbral de 0,80,
así que no se promueve — y no bajé el umbral. Cada umbral tiene su derivación
escrita al lado, y dos de los gates existen porque los documentos de gobierno
mentían: el model card listaba 7 gates de 8, omitiendo justamente el único que el
modelo no cumple, mientras el reporte de validación imprimía PASA para ese mismo
gate en una sección y "promoción bloqueada" en otra.

**Rechazar el 10% más riesgoso habría evitado $276,3M** en charge-offs, 2,15x lo
que logra rechazar al azar, y $942,1M de la pérdida realizada del período los
absorbió el contribuyente vía la garantía. También renuncia a **$1.990M de volumen
sano** —7,2x la pérdida evitada— y los dos números viajan en el mismo payload. Un
titular que muestra solo el numerador no es un titular.

**Un charge-off tarda una mediana de 51 meses en aparecer**, así que monitorear
desempeño en cosechas jóvenes es aritmética y no medición, y el proyecto se niega
a fingirlo. Lo que sí monitorea encontró algo: el SBA cambió el esquema de
categorías de `business_age` entre FY2018 y FY2021, y hoy el **84% de sus valores
cae en categorías que el modelo nunca vio**. El serving las manda a "desconocido",
así que el modelo no se degrada: pierde una variable del top tres entera y sigue
respondiendo con el mismo aplomo.

**En lo causal publiqué una no-identificación, no un efecto.** El porcentaje de
garantía es la única palanca que la SBA controla de verdad, y está determinada
administrativamente: R² 0,9145 contra celdas de método de procesamiento × tamaño
del préstamo, así que no queda solapamiento que explotar. En el umbral estatutario
de $150.000, el 83,1% de la ventana de ±$5k está exactamente en $150.000 —la
densidad está destruida, y con ella la regresión discontinua—. Condicionar por
tamaño quita el 38% del gradiente crudo y deja un residual cuyo signo es el que
predice la selección adversa. Un estimador aplicado donde sus supuestos no se
cumplen produce un número, no una estimación.

Validación out-of-time cruzando el shock COVID · en un régimen tipo 2007 el mismo
modelo cae a AUC 0,5456 y subestima el riesgo ocho veces, que es un entregable y
no una salvedad · 13 registros de decisión de arquitectura · `make reproduce`
asserta que las métricas publicadas son idénticas tras reentrenar · CI estuvo rojo
ocho commits seguidos antes de que lo notara, y el arreglo fue un script que
reproduce CI en local antes de empujar.

`Python` `LightGBM` `PyTorch` `DuckDB` `PySpark` `MLflow` `ONNX` `FastAPI` `Power BI`

---

### Inclusión financiera y crecimiento regional en Colombia
[`financial-inclusion-colombia`](https://github.com/DavinsonR/financial-inclusion-colombia) · [ver el atlas](https://proyecto-davirson-git.vercel.app/es/research/fintech-inclusion)

Pregunté si la inclusión financiera predice el crecimiento de los departamentos
de Colombia.

**No lo predice** — β = 0,0007, p = 0,90, con efectos fijos de entidad y tiempo
sobre 33 departamentos, 2019 a 2025, N = 228. Bootstrap salvaje por clúster
p = 0,89, placebo por permutación p = 0,68. Sin efectos de tiempo el mismo
coeficiente vale +0,024 con p < 0,001, y esa distancia es exactamente lo que
valía la tendencia nacional.

Publiqué el resultado con su especificación, su N, sus clústeres y sus pruebas.
También publiqué lo que salió mal: la adecuación muestral dio KMO 0,314 en acceso
y 0,404 en uso, por debajo del 0,5 que necesita un modelo factorial, así que se
descartó el PCA previsto. Forzarlo producía pesos implícitos negativos en
microcrédito — un índice que dice que más crédito es menos inclusión.

Diecinueve fuentes públicas con manifiesto sha256 · cada serie resuelta a código
municipal, 100 % de cobertura en los 34 cortes trimestrales · índice por dimensión
con pesos congelados y publicados · dos paneles anuales · atlas de los 1.123
municipios · batería completa contra la correlación espuria (CIPS, CCE, placebo
por permutación, shift-share, estudio de eventos, Moran, SAR/SDM).

`Python` `dbt` `DuckDB` `linearmodels` `Quarto` `BigQuery`

---

### Plataforma de datos de mercado
[`market-data-medallion`](https://github.com/DavinsonR/market-data-medallion) · [ver el laboratorio](https://proyecto-davirson-git.vercel.app/es/projects/trading-sim)

APIs públicas hacia un warehouse PostgreSQL con arquitectura medallion en dbt, un
motor de backtesting honesto encima, y un refresh diario en GitHub Actions que se
mantiene vivo sin servidor. 48 activos, más de 58.000 velas diarias, presupuesto cero.

**De 1.392 variantes de estrategia evaluadas, apenas una de cada ocho ganadoras
dentro de muestra sobrevivió a la validación fuera de muestra.** Publiqué todas
las que no. Las 42 variantes que combinan cinco señales a la vez ganaron cero
veces: más grados de libertad no es más señal, es más sitio donde esconder el ruido.

Una señal calculada en el cierre del día *t* ejecuta en la apertura del día *t+1*,
nunca en el cierre que la produjo, y un test de regresión comprueba que cortar el
futuro no cambia las señales pasadas. Comisiones y deslizamiento siempre puestos,
y el comprar y mantener paga lo mismo. 89 pruebas de calidad en dbt y 171 pruebas
unitarias en Python corren antes de publicar una sola cifra.

`Python` `dbt` `PostgreSQL` `pandera` `GitHub Actions` `Power BI`

---

### JARVIS — registro diario
[demo público, sin cuenta](https://jarvis-app-psi-sable.vercel.app/demo) · repositorio privado

El día completo —hábitos, cuerpo, sueño, alimentación, gasto— registrado en menos
de noventa segundos y con una mano, devuelto leído y no en crudo.

La mitad de la gente que empieza una app de seguimiento la abandona en el primer
mes, así que el diseño apunta a modos concretos de fallar: un hueco no es un
fallo, un hábito dominado se gradúa en vez de contarse como abandono, nada se
interpola y ninguna barra de progreso apunta a un peso objetivo. Un modelo de
datos de finanzas personales más seguimiento de salud sobre Postgres con RLS:
35 tablas, 22 vistas, unas 370 pruebas y un smoke test de RLS en CI.

`Next.js` `TypeScript` `Supabase` `RLS` `PWA`

---

### Cómo trabajo

- **Publico lo que no funcionó.** El resultado nulo, el KMO por debajo del
  umbral, la fuga de datos que encontré en mi propia app. La bitácora de
  ingeniería registra 28 defectos encontrados y corregidos, numerados uno a uno, y
  el repositorio de riesgo de crédito lleva el suyo propio — incluidos dos números
  publicados que tuve que retractar porque no replicaron en otra máquina, y una
  afirmación que repetí cuatro veces antes de medirla y encontrarla falsa. Un
  portafolio que solo enseña victorias no dice nada.
- **Toda cifra traza a una prueba.** Si un número aparece en un documento, sale
  de un test, de una fila del libro de verificación o de un test de dbt. En el
  repositorio de riesgo de crédito el gate tampoco le cree al artefacto: recomputa
  las métricas publicadas desde las predicciones guardadas antes de permitir que
  algo se promueva.
- **Las decisiones se escriben antes que el código.** Dieciséis ADR en el
  repositorio de investigación y trece en el de riesgo de crédito, cada uno con el
  supuesto que lo mata si falla.
- **Un control que no puede fallar no es un control.** Tres de los defectos que
  encontré en mi propio tooling reportaban éxito sin hacer nada: un verificador de
  cumplimiento que no detectaba nada, un hook que aceptaba justo lo que existía
  para rechazar, y una tubería que imprimía "aprobado" después de que el
  entrenamiento reventara. Cada uno tiene hoy un test que falla en el entorno
  donde antes pasaba en silencio.

### Qué busco

Roles remotos de Finance Data Analyst, Analytics Engineer y FP&A con
automatización — donde el criterio financiero y la ingeniería de datos se paguen
como una sola capacidad y no como dos mitades. También consultoría. Respondo en
español e inglés.

[LinkedIn](https://linkedin.com/in/davirson-novoa-ramirez-2721641b5) · davinsonnovoaramirez@gmail.com
