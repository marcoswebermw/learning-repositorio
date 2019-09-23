### Iniciando o Hadoop.  
  
> São 5 serviços Java que tem que estar executando:  
`DataNode`, `ResourceManager`, `NameNode`, `SecondaryNameNode`, `NodeManager`.  
Se um dos serviços não estiver rodando, será necessário parar o serviço do Hadoop, e reiniciar todo o processo, limpando os diretórios temporários e formatando o HDFS.  
  
```sh
# Acessando o diretório onde o hadoop foi instalado.
cd /usr/local/hadoop

# Formatando o sistema de arquivos distribuídos do Hadoop(HDFS).
# Eliminando os diretórios temporários.
rm -rf /usr/local/hadoop/tmp/* && ls -lha /usr/local/hadoop/tmp/

# Formatando o HDFS.
/usr/local/hadoop/bin/hdfs namenode -format

# Iniciando os serviços para execução do Hadoop.
/usr/local/hadoop/sbin/start-all.sh

# Listando os serviços.
jps

# Parando o serviço do Hadoop.
/usr/local/hadoop/sbin/stop-all.sh
```  
### Diretórios  
  
O comando `hdfs` será o responsável por gerenciar as operações no Hadoop.  

```sh
# Listando diretórios. Inicialmente estará vazio.
/usr/local/hadoop/bin/hdfs dfs -ls /

# Criando um diretório no HDFS.
/usr/local/hadoop/bin/hdfs dfs -mkdir /IGTI

# Criando um subdiretório.
/usr/local/hadoop/bin/hdfs dfs -mkdir /IGTI/FBD

# Incluindo um arquivo no subdiretório.
/usr/local/hadoop/bin/hdfs dfs -put /home/igti/Downloads/book.txt /IGTI/FBD

# Excluindo um arquivo do HDFS.
/usr/local/hadoop/bin/hdfs dfs -rm /IGTI/FBD/book.txt

# Excluindo um diretório do HDFS.
/usr/local/hadoop/bin/hdfs dfs -rmdir /IGTI/FBD
```  
  
### Arquivos  
  
```sh
# Exibindo o conteúdo de um arquivo com o 'cat'.
/usr/local/hadoop/bin/hdfs dfs -cat /IGTI/Resultado/part-r-00000
```  
  

### Ferramentas Auxiliares do Hadoop  
 
2) Ferramenta Gráfica Gerenciadora dos trabalhos pelo navegador: `localhost:8088/cluster`.   
2) Ferramenta Gráfica Gerenciadora do Hadoop pelo navegador: `localhost:9870`.  

Vá em `Utilities --> Browse the File System` para verificar o sistema de arquivos do Hadoop.  


### Experimentos com o pacote de Exemplos  
  
Nestes exemplos serão usados o comando hadoop, em cima de programas Java(jar), o pacote com os programas de exemplos `hadoop-mapreduce-examples-3.0.3.jar`, o programa `pi` ou `wordcount` contidos no pacote. No segundo exemplo, também serão usados um arquivo que serve como fonte dos dados, e um diretório de saída do processamento dos dados.  
  
**Calculando o valor de PI**  

Calculando o valor de `PI` com um algoritmo já implementado no Hadoop.  
  
```sh
/usr/local/hadoop/bin/hadoop jar /usr/local/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.0.3.jar pi 4 25
```  
  
**Contador de Palavras**  
  
```sh
/usr/local/hadoop/bin/hadoop jar /usr/local/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.0.3.jar wordcount /IGTI/FBD/book.txt /IGTI/ResultadoWordCount/

# Usando o cat para verificar a contagem de palavras(quantas vezes cada palavra aparece no texto).
/usr/local/hadoop/bin/hdfs dfs -cat /IGTI/Resultado/part-r-00000
```    
Será criado um diretório contendo um arquivo com os resultados do processamento.  
O arquivo gerado também pode ser baixado pela interface web.  

 
> O Hadoop irá instanciar um job, que poderá levar alguns minutos para executar, e vai mostrando um progresso da execução. O resultado do processo também poderá ser conferido na interface gráfica.  
  
  
### Criando um alias para o comando `dfs`, que é muito usado.  
  
```sh
alias dfs=/usr/local/hadoop/bin/hdfs dfs
```  
Depois é só passar os parâmetros.  

