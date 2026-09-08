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
  ingeniería registra 28 defectos encontrados y corregidos, numerados uno a uno.
  Un portafolio que solo enseña victorias no dice nada.
- **Toda cifra traza a una prueba.** Si un número aparece en un documento, sale
  de un test, de una fila del libro de verificación o de un test de dbt.
- **Las decisiones se escriben antes que el código.** Dieciséis ADR en el
  repositorio de investigación, cada uno con el supuesto que lo mata si falla.

### Qué busco

Roles remotos de Finance Data Analyst, Analytics Engineer y FP&A con
automatización — donde el criterio financiero y la ingeniería de datos se paguen
como una sola capacidad y no como dos mitades. También consultoría. Respondo en
español e inglés.

[LinkedIn](https://linkedin.com/in/davirson-novoa-ramirez-2721641b5) · davinsonnovoaramirez@gmail.com
