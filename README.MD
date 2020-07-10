# Email workers
Um projeto em docker, feito para fins de estudo, no qual introduzimos um deploy de um app fictício no qual mandamos mensagem por email.

# Como utilizar
Você pode iniciar usando o docker composer, através do comando:
```SHELL
docker-compose up -d --scale worker=3
```
Nesse caso, o app é iniciado com 3 instâncias do container worker para processamento da fila.
# Estrutura
O app é divido em containers, cada um representando um serviço do app, respeitando o paradigma de microservices e também isolamento de redes, temos: 

* ## Frontend
O frontend é um container contendo nginx, cujo o objetivo é funcionar como reverse proxy para a API do projeto e também a página que tem como objetivo ser a interface do usuário final com nosso app
* ## Banco de dados
Usamos um container postgreeSQL para guardar os dados da nossa aplicação.
* ## API
Responsável por receber as interações do usuário do frontend e validar as informações para o worker
* ## Worker
Responsável por receber as informações da API e enviar os emails fictícios
* ## Redis
Responsável por enviar as informações da API para o Worker, como o app pressupõe que pode ter várias instâncias do worker, o Redis é o responsável por enviar informações para a fila

## Networks:
Os container estão em networks separados, os mesmos definidos no composer são:

* ### banco: *Contém a API e o Banco de dados*
  ### web: *Contém o frontend e a API*
  ### fila: *contém a API, o Redis, e os workers
  