# PBD
Script SQL para o sistema de Check-list de tarefas:
CREATE TABLE Pessoas (
    id_pessoas serial primary key,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE Grupos (
    id_grupos serial primary key,
    nome VARCHAR(100) NOT NULL,
    descricao TEXT
);

CREATE TABLE Status (
    id_staus,
    concluida boolean NOT NULL
);


CREATE TABLE Atividades (
    id_atividades serial primary key,
    descricao VARCHAR(255) NOT NULL,
    data_criacao DATETIME DEFAULT CURRENT_TIMESTAMP,
    data_conclusao DATETIME,
    status_id INT,
    pessoa_id INT,
    grupo_id INT,
    FOREIGN KEY (status_id) REFERENCES Status(id),
    FOREIGN KEY (pessoa_id) REFERENCES Pessoas(id),
    FOREIGN KEY (grupo_id) REFERENCES Grupos(id)
);

CREATE TABLE Grupo_Pessoa (
    grupo_id INT,
    pessoa_id INT,
    PRIMARY KEY (grupo_id, pessoa_id),
    FOREIGN KEY (grupo_id) REFERENCES Grupos(id),
    FOREIGN KEY (pessoa_id) REFERENCES Pessoas(id)
);

# Explicação MER:
Uma pessoa pode ter várias atividades.
Um grupo pode ter várias atividades.
Cada atividade tem um status (concluída ou não).
Um grupo pode ter várias pessoas e uma pessoa pode fazer parte de vários grupos

# Exemplo de Insert:
-- Exemplo de inserção de pessoas
INSERT INTO Pessoas (nome, email) VALUES ('João Silva', 'joao@email.com'), ('Maria Oliveira', 'maria@email.com');

-- Exemplo de inserção de grupos
INSERT INTO Grupos (nome, descricao) VALUES ('Equipe A', 'Grupo de trabalho A'), ('Equipe B', 'Grupo de trabalho B');

-- Inserindo pessoas no grupo "Equipe A"
INSERT INTO Grupo_Pessoa (grupo_id, pessoa_id) VALUES 
(1, 1),  -- João Silva no Grupo A
(1, 2);  -- Maria Oliveira no Grupo A
