# Catálogo de dados

Você pode baixar os dados em um arquivo zipado [clicando aqui](https://drive.google.com/file/d/1SK9TbDIkT3rg5runs2jQJF1vlcjTdQ0J/view?usp=sharing).

## Dados Fictícios Gerados pelo 4Devs

Os dados aqui utilizados são fictícios e gerados pelo [4Devs](https://www.4devs.com.br/), um site que oferece ferramentas para criação de dados de teste de forma rápida e conveniente. Todos os dados apresentados neste projeto são estritamente fictícios e foram gerados exclusivamente para fins de demonstração e teste!

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

Informações detalhadas das consultas já realizadas em todas unidades.
| Coluna      | Descrição                                                       |
| ----------- | --------------------------------------------------------------- |
| ID_Paciente | ID único do paciente.                                           |
| ID_Medico   | ID do médico que fez o atendimento na consulta.                 |
| ID_Hospital | ID do hospital realizado o atendimento.                         |
| Data        | Datetime do início da consulta.                                 |
| Triagem     | Grau de risco definido na triagem.                              |
| Diagnostico | Diagnostico padrão preenchido pelo médico ao final da consulta. |

### Tabela "MEDICOS"

Registro dos médicos ativos ou inativos na instituição.
| Coluna        | Descrição                                  |
| ------------- | ------------------------------------------ |
| Nome          | Nome completo do médico.                   |
| Sexo          | Descrição do sexo M ou F.                  |
| Especialidade | Nome da especialização do médico.          |
| CRM           | Registro do conselho regional de medicina. |
| Telefone      | Número de telefone particular do médico.   |

## Tabela "INTERNACOES"

Registro das internações já registradas.
| Coluna      | Descrição                                       |
| ----------- | ----------------------------------------------- |
| ID_Consulta | ID único referente a consulta realizada.        |
| Quarto      | Número do quarto onde paciente ficou internado. |
| Entrada     | Datetime registrado no momento da internação.   |
| Saida       | Datetime registrado na saída do paciente.       |

## Tabela "HOSPITAL"

Informações cadastrais referente a unidade hospitalar.

| Coluna      | Descrição                              |
| ----------- | -------------------------------------- |
| ID_Hospital | ID único da unidade hospitalar.        |
| Nome        | Nome oficial.                          |
| Descrição   | Alcunha da unidade.                    |
| Telefone    | Telefone fixo da unidade.              |
| Endereço    | Endereço onde está situado o hospital. |
| CEP         | CEP do hospital.                       |
| Cidade      | Cidade onde está localizado.           |
| Estado      | Estado onde está localizado.           |
| CNPJ        | Número de CNPJ com pontuação padrão.   |
