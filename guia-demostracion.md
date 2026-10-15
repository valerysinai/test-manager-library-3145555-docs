# Guía de demostración y aceptación por la persona que presenta

Esta guía prepara T-22 sin afirmar que la presentación ante el evaluador haya ocurrido.
El [plan previo](plan-aceptacion-final.md) separa automatización, revisión visual y actuación humana.
Las casillas quedan deliberadamente sin marcar para quien haga la demostración.

## 1. Preparar el entorno

1. Revisar/fusionar los PR finales y usar las revisiones indicadas en su evidencia. Mantener
   los seis repositorios como carpetas hermanas y Docker con contenedores Linux disponible.
2. Seguir el [README de infra](https://github.com/valerysinai/test-manager-library-3145555-infra/blob/main/README.md)
   para configuración privada, certificados, arranque y confianza de la CA local. El preparador
   rechaza sobrescribir configuración: si ya existe, revisarla en lugar de regenerarla.
3. Usar una base de demostración aislada. No reutilizar una biblioteca con datos operativos.
   Las migraciones son de API y el administrador se toma del entorno, nunca de un usuario/clave
   impreso en esta guía, una URL o un archivo versionado.
4. Arrancar desde infra con `docker compose up --build -d --wait` y abrir el origen HTTPS
   configurado (por defecto `https://localhost:8443`). Validar el certificado conforme al README;
   no acreditar credenciales por HTTP ni desactivar TLS. No instalar confianza global sin decisión
   de la persona responsable del equipo.
5. Para obtener los tres vencidos, seguir las fases documentadas del
   [README de tool](https://github.com/valerysinai/test-manager-library-3145555-tool/blob/main/README.md)
   y C-04: entorno demo/Septiembre, 40 libros/10 socios/3 préstamos, recrear solo API en Octubre,
   login nuevo y otros 12 préstamos. No cambiar la fecha del equipo ni enviar loaned_at por API.
   Emplear un checkpoint nuevo y una base vacía; un avance parcial no se vuelve a ejecutar a ciegas.

`npm run verify` de infra reproduce la comprobación automatizada en otro proyecto y lo limpia
al terminar. Ese proyecto efímero no es la sesión que la persona usará para presentar.
Los datos de demostración deben ser sintéticos. No capturar login, contraseñas, tokens, headers,
archivo .env ni formularios de cuentas con credenciales introducidas.

## 2. Recorrido funcional

| Paso | Acción de la persona | Resultado que debe observar |
|---|---|---|
| Acceso | Intentar credenciales inválidas y luego entrar como admin | Error genérico; acceso válido sin revelar qué dato falló |
| Catálogo | Buscar por título/autor y categoría, probar una búsqueda sin coincidencias | Resultados paginados y total; vacío legible |
| Libro | Crear un libro sintético con ISBN de 13 dígitos y ejemplares positivos; abrir/editar | ISBN no editable; total/disponibles coherentes |
| Portada | Subir PNG/JPEG permitido y luego quitarlo | Imagen privada visible; sin portada después; no rutas de disco |
| Socios | Crear y consultar un socio sintético; intentar repetir su documento | Detalle y conteo sin devolver; duplicado rechazado sin una segunda alta |
| Préstamo | Elegir socio y de uno a tres libros distintos; intentar repetir uno en la selección | Una línea por libro; sin duplicados; vencimiento a 14 días |
| Inventario | Consultar el libro prestado e intentar darlo de baja con préstamo abierto | Descuento de un ejemplar; baja rechazada sin perder el histórico |
| Devolución | Devolver una línea y consultar otra vez | Un ejemplar repuesto; línea sin segundo botón de devolución; cerrado si no quedan pendientes |
| Vencidos | Abrir los tres vencidos preparados por tool, entrar a un préstamo y devolver | Libro/socio/instante/días visibles; desaparece la línea devuelta |
| Bloqueo | Intentar prestar a un socio que aún tenga una línea vencida | Rechazo del servidor; no se registra otro préstamo |
| Límite | Con un socio sin vencidos que tenga tres líneas abiertas, intentar otra | Rechazo del servidor; el conteo no supera tres |
| Histórico | Prestar un libro, cambiar después su título/categoría y consultar el periodo | Reporte conserva los valores congelados; sin desglose por socio u operador |
| Rango | Consultar reporte con fin anterior al inicio y luego sin préstamos en el rango | Error de rango; después vacío válido, no un error nuevo |
| Bibliotecario | Crear una cuenta librarian, cerrar sesión y entrar con ella | Sin edición de catálogo, reporte ni alta de cuentas; socios/préstamos/devoluciones disponibles |
| Sesión | Cerrar sesión y recargar | Token no conservado; vuelve al acceso sin mostrar datos de una sesión anterior |

No se crean cuentas de socios ni funciones de multas, reservas, renovaciones, correo o SMS.
Los escenarios de concurrencia y el umbral RNF-1 se acreditan con sus pruebas reales, no pulsando
rápido un botón ni mostrando una medición aislada del navegador.

## 3. Teclado y presentación

- [ ] Recorrer sin ratón los controles principales con Tab/Shift+Tab y activarlos con Enter/Espacio.
- [ ] Comprobar foco visible y enlace «Ir al contenido» sin perder la pantalla seleccionada.
- [ ] Confirmar etiquetas exactas, selects utilizables y errores legibles sin depender solo del color.
- [ ] Revisar móvil y escritorio: login, filtros, formularios, tablas, detalle, reporte y estados vacíos.
- [ ] En tablas con scroll interno, confirmar que todas las columnas y acciones son alcanzables.
- [ ] Revisar el contenido con zoom y las tecnologías de asistencia disponibles; registrar los límites.

La comprobación automática de contraste usa fondos reales y distingue texto normal/grande,
pero no certifica por sí sola WCAG ni todos los lectores de pantalla/dispositivos.

## 4. Evidencia y defensa SDD

- [ ] Identificar el requisito antes de enseñar la función y el plan publicado antes del código.
- [ ] Mostrar ejemplos de defecto reproducido y corregido: paginación, etiquetas y contraste.
- [ ] Distinguir pruebas de dominio/fakes, HTTP/motor, navegador real y revisión humana.
- [ ] Explicar separación Domain/Application/Adapters, composición única y migraciones propiedad de API.
- [ ] Explicar snapshots, estado derivado, transacción, xmin y bloqueo por socio sin renombrar entidades.
- [ ] Abrir los reportes completos de demo/RNF-1: 400 medidas, umbral por muestra, consultas y entorno.
- [ ] Entregar los seis enlaces de los forks con sus main y evidencias, sin publicar configuración privada.

## 5. Registro de la presentación humana

- Persona que presenta: ____________________
- Fecha y lugar: ____________________
- Revisiones de los repositorios: ____________________
- Escenarios completados y observaciones: ____________________
- Problemas o límites pendientes: ____________________

Este registro lo completa la persona después de ejecutar el recorrido. El agente no lo firma
ni marca por ella. La entrega original de las 11:00 a. m. se conserva: el evaluador determina
si acepta los avances posteriores; esta guía no modifica esa condición.
