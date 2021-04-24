---
title: 'Leyendo archivos CSV en PHP'
date: 2021-04-23T14:24:40-03:00
description: Diferentes formas de leer archivos CSV desde PHP
slug: leyendo_archivos_csv_en_php
draft: false
categories: [ desarrollo ]
tags: [ php, archivos, csv ]
---
#### Fuente y destino de datos
Dado un archivo CSV (comma-separated values) como fuente de datos para un sistema, se presenta como primer necesidad leer ese archivo de forma correcta para extraer y procesar la información que contiene.

Fuente de datos en formato CSV

{{< gist jogianotti a989c7fbcf5b6d864c0491469ca1294f "data.csv" >}}

Entidad a la cual serán convertidos estos datos

{{< gist jogianotti a989c7fbcf5b6d864c0491469ca1294f "Person.php" >}}

#### Funciones del sistema de archivos
Lectura de cada línea del archivo en orden, haciendo uso de las funciones ```fopen()```, ```fgetcsv()``` y ```fclose()```

{{< gist jogianotti a989c7fbcf5b6d864c0491469ca1294f "read_csv.php" >}}

#### Standar PHP Library
Una alternativa es usar la clase ```SplFileObject``` provista por la **Standard PHP Library (SPL)** que nos provee una abstracción para la manipulación de archivos.

{{< gist jogianotti a989c7fbcf5b6d864c0491469ca1294f "read_csv_spl.php" >}}

#### PHP League
Otra alternativa interesante es el uso de alguna biblioteca para la gestión de este tipo de archivos que provean funcionalidades extras o una interfaz simple de usar. En este ejemplo se usa la biblioteca para la manipulación de archivos CSV de **PHP League**. Aquí se muestra un ejemplo extraído de la documentación oficial.

{{< gist jogianotti a989c7fbcf5b6d864c0491469ca1294f "read_csv_league.php" >}}

#### Conclusión
Todas las formas presentadas aquí son en general simples y claras. Esta obtención de datos desde un archivo CSV se debe combinar con algoritmos de **búsqueda**, **unión**, **ordenamiento**, etc. Esos serán los próximos pasos.
