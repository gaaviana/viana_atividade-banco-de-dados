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