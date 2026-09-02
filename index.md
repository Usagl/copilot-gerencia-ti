# KNOWLEDGE GPT — Reporte Gerencia TI
**Versión:** 1.5  
**Tipo:** referencia funcional, semántica y visual.  
**Prioridad:** las instrucciones del GPT gobiernan el comportamiento. Este archivo explica cómo interpretar el dominio y los datos.

> IMPORTANTE: los ejemplos de este archivo son ilustrativos. Nunca deben utilizarse como datos reales. La fuente de verdad de cada ejecución son exclusivamente los TXT subidos por el usuario.

---

# 1. MODELO MENTAL DEL REPORTE

El agente convierte datos estructurados de Gestión TI en un informe ejecutivo estable.

```text
TXT DEL PERÍODO
      ↓
VALIDACIÓN
      ↓
HECHOS DECLARADOS/CALCULADOS
      ↓
INFORME_FINAL_CANONICO
      ├── respuesta
      └── Word
```

La respuesta y el Word representan el mismo contenido.

El objetivo no es narrar todo el TXT ni explicar la mecánica del análisis. El objetivo es mostrar información útil para Gerencia de forma compacta y verificable.

---

# 2. RECEPCIÓN POR LOTES

El usuario puede subir archivos en lotes de hasta 2.

Ejemplo:

```text
PDTI + EDA
AEP + DYN
SOPTI
"Listo, son todos"
```

Antes de la confirmación final: acumular, verificar recepción y no analizar.

Después de la confirmación: validar el conjunto completo y analizar todos los archivos juntos.

No mezclar períodos salvo comparación solicitada.

---

# 3. EQUIPOS Y ORDEN OFICIAL

1. Equipo de Proyectos Desarrollo TI (`PDTI`)
2. Equipo Desarrollo de Aplicaciones (`EDA`)
3. Equipo Desarrollo AEP (`AEP`)
4. DYNAMO (`DYN`)
5. Equipo Soporte TI (`SOPTI`)
6. Análisis de Tickets y Continuidad Operacional
7. Cierre Ejecutivo

La unidad de ejecución publicada es el EQUIPO.

Los nombres de responsables individuales pueden utilizarse para validación interna, pero no se publican.

---

# 4. ESTRUCTURA HABITUAL DEL TXT

```json
{
  "reporte": {},
  "proyectos": [],
  "desarrollos": [],
  "actividades": [],
  "tickets": [],
  "sistemas": []
}
```

`reporte`: período, fecha de corte, equipo, código.  
`proyectos`: iniciativas con seguimiento.  
`desarrollos`: desarrollos/mejoras con seguimiento.  
`actividades`: trabajo declarado en el período.  
`tickets`: registros de ticketera.  
`sistemas`: horas monitoreadas e incidencias.

---

# 5. DEFINICIÓN: porcentajeAvance

`porcentajeAvance` = avance acumulado de la iniciativa.

Válido:

> La iniciativa registra 78% de avance acumulado.

No interpretar como avance realizado dentro del período.

---

# 6. DEFINICIÓN: avancePeriodo

`avancePeriodo` es la principal fuente textual para describir qué cambió o qué se realizó durante el período.

Puede reformularse para claridad sin agregar beneficios, impactos, riesgos, consecuencias ni valoraciones.

Si está vacío, no concluir que no hubo trabajo.

---

# 7. REGLA: EVITAR REDUNDANCIA DE ESTADO

Las tablas ya comunican estado, etapa, avance y prioridad.

La prosa debe concentrarse en MOVIMIENTO y HECHOS NUEVOS.

## No publicar

> La iniciativa continúa En Proceso al corte.

> El desarrollo continúa En Proceso al corte.

> Registra estado Activo al corte.

> Las iniciativas continúan En Proceso al corte.

> A la fecha de corte permanece En Proceso.

Estas frases repiten una condición observable en la tabla y no aportan valor ejecutivo.

## Publicar

> Durante el período se instaló y configuró el servidor; continúa la habilitación DNS declarada.

> Se incorporaron cinco servicios al formato de disponibilidad y se validó el registro manual de incidentes.

La tabla contiene la foto del estado. La narrativa explica el movimiento.

---

# 8. REGLA: FINALIZACIÓN

Una iniciativa se considera finalizada durante el período solo si `fechaFinReal` está dentro del período.

`fechaFinPlanificada` no permite declarar atraso, riesgo, incumplimiento ni finalización.

No añadir aclaraciones como “al corte” para justificar que algo sigue abierto. El estado visible es suficiente.

---

# 9. REGLA: HITOS

Hito completado:
- estado `COMPLETADO`;
- fecha de finalización dentro del período.

Hitos futuros:
**Próximos hitos declarados**.

No tratarlos como compromisos garantizados.

---

# 10. REGLA: PRIORIDAD

Los cambios se obtienen de `historialPrioridad`.

Publicar:
- iniciativa;
- anterior → nueva;
- motivo solo si está declarado.

No interpretar automáticamente el cambio como riesgo o urgencia.

---

# 11. REGLA: ACTIVIDADES

Agrupar por:

```text
sistema + tipo + título
```

Repetidos = contador.

Sin sistema = `Otro`.

La cantidad no representa productividad ni esfuerzo.

---

# 12. TICKETS: UNIVERSOS

## AEP

Los tickets AEP se muestran exclusivamente dentro de la sección AEP.

Publicables:
- Considerados;
- Finalizados;
- En Proceso;
- % Finalizados;
- % En Proceso.

## SOPTI

El análisis general de tickets usa exclusivamente SOPTI.

Nunca consolidar AEP + SOPTI.

---

# 13. TICKETS: KPI

Participan:

```text
baseAnalisisKPI = true
```

Finalizados:

```text
CERRADO o RESUELTO
```

En Proceso:

```text
cualquier otro estado válido para KPI
```

Cálculos:

```text
% Finalizados = Finalizados / Considerados × 100
% En Proceso = En Proceso / Considerados × 100
```

---

# 14. TICKETS: DATOS INTERNOS

Normalmente NO publicar:
- `baseAnalisisKPI`;
- cantidad/motivo de exclusiones;
- merges;
- antigüedad;
- metodología;
- notas técnicas;
- SLA;
- explicación de filtros.

Estos datos sirven para cálculo/auditoría, no para el informe ejecutivo.

Solo mostrarlos si el usuario solicita auditoría.

---

# 15. TOP 10 SOPORTE TI

Se generan:
1. Top 10 Solicitantes.
2. Top 10 Temas de Ayuda.

Antes de ambos rankings excluir cualquier ticket si:

```text
tema/categoría = NO CORRESPONDE SOPORTE
OR correo = bhom_notificacion@bmc.com
OR asunto/título contiene [!!Spam]
```

Comparación insensible a mayúsculas/minúsculas.

Estos filtros afectan solo rankings, no KPI.

## Top 10 Solicitantes

Agrupar por solicitante y ordenar descendente.

Excluir integrantes TI identificables.

## Top 10 Temas

Agrupar por tema/categoría y ordenar descendente.

`NO CORRESPONDE SOPORTE` nunca aparece.

---

# 16. DISPONIBILIDAD OPERACIONAL — REGLA VIGENTE

La versión ejecutiva NO muestra disponibilidad por sistema.

La disponibilidad se comunica como UNA MÉTRICA GLOBAL del universo monitoreado.

Calcular:

```text
Uptime general =
SUMA(horasUptime) / SUMA(horasPeriodo) × 100

Downtime general =
SUMA(horasDowntime) / SUMA(horasPeriodo) × 100
```

No promediar porcentajes individuales.

Mostrar máximo 2 decimales.

## Formato preferido

| Métrica | Resultado |
|---|---:|
| Uptime general | 99,58% |
| Downtime general | 0,42% |

También puede usarse una tabla horizontal compacta:

| Uptime general | Downtime general |
|---:|---:|
| 99,58% | 0,42% |

## No publicar

- lista de todos los sistemas monitoreados;
- uptime individual por sistema;
- downtime individual por sistema;
- sistemas con 100% solo para demostrar que no tuvieron incidentes.

La lectura ejecutiva debe responder:

> ¿Cuál fue la disponibilidad general?

Los sistemas se utilizan después únicamente para contextualizar incidencias.

---

# 17. INCIDENCIAS OPERACIONALES

Después de la disponibilidad general mostrar las incidencias.

Agrupar por sistema SOLO cuando ese sistema tenga incidencias.

Campos publicables cuando existan:
- fecha;
- duración;
- causa;
- impacto;
- estado de resolución.

Ejemplo:

```text
Red WAN
26/08/2026 · 2,5 h
Causa: Intermitencia de enlace del proveedor.
Impacto: Conectividad degradada en terminal.
Estado: Resuelto.
```

No mostrar un bloque para sistemas sin incidencias.

No inventar campos vacíos.

Lógica ejecutiva:

```text
DISPONIBILIDAD GLOBAL
      ↓
INCIDENCIAS
      ├── Sistema A
      ├── Sistema B
      └── Sistema C
```

---

# 18. SECCIÓN FINAL CANÓNICA

## KPI Tickets Soporte TI
- Considerados
- Finalizados
- En Proceso
- % Finalizados
- % En Proceso

## Top 10 Solicitantes

## Top 10 Temas de Ayuda

## Disponibilidad Operacional
- Uptime general
- Downtime general

## Incidencias Operacionales
- agrupadas por sistema con incidencia

No intercalar metodología, exclusiones, antigüedad ni explicaciones internas.

---

# 19. ESTILO DE REDACCIÓN EJECUTIVA

Prioridad:

```text
HECHO NUEVO > CAMBIO > RESULTADO > CONTEXTO
```

Evitar texto que solo repita estado, fecha de corte, reglas de cálculo, condiciones obvias o información visible en la tabla.

## Poco eficiente

> Proxy Reverso Seaport registra 92% de avance acumulado y continúa En Proceso al corte.

## Preferido

> Durante el período se instaló y configuró el servidor; continúa la habilitación DNS declarada.

Si el 92% ya aparece en la tabla, no es obligatorio repetirlo en el párrafo.

La tabla contiene la foto del estado. La narrativa explica el movimiento.

---

# 20. CONCLUSIONES

Publicar solo hechos declarados, calculados o comparados.

Adecuado:

> Durante el período finalizaron cuatro desarrollos.

> Se completaron diez hitos.

> Soporte TI registró 12 tickets considerados: 8 Finalizados y 4 En Proceso.

> La disponibilidad operacional general fue 99,58% de uptime y 0,42% de downtime.

> Se declararon tres incidencias operacionales.

No afirmar sin evidencia:
- buen/mal desempeño;
- productividad;
- sobrecarga;
- atraso;
- problema;
- eficiencia;
- ahorro;
- criticidad;
- cuello de botella.

---

# 21. INFORME_FINAL_CANONICO

El agente crea un único contenido maestro interno.

Una vez validado:
- no volver a resumir;
- no reanalizar;
- no recalcular;
- no cambiar selección de hechos.

La respuesta es su representación textual.

El Word es su representación documental.

---

# 22. WORD Y CAPACIDAD DE ARCHIVOS

El Knowledge no puede habilitar herramientas.

Cuando el GPT tenga una capacidad de ejecución/generación de archivos disponible, debe utilizarla para crear el `.docx` si el usuario pidió el informe.

El Word:
- publica el INFORME_FINAL_CANONICO;
- no realiza un segundo análisis;
- no omite contenido;
- no añade conclusiones.

Si la capacidad no está habilitada, el GPT debe decirlo brevemente y no inventar enlaces.

Para un GPT destinado a producir documentos, habilitar una capacidad de ejecución de código/análisis de datos o una herramienta equivalente de creación de archivos.

---

# 23. CONTRATO VISUAL MARVAL

Mantener el formato actualmente validado.

## Página
- Carta/Letter;
- vertical;
- márgenes aprox. 1,27 cm;
- fondo blanco;
- sin pie ni numeración salvo solicitud.

## Tipografía
- Calibri;
- texto base 8 pt;
- títulos compactos;
- verde corporativo `#70AD47`;
- texto negro.

## Identidad
- logo MARVAL arriba a la derecha cuando exista;
- secciones principales en verde;
- línea horizontal verde;
- tablas compactas;
- alta densidad informativa.

## No usar
- dashboard;
- tarjetas grandes;
- sombras;
- degradados;
- fondos decorativos;
- WordArt;
- rediseños por período.

---

# 24. TABLAS

Las tablas deben concentrar datos observables.

Proyectos/Desarrollos:
- iniciativa;
- estado/etapa;
- avance acumulado;
- prioridad;
- avance del período cuando convenga.

Actividades:
- sistema;
- tipo;
- actividad;
- cantidad.

Tickets:
- indicador;
- resultado.

Disponibilidad:
- Uptime general;
- Downtime general.

Si una tabla ya contiene un dato, evitar repetirlo inmediatamente en una oración salvo que la narración agregue información nueva.

---

# 25. APROVECHAMIENTO DEL ESPACIO

El documento es **COMPACTO, NO RESUMIDO**.

- flujo de arriba hacia abajo;
- pocos espacios vacíos;
- sin página obligatoria por equipo;
- continuar siguiente equipo cuando exista espacio;
- tablas y bloques con altura dinámica;
- agregar páginas cuando sea necesario.

Prioridad:

```text
FIDELIDAD
> LEGIBILIDAD
> PERSISTENCIA VISUAL
> CANTIDAD DE PÁGINAS
```

---

# 26. REGLAS DE SALTO

- título unido al primer contenido;
- evitar títulos huérfanos;
- permitir continuidad natural entre páginas;
- no insertar saltos solo para que un equipo comience arriba;
- no reducir texto por debajo del mínimo visual para hacer caber contenido.

---

# 27. SECCIONES SIN DATOS

No inventar contenido.

Si una sección obligatoria requiere indicación:

> No se declararon elementos para esta sección durante el período.

Usar esta frase solo cuando sea necesaria para mantener claridad estructural. No llenar el documento con aclaraciones de ausencia si omitir el bloque es más limpio y no genera ambigüedad.

---

# 28. AUDITORÍA

La auditoría es una salida distinta del informe ejecutivo.

Solo si el usuario la pide pueden mostrarse:
- exclusiones;
- base KPI;
- merges;
- antigüedad;
- reglas;
- cálculos;
- evidencia.

No mezclar auditoría con el reporte gerencial.

---

# 29. CHECKLIST DE CONTENIDO

## Recepción
- carga confirmada;
- todos los archivos incluidos;
- períodos no mezclados.

## Datos
- cantidades y porcentajes correctos;
- finalizaciones/hitos/prioridades válidos;
- AEP y SOPTI separados;
- rankings filtrados;
- disponibilidad global correctamente ponderada.

## Redacción
- no responsables individuales;
- no mecánica interna;
- no inferencias;
- no frases redundantes de “En Proceso al corte”;
- narrativa centrada en movimiento.

## Continuidad
- no tabla de disponibilidad por sistema;
- Uptime general;
- Downtime general;
- sistemas solo donde existan incidencias.

## Word
- mismo contenido que respuesta;
- misma estructura;
- mismo formato MARVAL;
- no resumen secundario.

---

# 30. PRINCIPIOS DE RECUPERACIÓN

Cuando el GPT necesite decidir:

**¿Qué significa un campo?** → secciones 4–10.  
**¿Cómo tratar tickets?** → secciones 12–15.  
**¿Cómo tratar disponibilidad?** → secciones 16–17.  
**¿Qué mostrar al final?** → sección 18.  
**¿Cómo redactar sin redundancia?** → sección 19.  
**¿Cómo generar Word?** → secciones 21–23.  
**¿Cómo maquetar?** → secciones 23–26.

Principios permanentes:

1. TXT = hechos.
2. Knowledge = semántica y formato, no datos actuales.
3. Equipo = unidad de análisis.
4. Movimiento > repetición de estado.
5. Disponibilidad = métrica global.
6. Sistemas = contexto de incidencias.
7. Auditoría interna ≠ informe ejecutivo.
8. Respuesta = Word en contenido.
9. Ante duda, omitir antes que inferir.
