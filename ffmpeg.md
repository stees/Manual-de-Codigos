# geral
## lista de arquivos na pasta
`dir /s /b *.mp4 >listmp4.txt`

## roda o código depois de ffmpeg para todos os arquivos de tipo mp4 na pasta (%%i em arquivo .bat)
`for %%i in (*.mp4) do ffmpeg -i "%%i" -vn -c:a libmp3lame -write_xing 0 "%~ni.mp3"`

## juntar arquivos diferentes num mesmo video
`ffmpeg -i opening.mkv -i episode.mkv -i ending.mkv -filter_complex "[0:v] [0:a] [1:v] [1:a] [2:v] [2:a] concat=n=3:v=1:a=1 [v] [a]" -map "[v]" -map "[a]" output.mkv`

## extrai do arquivo os trechos entre 4-7, 17-26 e 74-91 segundos
`ffmpeg -i video.mp4 -vf "select='between(t,4,7)+between(t,17,26)+between(t,74,91)', setpts=N/FRAME_RATE/TB" -af "aselect='between(t,4,7)+between(t,17,26)+between(t,74,91)',asetpts=N/SR/TB" out.mp4`

## picota o arquivo em várias partes (-ss diz onde começa, -t diz DURAÇÃO, não tempo final)
`ffmpeg -i source-file.foo -ss 0 -t 600 first-10-min.m4v`
`ffmpeg -i source-file.foo -ss 600 -t 600 second-10-min.m4v`
`ffmpeg -i source-file.foo -ss 1200 -t 600 third-10-min.m4v`

# videos
## diminuir tamanho sem diminuir qualidade
`ffmpeg -i input.mp4 -crf 28 output.mp4`

## mudar resolução mantendo aspect ratio
`ffmpeg -i input.mp4 -vf "scale=iw/2:ih/2" output_half.mp4`

`ffmpeg -i input.mp4 -vf "scale=iw/3:ih/3" output_third.mp4`

## converte mkv pra mp4
`ffmpeg -i input.mkv -vcodec copy -acodec copy output.mp4`

## extrai todos os frames (-r = ffps, -t duração, -ss início, nome frame_1-1_0001, 0002, etc)
`ffmpeg -i arquivo.mkv -r 8 -t 1000 -ss 0:00 -f image2 ./frames/frame_1-1_%4d.png`

# áudios
## transformar em mp3 sem video (vn) e mesmo codec de audio (acodec copy)
`ffmpeg -i input.mp4 -vn -c:a libmp3lame -write_xing 0 output.mp3`

`ffmpeg -i input.mp4 -vn -acodec copy output.aac`

## convertendo pra mp3
### ogg -> mp3
`ffmpeg -i input.ogg -acodec libmp3lame output.mp3`

### FLAC -> mp3
`ffmpeg -i input.flac -ab 320k -map_metadata 0 -id3v2_version 3 output.mp3`

## aumentando velocidade de audio pra 1,2x
`ffmpeg -i input.mp3 -af "atempo=1.2" output.mp3`

## removendo silêncios do começo ao fim
`ffmpeg -i "INPUT.ogg" -af silenceremove=stop_periods=-1:stop_duration=1:stop_threshold=-90dB "OUTPUT.ogg"`

# videos + áudios
## juntando um audio a um video
`ffmpeg -i video.mp4 -i audio.wav -c:v copy -c:a aac -map 0:v:0 -map 1:a:0 output.mp4`

`ffmpeg -i tutorial-ffmpeg.mp4 -i tutorial-ffmpeg-audio.mp3 -c:v copy -c:a aac -map 0:v:0 -map 1:a:0 output.mp4`

## aumentando velocidade de video e audio pra 1,2x + diminuir tamanho sem diminuir qualidade
`ffmpeg -i input.mp4 -filter_complex "[0:v]setpts=0.83333*PTS[v];[0:a]atempo=1.2[a]" -map "[v]" -crf 28 -map "[a]" FINAL2.MP4`

`ffmpeg -i input.mp4 -filter_complex "[0:v]setpts=0.83333*PTS[rapido];[0:a]atempo=1.2[a];[rapido]scale=iw/3:ih/3[final]" -map "[final]" -crf 28 -map "[a]" FINAL2.MP4`