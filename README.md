# Taller: Análisis Exploratorio, Limpieza y Transformación de Datos (KDD)

Taller práctico de **Knowledge Discovery in Databases (KDD)** aplicado a un dataset transaccional de una cafetería, con datos intencionalmente "sucios" (`dirty_cafe_sales.csv`): valores faltantes, valores enmascarados (`ERROR`, `UNKNOWN`), inconsistencias relacionales y tipos de datos incorrectos.

**Autor:** David Mauricio Vargas Ramirez — ID: 824144

## Contenido del taller

El análisis está organizado en 8 partes, siguiendo el flujo clásico de KDD:

| Parte | Descripción |
|-------|-------------|
| 1 | Carga y exploración inicial de datos |
| 2 | Diagnóstico de calidad de datos (valores faltantes, mecanismos MAR/MCAR) |
| 3 | Limpieza y preparación (despeje algebraico, imputación por mediana) |
| 4 | Validación de reglas de negocio (`Total = Cantidad × Precio`) |
| 5 | Análisis Exploratorio de Datos (EDA): distribuciones, outliers, series de tiempo |
| 6 | Análisis bivariado e inferencial (Spearman, Chi-cuadrado, Kruskal-Wallis) |
| 7 | Transformación de datos: variables temporales, one-hot encoding, estandarización |
| 8 | Modelo de regresión lineal exploratorio y conclusiones de negocio |

## Estructura del repositorio

```
.
├── taller_kdd_cafe_sales.Rmd   # Documento fuente (R Markdown)
├── dirty_cafe_sales.csv        # Dataset de entrada (no incluido / agregar manualmente)
└── README.md
```

> **Nota:** el archivo `dirty_cafe_sales.csv` debe estar en la misma carpeta que el `.Rmd` para poder compilar el documento.

## Requisitos

### Paquetes de R

```r
install.packages(c(
  "readr", "dplyr", "ggplot2", "tidyr", "stringr",
  "lubridate", "naniar", "janitor", "broom", "zoo"
))
```

### Motor LaTeX (para compilar a PDF)

Se necesita una distribución LaTeX con los paquetes `geometry`, `fancyvrb` y `fvextra` (este último permite que el código y las salidas de consola se ajusten al ancho de la página en vez de desbordarse).

- **Con TinyTeX** (recomendado si usas R/RStudio en cualquier sistema):
  ```r
  tinytex::tlmgr_install("fvextra")
  ```
- **Con TeXLive del sistema en Fedora/RHEL:**
  ```bash
  sudo dnf install texlive-fvextra
  ```
- **Con TeXLive del sistema en Debian/Ubuntu:**
  ```bash
  sudo apt install texlive-latex-extra
  ```

## Cómo compilar

1. Clona el repositorio y coloca `dirty_cafe_sales.csv` en la raíz del proyecto.
2. Abre `taller_kdd_cafe_sales.Rmd` en RStudio.
3. Haz clic en **Knit → Knit to PDF**, o desde la consola de R:
   ```r
   rmarkdown::render("taller_kdd_cafe_sales.Rmd")
   ```

## Notas metodológicas

- El gráfico `vis_miss` de la Parte 2 se genera sobre una **muestra aleatoria de 1.000 filas** (de un total de 10.000) por una razón puramente visual: dibujar una línea de 1 píxel por cada observación produce un efecto muaré al reescalar la imagen en el PDF. La muestra es representativa y no afecta ningún cálculo posterior; el resto del análisis (imputación, validación, EDA, modelado) usa siempre el dataset completo.
- Los mecanismos de pérdida de datos se clasificaron como **MAR** (`price_per_unit`, dependiente del producto) y **MCAR** (`payment_method`, homogéneo entre sedes), lo cual justifica las estrategias de imputación elegidas (mediana por producto vs. categoría explícita "No registrado").

## Licencia

Uso académico.
