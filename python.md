# pandas
## geral
### ler CSV (comprimido gzip)
 - arquivo `file`, separador `;` e decimal `,`, usando colunas da lista `colunas`
    ```
    df = pd.read_csv( file,\
                      sep=';',\
                      error_bad_lines=False,encoding='latin1',compression='gzip',warn_bad_lines=True,keep_default_na=False,\
                      usecols=colunas,decimal=','
                    )
    ```

### renomeando colunas de dataframe já existente
    df.rename( columns={\
                        "AREA CONSTRUIDA_x": "área apto",\
                        "AREA CONSTRUIDA_y": "área garagem"\
                       },\
                
                inplace=True 
             )

## processando colunas
### n primeiros caracteres
    df['coluna nova'] = df['coluna tal'].str[0:6]

### checar se contém sequência de caracteres
 - sem regex
    ```
    critério1 = df['coluna tal'].str.contains("apartamento em condomínio",case=False)
    temp['coluna nova'] = temp['coluna tal'].str[0:6]
    ```

 - com regex
    ```
    critério2 = df['coluna tal'].str.contains("garagem.*residencial",case=False,regex=True)
    ```

### extraindo linhas conforme os critérios
    df_filtrado = df[ (critério1 | critério2) & critério3 ].copy()

### criando colunas segundo critérios
    df['coluna nova'] = np.where( \
                                    (df['ano'] > 2006) & (df['ano'] < 2014), \
                                    '2007-2013', \
                                    '2014-2020'\
                                )

### criando colunas usando VLOOKUP, sem jogar fora quando não encontra
    df1.merge(df_busca, how='left', on='ID')

### aplicando função em uma coluna para criar uma nova
    df['coluna nova'] = df['coluna'].map( function , na_action='ignore' )

## gerando relatórios
### agrupando por certas colunas
    ```
    colunas_agregar = [ "província" ]

    agrega = {"área construída":'mean'}

    dftemp1 = df.groupby( colunas_agregar ).agg( agrega ).reset_index()
    ```



    ```

    ```            