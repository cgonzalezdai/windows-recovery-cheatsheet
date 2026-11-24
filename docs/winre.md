# WinRE y primeros pasos

[Inicio](../README.md) · [Chuleta](../CHEATSHEET.md)

## Acceso y protección

WinRE suele ofrecerse tras fallos repetidos de arranque. Si Windows funciona, usar Inicio avanzado en Configuración > Sistema > Recuperación o Mayús + Reiniciar. Desde un medio oficial de instalación, elegir reparar el equipo, no instalar. Verificar copia de datos y disponibilidad de clave BitLocker antes de modificar nada.

## Localizar Windows

En CMD de WinRE:

```bat
diskpart
list volume
exit
dir C:\Windows
dir D:\Windows
manage-bde -status
```

Verificar letra, tamaño, sistema de archivos y presencia de la instalación correcta. X: suele ser el propio entorno WinRE. No usar clean, format, delete partition ni asignar letras indiscriminadamente.

## Opciones menos disruptivas

- Reparación de inicio: probar y revisar SrtTrail.txt si falla.
- Desinstalar actualización: razonable si existe relación temporal; no demuestra que esa actualización fuera la causa.
- Restaurar sistema: comprobar qué cambios se revertirán y validar con reinicio.
- Configuración de inicio: 2/F2 registro, 4/F4 modo seguro, 5/F5 modo seguro con red, 9/F9 deshabilitar reinicio automático por error.

Las opciones dependen de la versión y el equipo. Si el almacenamiento no aparece o hay signos de daño físico, no insistir en reparaciones lógicas: proteger datos primero.

## Mantenimiento pendiente

```bat
DISM /Image:C:\ /Get-Packages /Format:Table
```

Consulta estados. Un paquete instalado o reemplazado no equivale a uno pendiente.

Si existe un motivo fundado para revertir una operación pendiente en una instalación que no arranca, consultar [DISM](dism.md). No repetir acciones fallidas sin nueva evidencia.

Fuente: [Opciones de recuperación](https://support.microsoft.com/es-es/windows/experience/backup-recovery/recovery-options-in-windows), [configuración de inicio](https://support.microsoft.com/es-es/windows/experience/startup-boot/windows-startup-settings).
