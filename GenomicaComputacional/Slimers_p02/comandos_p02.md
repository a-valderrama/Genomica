# Comandos de la Práctica 02

## Slimers

### Integrante 1: Badillo Macías Ricardo

### Integrante 2: Valderrama Silva Alejandro

# Parte 1

| Plataforma/compañía                        | Longitud de reads (pb) | # reads x run    | Tiempo  | Costo x 10^6 bases | Error (%) | Química                |
| ------------------------------------------ | ---------------------- | ---------------- | ------- | ------------------ | --------- | ---------------------- |
| **Primera** **generación**                 |                        |                  |         |                    |           |                        |
| Sanger/Life Technologies                   | 800                    | 1                | 2 hrs   | 2400               | 0.3       | Dideoxy terminator     |
| **Segunda generación**                     |                        |                  |         |                    |           |                        |
| 454 GS FLX+/Roche/0.7 Gb                   | 700                    | 1×10<sup>6</sup> | 24/48 h | 10                 | 1         | Pyrosequencing         |
| MiSeq/Illumina/15 Gb                       | 2x300                  | 3×10<sup>8</sup> | 27 h    | 0.13               | 0.8       | Reversible terminators |
| SOLiD/Life Technologies/120 Gb             | 50                     | 1×10<sup>9</sup> | 14 días | 0.13               | 0.01      | Ligation               |
| Retrovolocity/BGI/3000 Gb                  | 50                     | 1×10<sup>9</sup> | 14 días | 0.01               | 0.01      | Nanoball/ligation      |
| Ion PGM/Life Technologies/2 Gb             | 200                    | 5×10<sup>6</sup> | 2–5 h   | 1                  | 1.7       | Proton detection       |
| **Tercera generación**                     |                        |                  |         |                    |           |                        |
| SMRT/Pac Bio/1 Gb                          | >10,000                | 1×10<sup>6</sup> | 1–2 h   | 2                  | 12.9      | Real-time SMS          |
| Heliscope/Helicos/25 Gb                    | 35                     | 7×10<sup>9</sup> | 8 días  | 0.01               | 0.2       | Real-time SMS          |
| Nanopore/Oxford Nanopore Technologies/1 Gb | >5000                  | 6×10<sup>4</sup> | 48/72 h | <1                 | 34        | Real-time SMS          |

*Consultado en:* [https://www.intechopen.com/books/next-generation-sequencing-advances-applications-and-challenges/next-generation-sequencing-an-overview-of-the-history-tools-and-omic-applications](

# Parte 2

1. `awk 'BEGIN{P=1}{if(P==1||P==2){gsub(/^[@]/,">");print}; if(P==4)P=0; P++}' ERR486827_1.fastq > ERR486827_1.fasta`

   `awk 'BEGIN{P=1}{if(P==1||P==2){gsub(/^[@]/,">");print}; if(P==4)P=0; P++}' ERR486827_2.fastq > ERR486827_2.fasta`

2. `less ERR486827_1.fasta | grep -o \> | wc -l` -> *398824 secuencias*
   `less ERR486827_2.fasta | grep -o \> | wc -l` -> *398824 secuencias*
   Por lo tanto, **tienen la misma cantidad de secuencias.**

3. La función que resuelve este inciso está en la carpeta *scripts*, dentro del notebook **II-3**

# Parte 3
**Respuesta 1:**
Para descomprimir el archivo FastQC utilizamos: 

unzip fastqc_v0.11.9.zip

Nos creo una carpeta llamada FastQC nos movemos a esa carpeta:

cd FastQC

Asignamos los permisos de ejecución al archivo fastqc:

sudo chmod 111 fastqc 

Y lo volvemos ejecutable en cualquier lugar de la computadora:

sudo ln -s /home/ricardo/Descargas/FastQC/fastqc /usr/local/bin/fastqc


**Respuesta 2:**

Creamos el script de bash fastqc_run.sh

nano fastqc_run.sh   -> fastqc ERR486827_1.fastq ERR486827_2.fastq

Ejecutamos el archivo .sh

sudo sh fastqc_run.sh


**Respuesta 3:**
Abrimos los archivos .html de salida

 ERR486827_1_fastqc.html
 ERR486827_2_fastqc.html

Las lecturas son excelentes, ya que todas se encueentra en la región verde. Los cuales del 28-40 corresponde a excelente calidad.

El comportamiento de las calidades todas se mantienen en la región verde no hay lectura que sea menor a 37 y 38, cosa que nos fijamos en Per sequence quality scores,lo que indican que es de excelente calidad.
Y con respecto al contenido, los nucleotidos A y T tienen la misma cantidad, al igual que C y G y manteniendo la proporción entre ellos de 30 a 40 para A y T, y de 10 a 20 para C y G.



**Respuesta 4:**
>covertura = (cantidad de lecturas * longitud de lecturas) / total del tamaño del genoma (bp)
1 kb = 10000 bp
Tamaño del genoma = 580 kb = 580000 bp
>covertura = (398824 * 150)/580000 = 103.144137931 



# Parte 4
**Respuesta 1:**
Candidatus Carsonella 
Carsonella ruddii es una proteobacteria gamma endosimbionte. Tiene el segundo genoma más pequeño de todas las bacterias caracterizadas, por detrás de Hodgkinia cicadicola.​ Es un endosimbionte que está presente en todas las especies de Psyllida, unos insectos chupadores de savia

**Respuesta 2:**
La secuencia genomica se obtuvo utilizando el metodo de Illumina. Los bacteriocitos, células de insectos especializados, se diseccionaron y combinaron, de los cuales se extrajo el ADN, el ADN extraido se preparo usando el kit de preparación de la biblioteca de ADN de Nextera y se secuenció dentro de 1/4 de un carril en  Illumina, usando la química de secuenciación TruSeq SBS. Los archivos Fastq se generaaron con el software Casava 1.8.2.

https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5408110/

**Respuesta 3:**

>covertura = (cantidad de lecturas * longitud de lecturas) / total del tamaño del genoma (bp)
Tamaño del genoma = 160kb  = 160000 bp
Sacamos los datos para sacar la covertura al ejecutar FastQC, con los archivos del genoma del Candidatus Carsonella.  
El numero total de lecturas es de = 6423333
La longitud de lecturas va de 28-75, se tomo el valor mas grande.
>covertura = (6423333 * 75 )/160000 = 3010.93734375

**Respuesta 4:**
Para correr el FastQC hicimos otro archivo fastqc_run2.sh
La calidad se mantenia excelente hasta en los ultimos valores en donde baja a medio, a calidad media.
Entonces llegamos a la conclusión de que la calidad de las secuencias que nos dieron seria buena si se hubieran mantenido, asi que las consideramos media.

POdemos notar que los niveles de nucleotidos no son tan proporcionales y son variantes. la cantidad de A y T esta vez no son iguales, al igual que C y G. En donde todos los nucleotidos cambian de proporciones en unn comienzo.
**Respuesta 5:**
El Phred que utilizan nuestros datos esta entre el 36 y 37

**Respuesta 6:**

En nuestro caso la calidad disminuyo en la ultima parte de la longitd de nuestras lecturas, entonces para mantener la calidad debemos reducir la longitud de nuestras lecturas entonces para ello utilizaremos SolexaQA para recortar la entrada de las lecturas, y asi conservar siempre la calidad de nuestros archivos.
