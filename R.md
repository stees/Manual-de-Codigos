- [fontes](#fontes)
- [geral](#geral)

# fontes
 - [W3Schools](https://www.w3schools.com/r/)
 - [Tutorials Point](https://www.tutorialspoint.com/r/)

# geral
## variável:
 - atribuindo globalmente: 
   - `var <- "text"` ou `var <- 5`

 - tipo - checar:
   - `class( var )`, e para declarar inteiro, `var = 10L` ou `var = 1000L`

 - tipo - converter:
   - `var2 <- as.numeric( var1 )`

## texto (string):
 - concatenar:
   - `paste( string1 , string2 , sep=" " , collapse=NULL )`
   - sep = entre termos, collapse = entre resultados

 - extrair pedaços:
   - `substr( var , start = 1 , stop = 2 )`

 - preservar quebra de linha na atribuição da variável:
   - `cat( var )`

 - inserir caractere ilegal (e.g. aspas):
   - `str <- "Don't try \"this\" at home" `

 - len:
   - `nchar( str )`

 - achar sequência "Hello"
   - `grepl( "Hello" , str )`

## operações (numeric):
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
   - valor dentro de sequência? (vale para todo tipo)
       - `x %in% y`
   - multiplicação de matrizes
       - `matrix1 %*% matrix2`

## funções
 - criando
    ```
    myfunction <- function( var1, x ){

        paste( var1 , "test" )
        return( 5 * x )

    }
    ```

 - atribuindo variável localmente
   - ` var = "test" `

 - atribuindo variável global dentro de função
   - ` var <<- "test" `

## estruturas de dados - vetores/listas/matrizes:
 - criando vetores e listas
   - `numbers <- c(1, 2, 3)` ou ` numbers <- 1:3`, se usar com decimais, ele pula de 1 em 1
   - `numbers <- seq( from = 0, to = 100, by = 20 ) `, para pular diferente
   - `rep( numbers , each = 3 )`, repete cada elemento 3x
   - `rep( numbers , times = 3 )`, repete a sequência 3x
   - `rep( numbers , times = c(5,2,1) )`, repete cada um algum número de vezes
   - `Sys.glob(  file.path("./pasta1/pasta2/", "*.txt.gz")  )`, lista de arquivos

 - comprimento
   - `length(numbers)`

 - classificar
   - `sort(numbers)`

 - criando matrizes
   - `matrix( c(1,2,3,4,5,6) , nrow = 3, ncol = 2)`, 123 viram a primeira coluna, 456 a segunda
   - `cbind( thismatrix , c("strawberry", "blueberry", "raspberry") )`, adicionando coluna, para linha é `rbind`, serve para adicionar matrizes inteiras também
   - `thismatrix[ -c(1) , -c(1) ]`, remove primeira linha e primeira coluna

 - endereços
   - `numbers[ 1 ]` vetor - primeiro item
   - `thismatrix[ 1 , 2 ]` matriz - primeira linha, segunda coluna
   - `thismatrix[ 1 , ]` matriz - primeira linha
   - `numbers[ c(1,3) ]` vetor - primeiro e terceiro itens
   - `numbers[ c(-1) ]` vetor - todos menos último item
   - `thismatrix[ c(1,2) , ]` matriz - primeira e segunda linhas

 - loop por matriz
     ```
      for (rows in 1:nrow(thismatrix)) {
        for (columns in 1:ncol(thismatrix)) {
          print(thismatrix[rows, columns])
        }
      }
     ```

## estruturas de dados - arrays:
 - criando
   - `thisarray <- c(1:24)` array de 1 dimensão, valores 1 até 24
   - `multiarray <- array( thisarray, c(4,3,2) )` array de 2 dimensões, pegando valores do de cima e gerando matrizes de 4 linhas e 3 colunas

 - acessando
   - `dim(multiarray)` linhas, colunas e dimensões

## estruturas de dados - data frame:
 - criando dataframe vazio só com colunas e tipos
   - `Fruit_Market <- data.frame( fruit=character(0) , cost=numeric(0) , quantity=integer(0) )`

 - lendo
   - `read.csv( "./arquivo.txt" , header = TRUE )`, lê CSV normal
   - `read.csv2( "./arquivo.txt" , header = TRUE )`, para o caso de CSV com separador decimal `,` e separador de colunas `;` (Brasil)
   - `fread("data.csv.gz")`, lê CSV comprimido em GZ usando `library(data.table)` e pacote R.utils

 - adicionando coluna (`library(dplyr)`) usando alguma fórmula
   - `df %>% mutate( fórmula )`

 - juntando dois DataFrames
   - `New_Data_Frame <- rbind(Data_Frame1, Data_Frame2)`, verticalmente
   - `New_Data_Frame <- cbind(Data_Frame1, Data_Frame2)`, horizontalmente

 - funções úteis
   - `DATAHORA = as.POSIXct( DATAHORA , format="%m-%d-%Y %H:%M:%S" , tz="GMT" )`, transforma em `datetime` o texto da coluna DATAHORA, que tá em formato `mm-dd-yyyy hh:mm:ss`