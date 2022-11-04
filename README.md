# Setup packages R Kantar
Este repositório visa mostrar como instalar dois dos packages necessário à execução de funções de um Data Analyst na Kantar.  

**ROracle**: para conexão à bases de dados Oracle  
**RDCOMClient**: para envio de e-mails através do R  

São dois packages que não são mais mantidos por seus desenvolvedores, e por isso, exigem um malabarismo extra para instalar na versão mais atual do R (4+)

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
