# 🌿 Invu 2 Verde — Plataforma Geoespacial Interactiva

> **Barrio INVU 2 | Liberia, Guanacaste, Costa Rica**  
> Sitio web estático publicado en **GitHub Pages** que visualiza cartografía de alta precisión generada mediante fotogrametría con dron (4 cm/px).

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Activo-22c55e?logo=github)](https://asoto59g.github.io/Invu2-Verde/)
[![Leaflet](https://img.shields.io/badge/Leaflet-1.9.4-brightgreen)](https://leafletjs.com)
[![Three.js](https://img.shields.io/badge/Three.js-r160-black)](https://threejs.org)
[![Licencia](https://img.shields.io/badge/Licencia-Uso%20Educativo-blue)](#)

---

## 🗺️ ¿Qué es este proyecto?

**Invu 2 Verde** es una plataforma de información territorial desarrollada por [ABC Geomática Agrícola SRL](https://abcgeomatica.com) como herramienta de gestión ambiental y diagnóstico urbano para el Barrio INVU 2 en Liberia, Guanacaste, Costa Rica.

Fue generada a partir de un levantamiento aerofotogramétrico con dron (ortofoto 4 cm/px, 13 de octubre de 2026) y digitalización manual de infraestructura vial, peatonal, redes hidráulicas y cobertura verde.

**Objetivo:** Proveer a la comunidad y al gobierno local de información territorial precisa para la formulación de propuestas urbanas sostenibles.

---

## 🏗️ Estructura del Repositorio

```
Invu2-Verde/
├── index.html              # Página principal (estadísticas, accesos rápidos)
├── mapa.html               # Visor cartográfico interactivo (Leaflet)
├── modelo3d.html           # Visor de modelo 3D fotogramétrico (Three.js)
├── reflexion.html          # Página de visión comunitaria y propuestas
├── acerca.html             # Información del proyecto y equipo
├── README.md               # Este archivo
└── assets/
    ├── tiles/              # Teselas de la ortofoto (XYZ tiles, Zoom 15–21)
    │   └── {z}/{x}/{y}.png
    ├── models/             # Modelo 3D fotogramétrico (ODM/OpenDroneMap)
    │   ├── odm_textured_model_geo.obj   # Malla 3D
    │   ├── odm_textured_model_geo.mtl   # Materiales
    │   └── textures/                    # Texturas PNG (66 archivos)
    │       └── odm_textured_model_geo_material000X_map_Kd.png
    ├── Perimetro.geojson   # Límite del Barrio INVU 2 (polígono)
    ├── Calles.geojson      # Red vial (MultiLineString)
    ├── Aceras.geojson      # Red peatonal (MultiLineString)
    ├── alcantpluvial.geojson    # Alcantarillado pluvial (MultiLineString)
    ├── alcantsanitario.geojson  # Alcantarillado sanitario (MultiLineString)
    ├── parques.geojson     # Parques y áreas recreativas (MultiPolygon)
    └── areas_verdes.json   # Arborización y zonas verdes (MultiPolygon)
```

> ⚠️ **Nota sobre sistema de coordenadas:** Todos los archivos GeoJSON están en **EPSG:32616** (UTM Zona 16N). El visor los reproyecta automáticamente a WGS84 usando [proj4js](https://github.com/proj4js/proj4js).

---

## 📄 Páginas del Sitio

### `index.html` — Inicio
Página de presentación con:
- Indicadores clave del barrio (superficie, red vial, aceras, coberturas)
- Accesos directos al mapa y visor 3D
- Tarjetas de resumen de infraestructura y servicios municipales

### `mapa.html` — Mapa Interactivo
Visor cartográfico construido con **Leaflet.js** que incluye:

| Característica | Detalle |
|---|---|
| **Capa base** | Ortofoto de dron 4 cm/px (tiles XYZ locales, zoom 15–21) |
| **Capas base alternativas** | Satélite Esri, OpenStreetMap |
| **Capas vectoriales** | Perímetro, Calles, Aceras, Pluvial, Sanitario, Parques, Zonas Verdes |
| **Reproyección** | UTM EPSG:32616 → WGS84 con proj4js (automática) |
| **Simbología** | Colores diferenciados por tipo de capa + leyenda visual |
| **Tooltips** | Al deslizar el mouse (hover) o tocar en móvil: nombre de capa y campos |
| **Popups** | Al hacer clic: todos los campos del feature en tabla |
| **Control de capas** | Panel para activar/desactivar capas individualmente |
| **fitBounds** | El mapa se centra y ajusta al máximo zoom posible sobre el perímetro |

**Simbología de capas:**

| Capa | Color | Tipo |
|---|---|---|
| Límite INVU 2 | 🟡 Amarillo punteado | Polígono (sin relleno) |
| Calles | ⬛ Gris oscuro | Línea gruesa |
| Aceras | ⬜ Gris claro | Línea delgada |
| Alcant. Pluvial | 🔵 Celeste | Línea punteada |
| Alcant. Sanitario | 🔴 Rojo | Línea punteada |
| Parques | 🟢 Verde intenso | Polígono con relleno |
| Zonas Verdes | 🟩 Verde claro | Polígono con relleno |

### `modelo3d.html` — Visor 3D
Visor interactivo del modelo fotogramétrico construido con **Three.js**:

| Característica | Detalle |
|---|---|
| **Formato** | OBJ + MTL (generado con OpenDroneMap) |
| **Texturas** | 66 imágenes PNG en `assets/models/textures/` |
| **Recentrado** | El modelo se centra automáticamente compensando coordenadas UTM |
| **Cámara** | Perspectiva 45° con distancia adaptativa al tamaño del modelo |
| **Controles** | Rotar (clic+arrastrar), Zoom (rueda), Pan (clic derecho) con amortiguación |
| **Iluminación** | Luz ambiental + luz solar + luz de relleno |
| **Progreso** | Barra de progreso real durante la descarga |

### `reflexion.html` — Comunidad
Página con análisis cualitativo, propuestas de mejora urbana y visión comunitaria del barrio.

### `acerca.html` — Acerca de
Información sobre el proyecto, metodología, equipo y tecnologías utilizadas.

---

## 🛠️ Tecnologías Utilizadas

| Tecnología | Versión | Uso |
|---|---|---|
| [Leaflet.js](https://leafletjs.com) | 1.9.4 | Mapa interactivo 2D |
| [Three.js](https://threejs.org) | r160 | Visor 3D |
| [Proj4js](https://github.com/proj4js/proj4js) | 2.11.0 | Reproyección de coordenadas UTM→WGS84 |
| [Tailwind CSS](https://tailwindcss.com) | CDN | Estilos y diseño responsivo |
| [Font Awesome](https://fontawesome.com) | 6.4.0 | Iconografía |
| [OpenDroneMap](https://opendronemap.org) | — | Procesamiento fotogramétrico del modelo 3D |

---

## 📊 Datos Técnicos del Levantamiento

| Parámetro | Valor |
|---|---|
| Fecha de vuelo | 13 de Octubre, 2026 |
| Resolución de la ortofoto | 4 cm/px |
| Sistema de coordenadas | EPSG:32616 (UTM Zona 16N, WGS84) |
| Área total del barrio | 11.41 Ha |
| Cobertura de los tiles | Zoom 15 – 21 |
| Modelo 3D | OBJ + 66 texturas (ODM) |

---

## 📏 Indicadores del Barrio

| Infraestructura | Valor |
|---|---|
| Superficie total | 11.41 Ha |
| Red vial (calles) | 2,645 m |
| Red peatonal (aceras) | 4,430 m |
| Alcantarillado pluvial | 2,379 m |
| Alcantarillado sanitario | 2,474 m |
| Parques y áreas recreativas | 9,122 m² |
| Arborización y zonas verdes | ~15% del área total (1.71 Ha) |

---

## 🚀 Despliegue en GitHub Pages

El sitio es completamente estático (HTML + JS + Assets). Para desplegarlo:

1. Haz fork o clona el repositorio
2. Ve a **Settings → Pages** en GitHub
3. Selecciona la rama `main` y el folder raíz `/`
4. El sitio estará disponible en `https://<usuario>.github.io/<repositorio>/`

> **⚠️ Importante:** GitHub Pages es sensible a mayúsculas/minúsculas en nombres de archivos. Los nombres de los GeoJSON deben coincidir exactamente con las rutas en el código HTML.

---

## 🔧 Desarrollo Local

Para probar el sitio localmente necesitas un servidor HTTP (no puedes abrir `index.html` directamente en el navegador por restricciones CORS al cargar GeoJSON):

```bash
# Con Python
python -m http.server 8000

# Con Node.js (npx)
npx serve .

# Con VS Code: instala la extensión "Live Server"
```

Luego abre `http://localhost:8000` en tu navegador.

---

## 📋 Campos de las Capas GeoJSON

### Perímetro (`Perimetro.geojson`)
| Campo | Tipo | Descripción |
|---|---|---|
| `id` | Integer | Identificador del polígono |
| `AreaHa` | Float | Área en hectáreas |

### Calles (`Calles.geojson`)
| Campo | Tipo | Descripción |
|---|---|---|
| `id` | Integer | Identificador del segmento |
| `long` | Integer | Longitud del segmento en metros |

### Aceras (`Aceras.geojson`)
| Campo | Tipo | Descripción |
|---|---|---|
| `id` | Integer | Identificador del segmento |
| `long` | Integer | Longitud del segmento en metros |

### Alcantarillado Pluvial (`alcantpluvial.geojson`)
| Campo | Tipo | Descripción |
|---|---|---|
| `id` | Integer | Identificador del tramo |
| `long` | Integer | Longitud del tramo en metros |

### Alcantarillado Sanitario (`alcantsanitario.geojson`)
| Campo | Tipo | Descripción |
|---|---|---|
| `id` | Integer | Identificador del tramo |
| `long` | Integer | Longitud del tramo en metros |

### Parques (`parques.geojson`)
| Campo | Tipo | Descripción |
|---|---|---|
| `id` | Integer | Identificador del parque |
| `aream2` | Integer | Área en metros cuadrados |

### Áreas Verdes (`areas_verdes.json`)
| Campo | Tipo | Descripción |
|---|---|---|
| `fid` | Integer | ID de la feature (clasificación raster vectorizada) |
| `DN` | Integer | Valor digital del raster fuente (DN=1: vegetación) |

---

## 👥 Créditos

**Desarrollado por:** ABC Geomática Agrícola SRL  
**Levantamiento aerofotogramétrico:** ABC Geomática Agrícola SRL  
**Procesamiento fotogramétrico:** OpenDroneMap  
**Datos cartográficos:** © ABC Geomática Agrícola SRL, 2026  

---

## 📄 Licencia

Este proyecto es de uso educativo y comunitario. Los datos geoespaciales son propiedad de ABC Geomática Agrícola SRL. No se permite su reproducción comercial sin autorización expresa.

---

*Última actualización: Octubre 2026 | Inspección aerofotogramétrica: 13 de Octubre, 2026*
