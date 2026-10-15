# Resultado de aceptación ampliada y preparación de la evaluación

Esta etapa sigue al [plan previo](plan-aceptacion-final.md) `85449ba`. Se confirmó que los seis
forks integraron el cierre anterior: API 60bbcdd, App b5ef195, Infra f694448, Tool e4101e6,
Page 1578211 y Docs eba3a91. La nueva revisión de pantallas encontró un defecto de presentación;
las tres ramas de esta etapa siguen pendientes de revisión/fusión.

## Defecto reproducido y corrección preparada

La aceptación real encontró contraste insuficiente en 34 vistas de App b5ef195. El informe
anterior se conserva, con 227 observaciones repetidas por clase/estado. Teclado, ancho del
documento y nombres de controles pasaban; el contraste no se marcó como aprobado.
App publicó un plan antes de oscurecer diez colores en a9b74f9. Se mantienen diseño, layout,
texto, reglas, entidades, rutas y dependencias. No se modifica el negocio para aprobar la revisión.

## Resultado local posterior

Con API main 60bbcdd, App a9b74f9 e Infra/verificador 7f6ee24:

- 18 estados normales × 2 tamaños = 36 vistas, incluidos formularios, login, errores y vacíos.
- 3 estados de vencidos × 2 tamaños = 6 vistas: listado real, bloqueo y devolución.
- Cero observaciones de contraste del detector, controles sin nombre o ancho de documento excedido.
- Foco/enlace de salto, Tab/Enter y último enlace del menú alcanzable a 390 y 1440 px.
- Diez tablas/vistas con desplazamiento interno comprobado alcanzable; no se ocultan esas columnas.
- HTTPS confiable, roles, portada privada y reporte con API/PostgreSQL reales.
- Cambio de reloj solo en API demo, nuevo login y rechazo del token anterior, conforme a C-04.
- Préstamo a socio vencido rechazado con 409 MEMBER_HAS_OVERDUE; devolución desde UI elimina la fila.
- Datos, préstamo cerrado, stock y bytes de portada conservados tras recrear contenedores.
- Finalización con salida 0 y limpieza únicamente del proyecto de pruebas generado.

Se inspeccionaron muestras visuales de login, alta, detalle, error de socio, préstamo cerrado,
reporte y vencidos/bloqueo. La cobertura automática es mayor que esas muestras visuales.
La revisión de contraste toma los colores computados y los fondos reales; sus criterios se apoyan
en [W3C: contraste](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html) y
[foco visible](https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html). No certifica
WCAG completa ni todos los navegadores/lectores de pantalla. La prueba anterior tenía 34 vistas;
la posterior amplió cobertura a 42, por lo que no se describen como conjuntos idénticos.

## Evidencia publicada

- [App: corrección y comprobación de contraste](https://github.com/valerysinai/test-manager-library-3145555-app/blob/09b108f/evidence/text-contrast.md).
- [Infra: aceptación ampliada e informes conservados](https://github.com/valerysinai/test-manager-library-3145555-infra/blob/a7b3798/evidence/final-acceptance.md).
- [CI de App sobre a9b74f9](https://github.com/valerysinai/test-manager-library-3145555-app/actions/runs/38674670975).
- [CI de Infra sobre 7f6ee24](https://github.com/valerysinai/test-manager-library-3145555-infra/actions/runs/38675186829).

Las revisiones posteriores de evidencia y README no cambian el código probado. Estas ejecuciones
son comprobaciones automatizadas, no constancias de presentación humana.

## Presentación humana preparada, todavía no certificada

La [guía de demostración](guia-demostracion.md) incluye configuración según los README, el
recorrido por rol, casos de negocio y errores, preparación de tres vencidos mediante tool/C-04,
teclado, revisión móvil y defensa SDD. Tiene un registro humano sin completar: el agente no
firma ni marca una presentación que debe realizar la persona ante el evaluador.

La corrección App, el verificador Infra y estos documentos se entregan en PR separados. Después
de integrarlos, queda ejecutar la presentación humana y entregar los enlaces/evidencias por el
medio indicado. No hay otro repositorio ni función de producto prevista por esta revisión.
El plazo original y la decisión del evaluador sobre avances posteriores no se modifican.
