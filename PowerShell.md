# texto
## inserção de separadores em posições específicas (depois do caractere 4, 10, 17, etc)
`$lines = Get-Content "teste.txt"`
`ForEach ($x in $lines) {`
`    $y = "$($x[0..4] -join '')|$($x[5..10] -join '')|$($x[11..17] -join '')|$($x[18..999] -join '')"`
`    $z = $y -join '|'`
`    Write-Output $z | Out-File -FilePath "resultado.txt" -Append }`