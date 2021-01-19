## extraindo coordenadas de GPS de todas as fotos dentro de uma pasta
 - criar arquivo `.bat`:\
  `chcp 65001`\
  `exiftool -charset filename=UTF8 -@ "C:\caminho\list.txt" > out.txt`
  
 - criar arquivo `list.txt` com os argumentos:\
  `-charset`\
  `filename=UTF8`\
  `-filename`\
  `-gpslatitude`\
  `-gpslongitude`\
  `-n`\
  `-T`\
  `-r`\
  `C:\caminho\pasta\fotos\`

## inserindo coordenadas de GPS em todas as fotos de uma pasta
- inserindo latitude e longitude em decimal, valores de 42.5,42.5 (= 42°30'00''N, 42°30'00''E)\
`exiftool -exif:gpslatitude=42.5 -exif:gpslongitude=42.5 "C:\caminho\para o\arquivo.jpg"`
