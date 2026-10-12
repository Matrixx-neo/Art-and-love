# Cómo añadir o actualizar un jabón

El catálogo de la tienda se mantiene en `jabones.json`. Cada objeto `{ ... }`
representa un jabón. Al guardar el archivo, la web lo usa tanto para mostrar la
ficha como para incluir los jabones disponibles en los selectores de packs.

## Añadir una ficha

1. Coloca la fotografía optimizada en `images/jabones/` (crea esa carpeta en la
   raíz del proyecto si todavía no existe) y anota su ruta relativa, por ejemplo
   `images/jabones/jabon-nuevo.webp`. También puedes usar una URL pública segura
   que comience con `https://`.
2. Copia una ficha disponible en `jabones.json`, pégala como un nuevo objeto
   separado por una coma y actualiza los campos:

```json
{
  "id": "jabon-nombre-unico",
  "name": "Jabón Nombre",
  "cartName": "Jabón Nombre",
  "line": "renacer",
  "image": "images/jabones/jabon-nombre.webp",
  "alt": "Jabón artesanal Nombre, con ingrediente principal",
  "ingredients": "Ingrediente principal • Otro ingrediente",
  "size": "150 g",
  "tag": "Aceite de Oliva & Vitamina E",
  "description": "Descripción fiel del producto, sus ingredientes y su presentación.",
  "availability": "available",
  "price": 20,
  "launch": true
}
```

3. Guarda el JSON y comprueba la web en un servidor local. Para abrirla desde
   VS Code se puede usar la extensión Live Server; también sirve ejecutar
   `python -m http.server 8767` en la carpeta del proyecto y visitar
   `http://127.0.0.1:8767/`. No abras `index.html` directamente como archivo,
   porque el navegador bloquea la carga del catálogo JSON.

## Reglas de los campos

- `id`: único en todo el catálogo; usa minúsculas, números y guiones, sin espacios
  ni tildes.
- `line`: usa `equilibrio`, `renacer` o `vitalidad`.
- `image`: URL `https://` o ruta relativa dentro del proyecto. Evita rutas que
  salgan de la carpeta del sitio.
- `alt`: describe la fotografía para personas que usan lector de pantalla.
- `ingredients`, `description`, `name` y `cartName`: textos visibles; revisa
  tildes, ingredientes y presentación antes de publicar.
- `size`: opcional si el tamaño no está confirmado.
- `availability`: `available` requiere un `price` mayor que cero; `launch` debe
  ser `true` o `false`. `launch` determina si la promoción configurada en el
  sitio puede aplicarse al jabón.
- Para un jabón sin precio confirmado, usa `"availability": "inquiry"`,
  `"price": null` y `"launch": false`. Se mostrará una opción para preguntar por
  WhatsApp y no se podrá añadir al carrito.
- `selectable` es opcional. Si se omite, un jabón disponible aparece también en
  los selectores de packs. Usa `"selectable": false` únicamente cuando deba
  mostrarse en el catálogo pero no ofrecerse como opción de personalización,
  como ocurre con Dúo Armonía.

Evita publicar afirmaciones terapéuticas o promesas sobre resultados que no estén
confirmadas. Las fichas se muestran como texto seguro: el contenido del JSON no
debe contener HTML.
