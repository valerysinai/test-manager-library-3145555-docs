# Cierre verificado de los seis repositorios

Foto consultada el 15 de octubre de 2026 UTC (14 de octubre en America/Bogota).
El [plan de actualización](cierre-repositorios-plan.md), publicado en `b7d11b8`, precede a esta
foto. Se conserva main de docs `16cba02` como base de `feature/docs-api-completion`.
El registro inicial y el seguimiento API/React mantienen su cronología; este archivo actualiza
los estados sin atribuir resultados nuevos a revisiones antiguas.

## Publicado, fusionado y ejecutado

Se consultó `origin/main` de los seis forks, con checkouts sin cambios de producto pendientes.

| Repositorio | Main remoto observado | Estado de integración y evidencia |
|---|---|---|
| docs | `16cba02915125c1bb601343c6c7b11df914ec200` | Este cierre y las marcas verificadas del modelo siguen en `feature/docs-api-completion`, pendientes de PR/fusión |
| api | `60bbcdd8c45637d426455d4e24b028ea1af76157` | PR #6 fusionado; contiene el cierre `36a9f73`, corrección de paginación y cobertura C-08 |
| app | `77401f21ab595c016e5b49f6a59ebc8a3851cd00` | Implementación inicial fusionada; etiquetas `47a517d`, regresiones `88b20a9` y evidencia final `c94e5b0` pendientes de integrar |
| infra | `f694448a13b6851e10488353ce38c582677ad75c` | PR #1 fusionado; incluye la infraestructura verificada y el runner T-20 |
| tool | `e4101e63e8acdbbfcddf22573d2f992748fd5397` | PR #1 fusionado; contiene demo C-04 y medición C-07 con resultados íntegros |
| page | `15782114b232ff521704cba7de96fc32d04bb71c` | PR #1 fusionado; presentación estática React con evidencia T-23 |

Esta tabla fecha una consulta, no predice fusiones posteriores. Una suite verde o una rama
publicada no equivale a estar en main. El siguiente paso de integración son los PR de App y Docs;
no falta iniciar un séptimo repositorio ni otra función del producto.

## API · T-01 a T-19 y reglas del negocio

La [revisión final](https://github.com/valerysinai/test-manager-library-3145555-api/blob/36a9f73/evidence/api-final-review.md)
identifica planes previos, pruebas y correcciones. Sobre `68b41b0` pasaron localmente 172 pruebas
de núcleo y 28 de integración, con PostgreSQL 16 real, más cinco del detector de secretos.

| CI sobre 68b41b0 | Resultado | Alcance |
|---|---|---|
| [API bootstrap](https://github.com/valerysinai/test-manager-library-3145555-api/actions/runs/38671283487) | Éxito | Dominio, aplicación, arquitectura, adaptadores, composición y salud sin base |
| [API schema](https://github.com/valerysinai/test-manager-library-3145555-api/actions/runs/38671283430) | Éxito | HTTP, PostgreSQL, concurrencia, esquema, HTTPS real y rechazo de INSERT por psql |
| [API quality](https://github.com/valerysinai/test-manager-library-3145555-api/actions/runs/38671283428) | Éxito | Dependencias y patrones de secretos versionados |

La regresión de paginación falló primero en seis escenarios contra el motor. Se corrigió el
desbordamiento del offset de libros/socios/préstamos sin imponer un límite de página nuevo:
una página posterior al final devuelve 200, items vacío y total real. Se conserva la
[CI fallida previa](https://github.com/valerysinai/test-manager-library-3145555-api/actions/runs/38671009543).

C-08 cuenta ahora con dos bibliotecarios/procesos concurrentes creando el mismo documento:
201/409 `DOCUMENT_TAKEN` y un único socio. Se mantienen los otros tres protocolos de concurrencia:
último ejemplar, límite global por socio y devolución con un único incremento de stock.

Las nueve CHECK y el resto del modelo se comprobaron por introspección, escrituras inválidas,
reversa y reaplicación de migraciones. Las marcas motor de §4 en ambas copias del modelo reflejan
esa adaptación Laravel; no afirman instalaciones Python/.NET. Se conservan las seis tablas
singulares y `public.migrations` como metadata plural fuera del modelo. No se renombra nada.

## App e Infra · recorrido automatizado real

La [revisión final de App](https://github.com/valerysinai/test-manager-library-3145555-app/blob/c94e5b0/evidence/app-final-review.md)
documenta el cierre pendiente de fusión. Su
[CI sobre 88b20a9](https://github.com/valerysinai/test-manager-library-3145555-app/actions/runs/38672884000)
pasó con trece pruebas y build. Los casos DOM/API simulada incluyen dos regresiones de etiquetas
exactas, IDs distintos, asociación estable y foco; esos resultados no se atribuyen a Chromium.

Se repitió localmente el runner de infra main `f694448`, usando App `88b20a9` y API main `60bbcdd`.
El proyecto generado `library-check-1792032478675-b0c83510` terminó con salida 0 y limpieza.
Se verificaron motor vacío antes de migrar, HTTPS confiable y navegador real: login admin,
libro/portada, socio, préstamo/devolución, reporte 200 con una fila y alta/login de bibliotecario.
Se comprobaron permisos visibles, ausencia de errores JavaScript y disposición sin desbordamiento
horizontal en viewport 390×844. Las capturas de catálogo de móvil y escritorio se inspeccionaron.
Tras recrear contenedores se conservaron datos, préstamo cerrado, stock y bytes de portada.

El [runner y evidencia T-20](https://github.com/valerysinai/test-manager-library-3145555-infra/blob/b496573/evidence/t-20.md)
permiten reproducirlo. La
[CI inicial integrada](https://github.com/valerysinai/test-manager-library-3145555-infra/actions/runs/38644922242)
pasó con las revisiones anteriores que identifica ese informe; no se le atribuye esta ejecución
local nueva. La configuración y los certificados se preparan antes del comando de arranque.

## Tool · T-21 y RNF-1

El [plan y resultado original de tool](https://github.com/valerysinai/test-manager-library-3145555-tool/blob/e494a3a/evidence/t-21.md)
conservan su orden SDD y revisiones. La
[CI de tool](https://github.com/valerysinai/test-manager-library-3145555-tool/actions/runs/38667706097)
pasó en su entorno con API `590a012`.

La revisión final de API repitió ambos escenarios con tool `e494a3a`, API corregida `68b41b0`
e infra `b496573`. El [resumen demo](https://github.com/valerysinai/test-manager-library-3145555-api/blob/36a9f73/evidence/api-final-demo.json)
confirma 40 libros, 10 socios, 15 préstamos y exactamente tres líneas vencidas; token anterior
rechazado al cambiar solo el reloj de API y login nuevo. Todo el negocio entra por HTTPS, sin SQL,
fechas de préstamo de entrada ni endpoints añadidos.

El [reporte íntegro posterior](https://github.com/valerysinai/test-manager-library-3145555-api/blob/36a9f73/evidence/api-final-benchmark.json)
documenta otra base normal de 5.000 libros: cuatro consultas, 80 warmups excluidos, 400 medidas
y diagnóstico de diez clientes. Todas las 400 respuestas fueron válidas y estrictamente menores
de 300 ms: máximo 70,5113 ms, mediana 36,29535 ms y p95 50,0072 ms. Se conservan tiempos, estados,
consultas, commits, CPU/RAM y ubicación; no se sustituyó el criterio por p95 ni se descartaron
muestras. Pasa RNF-1 en ese entorno, sin prometer latencia en cualquier equipo.

## Page · T-23

La [evidencia de page](https://github.com/valerysinai/test-manager-library-3145555-page/blob/31523d6/evidence/t-23.md)
incluye plan previo, capturas y comandos. La
[CI sobre 752ecb0](https://github.com/valerysinai/test-manager-library-3145555-page/actions/runs/38669984762)
pasó. React genera HTML/CSS/SVG estáticos; Chromium los abrió bajo subruta, sin API, red exterior
ni JavaScript del sitio. Se comprobaron 320, 390, 768 y 1440 px, navegación, foco y contraste
de textos; las capturas se inspeccionaron. No se acredita una publicación en hosting.

## Cierre del proceso y pendientes reales

Se conservan producto, contrato, nombres, tecnología React/Laravel y propiedad de migraciones.
La validación documental detectó dos ejemplos DATABASE_URL con credenciales incrustadas en los
planes de referencia. El hallazgo se registró antes de sustituir ambos por instrucciones de entorno,
sin publicar sus valores, cambiar la obligatoriedad ni añadir excepciones al detector. El escaneo
del checkout final pasa; no se presenta como una revisión de todos los secretos de la historia Git.
Cada evidencia distingue lectura previa, implementación, pruebas simuladas, integración y fusión.
SDD-02/03/04/09/10 tienen correcciones y pruebas en API; las auditorías anteriores conservan su
fecha y pendientes de entonces. No se afirma haber identificado una supuesta trampa intencional.

Quedan la revisión/fusión de App y Docs, el recorrido manual en feria exigido por T-22 y una
revisión más amplia de todas las pantallas/tecnologías de asistencia. Una suite verde no certifica
perfección ni cumplimiento manual completo. El corte original de las 11:00 a. m. se conserva;
estos avances posteriores no modifican elegibilidad. Este cierre tampoco fusiona PR por la usuaria.

Las [comprobaciones documentales de cierre](verificacion-sdd.md#cierre-posterior-de-los-seis-repositorios)
registran alcance, resultados y reproducción del control.
