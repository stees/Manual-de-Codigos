# Youtube-dl

## MP3
- Baixando um álbum do YouTube no formato e numeração corretos, numa pasta no Desktop (trocar USER pelo seu usuário)
```
youtube-dl -o "C:/Users/USER/Desktop/%%(playlist)s/%%(playlist_index)s - %%(title)s.%%(ext)s" https://www.youtube.com/playlist?list=LINKPLAYLIST -x --audio-format "mp3"
```
