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
