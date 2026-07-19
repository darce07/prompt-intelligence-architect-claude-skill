# Plantilla: Workflow / Prompt chain

Para documentar un proceso de varios pasos, ya sea dentro de una skill (como los archivos de `workflows/` de esta misma skill) o como una cadena de prompts encadenados donde la salida de uno alimenta al siguiente.

## Cuándo usar esta plantilla

Cuando una tarea se resuelve mejor como una secuencia de pasos reproducibles que como una sola instrucción monolítica — especialmente si distintos pasos requieren distinto foco o nivel de detalle.

## Plantilla

```text
# Workflow: {{nombre}}

Cuándo usarlo: {{qué tipo de petición dispara este workflow en vez de otro}}

## Pasos
1. **{{Nombre del paso}}**. {{Qué hacer, con criterio de cuándo está completo.}}
2. **{{Nombre del paso}}**. {{...}}
3. **{{...}}**

## Formato de respuesta
```text
{{estructura de la salida final del workflow completo}}
```

## Fallos prohibidos en este workflow
- {{comportamiento que invalida el resultado aunque "parezca" correcto}}
- {{...}}
```

## Variante: prompt chain (pasos como prompts separados)

Cuando cada paso es literalmente una llamada separada al modelo (no una sección de instrucciones dentro de un solo prompt), documenta además:

```text
## Contrato entre pasos
| Paso | Entrada que recibe | Salida que produce | Formato exacto |
|---|---|---|---|
| {{paso 1}} | {{...}} | {{...}} | {{...}} |
| {{paso 2}} | {{salida del paso 1}} | {{...}} | {{...}} |

## Manejo de fallo intermedio
{{Qué pasa si un paso intermedio no puede producir la salida esperada —
¿se detiene la cadena, se reintenta, se marca el resultado como parcial?}}
```

## Notas de uso

Un workflow no necesita todos los pasos numerados si el proceso real tiene ramas condicionales — en ese caso, usa una tabla de decisión ("si la situación es X, sigue el paso Y") en vez de forzar una secuencia lineal que no refleja la realidad.
