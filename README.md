# Configuração reports e programas R Kantar
Este repositório visa mostrar como configurar um computador para executar reports da Kantar.

1. Packages que requerem um processo de instalação customizado
2. Fontes de dados ODBC para execução de reports


# Packages
Primeiro, há dois packages de R que são necessários à execução de funções de um Data Analyst na Kantar.  

* **ROracle**: para conexão à bases de dados Oracle  
* **RDCOMClient**: para envio de e-mails através do R  

São dois packages que não são mais mantidos por seus desenvolvedores, e por isso, exigem um esforço extra para instalar na versão mais atual do R (4+)



## RDCOMClient 
Pré-requisitos:
RStudio e RTools

1. Desabilitar configuração no RStudio:
Tools -> Global Options ->
![image](https://user-images.githubusercontent.com/55976107/199967211-4ba8fdaf-d8ac-4c2a-b6f0-8ea02656b77b.png)
2. Instalar packages:
```
install.packages("devtools")
install.packages("remotes")
```
3. Depois, executar os seguintes comandos:
```
options(download.file.method = "wininet")
remotes::install_github("BSchamberger/RDCOMClient", ref = "main")
```
4. Para confirmar que foi instalado
```
library(RDCOMClient)
Outlook <- COMCreate("Outlook.Application")
```

## ROracle

1. Instalar o Java JDK

Ele pode ser obtido em:
https://www.oracle.com/pt/java/technologies/downloads/

2. Configurar a variável de ambiente do Windos com a localização do Java (JAVA_HOME)

Aqui tem um guia de como configurar uma variável de ambiente do Windows:
https://phoenixnap.com/kb/windows-set-environment-variable#ftoc-heading-4  
Para esta nossa variável, indicar a pasta onde foi instalado o Java SDK:  
![image](https://user-images.githubusercontent.com/55976107/199969601-99d15c27-82fd-4cf9-bc90-dcf8516fbaf2.png)

3. No RStudio, instalar o package rJava
```
install.packages("rJava")
library(rJava)
```

4. Obter ficheiros do package RORacle e adicionar à pasta do R
A seguir, obteremos os ficheiros de um computador que já tenha este package instalado, e adicionaremos à biblioteca do R do computador que estamos configurando:

4.1 
Descarregar os ficheiros do package que disponibilizo [pelo seguinte link](https://github.com/rafabelokurows/Setup-packages-Kantar/blob/main/ROracle_1.3-2.tar.gz?raw=true). Depois, extrair este ficheiro.

4.2
No RStudio, descobrir a pasta da biblioteca, executando o seguinte comando:
```
.libPaths()
```
Este comando mostrará como resultado um ou dois caminhos, que são as bibliotecas de R neste computador:
![image](https://github.com/rafabelokurows/setup-reports-Kantar/assets/55976107/5094c4f6-a449-4a9a-b61e-78c4375414f3)

4.3 
Entrar em cada um destes diretórios e meter a pasta ROracle extraída na etapa 4.1.





<details>
  <summary><i>Como era feito antes - clique para ver mais</i></summary>
Pré-requisitos:
Oracle Database
Java SDK
RSTudio
RTools

1. Descobrir onde foi instalado **Oracle Client** e **RTools**  

Neste caso:
C:\Temp\WINDOWS.X64_180000_db_home e C:\rtools42

2. Configurar variáveis de ambiente do Windows

2.1 OCI_INC:  

![image](https://user-images.githubusercontent.com/55976107/199967934-7aa4834b-8cae-446a-9374-f944d72544ba.png)

2.2 OCI_LIB64:  

![image](https://user-images.githubusercontent.com/55976107/199968032-91edd025-b272-44f9-b143-ec01b55ab1d4.png)

2.3 ORACLE_HOME:  

![image](https://user-images.githubusercontent.com/55976107/199968145-3038cb86-3c18-473b-852b-912b8c6d73ad.png)

2.4 RTOOLS40_HOME:  

![image](https://user-images.githubusercontent.com/55976107/199968509-afb56e47-ccc4-4de9-b582-2bfe0692ac70.png)

2.5 Incluir caminho na variável PATH:  

![image](https://user-images.githubusercontent.com/55976107/199968208-7ccfd9fb-1597-4068-ba5d-5629962d4995.png)

2.6 JAVA_HOME:  

Apontando para a pasta onde foi instalado o Java SDK  

![image](https://user-images.githubusercontent.com/55976107/199969601-99d15c27-82fd-4cf9-bc90-dcf8516fbaf2.png)

2.7 TNS_ADMIN:  

Apontando para a pasta que contém o ficheiro TSNAMES.ORA (caso não tiver este ficheiro, solicitar a mim ou Filipe Neves, de Masterfile)  

![image](https://user-images.githubusercontent.com/55976107/199969777-29909b6e-83a0-4451-92d2-637b4ecc0bb3.png)

3 No RStudio, instalar package rJava
```
install.packages("rJava")
library(rJava)
```

4 Instalar package RORacle
É possível descarregar o package deste próprio repositório, [pelo seguinte link](https://github.com/rafabelokurows/Setup-packages-Kantar/blob/main/ROracle.zip?raw=true)
```
install.packages("C:\\Users\\BELOKUROWSR\\Desktop\\ROracle_1.3-2.tar.gz", repos = NULL, type="source",INSTALL_opts="--no-multiarch")
```

5 Testar se funcionou
```
library(ROracle)
source('K:/Portugal/Yoyo/Macros R Conexiones.R')
con=Conexio_ISEC_PT('64Bits')
query="select * from dual"
ROracle::dbGetQuery(con, query)
```
Resultado deve ser igual a:  

![image](https://user-images.githubusercontent.com/55976107/199972832-01a411ed-8246-40f7-84c4-12d30e119eec.png)

</details>

# Fontes de dados ODBC

As fontes de dados ODBC permitem uma conexão parametrizada e direta a uma base de dados específica. Por isso, os reports e programas que venho desenvolvendo em R utilizam esta forma de conexão a algumas de nossas bases de dados.  

Obs: Importante que elas sejam configuradas no **configurador 64 bits** do Windows.


1 Acessar o configurador 64 bits do Windows:   

![image](https://user-images.githubusercontent.com/55976107/205894268-16c43608-71d1-4e64-86b6-6f3c72b4d22b.png)

2 Clicar em add:  

![image](https://user-images.githubusercontent.com/55976107/205894777-a40f0f7c-f51d-4614-9936-dbb625f7ac4d.png)

3 Selecionar SQL Server e clicar em Finish:

![image](https://user-images.githubusercontent.com/55976107/205894976-d15a94f7-a251-4e64-8a97-1ee6f64ec9df.png)

4 Informar primeiro o nome da fonte de dados e o servidor à qual ela se conectará -> Next:  

Name: caticawi  
Server: KWSTCSQL002

![image](https://user-images.githubusercontent.com/55976107/205900057-64747dcf-0030-408d-b8c0-a9d7798ffd0a.png)

5 Selecionar autenticação SQL Server (2ª opção), informar o usuário e senha:

![image](https://user-images.githubusercontent.com/55976107/205900398-7f5aacad-9108-4efb-8c2c-7439a98e8179.png)

6 Selecionar a base de dados específica a qual esta fonte se conectará

Default database: CATICAWI

![image](https://user-images.githubusercontent.com/55976107/205900599-e4011dcd-c461-4a51-8832-2c7dea6a4a08.png)

7 Não precisa mudar nada, só clicar em Finish:

![image](https://user-images.githubusercontent.com/55976107/205900738-05c2bad5-4d96-4d7c-a799-6397fa7cc81f.png)

8 Por fim, é possível testar a conexão:

![image](https://user-images.githubusercontent.com/55976107/205900841-a00a2fc2-d8de-4a2d-a29f-84b0541250be.png)

Se o resultado for esse, deu tudo certo:  

![image](https://user-images.githubusercontent.com/55976107/205900974-448d3d7b-a79c-43c9-8f7b-552db5f52284.png)

As fontes de dados a configurar para os reports são:
1.
Name: caticawi
Server: KWSTCSQL002
Default database: CATICAWI

2.
Name: demopan
Server: KWSTCSQL002
Default database: DEMOPAN

3. 
Name: maestro
Server: KWSTCSQL002
Default database: MAESTRO

4.
Name: PANELSMART
Server: WKLN4PAPP0024
Default database: PANELSMART
