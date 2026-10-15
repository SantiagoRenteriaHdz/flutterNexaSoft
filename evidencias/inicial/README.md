# Práctica 01 — Estado inicial y recorrido

Fecha de ejecución: 14 de octubre de 2026 (America/Mexico_City).

## Procedencia y preparación

- Proyecto obtenido por clonación de `https://github.com/Irving2355/Dispositivos-Moviles-2026.git`, rama `grupo-7A`. No se recibió un ZIP; no fue necesario descomprimirlo.
- Commit original del profesor: `93f22d4` (`Clase 2026-10-13 - Grupo 7A`).
- Confirmada la presencia de `pubspec.yaml`, `lib/` y `assets/` en esta raíz.
- Se conservan intactos `lib/`, `assets/` y `test/` respecto del commit original.
- SDK usado: Flutter 3.47.0 y Dart 3.13.0, Windows.
- Rama local de preparación y evidencias: `codex/practica-01-estado-inicial`.

Comandos de preparación, con los espacios corregidos respecto del texto de la guía:

```powershell
flutter create . --project-name nexasoft_incidencias --platforms android,web,windows
flutter pub get
flutter devices
```

`flutter create` generó las carpetas de plataforma y actualizó `analysis_options.yaml` y `pubspec.lock`. Su primera ejecución terminó con un aviso sobre soporte de enlaces simbólicos para Windows. La ejecución posterior de `flutter pub get` terminó correctamente. No se cambiaron ajustes de seguridad del equipo.

Dispositivos detectados: Windows y Edge. Chrome no fue detectado por Flutter. Windows requiere Visual Studio con herramientas C++, que no están instaladas. `flutter run -d edge` no pudo iniciar el navegador con el depurador, por lo que se usó el servidor web y el navegador integrado:

```powershell
flutter run -d web-server --web-hostname 127.0.0.1 --web-port 7357
```

URL local: <http://127.0.0.1:7357/>. Este comando debe mantenerse en ejecución para usar la aplicación.

## Verificación técnica

- `flutter build web --release`: completado; salida en `build/web/`.
- `flutter test`: 1 prueba aprobada.
- `flutter analyze`: 3 avisos de nivel informativo: uso obsoleto de `value` en los formularios de detalle y alta, y uso de `BuildContext` después de una operación asíncrona en la pantalla principal. No se aplicaron correcciones.

## Recorrido y resultados observados

| Paso | Acción | Resultado | Evidencia |
| --- | --- | --- | --- |
| 1 | Abrir la aplicación | 10 registros; 5 pendientes, 2 en proceso y 3 resueltos | [Inicio](01-inicio.jpg) |
| 2 | Abrir INC-101 | Detalle de la impresora; estado Pendiente | [Detalle previo](02-detalle-antes.jpg) |
| 3 | Cambiar INC-101 a En proceso | El detalle muestra En proceso | [Estado cambiado](03-estado-cambiado.jpg) |
| 4 | Volver al listado | La fila cambia, pero los contadores muestran 5 + 3 + 3 para 10 registros | [Contadores](04-contadores.jpg) |
| 5 | Completar una incidencia ficticia | Título, descripción, cliente y categoría Redes capturados | [Formulario](05-formulario.jpg) |
| 6 | Registrar | Confirmación de éxito y 11 registros; el alta aparece primero | [Registro creado](06-registro-creado.jpg) |
| 7 | Buscar `WiFi` | 2 registros, incluido el nuevo | [Búsqueda WiFi](07-busqueda-WiFi.jpg) |
| 8 | Buscar `wifi` | 0 registros; búsqueda sensible a mayúsculas | [Búsqueda minúsculas](08-busqueda-minusculas.jpg) |
| 9 | Buscar `Prueba inicial` y abrir resultado | 1 resultado; detalle con los datos registrados | [Detalle nuevo](09-detalle-nuevo.jpg) |
| 10 | Recargar la página | Persisten 11 registros y el estado de INC-101; contadores ahora 5 + 3 + 3 = 11 | [Persistencia](10-persistencia.jpg) |

Incidencia creada: `INC-1792028793633000`, título `Prueba inicial - WiFi de laboratorio`, cliente `Cliente ficticio de capacitación`, categoría `Redes`, estado `Pendiente`. Descripción: `Incidencia ficticia para verificar el registro y la búsqueda durante la práctica 01.`

Los cambios de datos de esta exploración permanecen en el almacenamiento local del navegador de prueba. No se modificó la semilla JSON ni se restablecieron los datos de demostración.

## Hallazgos para contrastar con los tickets

1. El contador de pendientes quedó desactualizado tras cambiar de estado una incidencia. Antes de recargar, tras el alta, mostraba 6 pendientes + 3 en proceso + 3 resueltas para 11 registros. Al recargar se corrigió a 5 + 3 + 3. La evidencia demuestra el comportamiento observado; aquí no se determina su causa interna.
2. Las consultas `WiFi` y `wifi` produjeron resultados distintos. Comparar este comportamiento con el requisito del ticket correspondiente antes de corregirlo.

No se implementaron tickets en esta fase. Para cada ticket asignado, crear una rama a partir de esta base, por ejemplo `git switch -c codex/ticket-<identificador>`, y registrar por separado sus cambios y verificaciones.

Todas las capturas de esta carpeta se tomaron antes de modificar el código de la aplicación.
