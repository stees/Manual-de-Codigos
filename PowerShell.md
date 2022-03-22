# geral
## rodando scripts do PowerShell
` & "C:\caminho\para\pasta\script.ps1"`

## rodando comandos do CMD
`cmd /c --% COMANDO` (--% é para PowerShell não tentar processar o que vem depois como sua própria sintaxe)

## download
`Invoke-WebRequest "LINK" -OutFile OUTPUT.zip` (LINK baixado e exportado no arquivo OUTPUT.zip)

# texto
## justapor arquivos de texto
`cat example*.txt | sc allexamples.txt`

## inserção de separadores em posições específicas (depois do caractere 4, 10, 17, etc)
`$lines = Get-Content "teste.txt"`
`ForEach ($x in $lines) {`
`    $y = "$($x[0..4] -join '')|$($x[5..10] -join '')|$($x[11..17] -join '')|$($x[18..999] -join '')"`
`    $z = $y -join '|'`
`    Write-Output $z | Out-File -FilePath "resultado.txt" -Append }`
