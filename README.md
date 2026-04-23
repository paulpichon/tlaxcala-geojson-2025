# tlaxcala-geojson-2025
Este repositorio contiene datos GeoJSON de los 60 municipios de TLAXCALA

# GeoJSON de los Municipios de Tlaxcala

Este repositorio contiene la delimitación geográfica oficial de los **60 municipios del estado de Tlaxcala, México**.  

Los datos están organizados en un formato **GeoJSON (FeatureCollection)** estandarizado, optimizado para su uso en aplicaciones web, análisis de datos y sistemas de información geográfica (SIG).

---

## 🚀 Características del Dataset

- **Formato:** GeoJSON estándar (FeatureCollection)  
- **Cobertura:** 60 municipios de Tlaxcala  
- **Proyección:** WGS84 (EPSG:4326), compatible con la mayoría de las herramientas modernas  
- **Atributos:** Incluye claves geográficas oficiales (INEGI) y nombres de municipios  

---

## 📊 Estructura de los Datos

Cada objeto dentro del arreglo `features` representa un municipio y sigue este esquema:

```json
{
  "type": "Feature",
  "properties": {
    "CVEGEO": "29001",
    "CVE_ENT": "29",
    "NOMGEO": "Tlaxcala",
    "CVE_MUN": "001",
    "NOMMUN": "Amaxac de Guerrero",
    "cov_": 2068,
    "cov_id": 2069
  },
  "geometry": {
    "type": "MultiPolygon",
    "coordinates": [ ... ]
  }
}
```
## 📖 Diccionario de Propiedades
| Propiedad | Descripción |
|----------|------------|
| CVEGEO   | Clave concatenada de Entidad y Municipio (5 caracteres) |
| CVE_ENT  | Clave de la Entidad Federativa (29 para Tlaxcala) |
| NOMGEO   | Nombre del estado al que pertenece |
| CVE_MUN  | Clave del Municipio (tres dígitos) |
| NOMMUN   | Nombre oficial del municipio |
| cov_     | Identificador de cobertura interno |

## 🛠️ Cómo utilizar este archivo
🌐 En Web (JavaScript/Leaflet)
Puedes cargar el archivo directamente en un mapa interactivo:
```
fetch('tlaxcala.json')
  .then(res => res.json())
  .then(data => {
    L.geoJSON(data, {
      style: { color: "#ff7800", weight: 2 },
      onEachFeature: (feature, layer) => {
        layer.bindPopup(feature.properties.NOMMUN);
      }
    }).addTo(map);
  });
```


## 🐍 En Python (GeoPandas)

Para análisis de datos espaciales:
```
import geopandas as gpd

gdf = gpd.read_file('municipios_tlaxcala.json')
print(gdf.head())
gdf.plot()
```

## 📚 Fuente de los Datos

Este recurso ha sido procesado a partir de la información pública disponible en: 

[División Política de México Estatal y Municipal en GeoJSON 2024 - DataMX](https://datamx.io/ne/dataset/division-politica-de-mexico-estatal-y-municipal-en-geojson-2024).


## 📝 Licencia
Este repositorio se distribuye bajo la licencia de datos abiertos. 

Siéntete libre de clonarlo, modificarlo e integrarlo en tus proyectos. Se agradece la atribución a la fuente original de `DataMX`.

Repositorio creado para facilitar el acceso a información geoespacial de Tlaxcala.

`Hecho con ❤️ para la comunidad de datos abiertos en México.`






