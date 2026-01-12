# Analisis de Segmentacion y Calidad de Datos: ConnectaTel Latam

## Objetivo del Proyecto
El objetivo principal de este proyecto es evaluar el comportamiento de los clientes de ConnectaTel mediante el analisis de datos registrados hasta 2024. El estudio busca identificar perfiles estadisticos, detectar comportamientos atipicos y generar segmentos accionables que permitan diseñar estrategias de retencion y mejoras en la oferta comercial.

## Datasets Utilizados
El analisis se integra a partir de tres fuentes de datos:
* plans.csv: Informacion sobre tarifas, minutos/mensajes incluidos y costos excedentes.
* users_latam.csv: Perfil demografico de 4,000 usuarios (edad, ciudad, fecha de registro, plan).
* usage.csv: Detalle de 40,000 registros de uso real (llamadas y mensajes).

## Etapas del Analisis
1. Exploracion Inicial: Carga de datos y revision de estructuras con Pandas (.shape, .info).
2. Identificacion de Calidad: 
   - Deteccion de valores centinela (-999 en edad, "?" en ciudad).
   - Analisis de nulos (88% en churn_date, 11% en city).
   - Identificacion de registros con fechas inconsistentes (año 2026).
3. Limpieza de Datos: 
   - Imputacion de edad mediante la mediana (48 años).
   - Estandarizacion de valores nulos en columnas categoricas y de fecha.
   - Tratamiento de datos faltantes en uso (MAR) segun el tipo de servicio (call/text).
4. Agregacion y Estadistica: 
   - Construccion de un perfil por usuario (usage_agg) con metricas de mensajes, llamadas y minutos.
   - Analisis de distribucion de planes (65% Basico, 35% Premium).
5. Visualizacion de Distribuciones: 
   - Histogramas de edad, mensajes, llamadas y minutos comparando planes (hue='plan').
   - Analisis de sesgos y formas de distribucion (Normal y Sesgada a la derecha).
6. Identificacion de Outliers: Uso de diagramas de caja (Boxplots) y metodo IQR para definir limites de consumo extremo.
7. Segmentacion de Clientes: 
   - Segmentacion por Uso: Bajo uso, Uso medio y Alto uso.
   - Segmentacion por Edad: Joven, Adulto y Adulto Mayor.

## Tecnologias Utilizadas
* Lenguaje: Python 3.x
* Librerias: Pandas (procesamiento), Seaborn y Matplotlib (visualizacion).

## Instrucciones para Ejecucion
1. Clone el repositorio o descargue el archivo .ipynb.
2. Coloque los archivos CSV (plans, users_latam, usage) en la carpeta /datasets/ o en el mismo directorio del notebook.
3. Ejecute las celdas de forma secuencial. Es critico no saltar la etapa de Limpieza, ya que los valores centinela alteran significativamente las desviaciones estandar y los graficos de distribucion.

## Guia de Reproduccion
Para obtener los mismos resultados estadisticos:
- Verifique que la imputacion de la mediana se realice sobre la columna 'age' antes de cualquier agrupacion.
- Al combinar las tablas (merge), utilice un 'left join' desde la tabla de usuarios para mantener la integridad de la base de clientes.
- Los limites de outliers para minutos de llamada deben calcularse mediante IQR, identificando el limite superior en aproximadamente 61.85 minutos.
