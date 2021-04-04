## codificação UTF8
`chcp 65001`
 - extremamente útil para qualquer pessoa que não é dos EUA

## definir como variável um caminho específico
`set Caminho=C:\Users\users\Desktop`

## trocar para uma pasta
`cd "C:\caminho\da\pasta"`

## lista de arquivos na pasta
`dir /s /b *.mp4 >listmp4.txt`

## copia todos arquivos de extensão .xlsm do Desktop do "usuario" para a pasta do OneDrive
`robocopy "C:\Users\usuario\Desktop" "C:\Users\usuario\pasta" *.xlsm /z /it /is`
 - repete se falhar (/z)
 - copia se tiver mudado (/it)
 - copia se não tiver mudado (/is)
 
 ## definir a última pasta na ordem alfabética na variável "lastdir"
`for /F "tokens=*" %%a in ('dir /ad/b/od "C:\Users\caminho\pasta"') do set lastdir=%%a`

## gerar uma lista dos vídeos de canal/canais ou playlist/playlists no YouTube (`URL_CANAL1` e `URL_CANAL2`)
 - para funcionar, no caso de canais, tem que ser o link da lista de videos, tipo: `https://www.youtube.com/user/usuario/videos`
 - o separador que usei foi o `--` pois `|` e `/` parecia dar problema

### puxando nome dos vídeos, ID, datas de upload e durações
`youtube-dl -i -o "%(title)s -- %(id)s -- %(upload_date)s -- %(duration)s" --get-filename --skip-download URL_CANAL1 URL_CANAL2 > "%Caminho%\log.txt"

### convertendo arquivo resultante para UTF8
``powershell -command "Get-Content %Caminho%\log.txt" > "%Caminho%\log-utf8.txt"`
