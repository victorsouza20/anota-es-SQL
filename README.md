CREATE TABLE IF NOT EXISTS alunos (
    id_aluno INTEGER PRIMARY KEY AUTOINCREMENT,
    nome VARCHAR(100) NOT NULL,
    data_nascimento DATE,
    telefone VARCHAR(15) UNIQUE NOT NULL,
    email VARCHAR(100) NOT NULL,
    faixa_atual VARCHAR(10),
    data_ultima_troca_faixa DATE,
    data_cadastro DATE DEFAULT CURRENT_DATE,
    status VARCHAR(10) NOT NULL CHECK (status IN ('Ativo', 'Inativo'))
);


INSERT OR IGNORE INTO alunos (nome, data_nascimento, telefone, email, faixa_atual, data_ultima_troca_faixa, status)
VALUES 
('Victor Hugo Assis de Souza', '2006-08-20', '61986641682', 'victorguiness.8@gmail.com', 'Preta', '2024-07-13', 'Inativo'),
('Teste', '2000-01-01', '172836721', 'teste@email.com', 'Azul', '2023-01-01', 'Ativo');




CREATE TABLE IF NOT EXISTS turma (
    id_turma INTEGER PRIMARY KEY,
	id_aluno INTEGER NOT NULL,
	horario VARCHAR(100) NOT NULL,
	FOREIGN KEY (id_aluno)
	    REFERENCES alunos (id_aluno),
	    ON DELETE CASCADE
);

INSERT INTO turma (id_turma, id_aluno, horario)
VALUES (1, 1, '20:00');

SELECT t.id_turma, a.nome, t.horario                    -- 
FROM turma AS t
JOIN alunos AS a ON t.id_aluno = a.id_aluno;



	   
	   
CREATE TABLE IF NOT EXISTS pagamento (
    id_pagamento INTEGER PRIMARY KEY AUTOINCREMENT,
    id_aluno INTEGER NOT NULL,
    valor INTEGER NOT NULL,
    data_pagamento DATE NOT NULL,
    mes_referencia DATE NOT NULL,
    status VARCHAR(10) NOT NULL CHECK (status IN ('Pago', 'Pendente', 'Atrasado')),
    FOREIGN KEY (id_aluno)
        REFERENCES alunos(id_aluno)
        ON DELETE CASCADE
);
