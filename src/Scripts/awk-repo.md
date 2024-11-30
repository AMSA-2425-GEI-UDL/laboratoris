# Repositori d'exercicis - Axel Berral Lopez

Aquesta secció conté els exercicis realitzats pels estudiants de l'assignatura d'Administració i Manteniment de Sistemes i Aplicacions (AMSA).

## Exercicis



### Bàsics

**Imprimiu els noms de tots els pokémons de tipus planta de la primera generació. La columna 12 indica la generació i la columna 3 indica el tipus primari del pokémon.**

      awk -F, '$12 == 1 && $3 == "Grass" {print $2}' pokemon.csv


**Compta el nombre de pokémons de la primera generació que siguin de tipus aigua. La columna 3 indica el tipus primari del pokémon i la columna 12 la generació.**

      awk -F, '$12 == 1 && $3 == "Water" {count++} END {print count}' pokemon.csv


**Imprimiu el nom i l'atac de tots els pokémons de tipus drac de la primera generació. La columna 3 indica el tipus i la columna 7 (Atac).**

      awk -F, '$12 == 1 && $3 == "Dragon" {print $2, $7}' pokemon.csv


**Compta el nombre de pokémons de tipus psíquic de la primera generació que tinguin un atac superior a 70. La columna 3 indica el tipus primari del pokémon i la columna 7 l'atac.**

      awk -F, '$12 == 1 && $3 == "Psychic" && $7 > 70 {count++} END {print count}' pokemon.csv





### Intermedis

**Cerca el pokémon més ràpid i més lent de la primera generació, utilitzant la columna 10 (Velocitat).**

    awk -F, 'BEGIN{ max=0; min=1000 } $12 == 1 { if ($10 > max) { max=$10; pmax=$2 } if ($10 < min) { min=$10; pmin=$2 } } END{ print "Slowest: "pmin "\nFastest: "pmax }' pokemon.csv


**Imprimeix el nom i la defensa més alta de tots els pokémons de tipus roca de la primera generació, utilitzant la columna 9 (Defensa) i la columna 3 (Tipus primari).**

    awk -F, 'BEGIN{ max_def=0 } $12 == 1 && $3 == "Rock" { if ($9 > max_def) { max_def=$9; pmax=$2 } } END{ print "Pokémon with highest defense: "pmax ", Defense: "max_def }' pokemon.csv


**Cerca el pokémon amb la millor defensa especial (columna 11) i el pitjor atac especial (columna 8) de la primera generació.**

    awk -F, 'BEGIN{ max_sp_def=0; min_sp_atk=1000 } $12 == 1 { if ($11 > max_sp_def) { max_sp_def=$11; pmax_def=$2 } if ($8 < min_sp_atk) { min_sp_atk=$8; pmin_atk=$2 } } END{ print "Best Special Defense: "pmax_def "\nWorst Special Attack: "pmin_atk }' pokemon.csv


**Imprimeix el nom i la velocitat del pokémon de tipus gel amb la velocitat més baixa de la primera generació (columna 10).**

    awk -F, 'BEGIN{ min_speed=1000 } $12 == 1 && $3 == "Ice" { if ($10 < min_speed) { min_speed=$10; pmin=$2 } } END{ print "Slowest Ice-type: "pmin ", Speed: "min_speed }' pokemon.csv






### Avançats

**Implementeu un parser que transformi el fitxer pokemon.csv en un fitxer JSON només per als pokémons de la primera generació que siguin de tipus elèctric. Format: {"name": "Pikachu", "type": "Electric", "attack": 55, "defense": 40, ...}**

awk -F, '
BEGIN {
    print "["
}
BEGIN {
    print "["
}
$12 == 1 && $3 == "Electric" {
    printf("{\"name\": \"%s\", \"type\": \"%s\", \"attack\": %s, \"defense\": %s, \"speed\": %s, \"generation\": %s}", $2, $3, $7, $9, $10, $12)
    if (NR != FNR) print ","
}
END {
    print "]"
}' pokemon.csv > electric_pokemon.json





**Crea un fitxer JSON només per als pokémons de la primera generació que siguin llegendaris. Cada entrada ha de tenir nom, tipus principal i atac especial (columna 8).**


awk -F, '
BEGIN {
    print "["
}
$12 == 1 && $13 == "True" {
    printf("{\"name\": \"%s\", \"type\": \"%s\", \"special_attack\": %s}", $2, $3, $8)
    if (NR != FNR) print ","
}
END {
    print "]"
}' pokemon.csv > legendary_pokemon.json
