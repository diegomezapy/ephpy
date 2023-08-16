# ephpy
Encuesta Permanente de Hogares del Paraguay

Aquí puedes descargar todos los microdatos de la EPH desde el año 2006 hasta el 2022 en formato .SAV, es decir en formato SPSS



```{r}
#comando para pasar de sav a csv
# Cargamos la librería haven
library(haven)
# Cargamos el archivo SAV
datos_sav <- haven::read_sav("RO2_EPH2006.sav")
# Guardamos los datos en formato CSV
write.csv(datos_sav, file = "r02eph2006.csv", row.names = FALSE)

```


# Cargamos la librería haven
library(haven)

# Ruta de la carpeta donde se encuentran los archivos SAV
ruta_carpeta <- "/cloud/project/"

# Ciclo para procesar los archivos desde 2006 hasta 2022
for (anio in 2006:2022) {
  # Nombre del archivo SAV actual
  nombre_archivo_sav <- sprintf("RO02EPH_%d.sav", anio)
  
  # Cargamos el archivo SAV
  datos_sav <- read_sav(file.path(ruta_carpeta, nombre_archivo_sav))
  
  # Generamos el nombre del archivo CSV de salida
  nombre_archivo_csv <- sprintf("r02eph%d.csv", anio)
  
  # Ruta completa para guardar el archivo CSV
  ruta_csv <- file.path(ruta_carpeta, nombre_archivo_csv)
  
  # Guardamos los datos en formato CSV
  write.csv(datos_sav, file = ruta_csv, row.names = FALSE)
  
  cat("Archivo", nombre_archivo_csv, "convertido y guardado.\n")
}

