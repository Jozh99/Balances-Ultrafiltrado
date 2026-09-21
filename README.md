# Calculadora de Ultrafiltración de Leche

PWA para apoyar el anteproyecto de leche ultrafiltrada alta proteína / sin lactosa (tipo Lala 100), a desarrollar sobre el sistema UF existente en Lácteos Flores (MSS Project #180202, originalmente diseñado para suero dulce pasteurizado).

Sin dependencias externas (HTML/CSS/JS puro) — funciona offline una vez instalada como PWA.

## Qué calcula

1. **Balance de masa (concentración UF).** A partir de la composición de la leche de alimentación y de un % de proteína objetivo (o un VCF fijo), calcula el VCF, y la composición y flujo del retenido y el permeado.
2. **Diafiltración.** Calcula el agua de dilución necesaria para bajar la lactosa por debajo de la de la leche original (la concentración simple no reduce el % de lactosa).
3. **Estandarización de grasa de alimentación.** Como la grasa se concentra con el mismo VCF que la proteína, calcula qué % de grasa debe tener la leche de entrada para lograr el % de grasa objetivo en el producto.
4. **Capacidad del equipo.** Convierte los flujos del proceso a gpm y los compara contra los límites de diseño del ultrafiltrador (tomados del SOP / Manual del Operador del proyecto #180202) para detectar si un escenario excede la capacidad instalada.

Cada pestaña incluye una explicación breve y las fórmulas usadas. La pestaña "Supuestos y fórmulas" documenta el modelo de retención de membrana y las limitaciones de los cálculos.

**Importante:** son cálculos de nivel de anteproyecto (preliminares). No sustituyen una corrida piloto ni el análisis real de la leche de planta — los valores por defecto son de referencia bibliográfica.

## Desplegar en GitHub Pages

```bash
# 1. Crear el repositorio en GitHub (puede ser desde la web o con gh cli)
gh repo create Calculadora-UF-Leche --public --source=. --remote=origin

# 2. Subir el código
git init
git add .
git commit -m "Primera versión: calculadora de UF de leche"
git branch -M main
git remote add origin https://github.com/Jozh99/Calculadora-UF-Leche.git
git push -u origin main

# 3. Activar GitHub Pages
# En GitHub: Settings → Pages → Source: rama "main", carpeta "/ (root)" → Save
```

La app quedará publicada en `https://jozh99.github.io/Calculadora-UF-Leche/` (o el nombre de repo que elijas).

## Estructura

```
calculadora-uf-leche/
├── index.html      # App completa (HTML + CSS + JS, un solo archivo)
├── manifest.json    # Manifest de PWA
├── sw.js            # Service worker (caché offline)
├── icons/           # Íconos de la PWA
└── README.md
```

## Personalizar los límites del equipo

Los rangos de flujo de alimentación (120–300 gpm) y de permeado (12–50 gpm) en la pestaña "Capacidad del equipo" son editables directamente en el formulario — no hace falta tocar el código si el equipo cambia. Si quieres que queden como valores por defecto distintos, edítalos en `index.html` dentro de los campos `m4_feed_min`, `m4_feed_max`, `m4_perm_min`, `m4_perm_max`.
