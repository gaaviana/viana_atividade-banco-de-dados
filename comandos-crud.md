# CRUD - Consultas 

1) Faça uma consulta que mostre os alunos que nasceram antes do ano 2009

```sql
SELECT data_de_nascimento FROM alunos
WHERE data_de_nascimento < '2009-01-01';
```

2) Faça uma consulta que calcule a média das notas de cada aluno e as mostre com duas casas decimais.

```sql
SELECT nome_aluno, ROUND((nota1 + nota2) / 2.0, 2) AS media_notas
FROM alunos;
```
3) Faça uma consulta que calcule o limite de faltas de cada curso de acordo com a carga horária. Considere o limite como 25% da carga horária. Classifique em ordem crescente pelo título do curso.

```sql
SELECT nome_do_curso, carga_horaria * 0.25 AS limiteFaltas FROM cursos
ORDER BY nome_do_curso;
```
4) Faça uma consulta que mostre os nomes dos professores que são somente da área "desenvolvimento".

```sql
SELECT nome_professor FROM professores
WHERE area_de_atuacao = 'desenvolvimento'; 
```
5) Faça uma consulta que mostre a quantidade de professores que cada área ("design", "infra", "desenvolvimento") possui.

```sql
SELECT area_de_atuacao, COUNT(id_professor) AS QTD FROM professores
GROUP BY area_de_atuacao;
```
6) Faça uma consulta que mostre o nome dos alunos, o título e a carga horária dos cursos que fazem.

```sql
SELECT 
    alunos.nome_aluno AS nome, 
    cursos.nome_do_curso AS curso,
    cursos.carga_horaria AS cargaHoraria
FROM alunos JOIN cursos
ON alunos.curso_id = cursos.id_curso;
```
7) Faça uma consulta que mostre o nome dos professores e o título do curso que lecionam. Classifique pelo nome do professor.

```sql
SELECT 
    professores.nome_professor AS professor,
    cursos.nome_do_curso AS curso
FROM professores JOIN cursos
ON professores.curso_id = cursos.id_curso
ORDER BY professor;
```
8) Faça uma consulta que mostre o nome dos alunos, o título dos cursos que fazem, e o professor de cada curso.

```sql
SELECT 
    alunos.nome_aluno AS alunos,
    cursos.nome_do_curso AS cursos,
    professores.nome_professor AS professor
FROM alunos JOIN cursos ON alunos.curso_id = cursos.id_curso
            JOIN professores ON cursos.professor_id = professores.id_professor;
```
9) Faça uma consulta que mostre a quantidade de alunos que cada curso possui. Classifique os resultados em ordem descrecente de acordo com a quantidade de alunos.

```sql
SELECT 
    COUNT(alunos.id_aluno) AS alunos,
    cursos.nome_do_curso AS cursos
FROM alunos JOIN cursos ON alunos.curso_id = cursos.id_curso
GROUP BY cursos.nome_do_curso;

```
10) Faça uma consulta que mostre o nome dos alunos, suas notas, médias, e o título dos cursos que fazem. Devem ser considerados somente os alunos de Front-End e Back-End. Mostre os resultados classificados pelo nome do aluno.

```sql
SELECT 
    alunos.nome_aluno AS alunos,
    alunos.nota1,
    alunos.nota2,
    ROUND((alunos.nota1 + alunos.nota2) / 2.0, 2) AS media_notas,
    cursos.nome_do_curso AS cursos
FROM alunos JOIN cursos ON alunos.curso_id = cursos.id_curso
WHERE cursos.nome_do_curso IN ('Front-End', 'Back-End') -- IN verifica valores dentro de uma lista 
ORDER BY alunos;
```
11) Faça uma consulta que altere o nome do curso de Figma para Adobe XD e sua carga horária de 10 para 15.

```sql
UPDATE cursos SET nome_do_curso = 'Adobe XD', carga_horaria = 15
WHERE id_curso = 4;
```

12) Faça uma consulta que exclua um aluno do curso de Redes de Computadores e um aluno do curso de UX/UI.

```sql
DELETE FROM alunos WHERE id_alunos IN (7, 5); -- aluno de ux 7, aluno de redes de computadores 5
```

13) Faça uma consulta que mostre a lista de alunos atualizada e o título dos cursos que fazem, classificados pelo nome do aluno.

```sql
SELECT
    alunos.nome_aluno AS alunos
    cursos.nome_do_curso 
    FROM alunos JOIN cursos ON alunos.curso_id = cursos.id_curso
    ORDER BY alunos;
```

## 🔥 DESAFIOS 🔥
1. Criar uma consulta que calcule a idade do aluno

```sql
SELECT nome_aluno,
    TIMESTAMPDIFF(YEAR, data_de_nascimento, '2025-03-12') AS idade
FROM alunos
GROUP BY nome_aluno;
-- TIMESTAMPDIFF: calcula a diferença entre as data (medida de calculo, primeira data, segunda data)
```

2. Criar uma consulta que calcule a média das notas de cada aluno e mostre somente os alunos que tiveram a média maior ou igual a 7.

```sql
SELECT nome_aluno, ROUND((nota1 + nota2) / 2.0, 2) AS media_notas 
FROM alunos
GROUP BY nome_aluno
HAVING media_notas >= 7; -- HAVING: usado para filtrar resultados
```

3. Criar uma consulta que calcule a média das notas de cada aluno e mostre somente os alunos que tiveram a média menor que 7.

```sql
SELECT nome_aluno, ROUND((nota1 + nota2) / 2.0, 2) AS media_notas 
FROM alunos
GROUP BY nome_aluno
HAVING media_notas < 7;
```

4. Criar uma consulta que mostre a quantidade de alunos com média maior ou igual a 7.

```sql
SELECT COUNT(*) AS aprovados -- COUNT(*): utilizado para contar as linhas de toda a tabela, por isso o uso do * 
FROM alunos
WHERE (nota1 + nota2) / 2 >= 7; 
```