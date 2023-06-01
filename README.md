# coffee-quality
coffee_quality_tarea_2
---
title: "Tarea 2"
author: "Daniela Hidalgo B93905"
---

#### Grupo 02

### Graficación de la calidad del café según el Coffee Quality Institute (CQI)

### 1. Introducción

En este trabajo se encuentran datos relacionados con la calidad del café, tales como: altitud, país de origen, color, sabor, puntaje total, entre otras características, para desarrollarlo se hace uso del lenguaje de programación R con diferentes paquetes que crean histogramas, gráficos así como tablas que permiten comprender la información de una manera más clara y precisa. Los datos que son utilizados para graficar fueron extraídos del [Coffee Quality Institute (CQI)](https://github.com/fatih-boyar/coffee-quality-data-CQI), y se obtuvieron del enlace https://github.com/fatih-boyar/coffee-quality-data-CQI.

### 2.1. Carga de paquetes de R

```{r}
#| label: Carga-datos
#| warning: false
library(DT)
library(ggplot2)
library(plotly)
library(dplyr)
library(tidyverse)
library(ggthemes)
library(readr)
```

### 2.2. Carga de datos

```{r}
read_csv("C:/Users/danie/Downloads/tarea_2_PDG/coffee-quality.csv")
```

### 3.Tabla DT

```{r}

# Leer el archivo csv 
coffee_data <- read.csv(
  "C:/Users/danie/Downloads/tarea_2_PDG/coffee-quality.csv"
)

# tabla interactiva (DT) 
datatable(coffee_data[, c("Country_of_Origin", "Variety", "Color", "Altitude", "Total_Cup_Points")],
          options = list(pageLength = 10, lengthMenu = c(10, 20, 40)),
         filter="top")
```

### 4.1. Histograma

```{r}
p <- ggplot(coffee_data, aes(x = Total_Cup_Points)) +
  geom_histogram(binwidth = 1, color = "brown", fill = "gray") +
  geom_density(alpha = 0.2, fill = "orange") +
  labs(title = "Distribución de Total Cup Points",
       x = "Total Cup Points",
       y = "Frecuencia") +
  theme_test()

# Convertir a interactivo
ggplotly(p)
```

### 4.2. Gráfico de dispersión

```{r}

p <- ggplot(coffee_data, aes(x = Altitude, y = Total_Cup_Points)) +
  geom_point() +
  geom_smooth(method = "lm", se = FALSE, color = "blue") +
  labs(title = "Relación entre Altitude y Total Cup Points",
       x = "Altitude",
       y = "Total Cup Points") +
  theme_test()

# Convertir a interactivo
ggplotly(p, tooltip = c("Altitude", "Total_Cup_Points"))
```

### 4.3. Gráfico de caja

```{r}

p <- ggplot(coffee_data, aes(x = Color, y = Total_Cup_Points)) +
  geom_boxplot() +
  labs(title = "Distribución de Total Cup Points por Color",
       x = "Color",
       y = "Total Cup Points") +
  theme_test() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

# Convertir a interactivo
ggplotly(p)
```
