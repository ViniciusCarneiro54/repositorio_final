## Introdução

Esse projeto surgiu da minha necessidade de por em prática conteúdos estudados ao longo do tempo como SQL, Python, Cloud (AWS), PySpark e tipos de arquivos (JSON, CSV, Parquet). Nele eu simulei a criação de um banco de dados transacional para uma empresa pequena empresa de saúde que conta com dois hospitais de médio porte na capital mineira Belo Horizonte. Abaixo segue uma descrição das três etapas da modelagem de dados seguidas nesse projeto.

* **Modelo conceitual** - Aqui é onde nasce tudo, o responsável pela modelagem e implantação deve estar em contato contínuo com o usuário final e ou área de negócio, apurando como se dá o surgimento dos dados e quais as regras de negócio ali aplicadas, os processos e as necessidades, ou seja, basicamente aprender como funcionam as coisas ali naquela organização. Todas as demandas e regras aplicadas devem ser documentadas para utilização posterior, é de suma importância ouvir todos que fazem parte da rotina operacional, e quanto mais informação melhor! E lembre-se sua principal finalidade é capturar os requisitos de informação e regras de negócio sob o ponto de vista do negócio, nada de falar de tecnologia ainda!

*  **Modelo lógico** - Depois de compilar os requisitos do negócio, nessa etapa já começamos a pensar em chaves primarias, chaves estrangeiras e todo o esboço do modelo, aqui a modelagem é mais detalhada. Descrever com os dados serão armazenados e seus relacionamentos é importante, pois nesse nível as regras de integridade e normalização são estabelecidas para garantir a consistência dos dados. Aqui já são feitos rabiscos do diagrama do nosso banco, mas calma lá! Não necessariamente já definimos a tecnologia aqui, e tão pouco já é feita a criação do banco de dados.

* **Modelo físico** - Agora sim temos que definir uma tecnologia para implementar o que foi decidido no modelo lógico, ela é a representação física de tudo que foi definido antes. É importante escolher um banco de dados que se adapte e suporte as necessidades do negócio, levando em consideração os detalhes técnicos e de desempenho. E nosso caso especifico, decidimos por utilizar o SGBD MySQL!

Depois de finalizando o modelo físico esse foi o resultado, o catálogo dos dados pode ser visto !aqui 

![Diagrama do banco de dados](img/diagram.png)

## Pré-requisitos para execução desse projeto

- Python + libs (boto3, Pandas)
- Jupyter Nootebok (ou outro que abra arquivos .ipynb)
- Conta AWS

## Descrição dos serviços utilizados na nuvem
| Serviço      | Descrição                                                                                                                                                                                                                                                                           |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IAM          | Utilizado para gerenciamento de segurança, aqui configuramos as roles e policies para usuários e serviços que serão utilizados, dentre outras configurações relacionadas a segurança, sempre pensando no privilégio de acesso mínimo.                                                                                                                                                     |
| S3           | Serviço que oferece armazenamento altamente escalável e confiável, orientado a objetos.                                                                                                                                                                                                                  |
| Glue Catalog | Repositório centralizado de metadados que descreve os dados disponíveis, esses geralmente rastreados por crawlers, facilitando a pesquisa, consulta e acesso aos dados de várias fontes em um único local.                                                                          |
| Glue Crawler | Utilizamos esse serviço para examinar fontes de dados como arquivos em armazenamento S3, bancos de dados JDBC, tabelas do RDS dentre muitos outros, para extrair metadados e criar tabelas virtuais que permitem maior gerenciamento dos seus dados.                                |
| Glue Job     | É um conjunto de instruções ETL que se conecta a dados de origem, processa-os e os grava em um destino de dados. Eles podem ser escritos em Python ou Scala e agendados para execução periódica ou desencadeados por eventos, como a chegada de novos dados. |

## Catálogo de dados

### Tabela "PACIENTES"
Registro de todos pacientes que já consultaram alguma vez na instituição. 

| Coluna          | Descrição                                            |
| --------------- | ---------------------------------------------------- |
| Nome            | Nome completo do paciente.                           |
| Idade           | Idade do paciente.                                   |
| CPF             | Número do CPF.                                       |
| RG              | Número da cédula de registro geral.                  |
| Data nascimento | Data de nascimento do paciente.                      |
| Sexo            | Descrição sexo M ou F.                               |
| Signo           | Signo com base na data de nascimento.                |
| Mãe             | Nome completo da mãe.                                |
| Pai             | Nome completo do pai.                                |
| Email           | Endereço de correio eletrônico.                      |
| Senha           | Senha cadastrada para resultados de exames.          |
| Cep             | CEP da residência.                                   |
| Endereco        | Rua/avenida, etc da residência.                      |
| Número          | Número da residência.                                |
| Bairro          | Nome do bairro da residência.                        |
| Cidade          | Nome da cidade que o paciente reside.                |
| Estado          | Nome do estado referente a cidade.                   |
| Telefone fixo   | Número de telefone fixo se houver.                   |
| Celular         | Número de telefone móvel.                            |
| Altura          | Altura do paciente.                                  |
| Peso            | Peso na data do cadastro ou última consulta.         |
| Tipo sanguíneo  | Tipo sanguíneo do paciente caso haja tal informação. |
| Cor             | Tag gerada aleatoriamente pelo sistema.              |

### Tabela "CONSULTAS"
| Coluna      | Descrição                                                       |
| ----------- | --------------------------------------------------------------- |
| ID_Paciente | ID único do paciente.                                           |
| ID_Medico   | ID do médico que fez o atendimento na consulta.                 |
| ID_Hospital | ID do hospital realizado o atendimento.                         |
| Data        | Datetime do início da consulta.                                 |
| Triagem     | Grau de risco definido na triagem.                              |
| Diagnostico | Diagnostico padrão preenchido pelo médico ao final da consulta. |

### Tabela "MEDICOS"
| Coluna        | Descrição                                  |
| ------------- | ------------------------------------------ |
| Nome          | Nome completo do médico.                   |
| Sexo          | Descrição do sexo M ou F.                  |
| Especialidade | Nome da especialização do médico.          |
| CRM           | Registro do conselho regional de medicina. |
| Telefone      | Número de telefone particular do médico.   |

## Tabela "INTERNACOES"
| Coluna      | Descrição                                       |
| ----------- | ----------------------------------------------- |
| ID_Consulta | ID único referente a consulta realizada.        |
| Quarto      | Número do quarto onde paciente ficou internado. |
| Entrada     | Datetime registrado no momento da internação.   |
| Saida       | Datetime registrado na saída do paciente.       |

## Tabela "HOSPITAL"
