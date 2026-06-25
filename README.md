# Projeto-Banco-Loja
# Projeto Banco de Dados Loja

## Descrição

Este projeto foi desenvolvido utilizando SQL e MySQL com o objetivo de criar um banco de dados relacional para gerenciamento de clientes, produtos e pedidos.

## Estrutura do Banco

### Tabela Clientes

Armazena informações dos clientes.

### Tabela Produtos

Armazena informações dos produtos disponíveis.

### Tabela Pedidos

Armazena os pedidos realizados pelos clientes, relacionando clientes e produtos através de chaves estrangeiras.

## Relacionamentos

* Um cliente pode realizar vários pedidos.
* Um produto pode estar presente em vários pedidos.
* A tabela pedidos utiliza chaves estrangeiras para relacionar as tabelas clientes e produtos.

## Consultas

Foram utilizadas consultas JOIN para relacionar as tabelas e exibir:

* Cliente, produto, quantidade e data do pedido.
* Valor total de cada pedido.

## Tecnologias Utilizadas

* SQL
* MySQL
* GitHub
* VS Code

CREATE DATABASE loja;
USE loja;

CREATE TABLE clientes (
    id_cliente INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100),
    email VARCHAR(100),
    telefone VARCHAR(20)
);
CREATE TABLE produtos (
    id_produto INT PRIMARY KEY AUTO_INCREMENT,
    nome_produto VARCHAR(100),
    preco DECIMAL(10,2)
);
CREATE TABLE pedidos (
    id_pedido INT PRIMARY KEY AUTO_INCREMENT,
    id_cliente INT,
    id_produto INT,
    quantidade INT,
    data_pedido DATE,
    FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente),
    FOREIGN KEY (id_produto) REFERENCES produtos(id_produto)
);
INSERT INTO clientes (nome, email, telefone)
VALUES
('Maria Eliana', 'maria@email.com', '(85)99999-1111'),
('Ana Alice', 'ana@email.com', '(85)99999-2222'),
('João Silva', 'joao@email.com', '(85)99999-3333');


INSERT INTO produtos (nome_produto, preco)
VALUES
('Notebook', 3500.00),
('Mouse Gamer', 120.00),
('Teclado Mecânico', 250.00);

INSERT INTO pedidos (id_cliente, id_produto, quantidade, data_pedido)
VALUES
(1, 1, 1, '2026-06-25'),
(2, 2, 2, '2026-06-25'),
(3, 3, 1, '2026-06-25');

SELECT
c.nome AS Cliente,
p.nome_produto AS Produto,
pe.quantidade,
pe.data_pedido
FROM pedidos pe
INNER JOIN clientes c
ON pe.id_cliente = c.id_cliente
INNER JOIN produtos p
ON pe.id_produto = p.id_produto;

SELECT
c.nome,
p.nome_produto,
(pe.quantidade * p.preco) AS Total
FROM pedidos pe
INNER JOIN clientes c
ON pe.id_cliente = c.id_cliente
INNER JOIN produtos p
ON pe.id_produto = p.id_produto;
