## Davirson Novoa Ramírez

**Economista y consultor FP&A que construye la infraestructura de datos él mismo.
Leo un P&L y construyo el pipeline que lo alimenta.**

Tres años dentro de finanzas corporativas —tesorería, facturación y FP&A— para
operaciones en más de 15 países de América. Maestría en Economía en la
Pontificia Universidad Javeriana; tesis radicada, grado previsto para
noviembre de 2026.

**[proyecto-davirson-git.vercel.app](https://proyecto-davirson-git.vercel.app)**

---

### Inclusión financiera y crecimiento regional en Colombia
[`financial-inclusion-colombia`](https://github.com/DavinsonR/financial-inclusion-colombia) · [ver el atlas](https://proyecto-davirson-git.vercel.app/es/research/fintech-inclusion)

Pregunté si la inclusión financiera predice el crecimiento de los departamentos.
**No lo predice** — β = 0,0007, p = 0,90, con efectos fijos de entidad y tiempo.
Sin efectos de tiempo el mismo coeficiente vale +0,024 con p < 0,001: esa
distancia es lo que valía la tendencia nacional.

El resultado se publica con su especificación, su N, sus clústeres y sus
pruebas. También se publica el KMO de 0,314 que obligó a descartar PCA.

Warehouse de 19 fuentes públicas con manifiesto sha256 · índice por dimensiones
con pesos congelados y publicados · paneles departamental y municipal · atlas de
los 1.123 municipios · batería contra la correlación espuria (CIPS, CCE,
placebo por permutación, shift-share, estudio de eventos, Moran, SAR/SDM).

`Python` `dbt` `DuckDB` `linearmodels` `Quarto` `BigQuery`

---

### Plataforma de datos de mercado
[`market-data-medallion`](https://github.com/DavinsonR/market-data-medallion) · [ver el laboratorio](https://proyecto-davirson-git.vercel.app/es/projects/trading-sim)

APIs públicas → arquitectura medallion en Postgres con dbt → un backtester que
se niega a hacer trampa → refresh diario en GitHub Actions. 48 activos, sin
servidor y con presupuesto de cero.

La métrica que más me importa del proyecto no es el retorno: es cuántas
variantes que le ganaron al buy-and-hold en los datos con los que se
seleccionaron siguieron ganando en datos que nunca tocaron. Una señal ejecuta
en la apertura del día siguiente, nunca en el cierre que la produjo, y hay un
test de regresión que lo comprueba.

`Python` `dbt` `PostgreSQL` `pandera` `GitHub Actions` `Power BI`

---

### JARVIS — registro diario
[demo público, sin cuenta](https://jarvis-app-psi-sable.vercel.app/demo) · repositorio privado

El día completo —hábitos, cuerpo, sueño, alimentación, gasto— en menos de
noventa segundos y con una mano, devuelto leído y no en crudo.

La mitad de la gente abandona una app de seguimiento en el primer mes, así que
las decisiones de diseño apuntan a modos concretos de fallar: un hueco no es un
fallo, un hábito dominado se gradúa en vez de contarse como abandono, ningún
dato se interpola y ninguna barra de progreso apunta a un peso objetivo.

`Next.js` `TypeScript` `Supabase` `RLS` `PWA`

---

### Cómo trabajo

- **Publico lo que no me salió.** El resultado nulo, el KMO por debajo del
  umbral, la fuga de datos que encontré en mi propia app. Un portafolio que
  solo enseña victorias no dice nada.
- **Toda cifra traza a una prueba.** Si un número aparece en un documento,
  sale de un test, de una fila del libro de verificación o de un test de dbt.
- **Las decisiones se escriben antes que el código.** Dieciséis ADR en el
  repositorio de investigación, cada uno con el supuesto que lo mata si falla.

### Qué busco

Roles remotos de Finance Data Analyst, Analytics Engineer y FP&A con
automatización — donde el criterio financiero y la ingeniería de datos se
paguen como una sola capacidad y no como dos mitades. También consultoría.
Respondo en español e inglés.

[LinkedIn](https://linkedin.com/in/davirson-novoa-ramirez-2721641b5) · davinsonnovoaramirez@gmail.com
