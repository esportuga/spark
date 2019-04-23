# Instroducao ao Spark com Google Collab

<h2>Configuração do Google Collab</h2>

Para acessar o Google Collab é necessário logar com uma conta Google! Para acessar o Collab <a href="https://colab.research.google.com/" target="blank">clique aqui</a>.


Ao acessar o notebook pela primeira vez, você irá criar um Notebook Python3.
Após abrir o novo notebook faremos a instalação dos pacotes, configurar as variáveis de ambiente e iniciar o Spark! Para tanto, basta rodar os 3 conjuntos de código abaixo:

```bash
!apt-get install openjdk-8-jdk-headless -qq > /dev/null
!wget -q http://www-eu.apache.org/dist/spark/spark-2.4.1/spark-2.4.1-bin-hadoop2.7.tgz
!tar xf spark-2.4.1-bin-hadoop2.7.tgz
!pip install -q findspark
!pip install -q pyspark
```


Essa primeira parte do código é responsável por instalar o Java, baixar e instalar o Spark com o Hadoop, instalar o findSpark, que é utilizado para encontrar a instalação do Spark na máquina, e o PySpark, que é a API de Spark em Python. 

>IMPORTANTE: De tempos em tempos, eles removem as distribuições antigas do Spark do diretório da Apache. Se o código não funcionar para você, provavelmente você precisará atualizar a versão do Spark que está baixando.



Agora iremos definir as variáveis de ambiente e mostrar para o sistema onde buscar os arquivos necessários. Aqui é importante ressaltar que, caso você altere a versão do Spark que vai utilizar, é necessário também alterar o arquivo que está sendo enviado para a variável SPARK_HOME.

```python
import os
os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-8-openjdk-amd64"
os.environ["SPARK_HOME"] = "/content/spark-2.4.1-bin-hadoop2.7"
```

Nessa última etapa, encontraremos o Spark e iniciaremos uma sessão. 
Com o “local[*]” nosso processamento será distribuído em todos os cores da máquina que estamos utilizando. Se sua variável de ambiente estiver errada no comando anterior, o comando findspark.init() irá falhar.

```python
import findspark
findspark.init()
from pyspark.sql import SparkSession
spark = SparkSession.builder.master("local[*]").getOrCreate()
```

Pronto! Temos um ambiente configurado e rodando Spark! Agora é só sair codificando ;). Na próxima e última seção deste artigo, iremos apresentar alguns comandos que você pode fazer usando o pyspark.sql.
