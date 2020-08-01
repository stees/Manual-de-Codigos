## codificação UTF8
`chcp 65001`
 - extremamente útil para qualquer pessoa que não é dos EUA

## lista de arquivos na pasta
`dir /s /b *.mp4 >listmp4.txt`

## copia todos arquivos de extensão .xlsm do Desktop do "usuario" para a pasta do OneDrive
`robocopy "C:\Users\usuario\Desktop" "C:\Users\usuario\OneDrive" *.xlsm /z /it /is`
 - repete se falhar (/z)
 - copia se tiver mudado (/it)
 - copia se não tiver mudado (/is)
