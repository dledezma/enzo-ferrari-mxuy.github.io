## Anexo comandos Unix

### A1- Creación de estructura de directorios y archivos

``` bash
$pwd

Output:
/home/mobaxterm/MyDocuments/Campo-Mixteca
```



``` bash
$mkdir -p campo2021-{data/clima,data/phenology,data/morphology,scripts,analysis}

Output:
total 6
-rwx------    1 elfer    UsersGrp     218 Nov 18 20:58 Campo-Mixteca.Rproj
-rwx------    1 elfer    UsersGrp      50 Nov 18 19:13 TrabajoFinal.RData
-rwx------    1 elfer    UsersGrp      53 Nov 18 20:35 TrabajoFinal.Rhistory
drwxr-xr-x    1 elfer    UsersGrp       0 Nov 18 17:32 campo2021-analysis
drwxr-xr-x    1 elfer    UsersGrp       0 Nov 18 18:13 campo2021-data
drwxr-xr-x    1 elfer    UsersGrp       0 Nov 18 22:07 campo2021-scripts


```



### A2. Creación de tabla cruda de datos climáticos

Como hay registros repetidos, es necesario curar la base de datos:

```bash
$cd ../respaldos_tablas_Campo-Mixteca/
$pwd

Output:
/home/mobaxterm/MyDocuments/respaldos_tablas_Campo-Mixteca

$cat 2020_12_2021_07_Lama.txt 2021_06_2021_10_Lama.txt 2021_05_2021_06_Lama.txt > clima-raw.txt
```

El archivo **clima-raw.txt** aún tiene fechas innecesarias (del año 2020, etiquetas y filas duplicadas, por tanto, es necesario modificarlo con un pipe de Unix:

``` bash
$less clima-raw.txt | grep --colour -v 2020 | sort -n | uniq | less > clima-ordenado.txt
$head clima-ordenado.txt

Output:
Date    Time    Temp_Out        Hi_Temp Low_Temp        Out_Hum Dew_Pt  Wind_Speed      Wind_Dir        Wind_Run        Hi_Speed        Hi_Dir      Wind_Chill      Heat_Index      THW_Index       Bar     Rain    Rain_Rate       Heat_D_D        Cool_D_D        In_Temp In_Hum  In_Dew      In_Heat In_EMC  In_Air_Density  Soil1_Moist     Soil2_Moist     Soil3_Moist     Soil4_Moist     Soil_Temp1      Soil_Temp2      Soil_Temp3  Soil_Temp4      Wind_Samp       Wind_Tx ISS_Recept      Arc/Int
2021-05-01      10:00 p. m.     15.1    15.1    15.1    83      12.2    0       ---     0       0       ---     15.1    15.1    15.1    1056.3      0       0       0.269   0       19.7    60      11.7    19.4    11.05   1.241   ---     ---     ---     ---     ---     ---     ------      66      1       2.4     120
2021-05-02      01:00 p. m.     20.1    20.1    19.8    55      10.8    4.8     N       4.83    16.1    NE      20.1    19.7    19.7    1005.9      0       0       0       0.074   22.4    46      10.2    21.7    8.6     1.1717  ---     200     ---     200     18.9    18.9    20 20.6     313     4       24.6    60
2021-05-02      02:00 p. m.     21.8    21.9    19.7    47      10      6.4     NE      6.44    27.4    NNE     21.8    20.9    20.9    1004.9      0       0       0       0.144   21.9    45      9.4     20.9    8.45    1.1733  ---     200     200     200     18.9    18.9    20 20.6     1283    4       100     60
2021-05-02      03:00 p. m.     21.3    22.4    21.3    48      9.9     3.2     E       3.22    20.9    NE      21.3    20.3    20.3    1003.4      0       0       0       0.125   22.7    43      9.4     22      8.14    1.1684  200     200     200     200     18.9    18.9    20.6        21.1    1291    4       100     60
2021-05-02      04:00 p. m.     17.8    21.3    17.8    64      10.9    3.2     ENE     3.22    27.4    WSW     17.8    17.5    17.5    1003.2      0       0       0.021   0       21      49      9.9     20.1    9.05    1.1743  200     200     200     200     18.9    18.9    20.6        21.1    1307    4       100     60
2021-05-02      05:00 p. m.     11.4    17.8    9.4     82      8.4     6.4     WSW     6.44    37      WSW     11      11.3    10.9    1002.9      17.6    147.6   0.289   0       12.8    65      6.4     12.2    12.25   1.2109  2       4       2       35      18.3    18.3    18.9        20      1309    4       100     60
2021-05-02      06:00 p. m.     14.1    14.1    11.4    74      9.5     4.8     WSW     4.83    14.5    WSW     14.1    13.7    13.7    1002.7      0.6     2       0.178   0       16      59      8       15.3    10.95   1.1958  3       9       5       38      18.3    18.3    18.3        18.9    1288    4       100     60
2021-05-02      07:00 p. m.     13.2    14.1    13.1    82      10.2    1.6     NW      1.61    4.8     WNW     13.2    13.1    13.1    1003.9      0       0       0.215   0       15.8    60      8       15.1    11.14   1.1981  4       10      7       39      18.3    18.3    17.2        18.3    1288    4       100     60
2021-05-02      08:00 p. m.     12.9    13.7    12.9    75      8.6     0       W       0       4.8     SW      12.9    12.6    12.6    1004.6      0       0       0.227   0       14.5    61      7.1     13.8    11.25   1.2051  5       11      8       40      17.8    17.8    16.7        17.8    1309    4       100     60
```

Movemos el archivo al directorio **"C:/Users/elfer/Documents/Campo-Mixteca/campo2021-data/clima"**:

```bash
$mv clima-ordenado.txt ../Campo-Mixteca/campo2021-data/clima/
$cd ../Campo-Mixteca/campo2021-data/clima/
$ls 

Output:
clima-ordenado.txt

$less ~/MyDocuments/respaldos_tablas_Campo-Mixteca/clima-raw.txt |wc -l
15220

$less ~/MyDocuments/Campo-Mixteca/campo2021-data/clima/clima-ordenado.txt |wc -l
4361
```

