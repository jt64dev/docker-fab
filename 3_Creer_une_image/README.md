# Création du API node.js sous forme de container Docker

## Creation d'un api node

Créer un dossier et implémenter l'exemple en NodeJs et Express
https://expressjs.com/fr/starter/hello-world.html

tester avec `node app.js`

Maintenant que votre application fonctionne nous allons la mettre dans un container Docker.

## Containerisation

Creation d'un Dockerfile

    # Initial image that will be imported
    FROM node:lts-alpine
    # Installation location in the container created
    WORKDIR /usr/src/app
    # Copy the package.json first
    COPY package.json ./
    # Install the different dependencies
    RUN npm install
    # Copy the rest of the content
    COPY . .
    # Make sure that the "node" user executes the commands
    USER node
    # Launch the JS file.
    # Example : ["node", "run", "web"] | There will be a space between the different elements of the table.
    CMD ["node", "server.js"]
    # Open the following port to the outside world
    EXPOSE 3000

    # THINK AT .dockerignore !!

    # Create an image :
    # OPTION -t is for name this image
    # OPTION "." is for directory of the Dockerfile
    # docker build . -t {name}:{tag}

    # Create an container with this image
    # OPTION -p is for transfert the port to your local network
    # OPTION -d is for not launching the log.
    # OPTION --rm for delete container on close
    # docker run -p {MY_LOCAL_PORT}:{PORT_EXPOSE} {IMAGE_ID}

Creation d'un fichier **.dockerignore** pour ne pas copier le dossier des modules par exemple

    node_modules

Creation d'une image

    docker build . -t myserver:0.5

Exécuter l'image

    docker run -p 3000:3000 myserver:0.5

Déployer votre image sur DockerHub

    DockerHub à vous de jouer
