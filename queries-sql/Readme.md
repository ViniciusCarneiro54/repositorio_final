### Consultas SQL

Depois do banco criado e os dados devidamente inseridos, fiz algumas querys que deixo aqui o arquivo (.sql), para conexão utilizei o DBeaver, é bem simples a configuração e é possível encontras tutoriais facilmente.

_Observação: A conexão com o banco é permitida somente pelo meu endereço IP, e o mesmo será excluido após finalização do projeto._

<img src="https://github.com/ViniciusCarneiro54/repositorio_final/blob/main/img/DBeaver.png" width="610" height="555" />

1. Consultas realizadas por um médico especifico em Agosto de 2023:
  
```sql
SELECT * FROM CONSULTAS 
WHERE ID_MEDICO = 2 AND (YEAR(DATA) = 2023 AND MONTH(DATA) = 8); 
```

2. Pacientes que tiveram diagnóstico de COVID-19 em suas consultas:

```sql
SELECT C.ID_CONSULTA, C.ID_PACIENTE, P.NOME, C.DIAGNOSTICO, C.DATA
FROM CONSULTAS AS C
LEFT JOIN PACIENTES AS P ON C.ID_PACIENTE = P.ID_PACIENTE
WHERE C.DIAGNOSTICO LIKE '%COVID%';
```

3. Quantidade de consultas de cada paciente + idade calculada:

```sql
SELECT C.ID_PACIENTE, P.NOME, P.SEXO, TIMESTAMPDIFF(YEAR, P.NASCIMENTO, CURDATE()) AS IDADE, COUNT(*) AS QTD_CONSULTAS
FROM CONSULTAS AS C
LEFT JOIN PACIENTES AS P ON C.ID_PACIENTE = P.ID_PACIENTE 
GROUP BY ID_PACIENTE
ORDER BY QTD_CONSULTAS DESC;
```

4. Pacientes que possuem sangue tipo O- (doador universal) e idade menor que 35:

```sql
SELECT NOME, TELEFONE, EMAIL, TP_SANGUE, TIMESTAMPDIFF(YEAR, NASCIMENTO, CURDATE()) AS IDADE 
FROM PACIENTES 
HAVING TP_SANGUE = 'O-' AND IDADE < 35
ORDER BY IDADE;
```

4. Pacientes com idade maior que 30 que ficaram internados mais de 5 dias:

```sql
SELECT I.ID_INTERNACAO, I.ENTRADA, C.ID_CONSULTA, C.DIAGNOSTICO, P.NOME, 
	DATEDIFF(SAIDA, ENTRADA) AS DIAS_INTERNADOS, 
	TIMESTAMPDIFF(YEAR, P.NASCIMENTO, CURDATE()) AS IDADE
FROM INTERNACOES AS I
LEFT JOIN CONSULTAS AS C ON I.ID_CONSULTA = C.ID_CONSULTA
LEFT JOIN PACIENTES AS P ON C.ID_PACIENTE = P.ID_PACIENTE
HAVING DIAS_INTERNADOS > 5 AND IDADE > 30
ORDER BY DIAS_INTERNADOS DESC, IDADE DESC;
```

5. Quantidade de consultas de acordo com risco:

```sql
SELECT 
	COUNT(*) AS QTD_CONSULTAS,
	CASE 
		WHEN GRAU_RISCO = 1 THEN 'Não urgência'
		WHEN GRAU_RISCO = 2 THEN 'Pouco urgência'
		WHEN GRAU_RISCO = 3 THEN 'Urgência'
		WHEN GRAU_RISCO = 4 THEN 'Muita urgência'
		WHEN GRAU_RISCO = 5 THEN 'Emergência'
		ELSE 'Risco não fornecido'
	END AS RISCO
FROM CONSULTAS
GROUP BY RISCO
ORDER BY QTD_CONSULTAS;
```

6. Quantidade de consultas realizadas por cada médico:

```sql
SELECT C.ID_MEDICO, M.NOME, M.ESPECIALIDADE, COUNT(*) AS QTD_CONSULTAS
FROM CONSULTAS AS C
INNER JOIN MEDICOS AS M ON C.ID_MEDICO = M.ID_MEDICO 
GROUP BY C.ID_MEDICO 
ORDER BY QTD_CONSULTAS DESC;
```

7. Média de idade dos pacientes de acordo com quantidade de dias internados:

```sql
SELECT
	DATEDIFF(SAIDA, ENTRADA) AS DIAS_INTERNADOS, 
	ROUND(AVG(TIMESTAMPDIFF(YEAR, P.NASCIMENTO, CURDATE()))) AS MEDIA_IDADE
FROM INTERNACOES AS I
LEFT JOIN CONSULTAS AS C ON I.ID_CONSULTA = C.ID_CONSULTA
LEFT JOIN PACIENTES AS P ON C.ID_PACIENTE = P.ID_PACIENTE
GROUP BY DIAS_INTERNADOS
ORDER BY DIAS_INTERNADOS;
```
8.

```sql
```
9.

```sql
```
10.

```sql
```
