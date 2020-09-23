# geral
## buscar caractere literal
 - para procurar literalmente um ponto `.` sem que isso seja interpretado na sintaxe do regex, contrabarra antes -> `\.`

## repetições
 - adicionar `{x}` depois do que se quer ver repetir, x = número de repetições

## achar números e letras
 - números -> `(\d)`
 - letras minúsculas e maiúsculas -> `([a-z])` e `([A-Z])`
 - combinando letras minúsculas, maiúsculas e espaços -> `([a-zA-Z ]+)`
 - caracteres chineses/japoneses: Han -> `([\u3402-\uFA6D]+)`
 - caracteres japoneses: Hiragana -> `([\u3041-\u30A0\u30A0-\u31FF]+)`
 - caracteres japoneses: Katakana -> `([\u30A0-\u31FF]+)`
 - combinando todos caracteres japoneses -> `([\u3402-\uFA6D\u3041-\u30A0\u30A0-\u31FF]+)`
 
 - exemplo: achar sequências do tipo 3 letras e 4 números (e.g. ABC1234) -> `([a-z]){3}(\d){4}`
 
## substituir linhas repetidas ([fonte](https://www.regular-expressions.info/duplicatelines.html))
 - buscar por: `^(.*)(\r?\n\1)+$`
 - substituir por `$1`

