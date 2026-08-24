# Datos GeoJSON TLAXCALA
Este repositorio contiene datos GeoJSON de los 60 municipios y sus 1,741 localidades de TLAXCALA

# GeoJSON de los Municipios y Localidades de Tlaxcala

Este repositorio contiene la delimitación geográfica oficial de los **60 municipios del estado de Tlaxcala, México**, enriquecida con el catálogo de sus **1,741 localidades**.  

Los datos están organizados en un formato **GeoJSON (FeatureCollection)** estandarizado, optimizado para su uso en aplicaciones web, análisis de datos y sistemas de información geográfica (SIG).

---

## 🎯 ¿Por qué este repositorio?

Aunque existen algunos repositorios con datos GeoJSON de estados, municipios y localidades de México, no encontré ninguno dedicado exclusivamente a **Tlaxcala**; sí encontré algunos con todos los estados y sus respectivos municipios y localidades, pero este espacio busca ser algo más enfocado: un dataset solo para Tlaxcala, más ligero y fácil de mantener y encontrar.

Por eso este repositorio se quedará únicamente para Tlaxcala, con la esperanza de que otros desarrolladores añadan o aporten mejoras, correcciones o datos adicionales si lo creen necesario. ¡Toda contribución es bienvenida!

---

## 🚀 Características del Dataset

- **Formato:** GeoJSON estándar (FeatureCollection)  
- **Cobertura:** 60 municipios de Tlaxcala  
- **Localidades:** 1,741 localidades anidadas dentro de cada municipio, con nombre oficial, clave INEGI, altitud y coordenadas  
- **Proyección:** WGS84 (EPSG:4326), compatible con la mayoría de las herramientas modernas  
- **Atributos:** Incluye claves geográficas oficiales (INEGI), nombres de municipios y código postal  

---

## 📊 Estructura de los Datos

Cada objeto dentro del arreglo `features` representa un municipio e incluye sus localidades como propiedad anidada:

```json
{
  "type": "Feature",
  "properties": {
    "CVEGEO": "29001",
    "CVE_ENT": "29",
    "NOMGEO": "Tlaxcala",
    "CVE_MUN": "001",
    "NOMMUN": "Amaxac de Guerrero",
    "CODIGO_POSTAL": "90640",
    "LOCALIDADES": [
      {
        "clave": "0001",
        "nombre": "Amaxac de Guerrero",
        "altitud": 2300,
        "coordenadas": [-98.169569, 19.350286]
      },
      {
        "clave": "0002",
        "nombre": "San Damián Tlacocalpan",
        "altitud": 2504,
        "coordenadas": [-98.219293, 19.373136]
      }
    ]
  },
  "geometry": {
    "type": "MultiPolygon",
    "coordinates": [ ... ]
  }
}
```
## 📖 Diccionario de Propiedades

### Nivel municipio
| Propiedad | Descripción |
|----------|------------|
| CVEGEO   | Clave concatenada de Entidad y Municipio (5 caracteres) |
| CVE_ENT  | Clave de la Entidad Federativa (29 para Tlaxcala) |
| NOMGEO   | Nombre del estado al que pertenece |
| CVE_MUN  | Clave del Municipio (tres dígitos) |
| NOMMUN   | Nombre oficial del municipio |
| CODIGO_POSTAL | Código postal de referencia del municipio |
| LOCALIDADES | Arreglo con las localidades del municipio |

### Nivel localidad (`LOCALIDADES`)
| Campo | Descripción |
|-------|-------------|
| clave | Clave geográfica de la localidad (cuatro dígitos, INEGI) |
| nombre | Nombre oficial de la localidad |
| altitud | Altitud sobre el nivel del mar (metros) |
| coordenadas | Par `[longitud, latitud]` en WGS84 |

## 🛠️ Cómo utilizar este archivo
🌐 En Web (JavaScript/Leaflet)
Puedes cargar el archivo directamente en un mapa interactivo:
```js
fetch('tlaxcala.json')
  .then(res => res.json())
  .then(data => {
    L.geoJSON(data, {
      style: { color: "#ff7800", weight: 2 },
      onEachFeature: (feature, layer) => {
        const p = feature.properties;
        layer.bindPopup(`${p.NOMMUN} — ${p.LOCALIDADES.length} localidades`);
      }
    }).addTo(map);
  });
```

📍 Acceder a las localidades de cada municipio:
```js
data.features.forEach(municipio => {
  municipio.properties.LOCALIDADES.forEach(loc => {
    console.log(`${loc.nombre} (${loc.altitud} msnm): ${loc.coordenadas}`);
  });
});
```


## 🐍 En Python (GeoPandas)

Para análisis de datos espaciales:
```python
import geopandas as gpd

gdf = gpd.read_file('tlaxcala.json')
print(gdf.head())
gdf.plot()
```

Y para explorar las localidades:
```python
import json

with open('tlaxcala.json', encoding='utf-8') as f:
    data = json.load(f)

localidades = [
    loc
    for feature in data['features']
    for loc in feature['properties']['LOCALIDADES']
]
print(len(localidades))  # 1741
```

## 📚 Fuentes de los Datos

Este recurso ha sido integrado a partir de la información pública disponible en: 

- [División Política de México Estatal y Municipal en GeoJSON 2024 - DataMX](https://datamx.io/ne/dataset/division-politica-de-mexico-estatal-y-municipal-en-geojson-2024) — delimitación geográfica de los municipios.
- [INEGI - Área Geo Estadística Estatal, Municipal y Localidades (AGEEML)](https://www.inegi.org.mx/app/ageeml/) — catálogo de localidades: claves, nombres oficiales, altitud y ubicación.


## 📝 Licencia
Este repositorio se distribuye bajo la licencia de datos abiertos. 

Siéntete libre de clonarlo, modificarlo e integrarlo en tus proyectos. Se agradece la atribución a las fuentes originales de `DataMX` e `INEGI`.

Repositorio creado para facilitar el acceso a información geoespacial de Tlaxcala.

`Hecho con ❤️ para la comunidad de datos abiertos en México.`
