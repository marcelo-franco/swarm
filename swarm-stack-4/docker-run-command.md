# Instruções
------------
1. No comando "docker run" abaixo, substitua "<any swarm IP>" com o IP de um dos nós do seu swarm
2. Faça o deploy do arquivo de stack voting-app-stack.yml (presente neste subdiretório)
3. Copie o comando "docker run" e cole na sua linha de comando do docker. O diretório corrente deverá ter o arquivo "postb", cujo conteúdo será enviado como corpo da requisição POST 

Esse comando baixará a imagem "mfrancoatdocker/ab", e rodará o container que executa a aplicação "ab", da Apache, com os parametros especificados.
(https://httpd.apache.org/docs/2.4/programs/ab.html)

Note que:
1. o container será removido depois da execução do programa "ab"
2. há um volume compartilhado com o container (-v `pwd`:`pwd`), para acesso ao diretório corrente, onde deverá estar o arquivo "postb"
3. serão executados 1000 requisições POST (-n 1000 -p postb), com o máximo de 50 conexões concorrentes (-c 50)

docker run --rm --read-only -v `pwd`:`pwd` -w `pwd` mfrancoatdocker/ab -T "application/x-www-form-urlencoded" -p postb -c 50 -n 1000 http://<any swarm IP>:5000/