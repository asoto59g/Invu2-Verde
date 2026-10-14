# 🌿 Invu 2 Verde — Plataforma Geoespacial Interactiva

> **Barrio INVU 2 | Liberia, Guanacaste, Costa Rica**  
> Sitio web estático publicado en **GitHub Pages** que visualiza cartografía de alta precisión generada mediante fotogrametría con dron (4 cm/px).

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Activo-22c55e?logo=github)](https://asoto59g.github.io/Invu2-Verde/)
[![Leaflet](https://img.shields.io/badge/Leaflet-1.9.4-brightgreen)](https://leafletjs.com)
[![Three.js](https://img.shields.io/badge/Three.js-r160-black)](https://threejs.org)
[![Turf.js](https://img.shields.io/badge/Turf.js-6.5-orange)](https://turfjs.org/)
[![Licencia](https://img.shields.io/badge/Licencia-Uso%20Educativo-blue)](#)

---

## 🗺️ ¿Qué es este proyecto?

**Invu 2 Verde** es una plataforma de información territorial desarrollada por Alejandro Soto como herramienta de gestión ambiental y diagnóstico urbano para el Barrio INVU 2 en Liberia, Guanacaste, Costa Rica.

Generada a partir de un levantamiento aerofotogramétrico con dron (ortofoto 4 cm/px, 12 de octubre de 2026) y digitalización de infraestructura vial, peatonal, redes hidráulicas y cobertura verde.

link de portal:  https://asoto59g.github.io/Invu2-Verde/index.html

---

## 🏗️ Estructura del Repositorio

```
Invu2-Verde/
├── index.html              # Página principal (estadísticas, accesos rápidos)
├── mapa.html               # Visor cartográfico interactivo (Leaflet + GPS + Mediciones)
├── modelo3d.html           # Visor 3D fotogramétrico interactivo (Three.js estilo Sketchfab)
├── reflexion.html          # Página de visión comunitaria y propuestas
├── acerca.html             # Información del proyecto y equipo
├── README.md               # Este archivo
└── assets/
    ├── tiles/              # Teselas de la ortofoto (XYZ tiles, Zoom 15–21)
    │   └── {z}/{x}/{y}.png
    ├── models/             # Modelo 3D fotogramétrico (ODM/OpenDroneMap)
    │   ├── odm_textured_model_geo.obj   # Malla 3D
    │   ├── odm_textured_model_geo.mtl   # Materiales
    │   └── textures/                    # 67 texturas PNG
    ├── Perimetro.geojson       # Límite del Barrio INVU 2 (polígono)
    ├── Calles.geojson          # Red vial con condición ("Buena" vs "Regular")
    ├── Aceras.geojson          # Red peatonal
    ├── alcantpluvial.geojson    # Red de alcantarillado pluvial
    ├── alcantsanitario.geojson  # Red de alcantarillado sanitario
    ├── parques.geojson         # Parques y áreas recreativas
    └── zonas_verdes.geojson    # Arborización y zonas verdes vectorizadas
```

---

## 📄 Características de las Páginas

### 1. `mapa.html` — Visor Cartográfico y de Campo

| Funcionalidad | Descripción |
|---|---|
| **Capa Base Ortofoto** | Teselas locales de ortofoto a 4 cm/px (Zoom 15–22). |
| **Bases Alternativas** | Esri World Imagery (Satélite) y OpenStreetMap. |
| **Condición de Calles** | Representación diferenciada de red vial según su estado: **Buena** (línea sólida oscura) vs **Regular** (línea discontinua ámbar). |
| **Arborización y Parques** | Cobertura verde vectorizada (`zonas_verdes.geojson`) con popup de datos y resaltado hover. |
| **GPS del Teléfono** | Botón flotante para activar geolocalización en tiempo real con precisión en metros y marcador pulsante. |
| **Medición de Distancia** | Herramienta para trazar líneas continuas con cálculo geodésico exacto en metros y kilómetros. |
| **Medición de Área** | Herramienta para trazar polígonos y calcular superficie en m² y Hectáreas (Ha). |
| **Reproyección Automática** | Convierte automáticamente coordenadas UTM EPSG:32616 a WGS84 con `proj4js`. |
| **Simbología y Tooltips** | Leyenda completa en esquina inferior izquierda y tooltips interactivos al pasar el mouse o dedo en el teléfono. |

### 2. `modelo3d.html` — Visor 3D Estilo Sketchfab

| Funcionalidad | Descripción |
|---|---|
| **Vista Inicial** | Vista superior con zoom levemente inclinada (~72° desde horizontal), encuadrando el barrio con el máximo detalle. |
| **Controles Sketchfab** | • **1 dedo / Clic Izq:** Rotar órbita alrededor del pivote con amortiguación suave.<br>• **2 dedos / Clic Der:** Desplazamiento (Pan) en el plano de pantalla.<br>• **Rueda / Pellizco:** Zoom progresivo. |
| **Doble Clic (Pivote Dinámico)** | Al hacer doble clic sobre cualquier punto del modelo 3D, el centro de rotación se reubica suavemente en esa superficie con retícula visual indicadora. |
| **Barra Inferior Flotante** | Botones rápidos para: Vista Inicial, Vista en Planta (Cenital), Perspectiva 45°, Auto-Giro y Ayuda. |
| **Iluminación** | Luz ambiental hemisférica y luz direccional calibradas para texturas fotogramétricas ODM. |

---

## 📋 Simbología Oficial del Mapa

| Elemento | Estilo Visual | Propiedades en Popup |
|---|---|---|
| **Límite INVU 2** | 🟡 Línea discontinua amarilla | ID, Área (Ha) |
| **Calles (Buena)** | ⬛ Línea sólida gris oscuro (4px) | ID, Longitud (m), Condición (Buena) |
| **Calles (Regular)** | 🟠 Línea discontinua ámbar (4.5px) | ID, Longitud (m), Condición (Regular) |
| **Aceras** | ⬜ Línea discontinua gris claro (2px) | ID, Longitud (m) |
| **Alcant. Pluvial** | 🔵 Línea discontinua celeste (2.5px) | ID, Longitud (m) |
| **Alcant. Sanitario**| 🔴 Línea discontinua roja (2.5px) | ID, Longitud (m) |
| **Parques** | 🟢 Polígono verde esmeralda con borde | ID, Área (m²) |
| **Zonas Verdes** | 🟩 Polígono verde claro semitransparente | ID, FID, Clase DN |

---

## 👥 Créditos

**Desarrollado por:** oasotob@gmail.com
**Levantamiento aerofotogramétrico:** (12 de Octubre, 2026)  
**Procesamiento:** OpenDroneMap & QGIS  
