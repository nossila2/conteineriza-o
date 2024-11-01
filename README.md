# Conteinerização

O projeto consiste na execução de uma aplicação em nodejs na usados são usados containers segmentados em: nginx, frontend, backend e postgres. A figura abaixo ilustra a arquitetura:

![My Image](arquitetura_app.png)

**NGINX**

O container do nginx utiliza a última imagem disponível no dockerhub. Caso haja necessidade de atualização basta apenas apagar a imagem e baixá-la novamente. Relacionado ao docker-compose é copiado o arquivo chamado: appgues.teste.com.br.conf no qual está armezanada a configuração para receber requisição externa na porta 443 e direcionar a porta 3000 do container do fronted.

**FRONTEND**

o container do frontend usa a imagem personalizada gerada a partir do Dockerfile no qual possui as instruções de como aplicação deve ser iniciada. A imagem é baseada na última versão do alpine. Há uma variável de ambiente: NODE_VERSION onde é especificado a versão do node a ser instalado. Caso haja necessidade de atualização basta apenas mudar a variável com a versão e gerar uma nova imagem.  Existe uma limitação dessa aplicação em relação a versão do python. A mesma só funciona com versões até 3.10. Por esse motivo foram adicionados os repositórios do alpine na versão: v3.13. Com isso foi instalado o python na versão 3.8

**BACKEND**

o container do frontend usa a imagem personalizada gerada a partir do Dockerfile no qual possui as instruções de como aplicação deve ser iniciada. A imagem é baseada na última versão do alpine. As atualizações que podem ocorrer nessa imagem seria a do próprio alpine.

**POSTGRES**

O container do postgres utiliza a imagem na versão 12 disponível no dockerhub. Caso haja necessidade de atualização, basta apenas apagar a imagem e especificar no docker-compose a nova versão. Há uma volume mapeado no docker-compose para armazenar os dados do banco postgres.

**Docker-Compose**

O arquivo do docker-compose armezena todas as instruções para iniciar todos os container de forma sequencial e posteriormente permitir o acesso a aplicação via HTTP/HTTPS.

**Comandos**

Iniciar a aplicação (deve estar no diretório em que o arquivo docker-compose.yml esteja salvo):

**docker compose up -d**

Encerrar a aplicação 

**docker compose down** (deve estar no diretório em que o arquivo docker-compose.yml esteja salvo):

Gerar uma imagem nova do Nginx e Postgres:

**docker rmi (id da imagem)**

Na próxima inicialização a nova imagem será baixada do docker hub. O id da imagem deve ser adquirido a partir do comando: docker image

Gerar uma nova imagem do Frontend e Backend:

**docker build . -t frontend:v(numero da nova versão)** (deve estar no diretório em que o arquivo Dockerfile esteja salvo)

