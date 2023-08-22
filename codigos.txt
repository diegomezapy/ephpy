---
title: "Indicadores basados en la Encuesta Permanente de Hogares Contínua del Paraguy (EPHC)"
subtitle: "<center> Laboratorio de Investigación en Estadística Teórica y Aplicada ![](lieta_logo.jpg){width=0.75in} <br> Actualizada al año 2022 </center> "

author:
- name: Diego Bernardo Meza$^1$
  affiliation: $^1$Universidad Nacional de Asunción
  email: \email{dmeza.py@gmail.com}
#- name: Diego Meza$^2$
 #affiliation: $^2$Facultad de Ciencias Exactas y Naturales - UNA
  #email: \email{dmeza.py@gmail.com}
date: "`r format(Sys.time(), '%d %B %Y')`"

output:
  rmdformats::readthedown:
  highlight: zenburn
  #highlight: kate
  toc: true
  toc_float: true
  toc_depth: 4
  number_sections: true
  fig_caption: yes
#"tango", "pygments", "kate", "monochrome", "espresso", "zenburn", "haddock", and "textmate"
  #bibliography: references.bib
link-citations: true
css: custom.css
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

```{r, include=FALSE}
library(bookdown)
```


# Introducción

En la era actual de información y análisis, los microdatos provenientes de encuestas de hogares representan un valioso recurso para comprender diversos aspectos de la sociedad, incluyendo la demografía, el mercado laboral, la educación y la seguridad social. Estas encuestas capturan una vasta gama de información detallada y representativa de las características y comportamientos de los hogares y las personas que los componen. Mediante la explotación de estas fuentes de datos ricas y granulares, es posible generar indicadores precisos y significativos que impulsan la toma de decisiones informada en políticas públicas, investigaciones académicas y la comprensión general de tendencias sociales.

En este contexto, la herramienta R se erige como un pilar fundamental para aprovechar al máximo estos microdatos y traducirlos en información valiosa. R es un software de código abierto y gratuito, altamente flexible y robusto, que brinda una plataforma poderosa para manipular, visualizar y analizar datos de manera efectiva. Su comunidad activa de usuarios y desarrolladores ha creado una amplia gama de paquetes especializados, lo que permite realizar tareas complejas con facilidad. R se destaca por su capacidad para gestionar grandes conjuntos de datos, realizar análisis estadísticos avanzados y generar gráficos y visualizaciones atractivas.

Al emplear R en el análisis de microdatos de encuestas de hogares, los investigadores y analistas pueden identificar patrones y relaciones que son fundamentales para comprender los cambios sociales, económicos y demográficos. Desde la elaboración de perfiles demográficos hasta el estudio de las tendencias de empleo y educación, pasando por el análisis de la inclusión social a través de los programas de seguridad social, R ofrece un abanico de herramientas que facilitan la creación de indicadores precisos y relevantes.

En este documento, exploraremos cómo el uso de microdatos de encuestas de hogares en conjunto con el software R puede enriquecer nuestro entendimiento de la sociedad y proporcionar insights profundos en una variedad de temas. Descubriremos cómo el análisis detallado de estas fuentes de información, impulsado por la versatilidad de R, puede ser instrumental en la toma de decisiones, la planificación de políticas y la generación de conocimiento en campos clave.


# Fuente de datos

La Encuesta Permanente de Hogares (EPH) es llevado a cabo por el Instituto Nacional de Estadísticas (INE) y tiene como objetivo fundamental la generación de estadísticas que permitan monitorear trimestralmente las características clave del mercado laboral, así como otros aspectos socioeconómicos. Esta encuesta abarca a las personas que residen en hogares particulares ubicados en los departamentos de la Región Oriental y Pte. Hayes.

Para llevar a cabo este propósito, se ha establecido un tamaño muestral de 5,004 hogares por trimestre en el año 2023. La metodología empleada se basa en un enfoque de muestra semi-panel con una rotación del 50% de los hogares durante dos años consecutivos. Esto significa que en dos años seguidos, el 50% de los hogares se solapan entre los mismos trimestres, con el propósito principal de controlar los cambios reales en las características laborales.

La EPH comenzó su ejecución en la segunda semana de enero de 2017 y se ha mantenido en funcionamiento de manera continua hasta la fecha actual. En el anexo, se presentan los resultados correspondientes a veintiséis trimestres, abarcando desde el año 2017 hasta el 2023.

La relevancia de este material radica en su capacidad para proporcionar información sobre los indicadores clave de empleo. Esta información resulta esencial para la formulación, implementación y evaluación de políticas públicas orientadas a mejorar las condiciones de empleo y, por extensión, las condiciones de vida de la población en general.


# Gestión de los datos

## Transformación de las bases en formato SAV a csv

```{r, eval = FALSE}
library(haven)
```



```{r}
eph13 <- read_sav("R02_EPH2013.SAV",col_select = c("P02","P06","PEAA","PEAD","fexajustado"))
eph14 <- read_sav("R02_EPH2014.SAV",col_select = c("P02","P06","PEAA","PEAD","fexajustado"))
eph15 <- read_sav("R02_EPH2015.SAV",col_select = c("P02","P06","PEAA","PEAD","Fexajustado"))
eph16 <- read_sav("R02_EPH2016.SAV",col_select = c("P02","P06","PEAA","PEAD","FEX"))
eph17 <- read_sav("R02_EPH2017.SAV",col_select = c("P02","P06","PEAA","PEAD","FEX"))
eph18 <- read_sav("R02_EPH2018.sav",col_select = c("P02","P06","PEAA","PEAD","FEX"))
eph19 <- read_sav("R02_EPH2019.sav",col_select = c("P02","P06","PEAA","PEAD","FEX"))
eph20 <- read_sav("R02_EPH2020.sav",col_select = c("P02","P06","PEAA","PEAD","FEX"))
eph21 <- read_sav("R02_EPH2021.sav",col_select = c("P02","P06","PEAA","PEAD","FEX"))
eph22 <- read_sav("R02_EPH2022.sav",col_select = c("P02","P06","PEAA","PEAD","FEX"))

```

```{r}
# Convert variable names to lowercase for all data frames
eph13 <- setNames(eph13, tolower(names(eph13)))
eph14 <- setNames(eph14, tolower(names(eph14)))
eph15 <- setNames(eph15, tolower(names(eph15)))
eph16 <- setNames(eph16, tolower(names(eph16)))
eph17 <- setNames(eph17, tolower(names(eph17)))
eph18 <- setNames(eph18, tolower(names(eph18)))
eph19 <- setNames(eph19, tolower(names(eph19)))
eph20 <- setNames(eph20, tolower(names(eph20)))
eph21 <- setNames(eph21, tolower(names(eph21)))
eph22 <- setNames(eph22, tolower(names(eph22)))

```

```{r, eval = FALSE}
eph13$year<-2013
eph14$year<-2014
eph15$year<-2015
eph16$year<-2016
eph17$year<-2017
eph18$year<-2018
eph19$year<-2019
eph20$year<-2020
eph21$year<-2021
eph22$year<-2022
```

```{r, eval = FALSE}
names(eph13)
```

```{r, eval = FALSE}
names(eph14)
```

```{r, eval = FALSE}
names(eph15)
```

```{r, eval = FALSE}
names(eph16)
```

```{r, eval = FALSE}
names(eph17)
```

```{r, eval = FALSE}
names(eph18)
```


```{r, eval = FALSE}
library(dplyr)
eph13 <- eph13 %>%
  select(year,area,p09,p03, p06, p02, peaa,cate_pea,pead, e01aimde,b10,b11,s01a, fexajustado) %>%
  filter(peaa == 1 & e01aimde > 0) %>%
  rename(fex = fexajustado)
names(eph13)
str(eph13)

```


```{r, eval = FALSE}
library(dplyr)
eph14 <- eph14 %>%
  select(year,area,p09,p03, p06, p02, peaa,cate_pea,pead, e01aimde,b10,b11,s01a, fexajustado) %>%
subset(peaa==1 & e01aimde>0) %>%
  rename(fex = fexajustado)
names(eph14)
str(eph14)
```

```{r, eval = FALSE}
library(dplyr)
eph15 <- eph15 %>%
  select(year,area,p09,p03, p06, p02, peaa,cate_pea,pead, e01aimde,b10,b11,s01a, fexajustado) %>%
subset(peaa==1 & e01aimde>0) %>%
  rename(fex = fexajustado)
names(eph15)
str(eph15)
```


```{r, eval = FALSE}
library(dplyr)
eph16 <- eph16 %>%
  select(year,area,p09,p03, p06, p02, peaa,cate_pea,pead, e01aimde,b10,b11,s01a, fex) %>%
subset(peaa==1 & e01aimde>0)
names(eph16)
str(eph16)
```



```{r, eval = FALSE}
library(dplyr)
eph17 <- eph17 %>%
  select(year,area,p09,p03, p06, p02, peaa,cate_pea,pead, e01aimde,b10,b11,s01a, fex) %>%
subset(peaa==1 & e01aimde>0)
names(eph17)
str(eph17)
```


```{r, eval = FALSE}
library(dplyr)
eph18 <- eph18 %>%
  select(year,area,p09,p03, p06, p02, peaa,cate_pea,pead, e01aimde,b10,b11,s01a, fex) %>%
subset(peaa==1 & e01aimde>0)
names(eph18)
str(eph18)
```


```{r, eval = FALSE}
library(dplyr)
eph19 <- eph19 %>%
  select(year,area,p09,p03, p06, p02, peaa,cate_pea,pead, e01aimde,b10,b11,s01a, fex) %>%
subset(peaa==1 & e01aimde>0)
names(eph19)
str(eph19)
```


```{r, eval = FALSE}
library(dplyr)
eph20 <- eph20 %>%
  select(year,area,p09,p03, p06, p02, peaa,cate_pea,pead, e01aimde,b10,b11,s01a, fex) %>%
subset(peaa==1 & e01aimde>0)
names(eph20)
str(eph20)
```


```{r, eval = FALSE}
library(dplyr)
eph21 <- eph21 %>%
  select(year,area,p09,p03, p06, p02, peaa,cate_pea,pead, e01aimde,b10,b11,s01a, fex) %>%
subset(peaa==1 & e01aimde>0)
names(eph21)
str(eph21)
```



```{r, eval = FALSE}
library(dplyr)
eph22 <- eph22 %>%
  select(year,area,p09,p03, p06, p02, peaa,cate_pea,pead, e01aimde,b10,b11,s01a, fex) %>%
subset(peaa==1 & e01aimde>0)
names(eph22)
str(eph22)
```



```{r, eval = FALSE}
# Juntar todas las bases en una sola 
baseEPH<-rbind(eph13,eph14,eph15,eph16,eph17,eph18,eph19,eph20,eph21,eph22)
table(baseEPH$year)

# Guardamos los datos combinados en un archivo CSV
write.csv(baseEPH, file = "baseEPH.csv", row.names = FALSE)

```



# Socio-demográficas


```{r, echo = FALSE}
#cargar la base compilada
eph<-read.csv("baseEPH.csv")
names(eph)
str(eph)

```


## FEX
```{r, echo = FALSE}

table1=aggregate(fex~year,eph,sum)
table1


```

```{r}
library(ggplot2)
library(plotly)

# Crear un gráfico ggplot con escala de colores
gg <- ggplot(table1, aes(x = factor(year), y = fex, fill = fex)) +
  geom_bar(stat = "identity") +
  scale_fill_gradient(low = "lightblue", high = "blue") +  # Escala de colores
  labs(x = "Año", y = "Fex") +
  theme_minimal()

# Convertir el gráfico ggplot a un gráfico interactivo con plotly
gg_interactive <- ggplotly(gg)

# Mostrar el gráfico interactivo
gg_interactive

```



## P06


```{r, echo = FALSE}
eph$p06 <- factor(eph$p06, labels = c("Hombres", "Mujeres"))

```


```{r, echo = FALSE}
table1=aggregate(fex~year+p06,eph,FUN=sum)
```


```{r, echo = FALSE}
library(dplyr)
library(tidyr)

# Calcular las sumas de fex para cada año
year_totals <- eph %>% group_by(year) %>%  summarise(Total = sum(fex))

# Calcular las sumas de fex para cada combinación de year y p06
freq_table <- eph %>%  group_by(year, p06) %>%  summarise(Cantidad = sum(fex)) %>%
  left_join(year_totals, by = "year") %>%  mutate(Porcentaje = (Cantidad / Total) * 100)

# Convertir a tabla de frecuencias con porcentajes
pivot_freq_table <- freq_table %>%  pivot_wider(names_from = p06, values_from = c(Cantidad, Porcentaje))

print(pivot_freq_table)


```

```{r, echo = FALSE}
library(ggplot2)
library(plotly)

# Crear el gráfico interactivo de líneas usando plotly
plot <- ggplot(freq_table, aes(x = year, y = Cantidad, group = p06, color = as.factor(p06))) +
  geom_line() +
  geom_point() +
  labs(title = "Evolución de la cantidad de P06 por Año", x = "Año", y = "Cantidad") +
  scale_color_discrete(name = "P06") +
  scale_x_continuous(breaks = freq_table$year)

# Convertir el gráfico de ggplot a uno interactivo usando plotly
interactive_plot <- ggplotly(plot)

interactive_plot

```

```{r, echo = FALSE}
library(ggplot2)
# Crear el gráfico de líneas
ggplot(freq_table, aes(x = year, y = Porcentaje, group = p06, color = as.factor(p06))) +
  geom_line() +
  geom_point() +
  labs(title = "Evolución de los Porcentajes de P06 por Año", x = "Año", y = "Porcentaje") +
  scale_color_discrete(name = "P06")+
  scale_x_continuous(breaks = freq_table$year)
```


```{r, echo = FALSE}

library(dplyr)

# Definir los límites de los grupos de edades
age_bins <- c(0, 13, 29, 59, Inf)

# Crear una nueva variable categórica para los grupos de edades
eph_with_age_groups <- eph %>%
  mutate(age_group = cut(p02, breaks = age_bins, labels = c("0-13", "14-29", "30-59", "60+"), right = FALSE))

# Calcular las sumas de fex para cada combinación de año y grupo de edad
age_group_totals <- eph_with_age_groups %>%
  group_by(year, age_group) %>%
  summarise(Total = sum(fex))

# Calcular los porcentajes para cada combinación de año y grupo de edad
freq_table_age_groups <- age_group_totals %>%
  group_by(year) %>%
  mutate(Percentage = (Total / sum(Total)) * 100)

print(freq_table_age_groups)


```




```{r, echo = FALSE}

library(ggplot2)
# Crear el gráfico de líneas
ggplot(freq_table_age_groups, aes(x = year, y = Total, group = age_group, color = as.factor(age_group))) +
  geom_line() +
  geom_point() +
  labs(title = "Evolución de los Porcentajes de Sexo por Año", x = "Año", y = "Porcentaje") +
  scale_color_discrete(name = "age_group")+
  scale_x_continuous(breaks = freq_table$year)

```



```{r, echo = FALSE}
library(ggplot2)
# Crear el gráfico de líneas
ggplot(freq_table_age_groups, aes(x = year, y = Percentage, group = age_group, color = as.factor(age_group))) +
  geom_line() +
  geom_point() +
  labs(title = "Evolución de los Porcentajes de P06 por Año", x = "Año", y = "Porcentaje") +
  scale_color_discrete(name = "age_group")+
  scale_x_continuous(breaks = freq_table$year)

```


# Laborales


## Situación de ocupación (PEAA)







## Categoría de ocupación de ocupación (CATE_PEA)



## Tipo de ocupación (TIPO_PEA)


## Rama de la ocupación principal (RAMA_PEA)

## Informalidad laboral 



## Categoría de ocupación de ocupación (CATE_PEA)


## Pobreza extrema y no extrema



# Educación



## Analfabetismo 


## Asiste actualmente a una institución educativa


## Población en edad escolar no escolarizada


## Condición NINI


##  Nivel educativo












# Salud



## Tenencia de seguro médico (S01a)





## Previsión social
## Tenencia de aportes a una caja de jubilaciones (b10)


# Tableros (dashboard) {.tabset}
## Socio-demográficos


## Laborales

## Educativos

## Salud

## Seguridad social



