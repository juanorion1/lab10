# Protocolo de Code Review Forense

> **Cuándo ejecutar**: Después de que **todos** los bloques de implementación estén completos.
> La revisión por bloque ya ocurrió en la fase I. Este protocolo es la **auditoría final del conjunto**.

> **Postura por defecto**: Asumir que algo está mal hasta demostrar lo contrario.
> No se hace commit sin completar este protocolo.

---

## Eje 1: Alucinaciones

> La IA inventa con confianza. Verifica existencia real de todo lo referenciado.

- [ ] Las librerías importadas existen y tienen la versión correcta
- [ ] Los métodos y funciones llamados existen en esas librerías
- [ ] Las rutas de archivos referenciadas existen en el proyecto
- [ ] No hay dependencias en el código que no estaban en el brief

**Notas / hallazgos:**
<!-- Documenta aquí cualquier alucinación encontrada -->

---

## Eje 2: Lógica de negocio

> El código puede funcionar técnicamente y estar mal lógicamente.

- [ ] La lógica implementada refleja exactamente lo que el brief pedía
- [ ] Los casos borde definidos en el brief están cubiertos en el código
- [ ] No hay suposiciones implícitas en el código que no estaban en el brief

**Notas / hallazgos:**
<!-- Documenta aquí cualquier discrepancia lógica -->

---

## Eje 3: Seguridad

- [ ] Los inputs del usuario están siendo validados
- [ ] No se expone información sensible en logs o mensajes de error
- [ ] No se introducen dependencias con vulnerabilidades conocidas
- [ ] El manejo de errores es el que se definió en el brief

**Notas / hallazgos:**
<!-- Documenta aquí cualquier vulnerabilidad encontrada -->

---

## Eje 4: Contexto del brief

> La IA puede perder restricciones del brief a medida que avanza.

- [ ] Se respetaron **todas** las restricciones definidas en el brief
- [ ] No se tocó ningún archivo o carpeta que estaba prohibido
- [ ] La Definition of Done está completamente cubierta

**Notas / hallazgos:**
<!-- Documenta aquí cualquier restricción violada -->

---

## Eje 5: Código innecesario

> La IA tiende a generar más de lo que se pidió.

- [ ] No hay código que nadie pidió y que igual apareció
- [ ] No hay abstracciones o generalizaciones que no estaban en el plan
- [ ] El código generado es el mínimo necesario para cumplir el brief

**Notas / hallazgos:**
<!-- Documenta aquí cualquier exceso de código -->

---

## Pregunta de cierre

> Aplica esta pregunta a **cada archivo** modificado o creado:

**¿Debería este código existir y ser enviado a producción?**

| Archivo | Decisión | Acción |
|---------|----------|--------|
| <!-- nombre_archivo --> | ✅ Sí / ⚠️ Parcialmente / ❌ No | <!-- acción requerida --> |
| <!-- nombre_archivo --> | ✅ Sí / ⚠️ Parcialmente / ❌ No | <!-- acción requerida --> |

### Guía de decisión

- **✅ Sí** → Puede ir al commit.
- **⚠️ Parcialmente** → Identifica qué parte no debería estar, corrígela y vuelve a revisar solo esa parte.
- **❌ No** → Descarta el bloque. Regresa a la fase correspondiente:
  - **Brief** si el contexto era incompleto
  - **Plan** si la estructura era incorrecta
  - **Implementación** si el error es de ejecución

---

## Resultado final

- [ ] **Todos los ejes pasaron** → Commit aprobado ✅
- [ ] **Se detectaron problemas** → Regresar a la fase correspondiente (B / P / I), **no parchear**
