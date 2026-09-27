# Plan de pruebas: SauceDemo (Swag Labs)

| | |
|---|---|
| **Proyecto** | Pruebas manuales del flujo de compra de SauceDemo |
| **Tester** | Johan Felipe Quiñones Diaz |
| **Versión del plan** | 1.0 |
| **Fecha de inicio** | 27 de septiembre de 2026 |
| **Aplicación** | https://www.saucedemo.com |

---

## 1. Propósito

Este plan define qué se va a probar en SauceDemo, cómo, con qué criterios y en qué orden. Sirve de guía durante la ejecución y como registro de las decisiones tomadas.

## 2. Sistema bajo prueba

SauceDemo (Swag Labs) es una tienda en línea de práctica publicada por Sauce Labs. Vende seis productos y tiene un flujo de compra completo: inicio de sesión, catálogo, detalle de producto, carrito, checkout en dos pasos y confirmación del pedido.

**Módulos**

| Módulo | Página | Funciones principales |
|---|---|---|
| Login | `/` | Iniciar sesión y mostrar mensajes de error |
| Catálogo | `/inventory.html` | Listar productos, ordenar, agregar y quitar del carrito |
| Detalle de producto | `/inventory-item.html` | Ver un producto, agregarlo o quitarlo, volver al catálogo |
| Carrito | `/cart.html` | Ver y quitar productos, seguir comprando, ir al checkout |
| Checkout | `/checkout-step-one.html`, `/checkout-step-two.html`, `/checkout-complete.html` | Datos de envío, resumen con totales y confirmación |
| Menú lateral | Todas las páginas internas | All Items, About, Logout, Reset App State |

**Usuarios de prueba**

La contraseña de todos los usuarios aparece en la propia página de inicio de SauceDemo.

| Usuario | Para qué sirve en este proyecto |
|---|---|
| `standard_user` | Usuario normal. Es la **referencia de comportamiento correcto** (oráculo). |
| `locked_out_user` | Usuario bloqueado. No debe poder entrar. |
| `problem_user` | Trae fallas intencionales de funcionalidad y de interfaz. |
| `performance_glitch_user` | Trae demoras intencionales. |
| `error_user` | Trae errores intencionales en algunas acciones. |
| `visual_user` | Trae fallas visuales intencionales. |

## 3. Alcance

**Dentro del alcance**

- Flujo de compra completo en los seis módulos.
- Mensajes de error y validaciones de formularios.
- Cálculo de subtotal, impuesto y total en el checkout.
- Comportamiento de los seis usuarios de prueba, comparado contra `standard_user`.
- Compatibilidad básica: Chrome y Firefox en escritorio, y vista móvil simulada con Chrome DevTools.

**Fuera del alcance**

- Pagos reales. SauceDemo no tiene pasarela de pago.
- Pruebas de API o de base de datos.
- Pruebas de carga o estrés (muchos usuarios al mismo tiempo).
- Pruebas de seguridad avanzadas (inyección, manipulación de sesión).
- Auditoría completa de accesibilidad (WCAG).
- Contenido del sitio de Sauce Labs al que lleva el enlace "About"; solo se verifica que abra.
- Automatización. Queda como próximo paso.

## 4. Base de prueba: requisitos

SauceDemo no publica un documento de requisitos. Por eso los requisitos de este proyecto salen de dos fuentes:

- **Observado:** comportamiento de `standard_user` que se toma como correcto.
- **Inferido:** lo que se espera de cualquier tienda en línea aunque la app no lo haga. Estos requisitos los propone el tester y, en un equipo real, habría que confirmarlos con el dueño del producto antes de reportar un bug.

| ID | Requisito | Fuente |
|---|---|---|
| REQ-01 | El usuario con credenciales válidas accede al catálogo. | Observado |
| REQ-02 | El sistema muestra un mensaje claro cuando faltan datos o las credenciales son incorrectas. | Observado |
| REQ-03 | Un usuario bloqueado no puede ingresar. | Observado |
| REQ-04 | Seguridad básica: la contraseña se oculta, las páginas internas exigen sesión y el logout cierra la sesión. | Observado |
| REQ-05 | El catálogo muestra todos los productos con imagen, nombre, descripción y precio correctos. | Observado |
| REQ-06 | Los productos se pueden ordenar por nombre y por precio, en ambos sentidos. | Observado |
| REQ-07 | El usuario puede agregar y quitar productos, y el contador del carrito se actualiza. | Observado |
| REQ-08 | El detalle de producto muestra la misma información que el catálogo y permite volver. | Observado |
| REQ-09 | Nombre, apellido y código postal son obligatorios en el checkout. | Observado |
| REQ-10 | Los datos de envío deben tener un formato válido (no solo espacios; código postal válido). | Inferido |
| REQ-11 | El resumen calcula bien subtotal, impuesto y total. | Observado |
| REQ-12 | No se puede comprar con el carrito vacío. | Inferido |
| REQ-13 | El usuario puede cancelar o finalizar la compra; al finalizar se confirma el pedido y el carrito queda vacío. | Observado |
| REQ-14 | Las opciones del menú lateral hacen lo que indican. | Observado |
| REQ-15 | Todos los usuarios habilitados obtienen el mismo comportamiento funcional y visual que `standard_user`. | Inferido |
| REQ-16 | Las páginas cargan en 3 segundos o menos. | Inferido |
| REQ-17 | El flujo de compra funciona en Chrome, en Firefox y en vista móvil. | Inferido |

La relación entre cada requisito y sus casos de prueba (matriz de trazabilidad) está en la hoja **Requisitos** del Excel.

## 5. Estrategia de prueba

**Enfoque basado en riesgo.** Se prueba primero y más a fondo lo que más daño causaría si falla:

| Riesgo | Impacto | Prioridad de prueba |
|---|---|---|
| El cliente no puede iniciar sesión o terminar la compra | Venta perdida | Alta |
| El precio o el total no coinciden con lo que se muestra | Cobro incorrecto, reclamos | Alta |
| Un usuario sin permiso accede a páginas internas | Riesgo de seguridad | Alta |
| El carrito no refleja lo que el cliente eligió | Pedido equivocado | Alta |
| Ordenamiento, navegación o menú fallan | Mala experiencia | Media |
| Fallas visuales menores | Imagen de marca | Baja |

**Técnicas de diseño de casos**

| Técnica | Cómo se aplica aquí |
|---|---|
| Partición de equivalencia | Credenciales válidas, inválidas y de usuario bloqueado. |
| Valores límite | Carrito con 0, 1 y 6 productos (mínimo, uno y máximo). |
| Pruebas negativas | Campos vacíos, solo espacios, caracteres especiales. |
| Transición de estados | Botón "Add to cart" ↔ "Remove"; sesión iniciada ↔ cerrada. |
| Comparación con oráculo | El mismo flujo con cada usuario, comparado contra `standard_user`. |
| Exploratoria con tiempo límite | Sesiones de 30 minutos con una misión definida (ver abajo). |

**Sesiones exploratorias planeadas (Fase 3b)**

| Sesión | Misión | Duración |
|---|---|---|
| EXP-01 | Explorar `problem_user` en todo el flujo de compra para descubrir fallas que los casos escritos no cubren | 30 min |
| EXP-02 | Explorar `error_user` intentando todas las acciones posibles en catálogo y checkout | 30 min |
| EXP-03 | Explorar `visual_user` comparando cada pantalla contra `standard_user`, lado a lado | 30 min |

Cada sesión se registra con fecha, lo que se probó y lo que se encontró. Los hallazgos se agregan como casos nuevos o como bugs.

**Buenas prácticas durante la ejecución**

- Usar una **ventana de incógnito nueva** por cada usuario. SauceDemo guarda el carrito en el navegador, y los restos de una prueba pueden alterar la siguiente.
- Reproducir cada bug **al menos dos veces** antes de reportarlo.
- Tomar la captura **en el momento** del fallo, no después.
- No copiar hallazgos de otros repositorios públicos: cada bug se reproduce y se documenta con evidencia propia.

## 6. Entorno de prueba

| Elemento | Detalle |
|---|---|
| Sistema operativo | [Tu sistema operativo y versión] |
| Navegador principal | Google Chrome [versión: se ve en `chrome://settings/help`] |
| Navegador secundario | Mozilla Firefox [versión: menú › Ayuda › Acerca de Firefox] |
| Vista móvil | Chrome DevTools (`F12` › ícono de celular), dispositivo iPhone 12 Pro (390 × 844) |
| Resolución de escritorio | [Tu resolución, por ejemplo 1920 × 1080] |
| Herramientas | Excel / Google Sheets, herramienta de capturas del sistema, GitHub |

## 7. Criterios de entrada, salida y suspensión

**Entrada: se empieza a ejecutar cuando…**

- SauceDemo está disponible.
- Los requisitos y los casos de prueba están revisados (Fases 1 y 2 terminadas).
- El entorno está listo y las versiones de los navegadores anotadas.

**Salida: se da la ejecución por terminada cuando…**

- El 100 % de los casos de prioridad **Alta** está ejecutado.
- Al menos el 90 % del total de casos está ejecutado.
- Cada caso fallido tiene un bug asociado, con evidencia.
- Cada bug fue reproducido al menos dos veces o quedó marcado como "No reproducible".
- La hoja **Resumen** y la sección 6 del README están actualizadas.

> Como SauceDemo es una app de práctica, nadie va a corregir los bugs. Por eso el criterio de salida no es "cero bugs críticos abiertos", como sería en un proyecto real, sino que **todos los bugs estén documentados** y se pueda dar una recomendación clara.

**Suspensión: se pausa la ejecución si…**

- SauceDemo está caído o cambia de forma importante. Se anota la fecha y se retoma cuando vuelva.
- Un bug impide continuar un flujo. Los casos que dependen de ese flujo se marcan como **Bloqueado** y se sigue con los demás.

## 8. Clasificación de bugs

**Severidad: qué tan grave es el daño**

| Severidad | Definición | Ejemplo de referencia |
|---|---|---|
| Crítica | Bloquea una función principal y no hay forma de evitarlo. | No se puede terminar ninguna compra. |
| Alta | Una función importante falla o muestra datos incorrectos. | El total cobrado no coincide con los precios. |
| Media | Falla una función secundaria o hay un problema de interfaz que confunde. | El ordenamiento por precio no funciona. |
| Baja | Problema cosmético que no afecta el uso. | Un ícono desalineado. |

**Prioridad: qué tan pronto habría que corregirlo**

| Prioridad | Definición |
|---|---|
| Alta | Corregir antes de salir a producción. |
| Media | Corregir en la siguiente versión. |
| Baja | Corregir cuando haya tiempo. |

Cada bug se documenta con la [plantilla de bug](reportes-de-bugs/PLANTILLA-BUG.md) y se registra en la hoja **Bugs** del Excel.

## 9. Riesgos del proyecto

| Riesgo | Mitigación |
|---|---|
| No hay requisitos oficiales. | Requisitos marcados como observados o inferidos; `standard_user` como referencia. |
| La app es pública y puede cambiar sin aviso. | Anotar fecha y navegador en cada ejecución y guardar evidencia. |
| Datos que quedan en el navegador alteran los resultados. | Ventana de incógnito nueva por usuario. |
| El tiempo no alcanza para todos los casos. | Ejecutar primero todos los casos de prioridad Alta. |

## 10. Entregables

| Entregable | Ubicación |
|---|---|
| Plan de pruebas (este documento) | `plan-de-pruebas.md` |
| Casos de prueba, trazabilidad y registro de bugs | `casos-de-prueba/casos-de-prueba-saucedemo.xlsx` |
| Copia de los casos para ver en GitHub | `casos-de-prueba/casos-de-prueba.csv` |
| Reportes de bugs | `reportes-de-bugs/BUG-XXX.md` |
| Evidencias | `evidencias/` |
| Resumen de resultados y conclusiones | `README.md`, secciones 6 y 7 |

## 11. Hoja de ruta

Las duraciones son sugeridas; ajústalas a tu disponibilidad. Al terminar cada fase, sube los cambios a GitHub con el mensaje sugerido. Así el historial del repositorio muestra que el proyecto se construyó paso a paso, como pide la consigna.

| Fase | Qué se hace | Duración sugerida | Entregable | Mensaje para GitHub | Fecha real |
|---|---|---|---|---|---|
| **0. Preparación** | Crear el repositorio y subir el plan y las plantillas. | 1 día (hoy) | Repositorio publicado | `Plan de pruebas inicial` | 27/09/2026 |
| **1. Análisis de requisitos** | Recorrer la app con `standard_user` durante 30 a 45 minutos. Revisar los 17 requisitos, ajustarlos y anotar dudas. | 1 día | Hoja Requisitos revisada | `Requisitos revisados` | |
| **2. Diseño de casos** | Revisar los 50 casos del borrador: ajustar pasos y resultados esperados, agregar los que falten. | 1 a 2 días | Casos listos para ejecutar | `Casos de prueba listos` | |
| **3a. Ejecución, ciclo 1** | Ejecutar TC-001 a TC-040 (funcionalidad base, casi todo con `standard_user`) en Chrome. Registrar el resultado y reportar bugs. | 2 días | Estados y primeros bugs | `Ciclo 1 ejecutado` | |
| **3b. Ejecución, ciclo 2** | Ejecutar TC-041 a TC-050 (usuarios especiales, Firefox y móvil) y las sesiones EXP-01 a EXP-03. | 2 días | Bugs con evidencia | `Ciclo 2 ejecutado y bugs reportados` | |
| **4. Evaluación** | Volver a probar cada bug para confirmarlo. Completar la hoja Resumen y la sección 6 del README. | 1 día | Métricas finales | `Resultados y métricas` | |
| **5. Cierre** | Escribir las conclusiones (sección 7), revisar el checklist y compartir el link con el coach. | 1 día | Proyecto terminado | `Conclusiones y cierre` | |

**Total estimado:** de 9 a 10 días de trabajo.

## 12. Métricas

Todas se calculan solas en la hoja **Resumen** del Excel a medida que se llena la columna "Estado".

| Métrica | Fórmula |
|---|---|
| % de ejecución | Casos ejecutados ÷ total de casos |
| % de aprobación | Casos aprobados ÷ casos ejecutados |
| Cobertura de requisitos | Requisitos con al menos un caso ejecutado ÷ total de requisitos |
| Bugs por severidad | Conteo de bugs en cada nivel |
| Bugs por módulo y por usuario | Muestra dónde se concentran las fallas |
