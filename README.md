//// Trabalho realizado para materia de Banco de Dados da Fatec. O projeto consiste em criar um banco para uma biblioteca, inserir dados e criar consultas. 

INSERT INTO `ALUNOS` (`NOME`)
VALUES (‘Nicole Bla Bla Bla de Andrade’),
(‘Guilherme Bla Bla Bla Oliveira’);




DROP DATABASE IF EXISTS `biblioteca`;
CREATE DATABASE `biblioteca`;
USE `biblioteca`;



CREATE TABLE `biblioteca`.`aluguel` (
id INT NOT NULL AUTO_INCREMENT,
data_inicio DATE NOT NULL,
data_devolucao DATE NOT NULL,
valor_total FLOAT NOT NULL,
pago_sim_nao INT NOT NULL,
PRIMARY KEY (`id`)
);



CREATE TABLE `biblioteca`.`cliente` (
id INT NOT NULL AUTO_INCREMENT,
nome_cliente VARCHAR(100) NOT NULL,
cpf VARCHAR(11) UNIQUE NOT NULL,
endereco VARCHAR(100) NOT NULL,
 PRIMARY KEY (`id`)
);



CREATE TABLE `biblioteca`.`formas_de_pagamento` (
id INT NOT NULL AUTO_INCREMENT,
pix INT NOT NULL,
dinheiro INT NOT NULL,
cartao_debito INT NOT NULL,
cartao_credito INT NOT NULL,
PRIMARY KEY (`id`)
);



CREATE TABLE `biblioteca`.`genero` (
id INT NOT NULL AUTO_INCREMENT,
titulo_genero VARCHAR(40) NOT NULL,
PRIMARY KEY (`id`)
);



CREATE TABLE `biblioteca`.`autor` (
id INT NOT NULL AUTO_INCREMENT,
nome_autor VARCHAR(100) NOT NULL,
data_nascimento DATE NOT NULL,
nacionalidade VARCHAR(50) NOT NULL,
PRIMARY KEY (`id`)
);
 
 
CREATE TABLE `biblioteca`.`livro` (
id INT NOT NULL AUTO_INCREMENT,
titulo_livro VARCHAR(150) NOT NULL,
data_publicacao DATE NOT NULL,
valor_livro FLOAT NOT NULL,
genero_id INT NOT NULL,
autor_id INT NOT NULL,
PRIMARY KEY (`id`),
FOREIGN KEY (`genero_id`) REFERENCES `genero` (`id`),
FOREIGN KEY (`autor_id`) REFERENCES `autor` (`id`)
);



CREATE TABLE `biblioteca`.`livro_aluguel` (
id INT NOT NULL AUTO_INCREMENT,
aluguel_id INT NOT NULL,
livro_id INT NOT NULL,
PRIMARY KEY (`id`),
FOREIGN KEY (`aluguel_id`) REFERENCES `aluguel` (`id`),
FOREIGN KEY (`livro_id`) REFERENCES `livro` (`id`)
);



CREATE TABLE `biblioteca`.`cliente_aluguel` (
id INT NOT NULL AUTO_INCREMENT,
aluguel_id INT NOT NULL,
cliente_id INT NOT NULL,
PRIMARY KEY (`id`),
FOREIGN KEY (`aluguel_id`) REFERENCES `aluguel` (`id`),
FOREIGN KEY (`cliente_id`) REFERENCES `cliente` (`id`)
);



CREATE TABLE `biblioteca`.`formasdepagamento_aluguel` (
id INT NOT NULL AUTO_INCREMENT,
formas_de_pagamento_id INT NOT NULL,
aluguel_id INT NOT NULL,
PRIMARY KEY (`id`),
FOREIGN KEY (`aluguel_id`) REFERENCES `aluguel` (`id`),
FOREIGN KEY (`formas_de_pagamento_id`) REFERENCES `formas_de_pagamento` (`id`)
);


\\ Inserindo os dados.

INSERT INTO `cliente` (`nome_cliente`, `cpf`, `endereco`)
VALUES ('John Andrew Winchester', '78945612321', 'Rua dos Pactos com olhos amarelos, 50'),
('Mary Campbell Winchester', '56478912336', 'Rua dos queimados, 80'),
('Dean Campbell Winchester', '75751236428', 'Rua dos mimicos, 500'),
('Samuel Campbell Winchester', '78451236912', 'Rua da velhice, 90'),
('Bob Singer', '12365478923', 'Rua dos leviatã, 50'),
('Pamela Bakers', '78945612391', 'Rua das cegas, 89'),
('Jody Mills', '12358964789', 'Rua dos xerifes, 78'),
('Jack Clain Winchester', '65412398756', 'Rua dos neflins, 96'),
('Jessica Moore', '986325417', 'Rua das namoradas, 54'),
('Kevin Tran', '45636978912', 'Rua dos profetas, 63'),
('Bella Talbot', '235897469', 'Rua das ladras, 171');



INSERT INTO `livro` (`titulo_livro`, `data_publicacao`, `valor_livro`, `genero_id`, `autor_id`)
VALUES
('A mulher de branco', '2000-05-10', '50.90', '5', '1'),
('Missao dolorosa', '2005-08-11', '99.99', '2', '1'),
('Local Misterioso', '2009-10-06', '51.90', '2', '2'),
('Todo mundo odeia Meta-historia', '2011-10-05', '59.90', '3', '2'),
('Route 666', '2005-10-11', '20.99', '1', '5'),
('Sem saida', '1999-06-10', '15.90', '3', '4'),
('Croatoan', '1985-12-10', '15.90', '2', '3'),
('Caminhante noturno', '2001-02-02', '58.99', '1', '4'),
('Carry On', '2020-12-11', '100.00', '1', '2'),
('Dom casmurro', '1899-10-10', '55.90', '4', '5');



INSERT INTO `genero` (`titulo_genero`)
VALUES
('Romance'),
('Fantasia'),
('Poesia'),
('Literatura'),
('Terror');



INSERT INTO `autor` (`nome_autor`, `data_nascimento`, `nacionalidade`)
VALUES
(`Chuck Religion`, `23-05-185`, `Americano`),
('Metatron Escrivan', '1992-06-10', 'Irlandes'),
('Charlie Bradbury', '2003-05-08', 'Americana'),
('Clair Novak', '1975-11-04', 'Canadense'),
('Castiel Angelos', '1974-10-06', 'Mexicano'),
('Machado de Assis', '1899-01-12', 'Brasileiro');



INSERT INTO `aluguel` (`data_inicio`, `data_devolucao`, `valor_total`, `pago_sim_nao`)
VALUES 
('2023-10-15', '2023-11-10', '5.90', 1),
('2023-12-01', '2023-12-04', '6.90', 0),
('2023-11-05', '2023-12-01', '14.00', 1),
('2023-04-04', '2023-04-20', '5.90', 1),
('2022-11-10', '2023-11-10', '80.00', 1),
('2023-11-10', '2023-12-01', '6.90', 1),
('2023-10-01', '2023-12-05', '16.90', 0),
('2023-11-02', '2023-12-02', '8.90', 1),
('2023-11-04', '2023-12-04', '13.90', 0),
('2023-11-15', '2023-12-05', '5.90', 1);


INSERT INTO `formas_de_pagamento`(`pix`, `dinheiro`, `cartao_debito`, `cartao_credito`)
VALUES ('1', '2', '3', '4');



INSERT INTO `livro_aluguel` (`aluguel_id`, `livro_id`)
VALUES 
('1', '2'),
('2', '5'),
('1', '3'),
('3', '2'),
('5', '5'),
('1', '5'),
('4', '4'),
('7', '1'),
('8', '2');


INSERT INTO `formasdepagamento_aluguel` (`formas_de_pagamento_id`, `aluguel_id`)
VALUES
('1', '1'),
('3', '2'),
('1', '3'),
('3', '4'),
('1', '5'),
('4', '6'),
('2', '7'),


INSERT INTO `cliente_aluguel` (`aluguel_id`, `cliente_id`)
VALUES
('1', '1'),
('2', '2'),
('2', '1'),
('1', '2'), 
('3', '4'),
('5', '6'),
('6', '2'),
('4', '8'),
('7', '5'),
('9', '1');








Consultas:

01- Seleciona todos os clientes e seus endereços:
SELECT nome_cliente, endereco
FROM cliente;

02- Seleciona todos os livros ordenados por titulo:
SELECT titulo_livro FROM livro ORDER BY titulo_livro;

03- Seleciona todos os autores da nacionalidade brasileira:
SELECT * FROM autor WHERE nacionalidade = 'Brasileiro';

04- Seleciona todas as datas de devolução do maior para o menor:
SELECT * FROM aluguel ORDER BY data_devolucao DESC;

05- Seleciona os livros publicados após 2000 ordenados por data de publicação:
SELECT titulo_livro, data_publicacao
FROM livro
WHERE data_publicacao > '2000-01-01'
ORDER BY data_publicacao;

06- Mostrar os cinco livros mais caros:
SELECT titulo_livro, valor_livro
FROM livro
ORDER BY valor_livro DESC
LIMIT 5;

07- Calcular o valor médio dos aluguéis pagos:
SELECT AVG(valor_total) AS media_valor
FROM aluguel
WHERE pago_sim_nao = 'sim';

08- Calcular o valor total de todos os livros agrupados por gênero:
SELECT genero.titulo_genero, SUM(livro.valor_livro) AS total_valor
FROM genero
JOIN livro ON genero.id = livro.genero_id
GROUP BY genero.titulo_genero;

09 Lista de livros por gênero:
SELECT livro.titulo_livro, genero.titulo_genero
FROM livro
JOIN genero ON livro.genero_id = genero.id
ORDER BY genero.titulo_genero, livro.titulo_livro;

10 Mostrar os clientes que não alugaram:
SELECT cliente.*
FROM cliente
LEFT JOIN cliente_aluguel ON cliente.id = cliente_aluguel.cliente_id
WHERE cliente_aluguel.id IS NULL;

11 Livros publicados após 2010:
SELECT *
FROM livro
WHERE data_publicacao > '2010-01-01';

12 Mostrar todos os clientes que pagaram em dinheiro:
SELECT aluguel.data_inicio, aluguel.valor_total
FROM aluguel
JOIN formasdepagamento_aluguel ON aluguel.id = formasdepagamento_aluguel.aluguel_id
WHERE formasdepagamento_aluguel.formas_de_pagamento_id = 2;

13- Listar todos os livros de um determinado autor:
SELECT livro.titulo_livro, autor.nome_autor
FROM livro
JOIN autor ON livro.autor_id = autor.id
WHERE autor.nome_autor = 'Chuck Religion';

14- Quantidade de alugueis por cliente: 
SELECT cliente.nome_cliente, COUNT(aluguel.id) AS total_alugueis
FROM cliente
LEFT JOIN cliente_aluguel ON cliente.id = cliente_aluguel.cliente_id
LEFT JOIN aluguel ON cliente_aluguel.aluguel_id = aluguel.id
GROUP BY cliente.nome_cliente;

15- Listar os livros alugados por um cliente especifico: 
SELECT cliente.nome_cliente, livro.titulo_livro
FROM cliente
JOIN cliente_aluguel ON cliente.id = cliente_aluguel.cliente_id
JOIN aluguel ON cliente_aluguel.aluguel_id = aluguel.id
JOIN livro_aluguel ON aluguel.id = livro_aluguel.aluguel_id
JOIN livro ON livro_aluguel.livro_id = livro.id
WHERE cliente.nome_cliente = 'John Andrew Winchester';

16-Listar um top 5 dos clientes que mais alugaram livros: 
SELECT cliente.nome_cliente, COUNT(aluguel.id) AS total_alugueis
FROM cliente
LEFT JOIN cliente_aluguel ON cliente.id = cliente_aluguel.cliente_id
LEFT JOIN aluguel ON cliente_aluguel.aluguel_id = aluguel.id
GROUP BY cliente.nome_cliente
ORDER BY total_alugueis DESC
LIMIT 5;

17-Listar os livros alugados por cliente e ordenados pela data de inicio: 
SELECT cliente.nome_cliente, livro.titulo_livro, aluguel.data_inicio
FROM cliente
JOIN cliente_aluguel ON cliente.id = cliente_aluguel.cliente_id
JOIN aluguel ON cliente_aluguel.aluguel_id = aluguel.id
JOIN livro_aluguel ON aluguel.id = livro_aluguel.aluguel_id
JOIN livro ON livro_aluguel.livro_id = livro.id
ORDER BY cliente.nome_cliente, aluguel.data_inicio;

18 Encontrar clientes que já fizeram mais de 1 aluguel:
SELECT cliente.nome_cliente, COUNT(cliente_aluguel.cliente_id) AS quantidade_alugueis
FROM cliente
JOIN cliente_aluguel ON cliente.id = cliente_aluguel.cliente_id
GROUP BY cliente.nome_cliente
HAVING quantidade_alugueis > 1;


19- Calcular o valor total recebido em cada forma de pagamento
SELECT formas_de_pagamento.*, SUM(formasdepagamento_aluguel.dinheiro) AS total_dinheiro
FROM formas_de_pagamento
JOIN formasdepagamento_aluguel ON formas_de_pagamento.id = formasdepagamento_aluguel.formas_de_pagamento_id
GROUP BY formas_de_pagamento.id;

20 – Encontrar alugueis pagos com cartão de credito
SELECT aluguel.*, formas_de_pagamento.cartao_credito
FROM aluguel
JOIN formasdepagamento_aluguel ON aluguel.id = formasdepagamento_aluguel.aluguel_id
JOIN formas_de_pagamento ON formasdepagamento_aluguel.formas_de_pagamento_id = formas_de_pagamento.id
WHERE formas_de_pagamento.cartao_credito > 0;

21- Listar os clientes que não pagaram ainda:
SELECT cliente.nome_cliente, aluguel.valor_total
FROM cliente
JOIN cliente_aluguel ON cliente.id = cliente_aluguel.cliente_id
JOIN aluguel ON cliente_aluguel.aluguel_id = aluguel.id
WHERE aluguel.pago_sim_nao = 0;

22- Visualizar o ID do aluguel:
SELECT id FROM aluguel;

23- Visualizar o ID do cliente:
SELECT id FROM cliente;
