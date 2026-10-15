# Plan previo de actualización del cierre

Se continúa `feature/docs-api-completion`, derivada de main `16cba02`, conservando la revisión
pendiente `8e62f0f`. Este documento precede a la actualización de estados de esta etapa.

## Fuentes y límites

Se consultan README, constitución, contrato, modelo, tasks en ambas versiones, decisiones C-01
a C-10, auditorías y registros. Los textos históricos mantienen su fecha y contexto; un seguimiento
nuevo enlaza ejecuciones por revisión y distingue explícitamente publicado/fusionado/verificado.
La estructura del producto, sus seis entidades y las diferencias singular/plural se conservan.

## Comprobaciones preparadas

1. Consultar origin/main de los seis forks y contrastar ascendencia de las revisiones entregadas.
2. Registrar API fusionada `60bbcdd`, sus 200 pruebas y la corrección de paginación; vincular la
   evidencia nueva de C-08, TLS, demo C-04 y medición completa C-07 sobre API `68b41b0`.
3. Contrastar App: main `77401f2` no contiene las etiquetas `47a517d`; conservar estado pendiente
   de fusión y registrar sus pruebas nuevas y la integración real únicamente después de ejecutarlas.
4. Citar T-20, T-21/RNF-1 y T-23 en las revisiones verificadas de infra/tool/page, sin atribuir a sus
   main actuales una prueba que usó otra fuente. Consultar estados de CI y fijar sus enlaces.
5. Publicar una foto actual en cierre-repositorios.md y enlazarla desde README/registros, sin
   reescribir las matrices históricas. Las marcas motor del modelo quedan respaldadas por API.
6. Validar referencias locales y equivalencia de spec, api-contract y data-model en ambas copias;
   no modificar requisitos ni promover a terminado lo que solo tiene análisis o mocks.

No se certifica el recorrido manual de feria ni accesibilidad completa. Los avances posteriores
al corte original no alteran su elegibilidad. Los PR quedan para revisión y fusión por la usuaria,
en inglés y dentro de sus forks. No se envían mensajes a terceros ni se realiza publicación externa.
