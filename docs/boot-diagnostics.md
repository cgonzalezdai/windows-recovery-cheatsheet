# Arranque, controladores y registros

[Inicio](../README.md) · [Chuleta](../CHEATSHEET.md)

## Delimitar fase

Distinguir firmware y detección del disco, gestor/cargador de arranque, kernel y sesión. Si modo seguro llega al escritorio, el arranque mínimo funciona; no demuestra que el gestor, todos los controladores o servicios estén sanos. Evitar reconstruir BCD por rutina.

## Modo seguro e inicio limpio

WinRE > Opciones avanzadas > Configuración de inicio > Reiniciar. 4/F4 mínimo; 5/F5 con red. F9 puede permitir observar un STOP, si existe. No deshabilitar protecciones como prueba genérica.

Si Windows permite configurar un inicio limpio: abrir msconfig, ocultar servicios de Microsoft, registrar estado y deshabilitar temporalmente los restantes, además de aplicaciones de inicio en Administrador de tareas. Reiniciar normalmente. Si funciona, reactivar por grupos para aislar el conflicto. Si falla, restaurar el estado anterior; no descartar todos los controladores. No alterar opciones avanzadas de arranque sin necesidad.

## Consultas

```bat
eventvwr.msc
devmgmt.msc
pnputil /enum-devices /problem
pnputil /enum-devices /class Net /connected
pnputil /enum-drivers
ipconfig /all
bcdedit /enum all
```

Ejecutar PnPUtil y BCDEdit desde CMD elevado. La consulta BCD por defecto se refiere al almacén activo; en WinRE comprobar cuál es antes de interpretar. No aplicar /set ni reconstruir sin identificar el objetivo. PnPUtil enumera estado y paquetes: un problema en modo seguro puede deberse a restricciones de ese modo.

## Evidencias

| Registro | Interpretación |
|---|---|
| Eventos Sistema | Correlacionar tiempo, proveedor y mensaje |
| Kernel-Power 41 | Apagado/reinicio no limpio; no identifica causa raíz |
| ntbtlog.txt | Controladores cargados/no cargados; no cargado no equivale a defectuoso |
| SrtTrail.txt | Pruebas de reparación de inicio; éxito parcial no equivale a arranque correcto |
| CBS/DISM | Fallos de mantenimiento y archivos requeridos |

Si existe un volcado STOP, abrirlo localmente con WinDbg, configurar símbolos si procede y usar `!analyze -v` como punto de partida. Los volcados de memoria pueden contener credenciales y otros datos sensibles. Si necesitas compartirlos con un servicio de soporte, utiliza un canal seguro y limita el acceso a las personas autorizadas.

Fuentes: [Diagnóstico avanzado de arranque](https://learn.microsoft.com/es-es/troubleshoot/windows-client/performance/windows-boot-issues-troubleshooting), [PnPUtil](https://learn.microsoft.com/es-es/windows-hardware/drivers/devtest/pnputil-command-syntax).
