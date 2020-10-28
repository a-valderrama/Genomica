# Comandos de la Práctica 01

## Alejandro T. Valderrama Silva

### <u>Parte I</u>

1. Versión del shell: **GNOME Shell 3.28.4** 
   - Lo conocimos por medio del comando: `GNOME Shell 3.28.4` 	
2. Creamos los directorios con el siguiente comando: `mkdir data/ filtered/ raw_data/ meta/ scripts/ figures/ archive/`
3. Acomodamos los directorios con los comandos: 
   - `mv filtered/ data/`
   - `mv raw_data/ data/`
4. Estos directorios organizan la información necesaria para reproducir los análisis realizados. De esta forma, al compartir algo del proyecto, podemos citarlo y compartirlo de forma flexible y controlada.
   - *data*: contiene los datos, puede tener otros nombres que dependerán de los datos que estamos guardando en este directorio; pero en general lo podemos dejar como *data* 
   - *meta*: aquí se guardan los metadatos. En general se guardan todos los archivos necesarios para procesar los datos. 
   - *scripts:* aquí guardamos todos los scripts necesarios para el análisis.
   - *figures*: es un directorio, opcional, en el que guardamos código que se utilice sólo para hacer las figuras de una publicación dada.
   - *archive*: es un directorio que no suele añadirse al repositorio remoto, pero es una buena práctica tenerlo para guardar cosas que no son tan importantes y que pueden llegar a necesitarse posteriormente.

### <u>Parte II</u>

1. Creamos el nuevo archivo con: `touch delay.sh`
2. Damos permisos de ejecución con: `chmod +x delay.sh`
3. Lo ejecutamos con: `./delay.sh`
4. Agregamos el comando para "dormirlo": `sleep 30`
5. Lo ejecutamos en segundo plano con: `./delay.sh &`
6. Luego lo cancelamos con: `kill 12035` -> el PID en nuestro caso

### <u>Parte III</u>

2. Renombramos archivos con:
   - `mv sequence.fasta sarscov2_genome.fasta`
   - `mv sequence.gff3 sarscov2_genome.gff3`
3. Copiamos la secuencia de la estructura con los siguientes comandos:
   - `mv sequence.fasta splike_c.faa`
   - `mv sequence\ \(1\).fasta splike_b.faa`
   - `mv sequence\ \(2\).fasta splike_a.faa`

### <u>Parte IV</u>

1. Creamos las ligas simbólicas suaves con los siguientes comandos:
   - `ln -s ../raw_data/splike_a.faa` 
   - `ln -s ../raw_data/splike_b.faa` 
   - `ln -s ../raw_data/splike_c.faa` 
2. Creamos el archivo *glycoproteins.faa* con: `touch glycoproteins.faa`
3. Obtenemos la primera línea de los tres archivos con los siguientes comandos (respectivamente):
   - `awk 'NR==1 {print; exit}' splike_a.faa`
   - `awk 'NR==1 {print; exit}' splike_b.faa`
   - `awk 'NR==1 {print; exit}' splike_c.faa`
4. Redireccionamos el contenido de los archivos *splike_\** a *glycoproteins.faa*  con: `cat splike_* > glycoproteins.faa`
5. Movemos los archivos con el comando: `mv data/raw_data/splike_*.faa archive/`. 
   - Con respecto a las "ligas simbólicas suaves", lo que pasa es que ya no existe el enlace que se hizo porque los archivos ya no están en la ubicación original. Por lo que las ligas que quedan están vacías.
6. Vemos el contenido de los archivos, las tres primeras lineas, con:
   - `zless sarscov2_assembly.fasta.gz | head -3`
     \>NODE_1_length_264_cov_161.042781
     CACAAATCTTAACACTCTTCCCTACACGACGCTCTTCCGATCTACGCCGGGCCATTCGTA
     CGAACCGATACCTGTGGTAAAGGGTCCTACTGTATGGTGGTACACGAGTAGTAGCAAATG
   - `less sarscov2_genome.fasta | head -3`
     \>NC_045512.2 Severe acute respiratory syndrome coronavirus 2 isolate Wuhan-Hu-1, complete genome
     ATTAAAGGTTTATACCTTCCCAGGTAACAAACCAACCAACTTTCGATCTCTTGTAGATCTGTTCTCTAAA
     CGAACTTTAAAATCTGTGTGGCTGTCACTCGGCTGCATGCTTAGTGCACTCACGCAGTATAATTAATAAC
   - El archivo *sarscov2_genome.fasta* describe el genoma del virus mientras que el el archivo *sarscov2_assembly.fasta.gz* describe su estructura. 
7. Contamos la cantidad de *headers* en cada archivo con:
   - `grep -o \> sarscov2_genome.fasta | wc -l` -> 1 header
   - `zless sarscov2_assembly.fasta.gz | grep -o \> | wc -l` -> 35 headers
8. Obtenemos las primeras 12 líneas con: `zless SRR10971381_R1.fastq.gz  | head -12`
   @SRR10971381.512_1
   GAGCACAATCAGACAACTACTATTCAAACAATTGTTGAGGTTCAACCTCAATTAGAGATGGAACTAACACCAGTTGTTCAGACTATTGAAGTGAATAGTTTTAGTGGTTATTTAAAACTTACTGACAATGTATACATTAAAAATGAAGAC
   +
   F/=/FFFAA/A/FFFAFFFF/AFFAFAAFFAFFF//F=FF//FFA=/FFFF//FFFFFFA/FFF//FFAFF//FAFF/A/F/A/FFFAF6FF6F/F/F//F/AFFFA6F/FFFFFFA/FFFFF6AFFFFF/FFFFFFFFF/F6FF6AF/=
   @SRR10971381.556_1
   AGGGGGTAAAAAAAAAAAAAAAAAAAAAAAAAAAATAAATTAAAAAAATAAAAAAAAAAAAATTAAAAATTAAAAAAAAAAAAAAAAATAAAATATTAATTACAAAAAAAATAAAAATAAAATAAAAAAAAATTAAAAATAAATAGGATA
   +
   ///FF//FFFF//FFFF/FFFFFFA//FFFFF/FF/=////AFAFFF////A=//AFFFFF////F/=//FF/=/FFFFFFFFFFFFFFFFFFF/FFFFFFF/FFFFFFF/FFFFFFFFFFFFFAFFFFFFFFFFFFFFFFFFAFFFFFF
   @SRR10971381.1428_1
   TTACATAAAAGAAAGAATGACTGATGAGAGAAGTAAGAGAAAAAAAAAAGTGAATTTAAAAATAAAAGAAAAAAAAAAAAAAATGTATGTAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGAAAAAAAA
   +
   ///AAFAAFFFFFFFFFFAFAAFFFAFFFFFFFAFFAFAFFFFFFFFFF///FFAA/AFFFF/FFFF//AFFFFFFFFFFF6F////F//FFFFFFFFFFFFAFFFAFFFFFF6A//F//FFF//A/F///=A//F///6///FFF////
   - Analizando el patrón veo que el caracter que me puede ayudar a obtener un conteo de secuencias es el **@**
   - Contamos la cantidad de secuencias con: `zless SRR10971381_R1.fastq.gz | grep -o \@ | wc -l` -> *130022 secuencias*
9. Tanto los archivos *.fna* como los *.fasta* contienen cadenas/secuencias que hacen referencia a nucleótidos, mientras que los *.faa* contienen cadenas/secuencias que hacen referencia a aminoácidos. 
   Por otro lado, los archivos *.fastq* hacen referencia a cadenas de nucleótidos y sus puntuaciones de calidad correspondientes (por cada cadena de nucleótidos).
10. Notamos que al ver el contenido de este tipo de archivos son `less` la lectura es un tanto caótica; resulta difícil interpretar la información y entender la agrupación de la misma. Mienras que con la bandera `-S` al truncar los espacios, la información queda acomodada de forma "bonita", donde es fácil diferenciar la información agrupada por columnas, y por lo tanto, interpretarla.
11. Reportamos la cantidad de genes que tiene el archivo con el comando: `cat sarscov2_genome.gff3 | awk -F"\t" '{print $3}' | grep -o 'gene' | wc -l` -> 11 genes.
    - El campo o la columna 3 corresponde al tipo de característica.
    - *CDS* se refiere a que es una secuencia de codificación de proteínas, mientras que *gene* se refiere a que es una secuencia de codificación del símbolo del gen primario.