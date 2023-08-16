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
