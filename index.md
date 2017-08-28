---
title       : Introducción a R
subtitle    : Estructura de datos en R
author      : Julio César Ramírez Pacheco
job         : Universidad del Caribe
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax,quiz, bootstrap, interactive] # {mathjax, quiz, bootstrap}
ext_widgets : {rCharts: [libraries/nvd3, libraries/leaflet, libraries/dygraphs]}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
#logo        : unicaribelogo.jpeg
#biglogo     : unicaribelogo.jpeg
logo        : uqroo.png
biglogo     : uqroo.png
assets      : {assets: ../../assets}
---

<style type="text/css">
body {background:grey transparent;
}
</style>



## Breve historia de R
> - ¿Qué es R?.
> - R es un dialecto de S. S fué implementado por John Chambers y Rick Becker en los laboratorios Bell en 1976.
> - En 1988, la versión 3 de S fue reescrita en C.
> - En 1998, la versión 4 de S fué anunciada y es la versión que más o menos se lleva hoy.
> - S fué adquirido por Insightful que creo el sistema S+ (versión comercial de S). En 1998, S ganó el prestigioso premio de software de la ACM.
> - Los fundamentos de S no han cambiado desde 1998.

--- .class #id 

## Breve historia de R (continuación)
> - R, por otro lado fué desarrollado por Ross Ihaka y Robert Gentleman en la Universidad de Auckland.
> - El proyecto fué iniciado en 1992 y la versión inicial fue presentada en 1995. La primera versión estable fue presentada hasta el año 2000 (llamada la versión 1.0.0).
> - La versión 3.0.2 fué lanzada hasta el 2013.

--- .segue bg:grey

## Características, ventajas y desventajas

---


## Características de R
> - Síntaxis similar a S.
> - Se puede ejecutar en cualquier sistema operativo (Windows, MacOSX, Linux, Unix) así como en playstation 3 y sistemas Android (mediante GNURoot).
> - Se presentan versiones nuevas de manera frecuente (actualmente la versión 3.3.2).
> - Tiene un sistema de gráficos muy sofisticado (utilizando paquetes como *ggplot* y *plot.ly*).
> - Muy útil de forma interactiva (desde la consola de *R*) y además contiene un lenguaje de programación muy poderoso.
> - Tiene una comunidad de programadores y seguidores muy activa y es muy fácil buscar la solución a un problema en particular.
> - Contiene mas de 8000 paquetes que incrementan la funcionalidad del lenguaje y además es de acceso libre.

--- .class #id 

## Desventajas de R
> - Está basado en ideas y tecnología de hace 40 años.
> - Tiene poco soporte para gráficos en 3D.
> - Los objetos se tienen que tener en memoria.
> - No es ideal para todos los problemas además de que en ocasiones suele ser lento.

--- .segue bg:grey

## Buscando ayuda en R

---

## Buscando ayuda

- Antes de pedir ayuda a algún compañero es buena idea intentar buscar ayuda dentro de `R` o bién buscar en los sitios de internet que ofrecen ayuda sobre `R`.
- Los comandos `help` y `?` llevan al usuario a la documentación de ayuda de las funciones de `R`, sobre un `dataset` u otro objeto.


```r
help("mean")   # también se puede ejercutar help('mean') o help(mean)
?mean          # se puede llamar igualmente ?'mean' o ?"mean"
?"+"
help.start()   # muestra la página general de ayuda en R
```
- Si se requiere pedir ayuda de una función (e.g., `lmModel`) en un paquete de `R` (e.g., `fractal`) se puede hacer como:

```r
help(lmModel, package ="fractal")
```

--- .class #id

## Ayuda (continuación)

- Para entrar a la ayuda de un paquete (e.g., `longmemo`) se ejecuta:


```r
help(package = "longmemo")
```
- En ocasiones es de utilidad ver ejemplos sobre la utilización de una función en `R`,

```r
example(sd)
```
- De igual forma, en ocasiones es de utilidad ver una demostración de uso de una función en `R`, esto se hace como:

```r
demo()     # Muestra las demonstraciones disponibles en los paquetes
demo(package="stats")   # Demostraciones en el paquete "stats"
demo("nlm")             # Demo para la función nlm
```

--- .class #id

## Ayuda (continuación)

- La funciones `help` y `?` son útiles si se sabe el nombre de la función. Sin embargo en ocasiones, no se conoce el nombre del comando para realizar cierta operación (e.g., para estimar la varianza agregada de un proceso fractal)
- La función `apropos()` busca objetos, incluyendo funciones en la sesión actual de `R`. 

```r
apropos("^glm") # Busca objetos que empiecen con la expresión glm
```
- La función `help.search()`, también abreviada como `??` busca en la documentación de todos los paquetes instalados en nuestro sistema `R`.

- De igual forma se puede ejecutar el comando `RSiteSearch()` que busca ayuda en **CRAN**.
- Internet proporciona otros medios como los **CRAN Task Views**, **Stack Overflow**, **R FAQs** y listas de correo de `R`.


--- .segue bg:grey



## Comandos básicos

---


## Comandos básicos en `R`

- Es importante conocer el directorio de trabajo actual, lo anterior se obtiene mediante el comando `getwd()` y se cambia con `setwd()`

```r
setwd("/Users/monoxide2000/Desktop/slidesMetodos_parte1/")
getwd()
```

```
## [1] "/Users/monoxide2000/Desktop/slidesMetodos_parte1"
```
- El comando `ls()` lista los objetos en el **environment** de `R`.

```r
ls()
```

```
## [1] "dato" "m"    "x"
```
- Se usan los símbolos `#` y `<-` para comentarios y asignar valores a una variable. Los comandos `quit()` o `q()` cierran `R`. 

--- .segue bg:grey


## Estructura de datos en R

---

## Estructuras de datos básicas

- `R` contiene 4 estructuras de datos básicas las cuales se pueden agrupar de acuerdo al tipo de datos que contienen o bien de acuerdo a su dimensionalidad.
- Básicamente se agrupan como:

|    | Homogéneo         | Heterogéneo   |
|----|-------------------|---------------|
| 1d | Vectores atómicos | Listas        |
| 2d | Matrices          | Dataframes    |
| nd | Array             |               |

- Las estructuras de datos más complejas se construyen a partir de éstas y podemos conocer la estructura mediante el comando `str()`, que es una abreviación para `structure`.

--- .class #id

## Estructuras de datos (continuación)

- A continuación se muestran ejemplos del comando `str()` para diversos tipos de datos.


```r
dato <- 1:5
str(dato)
```

```
##  int [1:5] 1 2 3 4 5
```

```r
x <- list(num=1, chr=c("a","b","c"),logi=c(T,T,F,T))
str(x)
```

```
## List of 3
##  $ num : num 1
##  $ chr : chr [1:3] "a" "b" "c"
##  $ logi: logi [1:4] TRUE TRUE FALSE TRUE
```

--- .segue bg:grey



## Vectores

---

## Vectores atómicos

- El vector es la estructura de datos más básica en `R`.  Los vectores se pueden clasificar como vectores atómicos y listas.
- Los vectores tienen tres propiedades cómunes:
  + El tipo, obtenido mediante el comando `typeof()` e indica qué es.
  + La longitud, obtenido mediante `length()` e indica cuántos elementos tiene.
  + Los atributos, definidos mediante `attributes()` o `attr()`, la cual sirve para especificar metadatos a los objetos.
- Como se mencionó anteriormente difieren en los tipos de datos que pueden contener (homogéneos o heterogéneos).

--- .class #id

## Vectores atómicos (continuación)
- Los vectores atómicos pueden ser de $6$ tipos: `character`, `numeric`, 'integer', `complex`, `logical` y `raw`.

| Ejemplo | Tipo de vector atómico |
| ------- | ---- |
| `"a"`, `"swc"` | `character` |
| `2`, `15.5` | `numeric` | 
| `2L` (se le añade el sufijo `L` para denotar un `integer`) | `integer` |
| `TRUE`, `FALSE` | `logical` |
| `1+4i`| `complex` | 

--- .class #id


## Vectores atómicos (continuación)
- En `R` se pueden crear vectores vacíos con el comando `vector()`. Por defecto el vector es lógico, sin embargo podemos crear vectores numéricos con `numeric()` o `vector("numeric")` de igual forma se pueden crear valores lógicos con `logical`, etc.

```r
vector()    # crea un vector lógico sin elementos (vacío)
```

```
## logical(0)
```

```r
vector(length=4)   # crea un vector lógico con 4 elementos (FALSE) = `vector("logical",4)`
```

```
## [1] FALSE FALSE FALSE FALSE
```

```r
vector("numeric", 4) # Crea un vector númerico con 4 elementos (por defecto 0)
```

```
## [1] 0 0 0 0
```

```r
numeric(4)  #idem
```

```
## [1] 0 0 0 0
```

--- .class #id

## Vectores atómicos (continuación)
- Además de los comandos anteriores `R` puede crear vectores atómicos mediante el comando `c()` que significa **combinar**.


```r
(x <- c(1,2.3,4.2,5.7,8))   # Crea un vector númerico.
```

```
## [1] 1.0 2.3 4.2 5.7 8.0
```

```r
(y <- c(1L,8L,9L))          # Crea un vector de enteros.
```

```
## [1] 1 8 9
```

```r
z <- c("a","letra","c")   # Crea un vector de caracteres
(im <- c(2+3i,4+5i))        # Crea un vector de números complejos.
```

```
## [1] 2+3i 4+5i
```

--- .class #id

## Vectores atómicos (continuación)
- Podemos examinar el tipo o clase objeto mediante los comandos `typeof()` y `class()`

```r
typeof(x)
```

```
## [1] "double"
```

```r
typeof(y)
```

```
## [1] "integer"
```

```r
class(im)
```

```
## [1] "complex"
```

--- .class #id

## Vectores atómicos (continuación)
- El comando `c()` me permite agregar elementos a un vector existente

```r
fir <- c("a","e","i")
let <- c("c","d","f")
tot1 <- c(fir,"u")
print(tot1)
```

```
## [1] "a" "e" "i" "u"
```

```r
tot2 <- c(let,"m")
tot2
```

```
## [1] "c" "d" "f" "m"
```

```r
tot <- c(tot1,tot2)
```

--- .class #id


## Vectores atómicos (continuación)
- Se pueden crear secuencias de vectores numéricos mediante el comando `:`, que crea secuencias e intervalos de $\pm 1$.

```r
2:6   # Crea un vector del 2 al 6 e intervalos de 1
```

```
## [1] 2 3 4 5 6
```

```r
6.1:3 # Crea un vector iniciando en 3.1
```

```
## [1] 6.1 5.1 4.1 3.1
```

--- .class #id

## Vectores atómicos (continuación)
- El comando `:` se puede generalizar mediante el comando `seq` el cual genera secuencias de cualquier longitud y espaciado en un intervalo.

```r
seq(from=2, to = 5, by=2)
```

```
## [1] 2 4
```

```r
seq(from=2, to = 5, length=6)
```

```
## [1] 2.0 2.6 3.2 3.8 4.4 5.0
```

```r
seq(2,5,length=6)
```

```
## [1] 2.0 2.6 3.2 3.8 4.4 5.0
```

--- .class #id


## Vectores atómicos (continuación)
- ¿Qué sucede si en un vector atómico mezclamos objetos de diferentes tipos?
- `R` en este caso creará el vector con mayor jerarquía. Por ejemplo:

```r
(x <- c(1.6,"a"))
```

```
## [1] "1.6" "a"
```

```r
(x <- c(TRUE,2))
```

```
## [1] 1 2
```

```r
(x <- c(2.5,3+4i,1L))
```

```
## [1] 2.5+0i 3.0+4i 1.0+0i
```

--- .class #id

## Vectores atómicos (continuación)
- Las operaciones anteriores se llaman **forzado (coerción) implicito(a)**, sin embargo también se puede hacer de forma explicita mediante el comando `as.<nombre.clase>`, e.g.,

```r
as.numeric(c(T,T,F,T,F))
```

```
## [1] 1 1 0 1 0
```

```r
as.logical(c(1,-1,0,0,45,61))
```

```
## [1]  TRUE  TRUE FALSE FALSE  TRUE  TRUE
```

```r
as.logical(c("a","f","m"))
```

```
## [1] NA NA NA
```

--- .class #id

## Vectores atómicos (continuación)
- En ocasiones existe coerción implícita en las operaciones, e.g.,

```r
1 < "2"
```

```
## [1] TRUE
```

```r
sin(c(T,T,F,F))
```

```
## [1] 0.841471 0.841471 0.000000 0.000000
```

```r
!c(1.4,0,3)
```

```
## [1] FALSE  TRUE FALSE
```

--- .segue bg:grey

## Matrices

---


## Matrices
- Las matrices son un tipo especial de vector en `R`. Son simplemente vectores atómicos con el atributo dimensión.

```r
matrix(nrow = 2, ncol = 2)
```

```
##      [,1] [,2]
## [1,]   NA   NA
## [2,]   NA   NA
```

```r
vec   <- 5:10
mat   <-matrix(vec,nrow=3)
dim(mat)
```

```
## [1] 3 2
```

--- .class ·id

## Matrices
- Las matrices también se pueden crear asignándole el atributo dimensión a un vectos atómico, e.g.,

```r
vec        <- 3:12
dim(vec)   <- c(5,2)
vec
```

```
##      [,1] [,2]
## [1,]    3    8
## [2,]    4    9
## [3,]    5   10
## [4,]    6   11
## [5,]    7   12
```

```r
dim(vec)   <- c(4,4)
```

```
## Error in dim(vec) <- c(4, 4): dims [producto 16] no coincide con la longitud del objeto [10]
```

--- .class ·id

## Matrices
- Las matrices, por último se pueden crear mediante la concatenación de filas o columnas de vectores.

```r
rbind(c(1,2,3), c(2,4,5))
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]    2    4    5
```

```r
cbind(c(1,2,3), c("a","b","c"))
```

```
##      [,1] [,2]
## [1,] "1"  "a" 
## [2,] "2"  "b" 
## [3,] "3"  "c"
```

--- .segue bg:grey

## Listas

---

## Listas
- Las listas actuan como contenedores, a diferencia de los vectores atómicos el contenido puede ser de diversos tipos. Creamos una lista con el comando `as.list()` y hacemos la coerción a lista mediante `as.list()`

```r
x <- list(Numeros = c(3,4,9), logi = c(T,F), list(a=1,b="a"))
x
```

```
## $Numeros
## [1] 3 4 9
## 
## $logi
## [1]  TRUE FALSE
## 
## [[3]]
## [[3]]$a
## [1] 1
## 
## [[3]]$b
## [1] "a"
```

--- .class #id

## Listas (continuación)
- El comando `str()` me permite checar kla estructura de la lista de una forma más amena.

```r
x <- list(Numeros = c(3,4,9), logi = c(T,F), list(a=1))
str(x)
```

```
## List of 3
##  $ Numeros: num [1:3] 3 4 9
##  $ logi   : logi [1:2] TRUE FALSE
##  $        :List of 1
##   ..$ a: num 1
```

--- .segue bg:grey

## Dataframes

----

## Dataframes
- Los `dataframes` son los tipos de datos más populares en `R`.  
- Los `dataframes` se crean mediante la función `data.frame()` o bien en la lectura de archivos mediante los comandos `read.csv()`, `read.table()`.
- Podemos convertir un `dataframe` en una matriz por medio del comando `data.matrix()`.
Los comandos `nrow()` y `ncol()` permiten conocer el número de filas y columnas de un `dataframe`.
- Otras funciones útiles son: `head()`, `tail()`, `dim()`, `nrow()`, `ncol()`, `str()` y `names()

--- .class #id

## Dataframes (continuación)
- Como se mencionó con anterioridad el comando `data.frame()` genera un `dataframe`, e.g.,

```r
df <- data.frame(let = letters[1:10], num =1:10, vars = runif(10))
df
```

```
##    let num      vars
## 1    a   1 0.8071137
## 2    b   2 0.5978999
## 3    c   3 0.1921755
## 4    d   4 0.2367058
## 5    e   5 0.6841478
## 6    f   6 0.2301506
## 7    g   7 0.3992139
## 8    h   8 0.3550818
## 9    i   9 0.5604982
## 10   j  10 0.5383901
```

--- .class #id



