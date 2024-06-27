# **WGET para Windows**

## 1. Descargar e instalar wget
Ir a la página de GNU Wget for Windows y descarga la versión más reciente del archivo binario wget.exe:

```
[GNU wget](https://eternallybored.org/misc/wget/)
```

## 2. Mover el archivo wget.exe al PATH
Mover el archivo wget.exe a una carpeta de tu sistema que está en el PATH, como C:\Program Files\wget.

## 3. Agregar la carpeta al PATH: 
a. Busca "Editar variables de entorno" en el buscador de la barra inferior del Escritorio.
b. Haz clic en Variables de Entorno.
c. En la sección Variables del sistema, busca la variable Path y selecciona Editar.
d. Haz clic en Nuevo e ingresa la ruta a la carpeta donde moviste wget.exe, por ejemplo, C:\Program Files\wget.
e. Haz clic en Aceptar en todas las ventanas abiertas para aplicar los cambios.

## 4. Verificar la instalación 
Abrir GitBash y escribe el siguiente comando para verificar que wget se ha instalado correctamente y está en el PATH:

```
wget --version
```
Se verá la información sobre la versión de wget instalada, confirmando que la instalación fue exitosa.


# **IQTREE2 para Windows**

## 1. Descargar e instalar iqtree2
Crear una carpeta Iqtree y descarga iqtree2 comprimido zip para Windows.

```
wget https://github.com/iqtree/iqtree2/releases/download/v2.2.0/iqtree-2.2.0-Windows.zip
```

## 2. Descomprimir el archivo iqtree2-2.0-Windows.zip

```
unzip iqtree-2.2.0-Windows.zip
```

## 3. Mover el archivo descomprimido al PATH:
Mover el archivo descomprimido a C:\Program Files\Iqtree. 

## 4. Agregar la carpeta al PATH:
a. Busca "Editar variables de entorno" en el buscador de la barra inferior del Escritorio.
b. Haz clic en Variables de Entorno.
c. En la sección Variables del sistema, busca la variable Path y selecciona Editar.
d. Haz clic en Nuevo e ingresa la ruta a la carpeta Iqtree y a la subcarpeta del archivo       ejecutable, por ejemplo, C:\Program Files\Iqtree\bin
e. Haz clic en Aceptar en todas las ventanas abiertas para aplicar los cambios.

## 3. Verificar la instalación:
Abre GitBash y escribe el siguiente comando para verificar que IQ-TREE se ha instalado correctamente y está en el PATH:

```
iqtree2 -h
```
Este comando debe mostrar la ayuda de IQ-TREE, confirmando que la instalación ha sido exitosa.


# **Análisis de Concordancia**
En tres pasos:

## 1. Inferring gene/locus trees (Generar un archivo .treefile)

a. En el caso de tener un archivo fasta alineado (concantenado con todos los genes) y un archivo con la particion usar el siguiente script:

```
iqtree2 -s <ALN_FILE> -s <PARTITION_FILE> –prefix loci -T AUTO
```
De lo contrario continuar al paso b.


b. En el caso de tener varios archivos fasta alineados (varios genes, ejemplo COI, ND2 y RAG1) (Mi caso)

-Colocar los tres archivos (Binotatus_2024_COI.fasta, Binotatus_2024_ND2.fasta y Binotatus_2024_RAG1.fasta) en una carpeta llamada "Concord" (Ojo: los tres genes se obtienen luego de dividir la gran matriz alineada de preferencia).

-Salir un nivel anterior de la carpeta "Concord" y colocar en el script el nombre de la carpeta. Porque si se ejecuta en la misma carpeta se genera un archivo loci.log que obstaculiza al comando.

```
iqtree2 -S Concord --prefix loci -T AUTO
```

c. Se genera varios archivos, entre ellos "loci.trefile"  

```
loci.trefile
```

## 2. Astral Generar árbol de especies concenso de los genes

a. Descargar Astral

```
https://github.com/smirarab/ASTRAL?tab=readme-ov-file

```
Ir a la sección Installation y descargar el archivo ZIP.

b. Crear una carpeta "AstralRun" y copiar el archivo "loci.treefile" que se generó en la sección 1c.

c. Llamar a Astral usando el comando export desde la carpeta del archivo ejecutable astral.5.7.8.jar

```
export ASTRAL=/c/Users/Lenovo/Desktop/ProyectosBI/Astral/Astral/astral.5.7.8.jar
```

d. Correr Astral, indicando que archivo de entrada "loci.trefile" y el nombre del archivo de salida "test.Astra"

```
java -jar $ASTRAL -i loci.treefile -o test.Astra
```

e. Se genera un archivo "test.astra" que es el árbol consenso.

```
test.astra
```

## 3.	Gene Concordance Factor (gCF)

a. Copiar en una carpeta llamada "FactorC" los dos archivos: loci.treefile de la sección 1c y el archivo "test.Astra" de la sección 2e.

b. Correr iqtree2

```
iqtree2 -t test.Astra --gcf loci.treefile --prefix concord
```
c. Se generan varios archivos y escoger entre ellos, "concord.treefile".

```
concord.treefile
```

d. Abrir el archivo "concord.treefile" con el programa FigTree. 



