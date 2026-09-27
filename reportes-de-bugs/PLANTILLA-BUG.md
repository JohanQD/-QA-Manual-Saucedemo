# Plantilla de reporte de bug

> **Cómo usarla:** copia este archivo, renómbralo `BUG-001.md` (luego `BUG-002.md` y así sucesivamente) y reemplaza el texto entre corchetes. Registra también el bug en la hoja **Bugs** del Excel con el mismo ID.
>
> **Un buen título** dice dónde está el problema y qué pasa, en una línea. Formato: `[Módulo] usuario: qué falla`.
> Ejemplo de formato: `[Carrito] standard_user: el contador no se actualiza al quitar un producto`

---

# BUG-XXX: [Módulo] usuario: qué falla

| Campo | Detalle |
|---|---|
| **ID** | BUG-XXX |
| **Módulo** | [Login / Catálogo / Detalle / Carrito / Checkout / Menú] |
| **Usuario** | [standard_user / problem_user / …] |
| **Caso de prueba relacionado** | [TC-XXX] |
| **Severidad** | [Crítica / Alta / Media / Baja] |
| **Prioridad** | [Alta / Media / Baja] |
| **Frecuencia** | [Se reproduce 2 de 2 veces] |
| **Entorno** | [Chrome 1XX, Windows 11, 1920 × 1080] |
| **Fecha** | [DD/MM/AAAA] |

## Precondiciones

[Qué tiene que estar listo antes de empezar. Ejemplo: sesión iniciada con `standard_user` y un producto en el carrito.]

## Pasos para reproducir

1. [Primer paso]
2. [Segundo paso]
3. [Tercer paso]

## Resultado esperado

[Qué debería pasar.]

## Resultado obtenido

[Qué pasó en realidad.]

## Evidencia

![Descripción de la captura](../evidencias/BUG-XXX_descripcion.png)

## Notas

[Opcional: si con `standard_user` sí funciona, si pasa en otro navegador, ideas sobre la causa.]
