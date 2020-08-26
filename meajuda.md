# Não sei nada disso! Como começo?

Este aqui é um guia rápido para usar linguagens de programação para funções básicas, como as documentadas aqui.

## Pra quê mexer com isso?
Programar nada mais é do que deixar instruções pra máquina fazer coisas pra você. Isso é especialmente útil quando você tem alguma **tarefa repetitiva ou muito extensa**.
\
\
Os programas documentados aqui são, em boa parte, usados através do "prompt de comando" do Windows, que nada mais é do que um local em que você pode ter contato mais próximo com a máquina para fazer operações e fornecer instruções para ela executar diretamente.

### Exemplo de utilidade 1 - prompt de comando
Dos programinhas documentados aqui, o prompt de comando é o que mais aparece, já que vários são usados através dele, exceto o PowerShell e o regex. O prompt de comando, além de permitir usar outros programas, tem funções próprias como, por exemplo, copiar certos tipos de arquivos ou produzir listas de arquivos de uma pasta, etc - isso inclusive permite criar rotinas prontas pro computador executar!

### Exemplo de utilidade 2 - ffmpeg
O ffmpeg permite fazer edições simples de videos como cortar pedaços, deixar o áudio e o video mais rápidos ou mais lentos, adicionar um áudio em um arquivo de vídeo.

### Exemplo de utilidade 3 - regex
Já o regex pode ajudar a extrair informações padronizadas de textos grandes, como, por exemplo, extrair uma lista de endereços de um site sem precisar copiar um a um.

## Como começar
### Prompt de comando
Para começar a usar o prompt de comando, basta buscar por ele ("prompt de comando" ou busque por "cmd") na barra de iniciar.
\
Ao clicar, deve abrir uma janelinha preta mostrando o caminho de uma pasta. Você pode fazer algumas das tarefas que aparecem na parte do CMD deste manual.

### Programas usados através do prompt de comando
Para usar os programas que operam através do CMD, como o ffmpeg, o exiftool, etc, há dois jeitos: 1) rodar o CMD na pasta onde tem o exe do arquivo de cada programinha ou 2) configurar o sistema para entender que toda vez que digitar "ffmpeg" no prompt, é para ele executar o arquivo do ffmpeg, por exemplo.

### Linguagens usadas em outros ambientes
O Powershell tem sua interface própria - basta procurar por Powershell na barra do iniciar -, que também permite que se use comandos do CMD.
\
\
O regex pode ser usado em vários contextos; eu particularmente uso ele no VS Code, [um programa gratuito de edição de texto](https://code.visualstudio.com/download) que facilita muito na hora de programar qualquer coisa.

## Criando rotinas prontas
Para criar rotinas prontas para rodar no prompt de comando, deve-se usar um arquivo de extensão `.bat`, que pode ser criado no VS Code.
\
Este tipo de arquivo tem algumas particularidades:
1) deve começar com `@ ECHO OFF`;
2) toda vez que aparecer um `%` no código, ele precisa estar duplicado no arquivo `.bat`;
3) no final deve-se inserir `PAUSE` (para a janela ficar aberta depois do comando ser executado) ou `exit` (para a janela do prompt fechar depois do comando ser executado).

