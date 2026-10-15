# Verificación del PR de revisión SDD

Fecha: 14 de octubre de 2026. Base: `eab4cf729f749c67923c1615cb5f981b46c5ae39`,
main de docs al crear `feature/docs-sdd-review`.
Cambios de contenido: `a366a71` y `5422739`; el commit posterior incorpora este registro.

## Comprobaciones documentales de la primera revisión

- 31 archivos Markdown con enlaces relativos comprobados: sin destinos inexistentes.
- Los 38 criterios CA de spec.md aparecen una sola vez en la matriz del registro.
- Las 23 tareas de tasks.md tienen una fila de estado en la sección correspondiente.
- Los 6 RN y 5 RNF están incluidos una sola vez en su tabla de seguimiento.
- Los 16 nombres de métodos de prueba citados existen en el checkout de API revisado.
- Las referencias Markdown del registro están definidas y sus enlaces a archivos de API
  corresponden a objetos existentes en los commits indicados.
- Las correcciones comunes de tasks.md coinciden entre versiones. Se conserva la diferencia
  técnica de T-19: import-linter para Python y NetArchTest para .NET.
- spec.md, constitution.md, data-model.md, api-contract.md y los cuatro ADR de ambas versiones
  no cambian respecto de main.
- Las dependencias de tareas no cambian. La base común de esta rama y main es el commit
  indicado arriba.
- La comprobación de espacios del diff no encontró errores.

Se contrastaron también el main remoto y los PR existentes de API. El registro distingue
las fusiones de T-01 a T-06 de la rama T-07 publicada. Los cuatro repositorios restantes
se inspeccionaron localmente y solo contenían su README en los checkouts revisados.

## Alcance de esta verificación

Las comprobaciones validan referencias, cobertura documental de identificadores,
consistencia de las correcciones y conservación de los documentos protegidos.
No demuestran corrección completa del código ni equivalencia semántica de todas las
pruebas con el requisito. Esa revisión y las correcciones de API siguen en el plan SDD.

Los enlaces a CI conservan resultados ejecutados anteriormente. Este PR no vuelve a
ejecutar las suites de producto ni introduce cambios en API, app, infra, page o tool.
Los secretos, los límites completos de arquitectura y CA-01.3 siguen abiertos según
los hallazgos SDD-02 a SDD-04. Este PR es posterior al corte de entrega del README.

## Segunda revisión

La [segunda revisión](segunda-revision-sdd.md) añade un documento (32 Markdown en total)
y precisa la explicación del bloqueo pesimista en ambas copias de ADR-002.
Su decisión optimista permanece intacta. A diferencia de la primera revisión, ese ADR
sí tiene ahora una corrección de redacción técnica frente a main.
spec.md, constitution.md, data-model.md, api-contract.md y ADR-001/003/004 siguen sin cambios.
Los enlaces y la igualdad de los cuatro ADR entre versiones se vuelven a comprobar;
el análisis de fechas no se presenta como una prueba PHP ejecutada.

## Cierre posterior de los seis repositorios

La foto actual está en [cierre-repositorios.md](cierre-repositorios.md), preparada con plan previo
`b7d11b8` y precisión de seguridad `d0f3052`. Esta sección complementa las verificaciones históricas.

- 35 archivos Markdown comprobados: cero destinos relativos inexistentes.
- spec.md, api-contract.md, data-model.md y los cuatro ADR coinciden entre ambas referencias.
- Las estructuras del modelo, reglas, contrato, nombres y dependencias de tareas se conservan.
  En el modelo solo se actualizan estado/evidencia de restricciones ya verificadas en API.
- Se sustituyen dos ejemplos de DATABASE_URL con credenciales incrustadas por instrucciones de
  entorno. Solo cambia el ejemplo de configuración de esa fila en cada plan; no el requisito.
- El escáner de patrones del checkout encuentra cero coincidencias después de esa corrección.
  Antes encontró dos; no se suprimió ninguna regla ni se publicaron los valores encontrados.
- Se consultaron los main de los seis forks y CI de las revisiones indicadas. La integración local
  nueva pasó con API main 60bbcdd, infra main f694448 y App 88b20a9; los mocks quedan separados.
- El diff no contiene errores de espacios. Ningún resultado implica fusión de App/Docs ni feria.

Para reproducir el control de archivos relativos y equivalencia, ejecutar Python desde la raíz
de docs con el siguiente código (biblioteca estándar; no requiere conexión a la API):

```python
from pathlib import Path
from urllib.parse import unquote, urlsplit
import re
root = Path.cwd()
missing = []
files = list(root.rglob('*.md'))
for file in files:
    text = file.read_text(encoding='utf-8')
    targets = re.findall(r'\]\(([^\s)]+)(?:\s+"[^"]*")?\)', text)
    targets += re.findall(r'^\[[^\]]+\]:\s*(\S+)', text, flags=re.M)
    for raw in targets:
        target = raw.strip('<>')
        if not target or target.startswith('#') or urlsplit(target).scheme:
            continue
        path = unquote(target.split('#', 1)[0])
        if path and not (file.parent / path).exists():
            missing.append((str(file.relative_to(root)), path))
shared = ['spec.md', 'api-contract.md', 'data-model.md']
shared += ['adr/' + p.name for p in (root / 'spec-python/adr').glob('*.md')]
different = [name for name in shared if
    (root / 'spec-python' / name).read_text(encoding='utf-8') !=
    (root / 'spec-.net' / name).read_text(encoding='utf-8')]
print(len(files), 'Markdown;', len(missing), 'missing paths;', len(different), 'different shared files')
raise SystemExit(bool(missing or different))
```

Para aplicar a Docs el detector ya probado de API, desde la misma raíz:

```python
from pathlib import Path
import sys
sys.path.insert(0, str(Path.cwd().parent / 'test-manager-library-3145555-api/scripts'))
from check_secrets import scan
findings = scan(Path.cwd())
print('Tracked pattern findings:', len(findings))
raise SystemExit(bool(findings))
```

El detector revisa archivos versionados del checkout, incluidos nuevos documentos después de
añadirlos al índice Git. No acredita todo el historial remoto ni ausencia de cualquier secreto.
