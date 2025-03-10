
```sql
CREATE DATABASE tecinternet_escola_viana CHARACTER SET utf8mb4; 

CREATE TABLE professores (
    id_professor INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome_professor VARCHAR(255) NOT NULL,
    area_de_atuacao ENUM('design', 'desenvolvimento', 'infra') NOT NULL,
    curso_id INT NOT NULL -- chave estrangeira
);


CREATE TABLE cursos (
    id_curso INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome_do_curso VARCHAR(255) NOT NULL,
    carga_horaria INT NOT NULL,
    professor_id INT NULL -- chave estrangeira
);

CREATE TABLE alunos (
    id_aluno INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome_aluno VARCHAR(255) NOT NULL,
    data_de_nascimento DATE NOT NULL,
    nota1 DECIMAL(5,2) NOT NULL,
    nota2 DECIMAL(5,2) NOT NULL,
    curso_id INT NOT NULL -- chave estrangeira
);
```

```sql
ALTER TABLE professores 
    ADD CONSTRAINT fk_professores_cursos
    FOREIGN KEY (curso_id) REFERENCES cursos(id_curso);

ALTER TABLE cursos
    ADD CONSTRAINT fk_cursos_professores
    FOREIGN KEY (professor_id) REFERENCES professores(id_professor);

ALTER TABLE alunos 
    ADD CONSTRAINT fk_alunos_cursos
    FOREIGN KEY (curso_id) REFERENCES cursos(id_curso);
```

```sql
INSERT INTO cursos(nome_do_curso, carga_horaria)
VALUE (
    'Front-End',
    40
),
(
    'Back-End',
    80
),
(
    'UX/UI Design',
    30
),
(
    'Figma',
    10
),
(
    'Redes de Computadores',
    100
);

INSERT INTO professores(nome_professor, area_de_atuacao, curso_id)
VALUE (
    'Jon Oliva',
    'infra',
    5
),
(
    'Lemmy Kilmister',
    'design',
    4
),
(
    'Neil Peart',
    'design',
    3
),
(
    'Ozzy Osbourne',
    'desenvolvimento',
    2
),
(
    'David Gilmour',
    'desenvolvimento',
    1
);
```

```sql
UPDATE cursos SET professor_id = 5
WHERE id_curso = 1;

UPDATE cursos
SET professor_id = CASE
    WHEN id_curso = 2 THEN 4
    WHEN id_curso = 3 THEN 3
    WHEN id_curso = 4 THEN 2
    WHEN id_curso = 5 THEN 1

    ELSE professor_id 
END
WHERE id_curso IN (2, 3, 4, 5);
```

```sql
INSERT INTO alunos (nome_aluno, data_de_nascimento, nota1, nota2, curso_id) 
VALUES (
    'Ana Souza', 
    '04/12/1998', 
    8.5,
    7.0,  
    1
),
(
    'Carlos Pereira', 
    '02/20/1995', 
    6.5, 
    5.8, 
    3
),
(
    'Julia Silva', 
    '11/15/2000', 
    9.2, 
    8.7, 
    2
),
(
    'Miguel Santos', 
    '03/10/1997', 
    7.8,
    6.4, 
    4),
(
    'Lucas Oliveira', 
    '09/25/1996', 
    6.0,
    7.2,
    5
),
(
    'Mariana Costa', 
    '12/05/1999', 
    10.0, 
    9.5, 
    1
),
(
    'Felipe Almeida', 
    '01/18/2001', 
    5.5, 
    4.8, 
    3
),
(
    'Beatriz Martins', 
    '06/30/1998', 
    7.0, 
    6.9, 
    2
),
(
    'Rodrigo Gomes', 
    '08/10/1995', 
    6.8, 
    7.4, 
    4
),
(
    'Larissa Oliveira', 
    '05/22/1997', 
    9.3, 
    8.4, 
    5
);

UPDATE alunos
SET data_de_nascimento = CASE
    WHEN id_aluno = 1 THEN '1998-12-04'
    WHEN id_aluno = 2 THEN '1995-02-20'
    WHEN id_aluno = 3 THEN '2000-11-15'
    WHEN id_aluno = 4 THEN '1997-03-10'
    WHEN id_aluno = 5 THEN '1996-09-25'
    WHEN id_aluno = 6 THEN '1999-12-05'
    WHEN id_aluno = 7 THEN '2001-01-18'
    WHEN id_aluno = 8 THEN '1998-06-30'
    WHEN id_aluno = 9 THEN '1995-08-10'
    WHEN id_aluno = 10 THEN '1997-05-22'
END
WHERE id_aluno IN (1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

```