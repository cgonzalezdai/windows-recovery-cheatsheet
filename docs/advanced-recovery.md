# Reparación avanzada y alternativas

[Inicio](../README.md) · [Chuleta](../CHEATSHEET.md)

No saltar directamente al restablecimiento si conservar la instalación o conocer la causa raíz tiene valor.

## Investigar según indicios

| Indicio | Línea de trabajo |
|---|---|
| DISM no encuentra archivos | Identificar paquetes/componentes en CBS y DISM; origen compatible |
| Modo seguro sí, normal no | Inicio limpio, eventos y estado de controladores |
| STOP reproducible y volcado | WinDbg y símbolos; contrastar hipótesis con cambios recientes |
| Mensaje BCD/Boot Manager | Identificar UEFI/GPT o BIOS/MBR, partición y almacén correctos; seguir documentación específica |
| Errores de E/S o desaparición del disco | Proteger datos y evaluar almacenamiento con diagnóstico del fabricante |

No ejecutar listas genéricas de bootrec/bcdboot, modificar particiones ni desactivar controladores a ciegas. Si la causa no es clara, registrar hipótesis, prueba y resultado antes de cambiar otra cosa. Si se necesita análisis forense, preservar registros e imagen antes de reinstalar.

## Elegir recuperación

- Si Windows vuelve a iniciar normalmente, valorar reparación mediante Windows Update o instalación de reparación compatible que conserve aplicaciones y datos si está disponible. No asumir que puede iniciarse desde WinRE.
- Restablecer este equipo > Conservar mis archivos: reinstala Windows, retira aplicaciones y restablece configuración. Requiere copia comprobada y claves necesarias. Reinstalación local o descarga en la nube.
- Instalación limpia o Quitar todo: solo cuando se haya decidido explícitamente el alcance y protegido los datos. La opción de recompilación en la nube, si aparece, no es lo mismo que descarga en la nube conservando archivos.

Restablecer el sistema puede recuperar su funcionamiento sin identificar la causa del fallo. Si es importante evitar que la incidencia se reproduzca en otros equipos, conviene preservar las evidencias y continuar el diagnóstico antes de reinstalar.

Continuar con [verificación](recovery-checklist.md).

Fuentes: [Opciones de recuperación](https://support.microsoft.com/es-es/windows/experience/backup-recovery/recovery-options-in-windows), [diagnóstico avanzado de arranque](https://learn.microsoft.com/es-es/troubleshoot/windows-client/performance/windows-boot-issues-troubleshooting), [DISM](https://learn.microsoft.com/es-es/windows-hardware/manufacture/desktop/repair-a-windows-image).
