# Análisis del Mercado Eléctrico Español: Serie de Proyectos

Este repositorio agrupa una serie de pequeños proyectos independientes (cada uno en su propio cuaderno Jupyter) que, en conjunto, cubren todo el proceso de descarga, limpieza, análisis y predicción de precios del mercado eléctrico español.

## Estructura de Proyectos

### Cuadernos 

```text
00 Precios eléctricos                  - Visión general y definición del problema
01 Descarga OMIE                       - Obtención de datos del operador OMIE (mercado diario)
02 Análisis precios OMIE               - Exploración y visualización de precios OMIE
03 Datos MIBGAS                        - Descarga de datos del mercado MIBGAS (gas)
04 Análisis precios MIBGAS             - Análisis y tendencias de precios de gas
05 Descargas REE                       - Descarga de datos horarios y mensuales de REE
```

Cada cuaderno funciona de forma autónoma: puedes ejecutarlo por separado para reproducir esa fase del análisis.

## Objetivo Final

El propósito es integrar progresivamente todas estas fuentes de datos (mercado eléctrico, OMIE, MIBGAS, REE) y sus análisis intermedios, para culminar en un **proyecto de forecasting de precios eléctricos** basado en Machine Learning.

Pasos generales:

1. **Descarga de datos**: diferentes APIs y formatos.
2. **Procesado y limpieza**: unificar estructuras y fechas.
3. **Análisis exploratorio**: series temporales, correlaciones, visualizaciones.
4. **Modelado predictivo**: entrenamiento y evaluación de modelos ML para predicción de precios.

---


# Proyecto: Descarga y Preparación de Datos de Red Eléctrica (05 Descargas REE)

## Descripción

Este proyecto automatiza la descarga de datos históricos de la Red Eléctrica de España (REE) mediante su API pública y prepara la información para su análisis y modelado de predicción de precios eléctricos.

Está pensado para usuarios sin experiencia en programación avanzada, y se organiza en un cuaderno de Jupyter dividido en capítulos sencillos.

---

## Objetivos

1. Descargar datos horarios y mensuales de distintos apartados (mercados, demanda, generación, intercambios, balance, almacenamiento).
2. Guardar las respuestas de la API en archivos JSON, organizados por carpetas según categoría y widget.
3. Procesar esos JSON en tablas (DataFrames) listos para obtener series temporales.
4. Facilitar el posterior análisis y construcción de modelos de forecasting de precios eléctricos.

---

## Estructura de Carpetas

```
/Proyecto
├── Notebooks/
├── descargas/ree/
│   ├── mercados/
│   │   ├── componentes-precio-energia-cierre-desglose/
│   │   ├── energia-precios-ponderados-gestion-desvios/
│   │   ├── precios-mercados-tiempo-real/
│   │   └── servicio_ajuste/
│   ├── demanda/
│   │   ├── evolucion_demanda/
│   │   └── ire-general/
│   ├── generacion/
│   │   ├── evolucion-renovable-no-renovable/
│   │   ├── estructura-generacion/
│   │   └── potencia-instalada/
│   ├── intercambios/
│   │   └── todas-fronteras-fisicos/
│   ├── balance/
│   │   └── balance-electrico/
│   └── almacenamiento/
│       ├── energia-almacenamiento/
│       └── potencia-instalada/
```

Cada subcarpeta contendrá los archivos JSON descargados.

---

## Contenido del Notebook

El cuaderno de Jupyter se divide en capítulos:

1. **Configuración**

   * Definición de la ruta base de descargas.
   * Creación de carpetas automáticamente según la estructura.
2. **Funciones Genéricas**

   * `download_and_save_json(...)`:

     * Llama a la API en tramos (anual o mensual según el tipo de datos).
     * Guarda cada respuesta en un archivo JSON con nombres claros.
   * `parse_componentes_json(path, time_trunc)`:

     * Carga uno o varios JSON de una carpeta.
     * Extrae cada serie de datos (mediante `title` y `values`).
     * Construye una tabla donde cada columna es una serie y las filas están alineadas por fecha.
3. **Descargas por Capítulo**

   * Un bloque independiente para cada combinación categoría/widget.
   * Ejemplo:

     ```python
     download_and_save_json(
       'mercados',
       'componentes-precio-energia-cierre-desglose',
       '2014-01-01T00:00',
       '2025-06-19T23:59',
       'month',
       base_path
     )
     ```
4. **Procesado y Unificación**

   * Uso de `parse_componentes_json` para generar DataFrames maestros.
   * Ajustes de fechas a formato `YYYY-MM-DD` o incluyendo hora.

--- 

## Requisitos

* Python 3.x
* Jupyter Notebook
* Librerías Python: `requests`, `pandas`, `python-dateutil`

---

## Cómo Empezar

1. Clona o descarga este proyecto.
2. Abre el cuaderno en Jupyter.
3. Ejecuta el capítulo de **Configuración**.
4. Personaliza las llamadas a la API si deseas otros rangos de fechas.
5. Ejecuta los bloques de descarga y luego el de procesado.

Tras estos pasos, tendrás un conjunto de tablas listas para análisis y modelado de series temporales.

---

## Próximos Pasos

* Conversión de JSON a CSV o bases de datos (`sqlite`, `SQL`).
* Limpieza y validación de datos.
* Desarrollo de un modelo de Machine Learning para predecir precios horarios.


