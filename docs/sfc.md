# SFC: archivos protegidos de Windows

[Inicio](../README.md) · [Chuleta](../CHEATSHEET.md)

Desde CMD elevado en Windows:

```bat
sfc /verifyonly
sfc /scannow
```

El primero comprueba sin reparar; el segundo intenta reparar archivos protegidos. Son alternativas según objetivo, no es necesario ejecutar ambos siempre.

Desde WinRE, con instalación offline:

```bat
sfc /scannow /offbootdir=C:\ /offwindir=C:\Windows
```

Ejemplo únicamente si las rutas son correctas. La ubicación de arranque puede ser diferente de la de Windows; verificar ambas.

| Salida | Interpretación |
|---|---|
| Sin infracciones de integridad | No encontró daños en archivos protegidos; no excluye corrupción del almacén |
| Reparó archivos | Reiniciar y probar; revisar CBS si interesa identificar qué cambió |
| No pudo reparar algunos | Revisar CBS y estado del almacén con DISM |
| No pudo realizar operación | Verificar rutas, permisos, estado del volumen y entorno |

Para extraer líneas de SFC en CMD de Windows, sin alterar el registro original:

```bat
findstr /l /c:"[SR]" "%windir%\Logs\CBS\CBS.log"
```

El registro puede incluir operaciones de otras sesiones. Correlacionar marcas temporales. Después de una reparación DISM satisfactoria, volver a ejecutar SFC y comprobar el arranque.

Fuente: [SFC](https://learn.microsoft.com/es-es/windows-server/administration/windows-commands/sfc).
