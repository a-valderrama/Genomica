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

