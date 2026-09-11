# Conexion a la Base de Datos del Censo

Devuelve una conexion a la base de datos local. Esto corresponde a una
conexion a una base DuckDB compatible con DBI. A diferencia de
[`censo_tabla()`](https://docs.ropensci.org/censo2017/reference/censo_tabla.md),
esta funcion es mas flexible y se puede usar con dbplyr para leer
unicamente lo que se necesita o directamente con DBI para usar comandos
SQL.

## Uso

``` r
censo_conectar(dir = censo_path())
```

## Argumentos

- dir:

  La ubicacion de la base de datos en el disco. Por defecto es
  `censo2017` en la carpeta de datos del usuario de R o la variable de
  entorno `CENSO2017_DIR` si el usuario la especifica.

## Ejemplos

``` r
if (FALSE) { # \dontrun{
 DBI::dbListTables(censo_conectar())

 DBI::dbGetQuery(
  censo_conectar(),
  'SELECT * FROM comunas WHERE provincia_ref_id = 1'
 )
} # }
```
