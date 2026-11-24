# CHKDSK: sistema de archivos

[Inicio](../README.md) · [Chuleta](../CHEATSHEET.md)

Ejecutar desde CMD elevado, identificando antes el volumen correcto.

```bat
chkdsk C:
```

Diagnóstico sin solicitar reparación. Examina la estructura del sistema de archivos. Si el volumen está en uso, la interpretación puede ser menos fiable; WinRE permite examinar la instalación sin arrancarla.

| Resultado | Decisión |
|---|---|
| Sin errores | Continuar con SFC, DISM u otra hipótesis; no demuestra salud física |
| Inconsistencias lógicas | Copia verificada y considerar /f |
| Errores de E/S, lecturas fallidas o disco desaparece | Priorizar copia/imagen y diagnóstico del fabricante antes de reparar |

```bat
chkdsk C: /f
```

Repara errores lógicos; puede requerir bloquear el volumen o programar un reinicio.

```bat
chkdsk C: /r
```

Busca sectores defectuosos e intenta recuperar información legible; incluye /f. Puede ser muy costoso en tiempo y lectura. No usar por defecto ni como primera medida ante un disco físicamente inestable. SMART y pruebas del fabricante complementan, pero no garantizan salud.

Fuente: [CHKDSK](https://learn.microsoft.com/es-es/windows-server/administration/windows-commands/chkdsk).
