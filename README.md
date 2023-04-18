# Bonus

```
# Decidí usar el for de una de las tareas:
	Crear una tabla de dos columnas (col1: nombre viejo, col2: nombre nuevo)
	Usar un for y sed para buscar y reemplazar nombre por nombre
	
# Expresiones regulares: 
## Crear lista de nuevos nombres a partir del formato de GenBank

F: LOCUS\s+(\w+).+\sDEFINITION\s+(\w+) (\w+)([\s\S])*?/country="(\w+)([\s\S]*?)\/\/
R: >$1_COI_$2_$3_$5

## Crear lista de nombres antiguos
F: (>.+)\s+(.+\s+){10}
R: $1\n

# Subir nuevos nombres 
scp -i bio.pt.pem -P 37022 /mnt/c/Users/Surface/OneDrive\ \-\ Universidad\ del\ rosario/Escritorio/new_names bio.pt@172.25.255.10:/home/bio.pt/data/Parcial1/parcial1_CamiloPeralta/bonus

# Subir nombres antiguos
scp -i bio.pt.pem -P 37022 /mnt/c/Users/Surface/OneDrive\ \-\ Universidad\ del\ rosario/Escritorio/orig_names.fasta bio.pt@172.25.255.10:/home/bio.pt/data/Parcial1/parcial1_CamiloPeralta/bonus

# Crear tabla de nombres
paste -d "\t" orig_names.fasta new_names > texto

# For 
wc -l texto
count=$(seq -s " " 1 1 10)

for e in $count; 
    do  
        orig_name=$(awk -v var="$e" 'NR == var {print $1}' texto); 
          
        new_name=$(awk -v var="$e" 'NR == var {print $2}' texto); 
           
        sed -i "s/$orig_name/$new_name/" COI_sequences.fasta; 
            
  done




```
