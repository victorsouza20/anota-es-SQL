
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,  -- número único automático
    username VARCHAR(100) NOT NULL,        -- nome obrigatório
    password VARCHAR(100) NOT NULL,        -- senha obrigatória
    privilege INTEGER NOT NULL              -- nível de acesso
);


<!-- # CREATE TABLE Serve para criar uma nova tabela no banco.
# IF NOT EXISTS Evita erro caso a tabela já tenha sido criada antes.
# INTEGER Tipo de dado para números inteiros.
# VARCHAR(100) Tipo de dado para texto com limite de caracteres.
# NOT NULL Não permite deixar vazio.
# PRIMARY KEY É o identificador único de cada registro.
# AUTOINCREMENT O banco gera o número sozinho. -->



INSERT INTO users (id, username, password, privilege)
VALUES (2, 'victor', '12312321','1');

<!-- # INSERT Palavra-chave que significa inserir. É usada para adicionar um novo registro no banco de dados.
# INTO Significa dentro de. Indica em qual tabela os dados serão inseridos.
# VALUES Palavra-chave que indica os valores que serão inseridos nas colunas, na mesma ordem. (1, 'joao', '123456', 1) -->



SELECT * FROM !nome_da_tabela! ORDER BY username ASC;

<!-- SELECT * Significa selecionar todas as colunas da tabela.
FROM users Indica que os dados serão buscados da tabela chamada users.
ORDER BY username Organiza (ordna) os resultados com base na coluna username.
ASC (Ascending) Define que a ordenação será em ordem crescente, ou seja: -->

ORDER BY username DESC;
<!-- ordem decrescente, -->

ORDER BY privilege ASC, username DESC;

<!-- privilege: menor → maior
username: Z → A (dentro do mesmo privilege) -->



INSERT OR IGNORE INTO users (username, password, privilege)
VALUES ('victor', '12312321', 1);
<!-- IGNORE é usado para dizer ao banco: “Se acontecer algum erro de duplicidade ou violação de regra, não pare o comando — apenas ignore essa linha.” -->


//////////////////////////////////////////////////////////////////////////////////////////////////////////////


SELECT – Buscar dados
SELECT * FROM users;

<!-- # SELECT → comando para buscar dados
# * (asterisco) → significa todas as colunas
# FROM → indica de qual tabela
# users → nome da tabela
# ; → fim do comando -->



Buscar colunas específicas
SELECT username, privilege FROM users;

<!-- # SELECT username, privilege → buscar apenas essas colunas
# FROM users → da tabela users -->



Buscar com condição (WHERE)
SELECT * FROM users
WHERE username = 'joao';

<!-- SELECT * → todas as colunas -->
<!-- # FROM users → da tabela users
# WHERE → significa onde (filtro/condição)
# username = 'joao' → apenas registros onde o username seja "joao" -->


//////////////////////////////////////////////////////////////////////////////////////////////////////////////


UPDATE users
SET password = 'nova_senha'
WHERE id = 1;

<!-- # UPDATE Significa atualizar dados.
# users Nome da tabela onde a alteração será feita.
# SET Significa definir. É usado para indicar qual coluna será alterada e o novo valor.
# password = 'nova_senha' Está dizendo:Altere o valor da coluna password para nova_senha.
# WHERE Define a condição (qual registro será alterado).
# id = 1 (A alteração será feita apenas no usuário cujo id é 1.)
# ; (Indica o fim do comando.) -->



//////////////////////////////////////////////////////////////////////////////////////////////////////////////

DELETE FROM users
WHERE id = 2;

OU 

DELETE FROM users
WHERE nome = 'teste';

<!-- # DELETE → comando para excluir dados
# FROM → de qual tabela
# users → nome da tabela
# WHERE → condição (qual registro será apagado)
# id = 2 → apaga apenas o usuário com id igual a 2 -->


DELETE FROM users;

<!-- # DELETE FROM users → remove todos os registros da tabela
# Não tem WHERE, então não há filtro -->


//////////////////////////////////////////////////////////////////////////////////////////////////////////////

DROP TABLE nome_da_tabela;

<!-- DROP TABLE : O comando DROP TABLE apaga a tabela inteira do banco de dados. -->


//////////////////////////////////////////////////////////////////////////////////////////////////////////////

SELECT * FROM users WHERE privilege = 1;
SELECT * FROM users WHERE id > 3;
SELECT * FROM users WHERE username LIKE 'jo%';
SELECT * → buscar todas as colunas

<!-- FROM users → da tabela users
WHERE → condição (filtro)
privilege = 1 → apenas usuários com nível de permissão 1
id > 3 (O símbolo > significa maior que.)
= igual
> maior que
< menor que
>= maior ou igual
<= menor ou igual
<> ou != diferente

LIKE → usado para buscar padrões de texto
jo = começo do texto
% = qualquer sequência de caracteres

Curingas do LIKE
% → qualquer quantidade de caracteres
_ → apenas um caractere
Exemplos:
'jo%' → começa com jo
'%ao' → termina com ao
'%o%' → contém a letra o -->


SELECT * FROM users
ORDER BY username ASC;

<!-- ASC = crescente
DESC = decrescente

SELECT * Busca todas as colunas.
FROM users Da tabela users.
ORDER BY Significa ordenar por. É usado para organizar os resultados.
username A coluna que será usada para fazer a ordenação.
ASC Significa Ascending (ordem crescente).
; Fim do comando. -->



SELECT * FROM users
LIMIT 5;

<!-- SELECT * Busca todas as colunas.
FROM users Da tabela users.
LIMIT 5 Limita o resultado para apenas 5 registros.
; Fim do comando. -->


//////////////////////////////////////////////////////////////////////////////////////////////////////////////

CREATE TABLE clientes (
    id_cliente INT PRIMARY KEY,
    nome VARCHAR(100)
);

CREATE TABLE pedidos (
    id_pedido INT PRIMARY KEY,
    id_cliente INT,
    valor DECIMAL(10,2),
    FOREING KEY (id_cliente) REFERENCES clientes(id_cliente)
);


<!-- FOREING KEY (FK) é um campo (ou conjunto de campos) em uma tabela que faz referência à Primary Key (PK) de outra tabela. Ou seja:
PRIMARY KEY → identifica unicamente um registro na própria tabela
FOREING KEY → conecta uma tabela à outra -->
<!-- REFERENCES Significa literalmente:“Este campo depende daquele campo em outra tabela.” Ela é usada junto com FOREIGN KEY. -->



ON DELETE CASCADE
ON DELETE SET NULL
ON DELETE NO ACTION

<!-- ON DELETE : Define o que acontece quando o registro da tabela pai é deletado. -->
<!-- ON DELETE CASCADE : Se o registro pai for apagado, os registros filhos também são apagados automaticamente. Exemplo: Se apagar um cliente, todos os pedidos dele também serão apagados. -->
<!-- ON DELETE SET NULL : Quando o pai é apagado, o campo da tabela filha vira NULL. -->
<!-- ON DELETE RESTRICT : Impede que o registro pai seja apagado se houver registros filhos relacionados. -->
<!-- NO ACTION : verifica ao final da transação. -->




ON UPDATE
ON UPDATE CASCADE
ON UPDATE SET NULL
ON UPDATE RESTRICT
ON UPDATE NO ACTION

<!-- ON UPDATE : Define o que acontece quando o valor da chave primária do pai é alterado. -->
<!-- ON UPDATE CASCADE : Se a chave do pai mudar, o valor é atualizado automaticamente na tabela filha. -->
<!-- ON UPDATE SET NULL : Se o valor da chave mudar, o campo da tabela filha vira NULL -->
<!-- ON UPDATE RESTRICT : Impede a atualização da chave se houver registros filhos. -->
<!-- ON UPDATE NO ACTION : Funciona quase igual ao RESTRICT (verificação ao final da transação). -->


CREATE TABLE pedidos (
    id_pedido INT PRIMARY KEY,
    id_cliente INT,
    FOREIGN KEY (id_cliente)
    REFERENCES clientes(id_cliente)
    ON DELETE CASCADE
    ON UPDATE CASCADE
);

//////////////////////////////////////////////////////////////////////////////////////////////////////////////


<!-- data_pagamento DATE (isso na parte de criar a tabela) -->
INSERT INTO Pagamento (data_pagamento)
VALUES ('2026-02-28');

<!-- DATE: é um tipo usado para armazenar datas -->



peso FLOAT
valor DECIMAL(10,2)

<!-- FLOAT é um número com casas decimais aproximadas. -->
<!-- DECIMAL é um número com casas decimais exatas. -->


//////////////////////////////////////////////////////////////////////////////////////////////////////////////

SEMANA 2

SELECT Aluno.nome, Plano.nome
FROM Aluno
INNER JOIN Plano
ON Aluno.id_plano = Plano.id_plano;
<!-- O INNER JOIN serve para juntar dados de duas tabelas que possuem relacionamento entre si. -->
<!-- O SELECT define quais colunas você quer ver no resultado. -->
<!-- O ponto (.) em Aluno.nome serve para separar o nome da tabela do nome da coluna. -->
<!-- O FROM indica de qual tabela começa a consulta. -->
<!-- O INNER JOIN serve para juntar duas tabelas. -->
<!-- O ON define a condição da ligação entre as tabelas. Aqui está dizendo: O id_plano do aluno deve ser igual ao id_plano da tabela plano -->



SELECT Aluno.nome, Plano.nome
FROM Aluno
LEFT JOIN Plano
ON Aluno.id_plano = Plano.id_plano;
<!-- O LEFT JOIN mostra todos os registros da tabela da esquerda, mesmo que não exista correspondência na outra tabela. -->
<!-- O SELECT define quais colunas você quer ver no resultado. -->
<!-- O ponto (.) em Aluno.nome serve para separar o nome da tabela do nome da coluna. -->
<!-- O FROM indica de qual tabela começa a consulta. -->
<!-- O LEFT JOIN junta a tabela Aluno com Plano, mas com uma regra importante: Ele mostra TODOS os registros da tabela da esquerda (Aluno), mesmo que não exista correspondência na tabela da direita (Plano). -->
<!-- O ON define a condição da ligação entre as tabelas. Aqui está dizendo: O id_plano do aluno deve ser igual ao id_plano da tabela plano -->



SELECT 
f.nome AS funcionario,
c.nome AS chefe
FROM Funcionarios f
LEFT JOIN Funcionarios c
ON f.id_chefe = c.id;

<!-- O SELF JOIN é quando uma tabela faz JOIN com ela mesma.Muito usado quando existe hierarquia.Exemplo: funcionários e seus chefes. -->
<!-- SELECT Aqui você está escolhendo as colunas que quer ver no resultado.
f.nome → nome do funcionário
c.nome → nome do chefe
(O AS serve para dar um apelido para a coluna no resultado.) -->
<!-- FROM: A tabela Funcionarios terá o apelido "f" -->
<!-- SELF JOIN. A tabela Funcionarios está sendo ligada com ela mesma. -->
<!-- O ON define a condição da ligação entre as tabelas. Aqui está dizendo: O id_plano do aluno deve ser igual ao id_plano da tabela plano -->




SELECT id_plano, COUNT(*) 
FROM Aluno
GROUP BY id_plano;

<!-- GROUP BY: agrupa registros para fazer cálculos. Exemplo: quantidade de alunos por plano. -->
<!-- COUNT(*) → quantos registros existem naquele plano -->
<!-- FROM: Os dados estão vindo da tabela Aluno. -->
<!-- O GROUP BY serve para agrupar registros que possuem o mesmo valor. -->



SELECT id_plano, COUNT(*) 
FROM Aluno
GROUP BY id_plano
HAVING COUNT(*) > 5;

<!-- O HAVING filtra resultados depois do GROUP BY. Enquanto o WHERE filtra linhas, o HAVING filtra grupos.Exemplo: planos com mais de 5 alunos. -->
<!-- COUNT(*) → quantos registros existem naquele plano -->
<!-- FROM: Os dados estão vindo da tabela Aluno. -->
<!-- O GROUP BY serve para agrupar registros que possuem o mesmo valor. -->
<!-- HAVING : Aqui ele está dizendo: "Mostre apenas os planos que têm mais de 5 alunos." -->




SELECT COUNT(*) 
FROM Aluno;
<!-- COUNT conta registros. -->

Exemplo com GROUP BY:

SELECT id_plano, COUNT(*) 
FROM Aluno
GROUP BY id_plano;





SELECT SUM(valor)
FROM Pagamento;

OU

SELECT id_aluno, SUM(valor)
FROM Pagamento
GROUP BY id_aluno;


<!-- A função SUM() soma todos os valores de uma coluna.Aqui ela está somando:(valor): ou seja, todos os valores da coluna valor -->
<!-- FROM :Os dados estão vindo da tabela Pagamento. -->




SELECT AVG(valor)
FROM Pagamento;

OU

SELECT id_aluno, AVG(valor)
FROM Pagamento
GROUP BY id_aluno;

<!-- AVG: O AVG calcula a média. -->
<!-- A função AVG() significa Average (média). Ela pega todos os valores da coluna valor, soma eles e depois divide pela quantidade de registros. -->
<!-- FROM Os dados estão vindo da tabela Pagamento. -->


//////////////////////////////////////////////////////////////////////////////////////////////////////////////

