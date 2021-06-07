--------------------------------------------------------------------------------------------------------------------------------------------------------------

- Implementando Apache Kafka em ambiente Windows.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

- Data da ultima atualização do arquivo: 07/06/2021.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

1° Passo: Download no site https://kafka.apache.org/downloads.

- Faça de preferência o download da versão mais recente ou da versão que for de sua escolha.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

2° Passo: Criar estrutura de pastas para alocar o kafka. Temos como realizar a criação manualmente e/ou pelo Prompt de Comando, que seria o mais prático.

1º Método Manual: As pastas podem ser criadas manualmente com os nomes abaixo. 

- Criar no C: ou na partição de sua preferência.

```
C:\Kafka
C:\Kafka\application
C:\Kafka\data
C:\Kafka\data\zookeeper
C:\Kafka\tmp
C:\Kafka\tmp\kafka-logs
C:\Kafka\tmp\kafka-logs\1
C:\Kafka\tmp\kafka-logs\2
C:\Kafka\batch
```

* Nota1: Se seu disco/partição for (D:) ou qualquer outro nome, considere criar de acordo com seu disco e partição, onde basta substituir neste mesmo documento.

* Nota2: Notar que o diretório (C:\Kafka) é o principal e as demais pastas tem que ser criadas dentro deste repositório principal.

* Nota3: Será mais prático executar pelo método abaixo do Prompt de Comando.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

2º Método pelo Prompt de comando: Abrir o Prompt de comando e executar os seguintes comandos (pressione WIN + R, escreva cmd e aperte enter).

- Copie e cole os comandos abaixo diretamente no Prompt de Comando.

```
C:
mkdir C:\Kafka
mkdir C:\Kafka\application
mkdir C:\Kafka\data
mkdir C:\Kafka\data\zookeeper
mkdir C:\Kafka\tmp
mkdir C:\Kafka\tmp\kafka-logs
mkdir C:\Kafka\tmp\kafka-logs\1
mkdir C:\Kafka\tmp\kafka-logs\2
mkdir C:\Kafka\batch
```

- Nota: Se seu disco/partição for (D:) ou qualquer outro nome, considere criar de acordo com seu disco e partição, onde basta substituir neste mesmo documento.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

3º Passo:

Após criar as pastas em sua partição, vá até o arquivo que foi feito o download do 1º passo, faça a descompactção do arquivo, copie todo seu conteúdo e cole na pasta que foi criada para o kafka (C:\Kafka\application).

1º - Descompacte o arquivo que foi feito download.

2º - Copie seu conteúdo, que provalmente tem os nomes (bin, config, libs, site-docs, LICENSE, NOTICE).

3º - Cole esses arquivos na pastas (C:\Kafka\application) de acordo com o nome de sua partição, e se for a (C:) pode manter conforme o exemplo.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

4° Passo:

1º - Abrir pasta C:\Kafka\application\config\

2º - Copiar arquivo server.properties.

3º - Colar duas vezes o mesmo conteudo e renomear com os nomes abaixo. Manter o arquivo com nome de (server.properties). Atenção para renomear, pois, (.properties) é uma extensão, logo, ficar mais fácil você apertar CTRL+A (selecionar tudo) e colar em seguida, assim evitamos algum erro na colagem.

4º - server1.properties.

5º - server2.properties.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

5° Passo:

- Editar arquivo C:\Kafka\application\config\server1.properties.

1º - Setar broker id = 1 -> ficará: broker.id=1.

2º - Descomentar a linha e setar porta 9092 para o server1 -> ficará: listeners=PLAINTEXT://:9092.

3º - Setar diretório de logs para o diretório criado para o server1 -> log.dirs=/tmp/kafka-logs -> ficará: log.dirs=C:/Kafka/tmp/kafka-logs/1.

4º - Numero de partições por topico setar 2 -> ficará: num.partitions=2.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

6° Passo:

- Editar arquivo C:\Kafka\application\config\server2.properties.

1º - Setar broker id = 2 -> ficará: broker.id=2.

2º - Descomentar a linha e setar porta 9093 para o server1 -> ficará: listeners=PLAINTEXT://:9093.

3º - Setar diretório de logs para o diretório criado para o server1 -> log.dirs=/tmp/kafka-logs -> ficará: log.dirs=C:/Kafka/tmp/kafka-logs/2.

4º - Numero de partições por topico setar 2 -> ficará: num.partitions=2.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

7° Passo:

- Editar o arquivo C:\Kafka\application\config\zookeeper.properties.

- Setar o diretorio de dados(datadir) para o zookeeper -> dataDir=/tmp/zookeeper -> ficará: dataDir=C:/Kafka/data/zookeeper.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

8° Passo:

Abra o Prompt de comando e execute os comandos a seguir:

- Batch para Inicializar o Zookeeper e Kafka cluster.
- Copie e cole o comando abaixo diretamente no Prompt de Comando.
```
echo start C:\Kafka\application\bin\windows\zookeeper-server-start.bat C:\Kafka\application\config\zookeeper.properties > C:\Kafka\batch\Start_Zookeeper.bat
```
- Batch para Inicializar o Servidor 1 Kafka.
- Copie e cole o comando abaixo diretamente no Prompt de Comando.
```
echo start C:\Kafka\application\bin\windows\kafka-server-start.bat C:\Kafka\application\config\server1.properties > C:\Kafka\batch\Start_Kafka_Server1.bat
```

- Batch para Inicializar o Servidor 2 Kafka.
- Copie e cole o comando abaixo diretamente no Prompt de Comando.
```
echo start C:\Kafka\application\bin\windows\kafka-server-start.bat C:\Kafka\application\config\server2.properties > C:\Kafka\batch\Start_Kafka_Server2.bat
```

- Nota1: Caso não apareça nada no Prompt de Comando com a execução dos comandos, é porquê foram executados com sucesso.
- Nota2: Para verificar se os batchs foram criados, acessa o caminho: C:\Kafka\batch, ou com o nome de diretório que você tenha criado de acordo com sua partição, onde foi explicado nos passos acima.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

9° Passo:

- Abra no caminho (C:\Kafka\batch) ou no nome que você deu, as batchs criadas para inicializar o cluster.

- 1º - Start_Zookeper.bat
- 2º - Start_Kafka_Server1.bat
- 3º - Start_Kafka_Server2.bat

- Nota: Ao abrir as batchs (Start_Zookeper.bat, Start_Kafka_Server1.bat e Start_Kafka_Server2.bat) não feche as janela, pois, como estamos utilizando windows, está rodando em aplicação e não em serviço, então, caso essa janela seja fechada, irá interromper o servidor.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

10° Passo:

- Vamos criar dois topicos para teste.

- Batch para criar topico customer.
- Copie e cole o comando abaixo diretamente no Prompt de Comando.
```
echo start C:\Kafka\application\bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 2 --partitions 2 --topic customer_topic > C:\Kafka\batch\Create_customer_topic.bat
```

- Batch para criar topico product.
- Copie e cole o comando abaixo diretamente no Prompt de Comando.
```
echo start C:\Kafka\application\bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 2 --partitions 2 --topic product_topic > C:\Kafka\batch\Create_product_topic.bat
```

--------------------------------------------------------------------------------------------------------------------------------------------------------------

11º Passo:

- Após executar os comandos no Prompt de Comando do 10º passo, vamos criar os tópicos. Siga os passos abaixo:

- 1º - Entre no caminho: C:\Kafka\batch ou de acordo com seu nome de diretório/partição.
- 2º - Clique duas vezes no arquivo com nome (Create_customer_topic.bat), aguarde a abertura do Prompt de Comando e a mensagem (Created topic customer_topic). Pode fechar a janela.
- 3º - Clique duas vezes no arquivo com nome (Create_product_topic.bat), aguarde a abertura do Prompt de Comando e a mensagem (Created topic product_topic). Pode fechar a janela.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

12° Passo:

- Vamos agora, iniciar o serviço de producer e consumer, para assim podermos enviar e receber mensagens atraves do kafka broker (customer_topic).

- Batch para inicializar o serviço de producer para o topico customer_topic.
- Copie e cole o comando abaixo diretamente no Prompt de Comando.
```
echo start C:\Kafka\application\bin\windows\kafka-console-producer.bat --topic customer_topic --broker-list localhost:9092,localhost:9093 > C:\Kafka\batch\Producer_customer_topic.bat
```

- Vamos agora, criar a batch para iniciar o serviço de consumer, par aassim podermos receber mensagens do kafka broker (customer_topic)
- Copie e cole o comando abaixo diretamente no Prompt de Comando.
```
echo start C:\Kafka\application\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --from-beginning --topic customer_topic > C:\Kafka\batch\Consumer_customer_topic.bat
```

- Nota1: Caso não apareça nada no Prompt de Comando com a execução dos comandos, é porquê foram executados com sucesso.
- Nota2: Para verificar se os batchs foram criados, acessa o caminho: C:\Kafka\batch, ou com o nome de diretório que você tenha criado de acordo com sua partição, onde foi explicado nos passos acima.

- Testes:
- Agora vamos fazer um teste para verificar se o producer (produtor) e o consumer (consumidor) do tópico (customer_topic) estão funcionando normalmente de acordo com suas funções. Siga os passos abaixo:

- 1º: Matenha os arquivos (Start_Zookeeper.bat, Start_Kafka_Server1.bat e Start_Kafka_Server2.bat) do caminho (C:\Kafka\batch) abertos, pois, são os servidores rodando.
- 2º: Abra os arquivos (Producer_customer_topic.bat e Consumer_customer_topic.bat) do caminho (C:\Kafka\batch).
- 3º: Com o Prompt de Comando do arquivo (Producer_customer_topic.bat) aberto, perceba que ele fica com um (>), orientando que podemos escrever algo. Tente escrever "Testes" e de Enter.
- 4º: Com o Prompt de Comando do arquivo (Consumer_customer_topic.bat) aberto e depois de ter digitado "Testes" no passo acima, verifique se nesta janela atual aparece o "Testes" e caso apareça, significado que deu certo.
- 5º: Caso funcione corretamente, significa que o produtor e consumidor do tópico (customer_topic) estão funcionando corretamente.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

13° Passo:

- Vamos, iniciar o serviço de producer e consumer, para assim podermos enviar e receber mensagens atraves do kafka broker (product_topic).

- Batch para inicializar o serviço de producer para o topico product_topic.
- Copie e cole o comando abaixo diretamente no Prompt de Comando.
```
echo start C:\Kafka\application\bin\windows\kafka-console-producer.bat --topic product_topic --broker-list localhost:9092,localhost:9093 > C:\Kafka\batch\Producer_product_topic.bat
```

- Vamos, criar a batch para iniciar o serviço de consumer, par aassim podermos receber mensagens do kafka broker (product_topic).
- Copie e cole o comando abaixo diretamente no Prompt de Comando.
```
echo start C:\Kafka\application\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --from-beginning --topic product_topic > C:\Kafka\batch\Consumer_product_topic.bat
```

- Nota1: Caso não apareça nada no Prompt de Comando com a execução dos comandos, é porquê foram executados com sucesso.
- Nota2: Para verificar se os batchs foram criados, acessa o caminho: C:\Kafka\batch, ou com o nome de diretório que você tenha criado de acordo com sua partição, onde foi explicado nos passos acima.

- Testes:
- Agora vamos fazer um teste para verificar se o producer (produtor) e o consumer (consumidor) do tópico (product_topic) estão funcionando normalmente de acordo com suas funções. Siga os passos abaixo:

- 1º: Matenha os arquivos (Start_Zookeeper.bat, Start_Kafka_Server1.bat e Start_Kafka_Server2.bat) do caminho (C:\Kafka\batch) abertos, pois, são os servidores rodando.
- 2º: Abra os arquivos (Producer_product_topic.bat e Consumer_product_topic.bat) do caminho (C:\Kafka\batch).
- 3º: Com o Prompt de Comando do arquivo (Producer_product_topic.bat) aberto, perceba que ele fica com um (>), orientando que podemos escrever algo. Tente escrever "Testes" e de Enter.
- 4º: Com o Prompt de Comando do arquivo (Consumer_product_topic.bat) aberto e depois de ter digitado "Testes" no passo acima, verifique se nesta janela atual aparece o "Testes" e caso apareça, significado que deu certo.
- 5º: Caso funcione corretamente, significa que o produtor e consumidor do tópico (product_topic) estão funcionando corretamente.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

14° Passo:

- Vamos Verificar e descrever o status dos topicos do kafka.

- Batch para descrever o status do kafka para o topico customer_topic
```
echo start C:\Kafka\application\bin\windows\kafka-topics.bat --describe --zookeeper localhost:2181 --topic customer_topic > C:\Kafka\batch\Status_customer_topic.bat
```
- Batch para descrever o status do kafka para o topico product_topic
```
echo start C:\Kafka\application\bin\windows\kafka-topics.bat --describe --zookeeper localhost:2181 --topic product_topic > C:\Kafka\batch\Status_product_topic.bat
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------

Espero que este tutorial ajude com o a implementação do Apache Kafka no ambiente Windows.

--------------------------------------------------------------------------------------------------------------------------------------------------------------
