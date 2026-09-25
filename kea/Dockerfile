FROM debian:latest

# packages
RUN sed -i 's|main|main non-free|' /etc/apt/sources.list.d/debian.sources && apt-get update && apt-get install -y \
    iproute2 \
    git \
    unzip \
    curl

# cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Instala o serviço desejado - REMOVER
RUN apt-get update && apt-get install -y nginx

# Mantém o processo do Nginx em primeiro plano
CMD ["nginx", "-g", "daemon off;"]
