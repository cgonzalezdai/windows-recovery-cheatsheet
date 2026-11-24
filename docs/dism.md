# DISM: imagen y almacén de componentes

[Inicio](../README.md) · [Chuleta](../CHEATSHEET.md)

## Elegir el objetivo

CMD elevado. /Online trabaja con Windows en ejecución, también en modo seguro si está disponible. /Image apunta a una instalación offline. No usar /Online en WinRE para reparar por error el propio entorno de recuperación.

```bat
DISM /Online /Cleanup-Image /CheckHealth
DISM /Online /Cleanup-Image /ScanHealth
```

CheckHealth consulta indicadores de corrupción; ScanHealth realiza un examen más profundo. Si la imagen es reparable:

```bat
DISM /Online /Cleanup-Image /RestoreHealth
```

Desde WinRE, con C: verificado:

```bat
DISM /Image:C:\ /Cleanup-Image /ScanHealth
DISM /Image:C:\ /Cleanup-Image /RestoreHealth
```

No son una secuencia universal. RestoreHealth modifica la imagen y puede necesitar un origen.

## Origen alternativo

Comprobar versión, edición, arquitectura, idioma y nivel de mantenimiento. Un medio más antiguo o de otra rama puede no contener los componentes necesarios.

```bat
DISM /Online /Get-CurrentEdition
DISM /Get-WimInfo /WimFile:D:\sources\install.wim
```

Consultar winver en Windows. Elegir el índice real de la edición correspondiente. Ejemplo de plantilla para una imagen WIM compatible (sustituir INDICE; no ejecutar literalmente):

```bat
DISM /Online /Cleanup-Image /RestoreHealth /Source:WIM:D:\sources\install.wim:INDICE /LimitAccess
```

También es posible utilizar la carpeta Windows de una imagen correctamente montada. Para una instalación offline:

```bat
DISM /Image:C:\ /Cleanup-Image /RestoreHealth /Source:E:\mount\Windows
```

/LimitAccess evita recurrir a Windows Update para reparar una imagen online. No convertir un ESD en WIM cambiando la extensión. Consultar la documentación oficial si el medio contiene otro formato. No se afirma que este procedimiento se probara en el caso del Lab.

## Interpretar resultados

| Resultado | Acción |
|---|---|
| Imagen sana | Investigar otras capas según síntomas |
| Reparable | Evaluar RestoreHealth y origen |
| No reparable | Valorar recuperación/reinstalación |
| 0x800f0915 | No se encontró contenido de reparación; revisar origen y registros |
| 0x800f082f durante reversión | Fallo de operación; consultar registros antes de reintentar |
| Error 87 | Revisar parámetros y contexto; no acredita corrupción por sí mismo |

Un progreso del 100 % no implica éxito: leer el mensaje final y código. Los registros DISM pueden corresponder al entorno que ejecutó la herramienta, no al Windows objetivo. CBS suele estar en Windows\Logs\CBS\CBS.log.

## Revertir operaciones pendientes

Solo en recuperación de una instalación offline que no arranca, ante una hipótesis razonada de mantenimiento pendiente:

```bat
DISM /Image:C:\ /Cleanup-Image /RevertPendingActions
```

Es una modificación relevante. No usar en un sistema normal ni contra WinRE. No borrar manualmente WinSxS, pending.xml o claves del registro como atajo.

Tras una reparación exitosa, ejecutar SFC sobre el objetivo correcto y comprobar reinicio. Si falta un origen válido, considerar [reparación avanzada](advanced-recovery.md).

Fuentes: [Reparar imagen](https://learn.microsoft.com/es-es/windows-hardware/manufacture/desktop/repair-a-windows-image), [origen de reparación](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/configure-a-windows-repair-source?view=windows-11), [opciones DISM](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/dism-operating-system-package-servicing-command-line-options?view=windows-11).
