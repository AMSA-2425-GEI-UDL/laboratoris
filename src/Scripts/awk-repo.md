# Repositori d'exercicis

Aquesta secció conté els exercicis realitzats pels estudiants de l'assignatura d'Administració i Manteniment de Sistemes i Aplicacions (AMSA).

## Exercicis

### Bàsics
1. Comanda que fa un recompte dels pokemon de tipus Dragon --> awk -F ',' '$3 == "Dragon" {count++} END {print count}' pokemon.csv
2. Comanda que calcula la mitjana de l'estadística "Defensa" de tots els pokemons de la pokedex --> awk -F ',' '{sum += $7; count++} END {print "Average Defense: " sum/count}' pokemon.csv
3. Comanda que mostra els pokemon amb un id múltiple de 7 --> awk -F ',' '$1 % 7 == 0 {print $2 " has number " $1 ", which is a multiple of 7"}' pokemon.csv



### Intermedis
4. Comanda que mitjançant condicionals mostra un missatge segons si els pokemons tenen atac > 100 i velocitat > 80 --> awk -F ',' '{if ($6 > 100 && $10 > 80) print $2 ": High Attack and High Speed"; else if ($6 > 100 && $10 <= 80) print $2 ": High Attack but Low Speed"}' pokemon.csv


### Avançats
5. Comanda que per cada tipus 1 fa una mitjana de les estadístiques com ara atac, defensa... -->
awk -F ',' '
NR > 1 {  
    type = $3;  
    
    total_attack[type] += $6;     
    total_defense[type] += $7;   
    total_sp_atk[type] += $8;     
    total_sp_def[type] += $9;     
    total_speed[type] += $10;      

    count[type]++;  
}
END {
    print "Average stats per type:\n";

    for (type in total_attack) {
        avg_attack = total_attack[type] / count[type];
        avg_defense = total_defense[type] / count[type];
        avg_sp_atk = total_sp_atk[type] / count[type];
        avg_sp_def = total_sp_def[type] / count[type];
        avg_speed = total_speed[type] / count[type];

   printf "%s: Average Attack: %.2f, Average Defense: %.2f, Average Sp. Atk: %.2f, Average Sp. Def: %.2f, Average Speed: %.2f\n", type, avg_attack, avg_defense, avg_sp_atk, avg_sp_def, avg_speed;
    }
}' pokemon.csv
