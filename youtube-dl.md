# Youtube-dl

## MP3
- Baixando um álbum do YouTube no formato e numeração corretos, numa pasta no Desktop
  - trocar USER pelo seu usuário
  - trocar o link que contém LINKPLAYLIST para o link da playlist no youtube
```
youtube-dl -o "C:/Users/USER/Desktop/%%(playlist)s/%%(playlist_index)s - %%(title)s.%%(ext)s" https://www.youtube.com/playlist?list=LINKPLAYLIST -x --audio-format "mp3"
```
