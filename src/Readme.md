## Documentação notebooks

Neste repositório estão os três arquivos .ipynb utilizados nesse projeto, sendo o primeiro utilizado on-premisse e os outros dois referentes aos JOB's de processamento de dados do AWS Glue, ambos armazenados no AWS CodeCommit. Se deseja mais informações, cada um possuí anotações detalhadas do passo a passo. 

1. **ProjetoMedland** - Aqui estão os códigos para configurar o ambiente na nuvem (criar buckets s3, subir instância do RDS MySQL e criar o banco de dados, fazer upload dos arquivos, acionar JOB's e crawlers do Glue), também tratamos os dados das tabelas *'Hospitais'* , *'Médicos'* e *'Internações'* e esses são inseridos no banco via CRUD. Algumas bibliotecas utilizadas são: boto3, logging, mysql.connector, pandas, etc.

2. **Job1** - Escrito em PySpark para tratar os dados das tabela _'Pacientes'_ e _'Consultas'_ e salvar-los em um bucket.

3.  **Job2** - Segunda etapa no Glue para inserir os dados tratados no banco de dados.


