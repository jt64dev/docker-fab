# Docker, Firefox et le GUI sur Ubuntu - X11 obligatoire

## Lancement de Firefox

Créer un dossier firefoxgui
```
    mkdir firefoxgui
    cd firefoxgui
```
Information sur votre utilisateur
    ```id```

Vous aurez besoin de 
```
    uid
    gid
    username
```

Creation d'un Dockerfile
```
  FROM ubuntu:20.04
  RUN apt-get update
  # Installer Firefox
  RUN apt-get install -y firefox
  # Remplacer GID et USERNAME par vos info obtenu par id
  RUN groupadd -g GID USERNAME
  # Remplacer GID et USERNAME et UID
  RUN useradd -d /home/USERNAME -s /bin/bash -m USERNAME -u UID -g GID
  # Remplacer USERNAME
  USER USERNAME
  ENV HOME /home/USERNAME
  CMD /usr/bin/firefox
```

Creation de l'image

    docker build . -t guifirefox

Exécuter l'image
```
docker run -v /tmp/.X11-unix:/tmp/.X11-unix \
 -h $HOSTNAME -v $HOME/.Xauthority:/home/$USER/.Xauthority \
 -e DISPLAY=$DISPLAY guifirefox
```

Firefox devrait s'ouvrir... super utile :)
