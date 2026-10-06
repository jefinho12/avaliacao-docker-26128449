# Respostas · Avaliação Prática de Docker · Cooperativa AgroVale (Turma A)

Nome:
Matrícula:
Usuário do GitHub:
Usuário do Docker Hub:

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile ou compose vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?

  resposta: Usei a imagem base nginx:1.27-alpine. O tamanho final da imagem do portal ficou em 73.6MB.

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
   conferir que o `index.html` está lá dentro.

   resposta: O Nginx procura os arquivos em /usr/share/nginx/html/. Para conferir usei: docker run --rm jeffersonsera/agrovale-portal:1.0-26128449 ls -l /usr/share/nginx/html/

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.

Link público do repositório: https://hub.docker.com/r/jeffersonsera/agrovale-portal

4. Por que o `docker login` foi feito com um token de acesso e não com a senha da conta?

Porque o token é mais seguro que usar a senha da conta diretamente. Ele pode ser revogado sem precisar alterar a senha e é o recomendado para autenticação no Docker Hub.

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |
|---|---|---|---|---|
| 1 | WORKDIR | O diretório do Nginx estava incorreto | A página de manutenção não aparecia | Corrigi o diretório para `/usr/share/nginx` |
| 2 | COPY | O index.html não estava sendo copiado para a pasta correta | A mensagem "Voltamos em breve" não aparecia | Copiei o arquivo para `/usr/share/nginx/html/index.html` |
| 3 | CMD | O comando de inicialização do Nginx estava incorreto ou ausente | O container não permanecia executando corretamente | Corrigi o comando para iniciar o Nginx em primeiro plano |

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

 Em `-p 7042:80`, a porta 7042 é a porta do computador (host) e a porta 80 é a porta do container. Em `-p 80:7042`, a porta 80 é do computador e a 7042 é do container. Portanto, o segundo número é a porta do container.

## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS_DB_HOST` recebe `db` e não `localhost`?

 Porque dentro do Docker Compose os containers se comunicam pelo nome do serviço. O serviço do banco se chama `db`, então o WordPress usa `db` para encontrar o banco. Se usasse `localhost`, ele tentaria encontrar o banco dentro do próprio container do WordPress.

8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar
   a porta? Mostre o comando.

  Porque o banco só precisa ser acessado pelos outros containers da mesma rede Docker, então não é necessário publicar a porta 3306 no computador. Para consultar o banco sem publicar a porta, pode entrar diretamente no container usando `docker compose exec db`.

## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou,
   e por quê?

   9. Para derrubar a stack usei `docker compose down` e para subir novamente usei `docker compose up -d`.

O comando que poderia apagar o post seria `docker compose down -v`, porque a opção `-v` também remove os volumes. Como os dados do banco ficam armazenados no volume `db_data`, apagar esse volume faria os dados persistidos, incluindo o post criado no WordPress, serem perdidos.

10. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```
