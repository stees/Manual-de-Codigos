# geral
 - variável:
   - atribuindo globalmente: 
     - `var <- "text"` ou `var <- 5`
   - tipo - checar:
     - `class( var )`, e para declarar inteiro, `var = 10L` ou `var = 1000L`
   - tipo - converter:
     - `var2 <- as.numeric( var1 )`

 - texto (string):
   - concatenar:
     - `paste( string1 , string2 , sep=" " , collapse=NULL )`
     - sep = entre termos, collapse = entre resultados
   - preservar quebra de linha na atribuição da variável:
     - `cat( var )`
   - inserir caractere ilegal (e.g. aspas):
     - `str <- "Don't try \"this\" at home" `
   - len:
     - `nchar( str )`
   - achar sequência "Hello"
     - `grepl( "Hello" , str )`

 - operações (numeric):
   - divisão - resto:
     - `x %% y`
   - divisão - quociente:
     - `x %/% y`
   - lógica
     - `&` / `|` = e / ou elemento a elemento
     - `&&` / `||` = e / ou geral
     - `!` = não
   - operadores
     - sequência de números
       - `x <- 1:10`
     - valor dentro de sequência?
       - `x %in% y`
     - multiplicação de matrizes
       - `matrix1 %*% matrix2`

 - funções
   - criando:
       ```
       myfunction <- function( var1, x ){

           paste( var1 , "test" )
           return( 5 * x )

       }
       ```
   - atribuindo variável localmente: 
     - ` var = "test" `
   - atribuindo variável global dentro de função:
     - ` var <<- "test" `

 - estruturas de dados - vetores e listas:
   - criando
     - `numbers <- c(1, 2, 3)` ou ` numbers <- 1:3`, se usar com decimais, ele pula de 1 em 1
     - `numbers <- seq( from = 0, to = 100, by = 20 ) `, para pular diferente
     - `rep( numbers , each = 3 )`, repete cada elemento 3x
     - `rep( numbers , times = 3 )`, repete a sequência 3x
     - `rep( numbers , times = c(5,2,1) )`, repete cada um algum número de vezes
   - comprimento
     - `length(numbers)`
   - classificar
     - `sort(numbers)`
   - acessando
     - `numbers[1]` primeiro item
     - `numbers[c(1,3)]` primeiro e terceiro itens
     - `numbers[c(-1)]` todos menos último item