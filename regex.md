# geral
## buscar caractere literal
 - para procurar literalmente um ponto `.` sem que isso seja interpretado na sintaxe do regex, contrabarra antes -> `\.`

## repetições
 - adicionar `{x}` depois do que se quer ver repetir, x = número de repetições

## achar números e letras
 - números -> `(\d)`
 - letras -> `([a-z])`
 
 - exemplo: achar sequências do tipo 3 letras e 4 números (e.g. ABC1234) -> `([a-z]){3}(\d){4}`
