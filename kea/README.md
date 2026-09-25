Build da imagem:

    docker build --no-cache -t kea .
    docker login
    docker images
    docker tag latest:latest uspdev/kea:latest
    docker tag kea:latest uspdev/kea:latest
    docker push uspdev/kea:latest

