- [fontes](#fontes)
- [geral](#geral)
  - [variável](#variável)
  - [texto (string)](#texto-string)
  - [operações (numeric)](#operações-numeric)
  - [funções](#funções)
  - [estruturas de dados - vetores/listas/matrizes](#estruturas-de-dados---vetoreslistasmatrizes)
  - [estruturas de dados - arrays](#estruturas-de-dados---arrays)
  - [estruturas de dados - data frame](#estruturas-de-dados---data-frame)

# fontes
 - [W3Schools](https://www.w3schools.com/r/)
 - [Tutorials Point](https://www.tutorialspoint.com/r/)

# geral
## variável
### atribuindo globalmente
 - `var <- "text"` ou `var <- 5`

### tipo - checar
 - `class( var )`, e para declarar inteiro, `var = 10L` ou `var = 1000L`

### tipo - converter
 - `var2 <- as.numeric( var1 )`

## texto (string)
### concatenar
 - `paste( string1 , string2 , sep=" " , collapse=NULL )`
 - sep = entre termos, collapse = entre resultados

### extrair pedaços
 - `substr( var , start = 1 , stop = 2 )`

### preservar quebra de linha na atribuição da variável
 - `cat( var )`

### inserir caractere ilegal (e.g. aspas)
 - `str <- "Don't try \"this\" at home" `

### len
 - `nchar( str )`

### achar sequência "Hello"
 - `grepl( "Hello" , str )`

## operações (numeric)
### divisão - resto
 - `x %% y`

### divisão - quociente
 - `x %/% y`

### lógica
 - `&` / `|` = e / ou elemento a elemento
 - `&&` / `||` = e / ou geral
 - `!` = não

### operadores
 - sequência de números
       - `x <- 1:10`
 - valor dentro de sequência? (vale para todo tipo)
       - `x %in% y`
 - multiplicação de matrizes
       - `matrix1 %*% matrix2`

## funções
### criando

    myfunction <- function( var1, x ){

        paste( var1 , "test" )
        return( 5 * x )

    }


### atribuindo variável localmente
 - ` var = "test" `

### atribuindo variável global dentro de função
 - ` var <<- "test" `

## estruturas de dados - vetores/listas/matrizes
### criando vetores e listas
 - `numbers <- c(1, 2, 3)` ou ` numbers <- 1:3`, se usar com decimais, ele pula de 1 em 1
 - `numbers <- seq( from = 0, to = 100, by = 20 ) `, para pular diferente
 - `rep( numbers , each = 3 )`, repete cada elemento 3x
 - `rep( numbers , times = 3 )`, repete a sequência 3x
 - `rep( numbers , times = c(5,2,1) )`, repete cada um algum número de vezes
 - `Sys.glob(  file.path("./pasta1/pasta2/", "*.txt.gz")  )`, lista de arquivos

### comprimento
 - `length(numbers)`

### classificar
 - `sort(numbers)`

### criando matrizes
 - `matrix( c(1,2,3,4,5,6) , nrow = 3, ncol = 2)`, 123 viram a primeira coluna, 456 a segunda
 - `cbind( thismatrix , c("strawberry", "blueberry", "raspberry") )`, adicionando coluna, para linha é `rbind`, serve para adicionar matrizes inteiras também
 - `thismatrix[ -c(1) , -c(1) ]`, remove primeira linha e primeira coluna

### endereços
 - `numbers[ 1 ]` vetor - primeiro item
 - `thismatrix[ 1 , 2 ]` matriz - primeira linha, segunda coluna
 - `thismatrix[ 1 , ]` matriz - primeira linha
 - `numbers[ c(1,3) ]` vetor - primeiro e terceiro itens
 - `numbers[ c(-1) ]` vetor - todos menos último item
 - `thismatrix[ c(1,2) , ]` matriz - primeira e segunda linhas

### loop por matriz
      for (rows in 1:nrow(thismatrix)) {
        for (columns in 1:ncol(thismatrix)) {
          print(thismatrix[rows, columns])
        }
      }

## estruturas de dados - arrays
### criando
 - `thisarray <- c(1:24)` array de 1 dimensão, valores 1 até 24
 - `multiarray <- array( thisarray, c(4,3,2) )` array de 2 dimensões, pegando valores do de cima e gerando matrizes de 4 linhas e 3 colunas

### acessando
 - `dim(multiarray)` linhas, colunas e dimensões

## estruturas de dados - data frame
### atribuindo nomes de colunas para dataframe já existente
 - `colnames( df ) <- c( "col1","col2","col3" )`

### lendo
 - `read.csv( "./arquivo.txt" , header = TRUE )`, lê CSV normal
 - `read.csv2( "./arquivo.txt" , header = TRUE )`, para o caso de CSV com separador decimal `,` e separador de colunas `;` (Brasil)
 - `fread("data.csv.gz")`, lê CSV comprimido em GZ usando `library(data.table)` e pacote R.utils

### coluna
 - `df$coluna <- fórmula `, adicionando coluna usando alguma fórmula

 - adicionando coluna com várias condições
    ```
    df$HORARIO <- case_when(
                            ( hour(df$DATAHORA) %/% 6 ) == 0 ~ "0 - Madrugada",
                            ( hour(df$DATAHORA) %/% 6 ) == 1 ~ "1 - Manhã",
                            ( hour(df$DATAHORA) %/% 6 ) == 2 ~ "2 - Tarde",
                            ( hour(df$DATAHORA) %/% 6 ) == 3 ~ "3 - Noite",
                          )
    ```

 - `df$coluna1`, chamando coluna1 do dataframe `df`
 - `mean(df$coluna1)`, valor médio de coluna1
 - `max(df$coluna1)`, valor máximo de coluna1
 - `which.max(df$coluna1)`, qual linha contém o valor máximo de coluna1
 - `rownames(df)[which.max(df$coluna1)]`, nome da linha que contém o valor máximo de coluna1


### juntando dois DataFrames
 - `New_Data_Frame <- rbind(Data_Frame1, Data_Frame2)`, verticalmente
 - `New_Data_Frame <- cbind(Data_Frame1, Data_Frame2)`, horizontalmente

### funções úteis
 - `df$DATAHORA <- as.POSIXct( df$DATAHORA , format="%m-%d-%Y %H:%M:%S" , tz="GMT" )`, transforma em `datetime` o texto da coluna `DATAHORA` do dataframe `df`, que tá em formato `mm-dd-yyyy hh:mm:ss`

 - tabela dinâmica de `df`, nas linhas coluna1, nos valores a média da coluna2 removendo os NA indo para coluna "media", [fonte](https://rstudio-conf-2020.github.io/r-for-excel/pivot-tables.html#group_by-summarize)
      ```
      df %>%
        group_by( coluna1 ) %>%
        summarize( media = mean( coluna2 , na.rm = TRUE) )
      ```

### Espacializando uma tabela 
 - Pegando só latlong
    ```
    xy <- df[,c(4,5)]
    ```

 - Tirando NA
    ```
    xy$is_na = ifelse(is.na(xy$LONGITUDE), TRUE, FALSE)
    index = xy$is_na == TRUE
    xy[index, "LONGITUDE"] <- 0
    xy[index, "LATITUDE"] <- 0

    ```

 - Spatial Points Data Frame
    ```
    spdf <- SpatialPointsDataFrame( coords = xy , data = df , proj4string = CRS("+proj=longlat +datum=WGS84 +ellps=WGS84 +towgs84=0,0,0") )
    ```

### Mostrando pontos
    ggplot(as.data.frame(df),aes(x=LONGITUDE,y=LATITUDE))+
    geom_point(col="red")+
    coord_equal()