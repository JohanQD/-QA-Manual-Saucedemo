# Proyecto QA manual: SauceDemo (Swag Labs)

**Pruebas funcionales manuales del flujo de compra de una tienda en línea, de principio a fin: inicio de sesión, catálogo, carrito y checkout.**

| | |
|---|---|
| **Estado** | 🟡 En progreso: Fase 1, análisis de requisitos |
| **Tester** | [Tu nombre completo] |
| **Tipo de prueba** | Manual, funcional, de caja negra |
| **Casos de prueba** | 50 diseñados · 0 ejecutados |
| **Bugs reportados** | 0 (se actualiza durante la ejecución) |

**Documentos del proyecto**

- 📋 [Plan de pruebas y hoja de ruta](plan-de-pruebas.md)
- 📊 [Casos de prueba (vista rápida en GitHub)](casos-de-prueba/casos-de-prueba.csv) · [Descargar Excel completo](casos-de-prueba/casos-de-prueba-saucedemo.xlsx)
- 🐞 [Reportes de bugs](reportes-de-bugs/)
- 📸 [Evidencias](evidencias/)

---

## 1. Información general

| Campo | Detalle |
|---|---|
| **Nombre del proyecto** | Pruebas manuales del flujo de compra de SauceDemo |
| **Especialidad** | QA |
| **Fuente del proyecto** | SauceDemo (Swag Labs), una tienda en línea de práctica creada por Sauce Labs para entrenar testers. Trae varios usuarios de prueba, algunos con fallas intencionales. |
| **Link a la fuente original** | https://www.saucedemo.com |
| **Link al proyecto publicado** | https://github.com/[tu-usuario]/qa-manual-saucedemo |

## 2. Objetivo

Verificar que un cliente pueda iniciar sesión, elegir productos y completar una compra en SauceDemo sin errores, y que el precio que ve sea el que paga. El plan de pruebas busca prevenir los riesgos que más le cuestan a una tienda en línea: clientes que no pueden comprar, cobros con montos incorrectos y pantallas rotas que generan desconfianza. El resultado le sirve a un equipo de producto para decidir si una versión está lista para salir a producción.

## 3. Plan de trabajo

| # | Paso | Qué incluye | Estado |
|---|---|---|---|
| 1 | **Análisis de requisitos** | Explorar la app como lo haría un usuario y documentar los requisitos. Como SauceDemo no trae documentación, los requisitos se infieren del comportamiento de `standard_user` y de lo que se espera de cualquier tienda en línea. | 🟡 En progreso |
| 2 | **Diseño de casos de prueba** | Escribir los casos con técnicas de partición de equivalencia, valores límite, pruebas negativas y comparación entre tipos de usuario. Cada caso queda enlazado a un requisito (matriz de trazabilidad). | ✅ Borrador listo (50 casos) |
| 3 | **Ejecución de pruebas** | Ciclo 1 con `standard_user`. Ciclo 2 con los usuarios especiales, en otro navegador y en vista móvil. Cada fallo se documenta como bug, con evidencia. | ⬜ Pendiente |
| 4 | **Evaluación** | Calcular la cobertura de requisitos, el porcentaje de ejecución y de aprobación, y los bugs por severidad y por módulo. | ⬜ Pendiente |
| 5 | **Conclusiones y próximos pasos** | Resumir los hallazgos, las lecciones aprendidas y qué se automatizaría después. | ⬜ Pendiente |

El detalle de cada fase, con tiempos y entregables, está en la [hoja de ruta del plan de pruebas](plan-de-pruebas.md#11-hoja-de-ruta).

## 4. Preguntas clave

1. **¿Qué pasaría si uno de estos bugs llega a producción?** No todos los bugs pesan igual. Un cliente que no puede terminar la compra o que paga un precio distinto al que vio es dinero perdido y un posible reclamo. Un ícono torcido, no. ¿Cuáles de los bugs encontrados bloquearían la salida a producción y cuáles pueden esperar?
2. **¿Qué di por correcto sin que nadie lo confirmara?** SauceDemo no tiene documento de requisitos. Algunos comportamientos esperados los asumí yo; por ejemplo, que no se pueda comprar con el carrito vacío o que el código postal tenga un formato válido. En un equipo real, ¿quién debería confirmar esos requisitos antes de reportarlos como bugs?
3. **¿Qué quedó por fuera y qué riesgo implica?** Este proyecto no cubre pagos reales, accesibilidad, seguridad a fondo ni rendimiento con muchos usuarios a la vez. ¿Cuál de esos huecos sería el más peligroso en una tienda real?

## 5. Qué se hizo y cómo

> Esta sección se completa durante la ejecución (Fases 3 y 4). Lo que aparece abajo es lo planeado; se ajusta con lo que realmente se haga.

**Tipos de prueba aplicados**

- Pruebas funcionales positivas: el camino feliz del flujo de compra.
- Pruebas negativas: campos vacíos, credenciales incorrectas, usuario bloqueado, carrito vacío.
- Pruebas de interfaz: imágenes, precios, textos y botones correctos.
- Pruebas comparativas por tipo de usuario: el mismo flujo con cada usuario, usando `standard_user` como referencia de comportamiento correcto.
- Pruebas exploratorias con límite de tiempo, para encontrar lo que los casos escritos no cubren.
- Compatibilidad básica: Chrome, Firefox y vista móvil.

**Herramientas**

- Excel / Google Sheets: casos de prueba, trazabilidad y registro de bugs.
- Chrome DevTools: vista móvil y consola de errores.
- Herramienta de capturas del sistema (en Windows, `Win + Shift + S`; en Mac, `Cmd + Shift + 4`): evidencia de cada bug.
- GitHub: publicación del proyecto e historial de avances.

**Criterios de aceptación.** Ver el [plan de pruebas, sección 7](plan-de-pruebas.md#7-criterios-de-entrada-salida-y-suspensión).

**Decisiones tomadas durante la ejecución**

- _Pendiente: anotar aquí cualquier cambio de plan y por qué se hizo._

## 6. Resultados

> Se completa al terminar la Fase 4. Los números salen de la hoja **Resumen** del Excel.

| Métrica | Resultado |
|---|---|
| Casos ejecutados | _— de 50_ |
| Casos aprobados | _—_ |
| Casos fallidos | _—_ |
| Casos bloqueados | _—_ |
| Cobertura de requisitos | _— de 17_ |
| Bugs encontrados | _—_ |

**Bugs por severidad**

| Crítica | Alta | Media | Baja |
|---|---|---|---|
| — | — | — | — |

**Bugs más importantes**

| ID | Título | Módulo | Usuario | Severidad |
|---|---|---|---|---|
| _BUG-001_ | _Pendiente_ | | | |

## 7. Conclusiones

> Se completa en la Fase 5. Preguntas guía:

- **¿Qué aprendí?** _Pendiente_
- **¿Qué mejoraría con más tiempo o recursos?** _Pendiente_
- **¿Qué parte mencionaría en una entrevista?** _Pendiente_

## 8. Checklist antes de publicar

- [ ] El README explica el proyecto sin necesidad de revisar todo el detalle
- [ ] Archivos organizados, sin pruebas sueltas ni versiones viejas
- [ ] Sin credenciales ni datos sensibles en el repositorio (solo se mencionan los usuarios de práctica que SauceDemo publica en su propia página de inicio)
- [ ] Link a la fuente original incluido y funcionando
- [ ] Proyecto publicado y accesible
- [ ] Link compartido con mi coach

---

## Estructura del repositorio

```
qa-manual-saucedemo/
├── README.md                     ← este documento
├── plan-de-pruebas.md            ← alcance, estrategia, criterios y hoja de ruta
├── casos-de-prueba/
│   ├── casos-de-prueba-saucedemo.xlsx   ← archivo de trabajo (casos, requisitos, bugs, resumen)
│   └── casos-de-prueba.csv              ← copia de los casos para verlos en GitHub
├── reportes-de-bugs/
│   ├── PLANTILLA-BUG.md          ← formato para cada bug
│   └── BUG-001.md, BUG-002.md…
└── evidencias/
    └── capturas de pantalla de cada bug
```
