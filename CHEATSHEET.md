# Chuleta de herramientas y comandos

[Inicio](README.md) · [Referencias](docs/references.md)

**D** = diagnóstico, **R** = reparación/modificación, **A** = alto impacto. CMD elevado salvo indicación. WinRE: símbolo del sistema de recuperación; Windows: instalación en ejecución (incluido modo seguro si la herramienta funciona). C: y D: son ejemplos: verifica las letras. Los comandos D pueden escribir registros o archivos de salida.

## 1. Identificar instalación y entorno

| Comando | Entorno | Impacto | Finalidad / siguiente paso |
|---|---|---|---|
| `diskpart` → `list volume` → `exit` | WinRE / Windows, admin | D | Enumerar volúmenes; no usar operaciones de borrado |
| `dir C:\Windows` | WinRE, admin | D | Confirmar instalación; probar otra letra si no existe |
| `manage-bde -status` | WinRE / Windows, admin | D | Consultar cifrado y bloqueo; obtener clave por vía segura si procede |
| `winver` | Windows, usuario | D | Versión y compilación |
| `DISM /Online /Get-CurrentEdition` | Windows, admin | D | Edición para seleccionar origen compatible |
| `DISM /Image:C:\ /Get-Packages /Format:Table` | WinRE, admin | D | Estado de paquetes; buscar evidencia de mantenimiento pendiente |

## 2. Disco y archivos protegidos

| Comando | Entorno | Impacto | Finalidad / siguiente paso |
|---|---|---|---|
| `chkdsk C:` | WinRE / Windows, admin | D | Examinar NTFS; si hay errores, decidir reparación o protección de datos |
| `chkdsk C: /f` | WinRE / Windows, admin | R | Corregir errores lógicos; puede exigir reinicio |
| `chkdsk C: /r` | WinRE / Windows, admin | R | Buscar sectores ilegibles, recuperar datos legibles; incluye /f y puede tardar mucho |
| `sfc /verifyonly` | Windows, admin | D | Comprobar archivos protegidos sin repararlos |
| `sfc /scannow` | Windows, admin | R | Comprobar y reparar archivos protegidos |
| `sfc /scannow /offbootdir=C:\ /offwindir=C:\Windows` | WinRE, admin | R | SFC sobre instalación offline; adaptar ambas rutas |

No usar CHKDSK como prueba definitiva de salud física. Si se sospecha avería, proteger datos antes de /f o /r.

## 3. DISM

| Comando | Entorno | Impacto | Finalidad / siguiente paso |
|---|---|---|---|
| `DISM /Online /Cleanup-Image /CheckHealth` | Windows, admin | D | Consultar corrupción registrada; ScanHealth si hace falta |
| `DISM /Online /Cleanup-Image /ScanHealth` | Windows, admin | D | Examinar almacén; RestoreHealth si es reparable |
| `DISM /Online /Cleanup-Image /RestoreHealth` | Windows, admin | R | Reparar con origen disponible; SFC después si éxito |
| `DISM /Image:C:\ /Cleanup-Image /ScanHealth` | WinRE, admin | D | Examinar instalación offline |
| `DISM /Image:C:\ /Cleanup-Image /RestoreHealth` | WinRE, admin | R | Reparar imagen offline; puede necesitar origen compatible |
| `DISM /Image:C:\ /Cleanup-Image /RevertPendingActions` | WinRE, admin | A | Revertir mantenimiento pendiente de instalación que no arranca; solo si justificado |
| `DISM /Get-WimInfo /WimFile:D:\sources\install.wim` | Windows / WinRE, admin | D | Identificar índices de una imagen de instalación WIM |
| `DISM /Online /Cleanup-Image /RestoreHealth /Source:WIM:D:\sources\install.wim:INDICE /LimitAccess` | Windows, admin | R | Reparación con WIM compatible; sustituir INDICE por el real |

`/Online` identifica el Windows en ejecución, no la conectividad. En WinRE usa /Image para la instalación que quieres reparar. Consulta [DISM](docs/dism.md) antes de usar un origen externo.

## 4. Inicio y evidencias

| Herramienta / comando | Entorno | Impacto | Finalidad / siguiente paso |
|---|---|---|---|
| `eventvwr.msc` | Windows | D | Eventos de Sistema; correlacionar fecha y componente |
| `devmgmt.msc` | Windows | D al consultar | Estado de dispositivos y códigos de problema |
| `pnputil /enum-devices /problem` | Windows, admin | D | Enumerar dispositivos con problemas |
| `pnputil /enum-devices /class Net /connected` | Windows, admin | D | Inventario de adaptadores conectados |
| `pnputil /enum-drivers` | Windows, admin | D | Paquetes de controladores de terceros |
| `ipconfig /all` | Windows | D | Estado de red; no equivale a prueba de Internet |
| `bcdedit /enum all` | Windows, admin | D | Consultar BCD del sistema; en WinRE identificar almacén correcto |
| `msconfig` | Windows, admin | R al modificar | Inicio limpio; guardar estado y revertir |
| WinDbg, `!analyze -v` | Windows, con volcado | D | Analizar STOP; no asumir culpable por un nombre de módulo |

## 5. Registros útiles

| Ruta relativa a la instalación | Utilidad |
|---|---|
| `Windows\System32\LogFiles\Srt\SrtTrail.txt` | Reparación de inicio |
| `Windows\ntbtlog.txt` | Registro de arranque cuando se habilita |
| `Windows\Logs\CBS\CBS.log` | Mantenimiento de componentes y SFC |
| `Windows\Logs\DISM\dism.log` | Operaciones DISM en ese entorno; en WinRE puede estar en X: |
| `Windows\Minidump\` / `Windows\MEMORY.DMP` | Volcados si fueron generados y guardados |

## 6. Recuperación sin comandos

| Opción | Impacto | Cuándo |
|---|---|---|
| Reparación de inicio | R | Fallo de arranque |
| Desinstalar actualización | R | Inicio del fallo tras actualización |
| Restaurar sistema | R | Punto anterior válido; puede revertir aplicaciones/controladores |
| Modo seguro (4/F4) | D | Comparar inicio con conjunto mínimo |
| Modo seguro con red (5/F5) | D | Si se necesita red; puede estar limitada |
| Restablecer conservando archivos | A | Cuando compensa reinstalar; elimina aplicaciones y configuración |
| Instalación limpia / quitar todo | A | Solo con decisión expresa, copia verificada y alcance comprendido |

Antes de restablecer, valorar alternativas de [reparación avanzada](docs/advanced-recovery.md). Después usar la [lista de verificación](docs/recovery-checklist.md).
