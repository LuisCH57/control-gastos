# Control de gastos personales

Aplicación web para registrar gastos en soles, ver en qué categoría se gasta más y consultar el total en otras monedas con el tipo de cambio del día.

**Demo:** https://luisch57.github.io/control-gastos/

## Funcionalidades

- Registrar gastos con descripción, monto, fecha y categoría.
- Validar el formulario antes de guardar (campos vacíos o montos no válidos).
- Ver el total gastado y un resumen por categoría con barras de porcentaje.
- Eliminar gastos del historial, con confirmación.
- Conservar los datos al cerrar o recargar el navegador.
- Convertir el total a otras monedas (USD, EUR, CLP, COP, MXN, BRL, ARS) con una API pública.

## Tecnologías

- HTML y CSS (Grid, Flexbox y media queries)
- JavaScript sin librerías: DOM, eventos y `fetch` con `async`/`await`
- `localStorage` y JSON para guardar los datos en el navegador
- [ExchangeRate-API](https://www.exchangerate-api.com) (acceso abierto, sin clave) para los tipos de cambio
- Git y GitHub Pages

## Cómo funciona

Toda la aplicación gira en torno a una lista de gastos, que es la única fuente de verdad. Cada vez que algo cambia, se siguen tres pasos:

1. Modificar la lista.
2. Guardarla en `localStorage`.
3. Volver a dibujar la pantalla completa a partir de la lista (`render()`).

## Decisiones técnicas

- **Montos en céntimos:** S/ 12.50 se guarda como `1250`. Así se evitan los errores de redondeo de los números decimales (en JavaScript, `0.1 + 0.2` da `0.30000000000000004`).
- **`textContent` en lugar de insertar HTML:** lo que escribe el usuario se muestra siempre como texto y nunca se ejecuta como código.
- **Caché del tipo de cambio:** la API se actualiza una vez al día y limita las peticiones, así que la respuesta se guarda en `localStorage` hasta la siguiente actualización.
- **Manejo de errores:** si no hay conexión o la API falla, la app muestra un mensaje claro y un botón para reintentar.

## Problemas encontrados

- Al publicar, la carpeta del proyecto quedó conectada al repositorio de mi portafolio y lo reemplazó. Lo detecté con `git remote -v`, le di a este proyecto su propio repositorio y recuperé el portafolio con `git revert`, sin perder historial.

## Limitaciones y mejoras futuras

- Los datos viven solo en el navegador donde se registran: no se sincronizan entre dispositivos. Una base de datos con un backend resolvería esto.
- Agregar edición de gastos y filtros por mes.

## Cómo ejecutarlo

1. Descarga o clona este repositorio.
2. Abre `index.html` con la extensión Live Server de VS Code.
