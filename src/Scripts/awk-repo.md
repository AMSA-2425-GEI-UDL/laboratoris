# Repositori d'exercicis

Aquesta secció conté els exercicis realitzats pels estudiants de l'assignatura d'Administració i Manteniment de Sistemes i Aplicacions (AMSA).

## Exercicis 

### Bàsics

**Ejemplo 1:**
Mostrar solo las primeras 10 líneas del archivo pokemon.csv usando cat. Se utiliza cat para mostrar todo el archivo pokemon.csv y luego head para limitar la salida a las primeras 10 líneas:

cat pokemon.csv | head -n 10


**Ejemplo 2:**
Buscar Pokémon cuyo nombre contenga exactamente 6 letras usando grep. La expresión regular ^.{6}, busca cualquier línea que comience con exactamente 6 caracteres seguidos de una coma:

grep -E "^.{6}," pokemon.csv

Usando awk, sería:

awk -F, 'length($2) == 6 {print $2}' pokemon.csv


**Ejemplo 3:** 
Buscar Pokémon con velocidad mayor a 100 y defensa especial menor a 80 usando awk:

awk -F, '$11 > 100 && $10 < 80 {print $2, $11, $10}' pokemon.csv


### Intermedis

**Ejemplo 4:**
Añadir una columna con la media aritmética de los atributos. Se añade una nueva columna llamada Avg en la cabecera y calcula la media de las estadísticas para cada Pokémon, imprimiéndola en una nueva columna:

awk -F, 'NR==1 { print $0 ",Avg"; next } { avg = ($6+$7+$8+$9+$10+$11)/6; print $0 "," avg }' pokemon.csv


**Ejemplo 5:**
Comprobación de si el Total es igual a la suma de los atributos usando variables. Se define una variable llamada total_suma que almacena la suma de las estadísticas del Pokémon (columnas 6 a 11). Luego, se compara con la columna 5, que contiene el valor del Total:

awk -F, '{ total_suma = $6+$7+$8+$9+$10+$11; print $2"->Total="$5"=="total_suma }' pokemon.csv


### Avançats
