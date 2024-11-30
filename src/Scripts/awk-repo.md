# Repositori d'exercicis

Aquesta secció conté els exercicis realitzats pels estudiants de l'assignatura d'Administració i Manteniment de Sistemes i Aplicacions (AMSA).

## Exercicis
5 exercicis
### Bàsics
Filtra per Fire & Water.
```awk
grep -E 'Fire|Water' pokemon.csv | cut -d, -f2,3,10
```
### Intermedis
Busca els Pokémon de tipus "Dragon" i troba el que té el màxim "Sp. Atk", mostrant el nom i el valor.
```awk
awk -F, '$3 == "Dragon" {if($9 > max_special_atk) {max_special_atk = $9; dragon_pokemon = $2}} END {print "Dragon Pokemon with highest Sp. Atk:", dragon_pokemon, "with", max_special_atk, "Sp. Atk"}' pokemon.csv
```
Comptabilitza els Pokémon amb velocitat superior a 100 i determina el més ràpid, mostrant el nombre total i el nom del Pokémon més ràpid amb la seva velocitat.
```awk
awk -F, 'NR > 1 && $11 > 100 {fast_count++; if($11 > max_speed) {max_speed = $11; fastest_pokemon = $2}} END{print "Number of Pokemon with Speed > 100:", fast_count; print "Fastest Pokemon:", fastest_pokemon, "with", max_speed, "Speed"}' pokemon.csv
```
### Avançats

CSV --> JSON
```awk
awk -F, '
BEGIN {
    print "["
}
NR > 1 {
    printf "  {\n"
    printf "    \"Name\": \"%s\",\n", $2
    printf "    \"Type 1\": \"%s\",\n", $3
    printf "    \"Type 2\": \"%s\",\n", $4
    printf "    \"Total\": %d,\n", $5
    printf "    \"HP\": %d,\n", $6
    printf "    \"Attack\": %d,\n", $7
    printf "    \"Defense\": %d,\n", $8
    printf "    \"Sp. Atk\": %d,\n", $9
    printf "    \"Sp. Def\": %d,\n", $10
    printf "    \"Speed\": %d,\n", $11
    printf "    \"Generation\": %d,\n", $12
    printf "    \"Legendary\": %s\n", ($13 == "False" ? "false" : "true")
    printf "  }%s\n", (NR == 2 ? "" : ",")
}
END {
    print "]"
}' pokemon.csv > pokemon.json
```
ANALISIS TIPOS PROMEDIOS
```awk
awk -F, '
BEGIN {
    print "Análisis de Pokémon por tipo:"
}

    #Comienza a procesar desde la segunda línea
NR > 1 {
    #Ignorar líneas con el tipo "Type 1" o entradas vacías
    if ($3 == "" || $3 == "Type 1") {
        next;
    }

    #Sumar estadísticas para cada tipo
    total[$3] += $5;   #Total de estadísticas
    count[$3]++;       #Contador de Pokémon por tipo

    if ($4 != "") {   #Verifica si hay un segundo tipo
        total[$4] += $5;
        count[$4]++;
    }
}

END {
    # Imprimir encabezados de la tabla
    printf "+-----------+-------------------------------+\n"
    printf "| Tipo      | Promedio de Estadísticas Totales |\n"
    printf "+-----------+-------------------------------+\n"

    #Calcula y guarda promedios por tipo
    for (tipo in total) {
        promedio = total[tipo] / count[tipo];
        promedios[tipo] = promedio;  #Guarda el promedio
    }

    #Ordena los tipos según el promedio de estadísticas
    n = asorti(promedios, tipos_ordenados);  #Ordena los índices de los tipos

    #Imprime los promedios en orden descendente
    for (i = n; i >= 1; i--) {
        tipo = tipos_ordenados[i];
        printf "| %-9s | %.2f                       |\n", tipo, promedios[tipo];
    }
    printf "+-----------+-------------------------------+\n"
}' pokemon.csv
```
