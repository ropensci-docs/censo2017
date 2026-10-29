# Poblacion por Nivel Educacional en la Region del Bio Bio

Proporciona la cuenta y porcentaje por comuna de las personas de la
Region del Bio Bio de acuerdo al maximo nivel educacional que reportan
(e.g. primaria, secundaria, universitaria, etc.)

## Formato

Un tibble con 860 observaciones en las siguientes 4 variables.

- `comuna`:

  codigo de comuna (15 regiones)

- `nivel_educ`:

  maximo nivel educacional alcanzado (ver la vinieta con los links a la
  descripcion de codigos)

- `cuenta`:

  cantidad de personas censadas en la comuna

- `proporcion`:

  porcentaje que representan las personas censadas en la comuna

## Autor-a

Elaboracion propia con base en datos desagregados del Censo

## Ejemplos

``` r
nivel_educacional_biobio
#> # A tibble: 860 × 4
#>    comuna nivel_educ cuenta proporcion
#>    <chr>       <int>  <int>      <dbl>
#>  1 08101           1   4851    0.0217 
#>  2 08101           2   2701    0.0121 
#>  3 08101           3   3579    0.0160 
#>  4 08101           4    831    0.00372
#>  5 08101           5  37538    0.168  
#>  6 08101           6   5687    0.0254 
#>  7 08101           7  47356    0.212  
#>  8 08101           8  18641    0.0834 
#>  9 08101           9   5854    0.0262 
#> 10 08101          10   2653    0.0119 
#> # ℹ 850 more rows

if (FALSE) { # \dontrun{
# replicar el resultado usando dplyr directamente con SQL
# es ligeramente distinto a las vinietas que explican esta misma tabla
nivel_educacional_biobio <- tbl(censo_conectar(), "zonas") %>% 
 mutate(
  region = substr(as.character(geocodigo), 1, 2),
  comuna = substr(as.character(geocodigo), 1, 5)
 ) %>% 
 filter(region == "08") %>% 
 select(comuna, geocodigo, zonaloc_ref_id) %>%
 inner_join(select(tbl(censo_conectar(), "viviendas"),
  zonaloc_ref_id, vivienda_ref_id), by = "zonaloc_ref_id") %>%
 inner_join(select(tbl(censo_conectar(), "hogares"),
  vivienda_ref_id, hogar_ref_id), by = "vivienda_ref_id") %>%
 inner_join(select(tbl(censo_conectar(), "personas"),
  hogar_ref_id, nivel_educ = p15), by = "hogar_ref_id") %>%
 group_by(comuna, nivel_educ) %>%
 summarise(cuenta = n()) %>%
 group_by(comuna) %>%
 mutate(proporcion = cuenta * (1 / sum(cuenta))) %>% 
 arrange(comuna, nivel_educ)} # }
```
