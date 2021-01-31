## extraindo coordenadas de GPS de todas as fotos dentro de uma pasta
 - criar arquivo `.bat`:\
  `chcp 65001`\
  `exiftool -charset filename=UTF8 -@ "C:\caminho\list.args" > out.txt`
  
 - criar arquivo `list.args` com os argumentos:

  `-charset`\
  `filename=UTF8`\
  `-filepath`\
  `-s3`\
  `-ext`\
  `jpg`\
  `-r`\
  `-gpslatitude`\
  `-gpslongitude`\
  `-n`\
  `-T`\
  `-r`\
  `C:\caminho\pasta\fotos\`

## inserindo coordenadas de GPS
- em um arquivo -> inserindo latitude e longitude em decimal, valores de 42°30'00''N, 42°30'00''E, escrevendo por cima do original\
`exiftool -overwrite_original -exif:gpslatitude=42.5 -exif:gpslongitude=42.5 -gpslatituderef=N -gpslongituderef=E "C:\caminho\para o\arquivo.jpg"`

- em vários arquivos de uma pasta:
  - para isso, deve criar um arquivo de argumentos (`gps.args`), como colocado acima
  - para automatizar, pode fazer no Excel os comandos e ir replicando usando a função CONCAT
  - pode-se colocar o caractere "%" nos lugares onde deve haver quebra de linha e substituir depois usando regex por `\n`
  - deve-se colocar `-execute` antes de `-charset` para separar os comandos
  - o formato final do `gps.args` deve ficar assim:\
   `-execute`\
   `-charset`\
   `filename=UTF8`\
   `-overwrite_original`\
   `-exif:gpslatitude=-33.5156`\
   `-exif:gpslongitude=-51.1727`\
   `-gpslatituderef=S`\
   `-gpslongituderef=W`\
   `C:\caminho\pasta\fotos\foto1.jpg`\
   `-execute`\
   `-charset`\
   `filename=UTF8`\
   `-overwrite_original`\
   `-exif:gpslatitude=-41.3781`\
   `-exif:gpslongitude=-46.671727`\
   `-gpslatituderef=S`\
   `-gpslongituderef=W`\
   `C:\caminho\pasta\fotos\foto2.jpg`\
   `.`\
   `.`\
   `.`
  - feito isso, basta rodar o exiftool no CMD no mesmo local onde tá o `gps.args`:\
  `exiftool -@ gps.args`

## inserindo data que foto foi tirada
 - no caso do dia 23 de outubro de 2005 às 20:06:34, não precisando estar completo
 `exiftool -xmp:dateTimeOriginal="2005:10:23 20:06:34.33-05:00" "C:\caminho\para o\arquivo.jpg"`
