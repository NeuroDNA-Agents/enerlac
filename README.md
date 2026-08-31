# enerlac — Ranking solar-eólico de las provincias de la República Dominicana

Extracción y análisis reproducibles del estudio:

> *Optimización multicriterio para la priorización territorial del potencial solar
> y eólico: un ranking de las provincias de la República Dominicana mediante
> Entropía-TOPSIS* (convocatoria EnerLAC 2026).

El notebook [`ENERLAC_extraccion_analisis.ipynb`](ENERLAC_extraccion_analisis.ipynb)
reproduce, paso a paso, la construcción de la matriz de decisión (32 provincias × 4
criterios), el cálculo de pesos por **entropía de Shannon**, **CRITIC** e igualitario,
el procedimiento **TOPSIS** completo, el análisis de robustez con correlación de rangos
de **Spearman**, y la validación cruzada con la generación real de los parques eólicos
operativos.

## Contenido del repositorio

| Ruta | Descripción |
|------|-------------|
| `ENERLAC_extraccion_analisis.ipynb` | Notebook principal: extracción, análisis multicriterio, visualización y exportación. |
| `GeneracionFuenteSENI.xlsx` | Generación bruta por fuente del SIEN/CNE (contexto e histórico). |
| `Generaci_n y Consumo en Estaci_n 20XX.xlsx` | Generación por central 2024–2026 (validación cruzada de parques eólicos). |
| `outputs/` | Resultados generados por el notebook (matriz de decisión, ranking, figuras, libro de Excel). |
| `requirements.txt` | Dependencias de Python con versiones fijadas. |

Los cuatro criterios del modelo son `C1 = GHI`, `C2 = PVOUT`, `C3 = V10M` (velocidad de
viento a 10 m) y `C4 = POT_EOLICO` (potencial eólico específico).

## Instalación

Requiere **Python 3.12**. Desde la raíz del repositorio:

```bash
# 1. Crear y activar un entorno virtual
python -m venv venv

# Windows (PowerShell)
venv\Scripts\Activate.ps1
# macOS / Linux
source venv/bin/activate

# 2. Instalar las dependencias
pip install -r requirements.txt
```

`requirements.txt` incluye:

- **Núcleo** (`pandas`, `numpy`, `scipy`, `matplotlib`, `openpyxl`, `XlsxWriter`) —
  necesario para todo el análisis.
- **`ipykernel`** — para ejecutar el notebook desde Jupyter o VS Code.
- **Extracción raster opcional** (`rasterio`, `geopandas`, `rasterstats`) — solo para
  recalcular en vivo la estadística zonal del Global Solar Atlas (sección 1.2). Si estos
  paquetes no están instalados, el notebook lo detecta y continúa con la matriz de
  decisión publicada en el artículo.

## Uso

```bash
jupyter lab ENERLAC_extraccion_analisis.ipynb
```

o abre el notebook en VS Code y selecciona el intérprete `venv` como kernel. Ejecuta
todas las celdas en orden; los resultados se escriben en `outputs/`.

### Datos raster no incluidos (opcional)

La sección 1.2 usa los paquetes del *Global Solar Atlas* para la República Dominicana,
que **no** se distribuyen en este repositorio por su tamaño y licencia. Para ejecutarla,
descárgalos desde <https://globalsolaratlas.info/download/dominican-republic> y colócalos
en la raíz del repositorio:

- `Dominican-Republic_GISdata_LTAym_AvgDailyTotals_GlobalSolarAtlas-v2_AAIGRID.zip`
- `Dominican-Republic_GISdata_LTAy_DailySum_GlobalSolarAtlas_GEOTIFF.zip`

Los límites administrativos provinciales se descargan automáticamente de Natural Earth
(requiere conexión a internet).
