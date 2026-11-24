# Windows Recovery Cheatsheet

CLAUDIOGONZALEZ.ES | Lab de diagnóstico y recuperación de Windows. Referencia práctica de herramientas, comandos y procedimientos de reparación.

Guía de consulta para diagnosticar problemas de inicio de Windows 11, especialmente después de una actualización. No es una colección de comandos para ejecutar de principio a fin: el resultado de cada comprobación determina qué tiene sentido hacer después.

## Empezar aquí

- [Chuleta de herramientas y comandos](CHEATSHEET.md): consulta rápida, entorno, permisos, impacto e interpretación.
- [WinRE y primeros pasos](docs/winre.md)
- [CHKDSK: sistema de archivos](docs/chkdsk.md)
- [SFC: archivos protegidos](docs/sfc.md)
- [DISM: imagen y almacén de componentes](docs/dism.md)
- [Diagnóstico de arranque, registros y controladores](docs/boot-diagnostics.md)
- [Reparación avanzada y alternativas de recuperación](docs/advanced-recovery.md)
- [Checklist de recuperación](docs/recovery-checklist.md)
- [Referencias oficiales](docs/references.md)

## Elegir la siguiente comprobación

| Síntoma | Primera línea de investigación |
|---|---|
| El firmware no detecta el disco | Hardware y almacenamiento; proteger datos antes de reparar |
| Windows entra en recuperación tras actualizar | WinRE, desinstalación de actualización, restauración |
| Modo seguro funciona, arranque normal no | Inicio limpio, controladores, eventos, DISM |
| SFC no encuentra daños y el fallo continúa | DISM, registros y otras hipótesis según síntomas |
| DISM encuentra corrupción pero no puede reparar | Origen compatible y registros CBS/DISM |
| Error explícito de BCD o gestor de arranque | Diagnóstico específico de la fase de inicio |
| Pantalla azul con volcado | Código STOP, volcado y WinDbg |

## Precauciones

- **D — Diagnóstico:** consulta o examen; puede generar registros, pero no pretende reparar.
- **R — Reparación:** cambia archivos, configuración o estado del sistema.
- **A — Alto impacto:** puede retirar aplicaciones, deshacer cambios o afectar a datos; requiere copia verificada y decisión consciente.

Los ejemplos usan C: como instalación de Windows. En WinRE la letra puede ser distinta. Identifica el volumen antes de operar. Si BitLocker protege el equipo, ten disponible su clave de recuperación. En equipos administrados, sigue el procedimiento de TI.

## Contexto

Material complementario del Lab «Windows 11 no arranca: guía práctica de diagnóstico y recuperación» de [claudiogonzalez.es](https://claudiogonzalez.es/). No sustituye el diagnóstico específico ni garantiza una reparación.

Autor: [Claudio González](https://github.com/cgonzalezdai).
