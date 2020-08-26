## codificação UTF8
`chcp 65001`
 - extremamente útil para qualquer pessoa que não é dos EUA

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
