# Trabalho de Conclusão de Curso
# CFTV/IP com virtualização de NVR (Frigate)

## Contexto
A segurança física de uma rede é tão importante quanto a lógica.
Para isso uma das soluções encontradas no mercado é a utilização de câmeras para monitoramento dos ambientes.

## Solução implementada
### Frigate
Frigate é uma solução open source para implementação de um NVR (Network Video Recorder) de maneira virtualizada baseada em docker.

### Servidor
Para implementar o Frigate é preciso primeiramente de um servidor. Recomenda-se utilizar um servidor Debian 12 dedicado bare metal, mas sendo possível usar máquinas virtuais ou contêiners (LXC) com perca de performance.

[Guia para instalação do Debian 12](https://www.debian.org/releases/bookworm/amd64/index.pt.html)

### Instalação
Após a configuração do servidor, faça acesso à sua máquina e instale o Docker
```bash
apt update && apt upgrade
apt install docker
```
Depois que o Docker for instalado com sucesso crie os diretórios de configuração e armazenamento. Ex:
```bash
mkdir ~/config
mkdir ~/media
```
Com os diretórios criados, acesse o site de documentação do Frigate, e na aba "Install" faça o [cálculo do tamanho do SHM](https://docs.frigate.video/frigate/installation#calculating-required-shm-size) e [crie seu arquivo Docker](https://docs.frigate.video/frigate/installation#docker)

![Menu de seleção para o arquivo docker-compose.yml](docker-frigate.png)

```bash
docker compose up -d
```
