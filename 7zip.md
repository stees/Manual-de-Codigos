# geral
## configurando para poder rodar 7zip de qualquer pasta do computador, não só onde tem o 7z.exe
`set PATH=%PATH%;C:\Program Files\7-Zip\` \
`echo %PATH%`

# compressões
## txt -> gzip
`7z.exe a -tgzip votacao_secao_1998_AC.txt.gz votacao_secao_1998_AC.txt -sdel`
`for %i in (*.txt) do 7z.exe a -tgzip %~ni.txt.gz %i -sdel`
