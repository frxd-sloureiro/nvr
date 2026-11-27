# Trabalho de Conclusão de Curso
# CFTV/IP com virtualização de NVR (Frigate)

## Contexto
O Trabalho de Conclusão de Curso (TCC) consistia em estruturar uma rede completa, com todos os componentes e serviços mais comuns, como switches (core e distribuição), firewall, proxy, roteadores, servidor (GIT, NVR, LDAP, Monitoramento). O nosso grupo estava encarregado da configuração e implementação do CFTV/IP, utilizando um serviço de NVR virtualizado: o Frigate.

## Solução implementada
### Frigate
Frigate é uma solução open source para implementação de um NVR (Network Video Recorder) de maneira virtualizada baseada em docker.

### Servidor
Para implementar o Frigate é preciso primeiramente de um servidor. Recomenda-se utilizar um servidor Debian 12 dedicado bare metal, mas sendo possível usar máquinas virtuais ou contêiners (LXC) com perda de performance.

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
Com os diretórios criados, acesse o site de [documentação do Frigate](https://docs.frigate.video), e na aba "Install" faça o [cálculo do tamanho do SHM](https://docs.frigate.video/frigate/installation#calculating-required-shm-size) e [crie seu arquivo Docker](https://docs.frigate.video/frigate/installation#docker) de acordo com seu hardware e preferências.

![Menu de seleção para o arquivo docker-compose.yml](https://img.lightshot.app/f0z9NdnpRC-GoJSST6J4jg.png)

Depois da obtenção do arquivo docker-compose.yml, copie-o para o seu servidor/máquina e utilize o seguinte comando para instalar e habilitar o serviço:
```bash
docker compose up -d
```
***(Obs.: Após a execução do comando fique atento, pois o usuário e senha padrão da instalação aparecerão nos logs/terminal. Se for necessário para ver os logs pode se usar esse comando: `docker compose logs -f frigate`)***

### Configuração
Com o contêneir iniciado, inicie o navegador em sua máquina e abra https://IP_DO_SERVIDOR:8971 e use as credenciais que obteve nos logs para realizar login no Frigate.

![Tela de login do Frigate](https://img.lightshot.app/9U8PeFPTTEOJRMf1VNojQg.png)

Após feito login abra as configurações, vá na aba usuários e escolha uma nova senha para o usuário admin (e se for necessário, crie outros usuários)

![Tela de configuração de usuáriros](https://img.lightshot.app/gJTsfyegTpiHObmzIqK7PA.png)

Volte a tela inicial, clique em "Adicionar Câmera" e "+Add New Camera". Coloque as informações da sua câmera como nome, IP, usuário e senha (se necessário) e a porta de redirecionamento ONVIF. Caso suas câmeras não utilizem o protocolo ONVIF clique em "Manual Selection" e escolha devidamente a marca correspondente.

![Adição de câmeras](https://img.lightshot.app/ae7UFRRPTA-RGm8jKOhcBA.png)

Caso o reconhecimento da câmera for um sucesso, escolha a stream que desejar e ative as configurações (gravação e audio) que forem necessárias.

![Sucesso no reconhecimento da câmera](https://img.lightshot.app/Q-zUQh9xRgaaxf7t8B-5Eg.png)
![Configurações da stream](https://img.lightshot.app/65JR7_3lSUaQZlTL2vaGBw.png)

Depois de adicionda a primeira câmera, para as demais vá para Configurações -> Configuração Global -> Gerenciamento e repita os passos passados.

Com todas as câmeras devidamente configuradas é possível observar o vídeo de cada uma na página inicial, além de poder interagir individualmente com cada uma (Ex.: Iniciar imediatamente uma gravação). Há também outros serviços na aba lateral, como revisão e exportação de gravações/clipes. Caso haja qualquer dúvida de utilização consulte a [documentação oficial](https://docs.frigate.video/)

## Demonstração de Uso

### Clipe 1
<video width="auto" height="auto" controls>
  <source src="52.27.mp4" type="video/mp4">
</video>


### Clipe 2
<video width="auto" height="auto" controls>
  <source src="45.07.mp4" type="video/mp4">
</video>