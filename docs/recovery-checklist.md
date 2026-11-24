# Checklist de diagnóstico y recuperación

[Inicio](../README.md) · [Chuleta](../CHEATSHEET.md)

Copiar esta lista a un registro local de la incidencia y marcar únicamente lo realizado. No todos los puntos son necesarios en todos los casos.

## Antes de intervenir

- [ ] Síntoma exacto y cambios recientes registrados.
- [ ] Datos importantes respaldados y copia comprobada desde otro equipo.
- [ ] Clave de BitLocker disponible si procede.
- [ ] Instalación y volúmenes identificados.
- [ ] Dependencias y configuraciones necesarias para recuperar servicio inventariadas.

## Diagnóstico

- [ ] Fase de inicio delimitada.
- [ ] Opciones de WinRE evaluadas según síntomas.
- [ ] Comprobaciones CHKDSK, SFC y DISM seleccionadas según hipótesis.
- [ ] Resultados finales y códigos anotados (no solo porcentaje).
- [ ] Modo seguro, inicio limpio y registros evaluados si pertinentes.
- [ ] Riesgo de hardware y disponibilidad de origen de reparación considerados.
- [ ] Decisión de seguir investigando o recuperar documentada.

## Después de recuperar

- [ ] Arranque normal y reinicio repetido comprobados.
- [ ] Dispositivos y controladores necesarios operativos.
- [ ] Windows Update comprobado sin confundir pendiente con instalado.
- [ ] Red y servicios necesarios accesibles.
- [ ] Documentos, sincronización y copias verificados.
- [ ] Aplicaciones necesarias reinstaladas y configuradas.
- [ ] Configuración de inicio limpio revertida si procede.
- [ ] Funciones habituales del equipo probadas de extremo a extremo.
- [ ] Estado de la incidencia separado de la causa raíz: resuelta, no resuelta; causa confirmada, probable o desconocida.

No publicar nombres de host, usuarios, IP, credenciales, claves ni logs completos. Registrar la intervención real, no asumir que una sugerencia se ejecutó.
