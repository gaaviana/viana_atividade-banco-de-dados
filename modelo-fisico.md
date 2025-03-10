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