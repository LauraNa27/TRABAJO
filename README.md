# TRABAJO
```{r include=FALSE}
#Librerias utilizadas
pckg_list <- c('readxl','ggplot2', 'tidyverse', 'timsac', 'dplyr','tidyr', 'plotrix'); load_pkgs <- sapply(pckg_list, library, character.only = T)
```

```{r include=FALSE}
#Base de datos
setwd("~/DOC UNIVERSIDAD/10 SEMESTRE/OPCION DE GRADO/PRACTICAS/Bases proyecto")
Share2021 <- read_excel("Share2021 Ene Dic DTV.xlsx")
Share2022 <- read_excel("Share2022 Ene Dic DTV.xlsx", sheet = "BASE")

#Revision base de datos 

Share2022 <- data.frame(Share2022); summary(Share2022)
Share2021 <- data.frame(Share2021); summary(Share2021)
```

```{r include=FALSE}
#Renombrar las variables - Cambiar Mes 
Share2021 <- rename(Share2021,TX_2SubCategoria = TX..Segunda.SubCategoria., G_Autogestion = Grupo.de.Autogestion)

set.seed(123)
Share2021$Mes <- factor(Share2021$Mes, levels = c("202101", "202102", "202103", "202104", "202105", "202106", "202107", "202108", "202109", "202110", "202111", "202112"), labels = c("ENE", "FEB", "MAR", "ABR", "MAY", "JUN", "JUL", "AGO", "SEP","OCT","NOV", "DIC"))
table(Share2021$Mes)
Share2022$Mes <- factor(Share2022$Mes, levels = c("202201", "202202", "202203", "202204", "202205", "202206", "202207", "202208", "202209", "202210", "202211", "202212"), labels = c("ENE", "FEB", "MAR", "ABR", "MAY", "JUN", "JUL", "AGO", "SEP","OCT","NOV", "DIC"))

# Unión de las 2 bases 
base <- merge(Share2021, Share2022, all=TRUE)
str(base)
summary(base)
view(base)
write.csv2(base, file = 'base.csv', fileEncoding = 'Latin1', row.names = F)
```

BASE DE DATOS

```{r}
# Modificar variables- Convertir en factor 
base$Region=factor(base$Region);base$Pais=factor(base$Pais); base$Canal=factor(base$Canal); 
base$Fuente=factor(base$Fuente);base$Negocio=factor(base$Negocio);base$TX_2SubCategoria=factor(base$TX_2SubCategoria); 
base$Quarter=factor(base$Quarter);base$Mes=factor(base$Mes); base$TMP_FECHA = factor(base$TMP_FECHA); 
base$Share = factor(base$Share); base$Sig.TX = factor(base$Sig.TX); base$G_Autogestion = factor(base$G_Autogestion)

```




```{r}
# Modificar variables- Convertir en factor 

datos <- base

datos$Region=factor(datos$Region); datos$Pais=factor(datos$Pais); datos$Canal=factor(datos$Canal); datos$Fuente=factor(datos$Fuente);
datos$Negocio=factor(datos$Negocio);  datos$TX_2SubCategoria=factor(datos$TX_2SubCategoria); datos$Quarter=factor(datos$Quarter); base$Mes=factor(datos$Mes); datos$TMP_FECHA = factor(datos$TMP_FECHA);datos$Share = factor(datos$Share); datos$Sig.TX = factor(datos$Sig.TX); datos$G_Autogestion = factor(datos$G_Autogestion)

summary(datos)
```
