- [como começar](#como-começar)
  - [baixando o ffmpeg](#baixando-o-ffmpeg)
  - [rodando o ffmpeg](#rodando-o-ffmpeg)
- [geral](#geral)
  - [roda o código depois para todos os arquivos de tipo mp4 na pasta](#roda-o-código-depois-para-todos-os-arquivos-de-tipo-mp4-na-pasta)
  - [juntar arquivos diferentes num mesmo video (direto)](#juntar-arquivos-diferentes-num-mesmo-video-direto)
  - [juntar arquivos diferentes num mesmo video (usando arquivo separado)](#juntar-arquivos-diferentes-num-mesmo-video-usando-arquivo-separado)
  - [aplicando dois comandos no mesmo filtro](#aplicando-dois-comandos-no-mesmo-filtro)
  - [picotando arquivo](#picotando-arquivo)
  - [escrever saídas no prompt de comando para um arquivo de texto](#escrever-saídas-no-prompt-de-comando-para-um-arquivo-de-texto)
- [videos](#videos)
  - [diminuir tamanho sem diminuir qualidade](#diminuir-tamanho-sem-diminuir-qualidade)
  - [mudar resolução mantendo aspect ratio](#mudar-resolução-mantendo-aspect-ratio)
  - [converte mkv pra mp4](#converte-mkv-pra-mp4)
  - [extrai todos os frames (-r = ffps, -t duração, -ss início, nome frame_1-1_0001, 0002, etc)](#extrai-todos-os-frames--r--ffps--t-duração--ss-início-nome-frame_1-1_0001-0002-etc)
  - [gira 90 graus anti-horário e mantém os outros metadados](#gira-90-graus-anti-horário-e-mantém-os-outros-metadados)
  - [corta 100 do width (largura) do video](#corta-100-do-width-largura-do-video)
  - [inserir image.png entre 0 e 20 segundos, 25 pixels para baixo e para a direita do canto superior esquerdo](#inserir-imagepng-entre-0-e-20-segundos-25-pixels-para-baixo-e-para-a-direita-do-canto-superior-esquerdo)
- [áudios](#áudios)
  - [transformar em mp3 sem video (vn) e mesmo codec de audio (acodec copy)](#transformar-em-mp3-sem-video-vn-e-mesmo-codec-de-audio-acodec-copy)
  - [baixar áudio direto do YouTube](#baixar-áudio-direto-do-youtube)
  - [convertendo pra mp3](#convertendo-pra-mp3)
  - [aumentando velocidade de audio pra 1,2x](#aumentando-velocidade-de-audio-pra-12x)
  - [removendo silêncios do começo ao fim](#removendo-silêncios-do-começo-ao-fim)
  - [complexos](#complexos)
- [videos + áudios](#videos--áudios)
  - [juntando um audio a um video](#juntando-um-audio-a-um-video)
  - [aumentando velocidade de video e audio pra 1,2x + diminuir tamanho sem diminuir qualidade](#aumentando-velocidade-de-video-e-audio-pra-12x--diminuir-tamanho-sem-diminuir-qualidade)

# como começar
## baixando o ffmpeg
 - baixe [este arquivo](https://www.gyan.dev/ffmpeg/builds/ffmpeg-release-full.7z) compactado e descompacte em algum lugar fixo (por exemplo, no `C:\Arquivos de programas`)
 - o executável do ffmpeg estará na pasta `bin`, só que do jeito que tá, ele só vai conseguir rodar se os arquivos que quiser processar estiverem na mesma pasta `bin`
 - pra não precisar disso -> Iniciar > Configurações (logo acima de Desligar) > Editar variáveis de ambiente > Variáveis de ambiente (canto inferior direito)
 - na janela que abrir, no painel inferior "Variáveis de sistema", role até a variável "Path", clique nela e clique em "editar"
 - na janela "editar variável de ambiente", clique em "novo" e coloque o caminho pra onde ficou a pasta `bin` do ffmpeg, por exemplo: `C:\Arquivos de programas\ffmpeg\bin`

## rodando o ffmpeg
 - depois de editar as variáveis de sistema, você pode rodar o ffmpeg em qualquer pasta
 - para fazer isso, abra a pasta onde estão os vídeos que quer editar, e basta digitar "cmd" na barra de endereços de pasta e dar enter, que aí o prompt de comando vai rodar direto naquela pasta
 - rode o código desejado, como os vários abaixo
 - ATENÇÃO: aqueles que têm dois sinais de porcentagem (`%%`) devem ser trocados por apenas um (`%`) no caso de rodar direto pelo prompt

# geral
## roda o código depois para todos os arquivos de tipo mp4 na pasta
`for %%i in (*.mp4 *.mkv) do ffmpeg -i "%%i" -vn -c:a libmp3lame -write_xing 0 "%%~ni.mp3"` (%%, duplo por ser arquivo .bat)

## juntar arquivos diferentes num mesmo video (direto)
`ffmpeg -i opening.mkv -i episode.mkv -i ending.mkv -filter_complex "[0:v] [0:a] [1:v] [1:a] [2:v] [2:a] concat=n=3:v=1:a=1 [v] [a]" -map "[v]" -map "[a]" output.mkv`

## juntar arquivos diferentes num mesmo video (usando arquivo separado)
`ffmpeg -f concat -safe 0 -i lista.txt -c:a copy output.mp4`

formato do arquivo `lista.txt`:\
`file 'file:C:/caminho/para/o/arquivo/video.mp4'`\
`file 'file:C:/caminho/para/o/arquivo/video2.mp4'`\
`file 'file:C:/caminho/para/o/arquivo/video3.mp4'`

## aplicando dois comandos no mesmo filtro
`ffmpeg -i "input.mp4" -filter:v "scale=-1:480, fps=fps=30" "output.mp4"`

## picotando arquivo
### extraindo um trecho -> começando em 1 min, terminando em 2 min (-ss = onde começa, -t = onde termina)
`ffmpeg -t 00:02:00 -i "input.mp4" -ss 00:01:00 "output.mp4"`

### extraindo vários trechos -> entre 4-7, 17-26 e 74-91 segundos
`ffmpeg -i video.mp4 -vf "select='between(t,4,7)+between(t,17,26)+between(t,74,91)', setpts=N/FRAME_RATE/TB" -af "aselect='between(t,4,7)+between(t,17,26)+between(t,74,91)',asetpts=N/SR/TB" out.mp4`


## escrever saídas no prompt de comando para um arquivo de texto
`ffmpeg CÓDIGO > output.txt 2>&1`

# videos
## diminuir tamanho sem diminuir qualidade
 - O ideal é manter CRF entre 18 e 30, acima de 30 fica muito ruim, abaixo de 18 o arquivo fica muito grande\
    `ffmpeg -i "input nome pode ter espaços.mp4" -crf 25 "output.mp4"`

## mudar resolução mantendo aspect ratio
`ffmpeg -i input.mp4 -vf "scale=iw/2:ih/2" output_half.mp4`

`ffmpeg -i input.mp4 -vf "scale=iw/3:ih/3" output_third.mp4`

## converte mkv pra mp4
`ffmpeg -i input.mkv -vcodec copy -acodec copy output.mp4`

## extrai todos os frames (-r = ffps, -t duração, -ss início, nome frame_1-1_0001, 0002, etc)
`ffmpeg -i arquivo.mkv -r 8 -t 1000 -ss 0:00 -f image2 ./frames/frame_1-1_%4d.png`

## gira 90 graus anti-horário e mantém os outros metadados
`ffmpeg -i "input.m4v" -map_metadata 0 -metadata:s:v rotate="90" -codec copy "output.m4v"`

## corta 100 do width (largura) do video
`ffmpeg -i "in.mp4" -filter:v "crop=in_w-100:in_h" -c:a copy "out.mp4"`

## inserir image.png entre 0 e 20 segundos, 25 pixels para baixo e para a direita do canto superior esquerdo
`ffmpeg -i input.mp4 -i image.png \` \
`-filter_complex "[0:v][1:v] overlay=25:25:enable='between(t,0,20)'" \` \
`-pix_fmt yuv420p -c:a copy \` \
`output.mp4`

# áudios
## transformar em mp3 sem video (vn) e mesmo codec de audio (acodec copy)
`ffmpeg -i input.mp4 -vn -c:a libmp3lame -write_xing 0 output.mp3`

`ffmpeg -i input.mp4 -vn -acodec copy output.aac`

## baixar áudio direto do YouTube
`youtube-dl URL -x --audio-format "mp3"`

## convertendo pra mp3
### ogg -> mp3
`ffmpeg -i input.ogg -acodec libmp3lame output.mp3`

### FLAC -> mp3
`ffmpeg -i input.flac -ab 320k -map_metadata 0 -id3v2_version 3 output.mp3`

## aumentando velocidade de audio pra 1,2x
`ffmpeg -i input.mp3 -af "atempo=1.2" output.mp3`

## removendo silêncios do começo ao fim
`ffmpeg -i "INPUT.ogg" -af silenceremove=stop_periods=-1:stop_duration=1:stop_threshold=-90dB "OUTPUT.ogg"`

## complexos
### (velocidade 2.1) + (ogg -> mp3) + (deleta original)
`for %%i in (*.ogg) do ffmpeg -i "%%i" -filter:a "atempo=2.1" -acodec libmp3lame "%%~ni.mp3" && del "%%i"`

# videos + áudios
## juntando um audio a um video
`ffmpeg -i video.mp4 -i audio.wav -c:v copy -c:a aac -map 0:v:0 -map 1:a:0 output.mp4`

`ffmpeg -i tutorial-ffmpeg.mp4 -i tutorial-ffmpeg-audio.mp3 -c:v copy -c:a aac -map 0:v:0 -map 1:a:0 output.mp4`

## aumentando velocidade de video e audio pra 1,2x + diminuir tamanho sem diminuir qualidade
`ffmpeg -i input.mp4 -filter_complex "[0:v]setpts=0.83333*PTS[v];[0:a]atempo=1.2[a]" -map "[v]" -crf 28 -map "[a]" FINAL2.MP4`

`ffmpeg -i input.mp4 -filter_complex "[0:v]setpts=0.83333*PTS[rapido];[0:a]atempo=1.2[a];[rapido]scale=iw/3:ih/3[final]" -map "[final]" -crf 28 -map "[a]" FINAL2.MP4`
