# Lógica de portadas por asignatura

## Regla principal

Cada asignatura debe tener una portada propia y estable. La portada se define por
una combinación fija de:

1. La asignatura.
2. Su paleta de colores.
3. Su patrón geométrico.

El patrón y la paleta se asignan a la asignatura, no al contenido temporal de una
card. Una card de entrega, clase guardada o calificación debe conservar la
identidad visual de la asignatura relacionada.

## Reglas que deben respetarse

- No repetir una asignatura en dos cards si el contenido puede pertenecer a otra.
- No cambiar una asignatura arbitrariamente para llenar una card.
- No usar la portada de Historia de México para una entrega, clase o calificación
  de otra asignatura.
- No inferir una asignatura que no exista en `COURSES`.
- Si no existe una asignatura adecuada, dejar el contenido sin asignar o pedir
  confirmación; no inventar una materia.
- Las materias de ciencias exactas, como `Cálculo Diferencial`, sí existen y
  deben conservarse cuando el contenido corresponda a ellas.
- No modificar la paleta o el patrón de una asignatura desde una card temporal.
- Los cambios de estado (`En vivo`, `Próxima entrega`, `Clase guardada`,
  `Calificación`) cambian el copy y la acción, no la identidad visual.

## Asignaturas registradas actualmente

| Asignatura | Área | Paleta actual |
|---|---|---|
| Introducción a la Psicología | Ciencias sociales | `#6C63D9` → `#8B82F1` |
| Historia de México Contemporáneo | Humanidades | `#E77A47` → `#F3B05B` |
| Cálculo Diferencial | Ciencias exactas | `#2A9D8F` → `#55C9A6` |
| Comunicación Oral y Escrita | Comunicación | `#2878A8` → `#65B5D5` |
| Alfabetización Digital | Tecnología | `#C05BA5` → `#EB8BC5` |
| Inglés Técnico B1 | Idiomas | `#5171C5` → `#7EA4EC` |

La fuente de verdad de esta lista es el arreglo `COURSES` de `index.html`.

## Patrón geométrico

El patrón de referencia debe reutilizarse como una composición fija. Para cada
asignatura:

- Se conserva la distribución de figuras.
- Se conservan las formas, proporciones y posiciones.
- Solo se sustituyen los colores por la paleta asignada a la asignatura.
- El patrón puede escalarse para adaptarse al contenedor, pero no debe girarse,
  reordenarse ni repetirse de forma arbitraria.
- La adaptación de tamaño no debe recortar la composición.

Actualmente `courseArt()` usa `COURSE_ART_PATTERN`. Para cumplir completamente
esta regla, la implementación debe evolucionar a un mapa por asignatura, por
ejemplo:

```js
var COURSE_COVER_CONFIG = {
  'Introducción a la Psicología': {
    colors: ['#6C63D9', '#8B82F1'],
    pattern: 'psychology'
  },
  'Historia de México Contemporáneo': {
    colors: ['#E77A47', '#F3B05B'],
    pattern: 'history'
  },
  'Cálculo Diferencial': {
    colors: ['#2A9D8F', '#55C9A6'],
    pattern: 'calculus'
  }
};
```

El ejemplo muestra la estructura esperada; no implica que deban inventarse
patrones distintos sin una referencia visual aprobada.

## Cards principales

Las cuatro cards principales representan estados o acciones del panel, pero su
contenido debe vincularse a una asignatura real:

1. **Clase en vivo:** Introducción a la Psicología. Usa la imagen de clase
   proporcionada; es la excepción al patrón geométrico.
2. **Próxima entrega:** se selecciona la entrega positiva más cercana de una
   asignatura real que no esté usada innecesariamente en otra card.
3. **Clase guardada:** muestra la última clase impartida de su asignatura real y
   usa la portada de esa asignatura.
4. **Calificación:** muestra la última entrega calificada de su asignatura real y
   usa la portada de esa asignatura, sin agregar un tag si no se solicita.

Antes de renderizar estas cards se debe comprobar que no haya asignaturas
repetidas sin justificación y que la portada coincida con la asignatura del copy.

## Cambios futuros

Antes de agregar o modificar una portada:

1. Confirmar que la asignatura existe en `COURSES`.
2. Confirmar la paleta asignada.
3. Confirmar el patrón que le corresponde.
4. Verificar que la card no esté mostrando otra asignatura.
5. Verificar que el patrón no se haya girado, duplicado o cambiado sin petición
   explícita.
