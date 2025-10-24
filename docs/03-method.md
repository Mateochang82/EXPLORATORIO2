

# Analisis de nuestra variable objetivo G3


``` r
datos %>%
  summarise(
    n       = length(g3),
    media   = mean(g3),
    ds      = sd(g3),
    mediana = median(g3),
    minimo  = min(g3),
    maximo  = max(g3),
    Q1      = quantile(g3, 0.25),
    Q3      = quantile(g3, 0.75),
    IQR     = IQR(g3)
  )
```

```
##     n    media       ds mediana minimo maximo Q1 Q3 IQR
## 1 395 10.41519 4.581443      11      0     20  8 14   6
```

## Interpretacion de la variable

Comencemos a interpretar 1 por 1 las siguientes caracteristicas descriptivas:
**Media:**: Esta nos dio 10.42, el promedio de la nota final esta ligeramente por encima del punto medio de la escala (0-20)
**Mediana:** Esta con un valor de 11, esto esta cerca a la media, lo que sugiere una distribucion relativamente simetrica 
**Desviacion Estandar:** Esta nos indica la variabilidad considerable en los rendimientos de los estudiantes
**Rango 0-20:** Esto muestra todo el espectro de posibles calificaciones, desde reprobado hasta la nota maxima la cual es 20
**Q1 y Q3:** El 50% central de los estudiantes tiene notas entre los 8 y 14
**IQR:** Este nos dio 6, un rango intercuartilico amplio que confirma la dispersion de los resultados

## Histograma y boxplot

``` r
datos %>%
  ggplot(aes(x = g3)) +
  geom_histogram(aes(y = after_stat(density)),
                 binwidth = 1,           # ajusta si quieres barras más/menos anchas
                 fill = "#2c7fb8",
                 color = "white",
                 alpha = 0.6) +
  geom_density(color = "darkblue", linewidth = 1.2) +
  labs(
    title = "Distribución de la nota final (G3)",
    x = "G3",
    y = "Densidad"
  ) +
  theme_bw()
```

<img src="03-method_files/figure-html/unnamed-chunk-3-1.png" width="672" />

``` r
datos %>%
  ggplot(aes(x = "", y = g3)) +
  geom_boxplot(fill = "#a6cee3", color = "#1f78b4", outlier.color = "red") +
  stat_summary(fun = mean, geom = "point", shape = 20, size = 3, color = "black") +
  labs(
    title = "Diagrama de cajas y bigotes de G3",
    x = "",
    y = "G3"
  ) +
  theme_bw()
```

<img src="03-method_files/figure-html/unnamed-chunk-3-2.png" width="672" />

## Interpretacion de los graficos
Con el **histograma** podemos comprobar lo que habiamos visto anteriormente. El histograma nos muestra una distribucion aproximadamente siemtrica, con una concentracion en el rango medio (8-14)

En el **boxplot** vemos la mediana alrededor de 11, muy cercana a la media que representamos por el punto negro. Esto refuerza la idea de una distribucion equilibrida. No vemos valores atipicos mostrando que las calificacion al final son bastante equilibrado
