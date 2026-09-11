# Descarga la Base de Datos del Censo a tu Computador

Este comando descarga la base de datos completa como un unico archivo
zip que se descomprime para crear la base de datos local. Si no quieres
descargar la base de datos en tu home, ejecuta usethis::edit_r_environ()
para crear la variable de entorno CENSO2017_DIR con la ruta.

## Uso

``` r
censo_descargar(ver = NULL)
```

## Argumentos

- ver:

  La version a descargar. Por defecto es la ultima version disponible en
  GitHub. Se pueden ver todas las versiones en
  <https://github.com/pachamaltese/censo2017/releases>.

## Ejemplos

``` r
if (FALSE)  censo_descargar()  # \dontrun{}
```
