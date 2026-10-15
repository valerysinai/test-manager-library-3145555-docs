# Seguimiento API y React · 14 de octubre de 2026

Esta foto conserva las primeras revisiones de cierre. Las fusiones posteriores, la paginación
corregida, C-08 concurrente, las mediciones con API final y T-23 están en el
[cierre actualizado de los seis repositorios](cierre-repositorios.md).

Actualiza el estado de implementación sin cambiar historias, criterios, reglas, entidades ni contrato.
El [registro anterior](registro-sdd.md) y las revisiones conservan su foto histórica; sus pendientes
deben leerse junto a esta evidencia posterior. Base de docs main 16cba02.

## API

Base main b2fa106: T-01 a T-08 fusionados. Avance feature/api-completion, implementación c4e3d8c,
evidencia 590a012, pendiente de PR/fusión. El [plan previo](https://github.com/valerysinai/test-manager-library-3145555-api/blob/10c9b1b/evidence/api-completion-plan.md)
precede al código. La [evidencia de T-09 a T-19](https://github.com/valerysinai/test-manager-library-3145555-api/blob/590a012/evidence/api-completion.md)
relaciona cada tarea, sus pruebas y sus límites.

| Ejecución sobre c4e3d8c | Resultado consultado | Alcance |
|---|---|---|
| [Bootstrap](https://github.com/valerysinai/test-manager-library-3145555-api/actions/runs/38637457502) | Éxito | Núcleo, casos de uso, arquitectura, seguridad/disco y composición |
| [Schema](https://github.com/valerysinai/test-manager-library-3145555-api/actions/runs/38637457471) | Éxito | PostgreSQL 16, contrato HTTP, concurrencia, arranque, TLS, portadas 2/3 MB e INSERT inválidos por psql |
| [Quality](https://github.com/valerysinai/test-manager-library-3145555-api/actions/runs/38637457824) | Éxito | Patrones de secretos versionados y ejemplos sintéticos, sin valores en salida |

T-09/10/11 tienen fakes y persistencia/HTTP; T-12/13 usan PostgreSQL real. Se comprobaron los tres
protocolos concurrentes: último ejemplar 201/409, devolución 200/409 con un único incremento y
límite global por socio 201/422. T-14/15 usan Argon2id, JWT HS256, Clock y disco reales. T-16 recorre
rutas/códigos y permisos antes de entrada/existencia; T-17 verifica composición y login tras
migraciones explícitas de base vacía. T-18 añade ocho CHECK a la inicial: nueve en total, con
escrituras inválidas rechazadas y reversa/reaplicación. T-19 verifica límites y casos negativos
mediante la adaptación PHP de las herramientas de referencia.

Las marcas de §4 en ambas copias de data-model.md se actualizan a motor sobre esa ejecución
Laravel. No se añaden nuevas invariantes. public.migrations sigue siendo metadata plural fuera
de las seis entidades singulares; no se renombra.

Los hallazgos SDD-02/03/04/09/10 tienen correcciones y evidencia posterior en API: separación de
alcances de autorización, control de secretos, límites de dependencias/composición, fechas con
NUL y frontera decimal de portada. La comprobación estática y los recorridos ejecutados no
certifican ausencia de cualquier defecto o secreto posible.

## React

Base main 07d7b54. Rama feature/app-library. [Plan previo](https://github.com/valerysinai/test-manager-library-3145555-app/blob/3def570/evidence/t-22-plan.md)
publicado antes del código. [Evidencia](https://github.com/valerysinai/test-manager-library-3145555-app/blob/4ef90a1/evidence/t-22.md)
de once pruebas locales de cliente/interfaz y build correcto con Node 26.5/npm 11.17.
La [CI de React con once pruebas](https://github.com/valerysinai/test-manager-library-3145555-app/actions/runs/38639516506)
pasó sobre 4ef90a1 con compilación y control de patrones de secretos. La rama incorpora después
formato de código sin cambios funcionales; su resultado final se consulta en el PR.

Se implementan login, permisos, catálogo, socios, préstamo/devolución, vencidos, reporte y alta
de bibliotecarios. Token solo en memoria, contraseña sin recortar, HTTPS requerido, URLs de
portadas revocadas y validación definitiva en servidor. Sin nuevas entidades/operaciones de producto.

La foto inicial de T-22 tenía implementación/pruebas simuladas y aceptación integrada pendiente.
El navegador integrado no conectó al servidor local en esa revisión. La ejecución posterior de
Chromium real y la inspección de capturas se registran a continuación; no se atribuyen a los mocks.

## Verificación integrada posterior

Infra feature/infra-library b496573 contiene [evidencia T-20](https://github.com/valerysinai/test-manager-library-3145555-infra/blob/b496573/evidence/t-20.md).
Su plan 3fa9132 precede a Compose. La
[CI sobre 05483c3](https://github.com/valerysinai/test-manager-library-3145555-infra/actions/runs/38644922242)
pasó con API 590a012 y React 47a517d: base vacía antes de migrar, esquema propiedad de API,
HTTPS confiable, recorrido de navegador real y persistencia tras recrear contenedores.
La ejecución local también pasó. Se revisaron capturas de catálogo a 1440×1000 y viewport 390×844,
sin desbordamiento horizontal; no se atribuye esa revisión a todas las pantallas.

El navegador real detectó un fallo de identificación de etiquetas select que no demostraban los
mocks. Se corrigió label/htmlFor en React y su
[CI independiente](https://github.com/valerysinai/test-manager-library-3145555-app/actions/runs/38644082451)
pasó. En la fixture se corrigieron espera de navegación del reporte y conexión TLS nueva tras
recrear gateway. Se conserva el producto; las correcciones no se disfrazan como nuevas funciones.

## Estado del sistema tras esa verificación

| Tarea/requisito | Evidencia siguiente |
|---|---|
| T-20 / RNF-5 | Evidencia ejecutable disponible en infra; pendiente revisión/fusión, configuración/certificados se preparan antes del comando de arranque |
| T-21 / RNF-1 | tool: datos por API, tres líneas vencidas, reporte y medición con 5.000 libros |
| T-22 | Recorrido automatizado real y capturas del catálogo verificados; demostración manual en feria y revisión completa de pantallas/accesibilidad pendientes |
| T-23 | page: presentación estática independiente de API |

La aprobación de los PR y la evidencia integrada siguen separadas de una suite verde.
Se conserva el corte de las 11:00 a. m. America/Bogota. Los avances aquí citados son posteriores;
este seguimiento no cambia elegibilidad ni certifica la entrega completa.
