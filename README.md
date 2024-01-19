# Modelo de Banco de Dados | Grupo 4

Uma breve apresentação do nosso diagrama entidade relacionamento, com ilustrações e scripts pré-definidos para criação de tabelas inserção de dados e consultas simples para melhor visualização dos dados e como se comportam e interagem entre sí por meio de chaves primarias e estrangeiras.

![Image DER model](images/Diagrama%20ER%20de%20banco%20de%20dados.png)

Para assistir o vídeo, [clique aqui.](https://youtu.be/0TY0e2T97hI)

Todos os comandos a seguir são para postgre, você pode testar os scripts usados em [SQLITE](https://sqliteonline.com/).

~~~psql

-- CRIAÇÃO DE TABELAS

create table clientes(
  id_clientes serial PRIMARY KEY,
  nome VARCHAR(30) not NULL,
  sobrenome VARCHAR(100) not NULL,
  email VARCHAR(150) not NULL,
  telefone VARCHAR(20)
);

-- INSERÇÃO DE DADOS EM CLIENTES

insert into clientes(nome, sobrenome, email, telefone)
VALUES
('Devison', 'Santana', 'devison@proz.com', '(71) 99412-0000'),
('Emerson', 'Penelli', 'emerson@proz.com', '(11) 97425-6345'),
('Deividson', 'Coelho', 'deividson@proz.com', '(31) 97345-1092'),
('Gabriel', 'Hacker', 'gabriel@proz.com', '(31) 97638-2634'),
('Alvaro', 'Santos do Js', 'alvinhu@proz.com', '(35) 97830-4672');

-- CRIAÇÃO DE UMA NOVA TABELA

CREATE TABLE produtos(
  id_produtos serial PRIMARY KEY,
  nome VARCHAR(80) not NULL,
  descricao VARCHAR(100) not NULL,
  preco FLOAT not NULL
);

-- INSERÇÃO DE DADOS EM PRODUTOS

insert into produtos(nome, descricao, preco)
VALUES
('Tablet', 'EX DISPLAY : MSI Pro 16 Flex-036AU 15.6 MULTITOUCH All-In-On...', 499.00),
('Charlie', 'EX DISPLAY : MSI Pro 16 Flex-036AU 15.6 MULTITOUCH All-In-On...', 499.00),
('Bravo', 'EX DISPLAY : MSI Pro 16 Flex-036AU 15.6 MULTITOUCH All-In-On...', 499.00),
('Alpha', 'EX DISPLAY : MSI Pro 16 Flex-036AU 15.6 MULTITOUCH All-In-On...', 999.00),
('Zulu', 'EX DISPLAY : MSI Pro 16 Flex-036AU 15.6 MULTITOUCH All-In-On...', 499.00),
('inspiron 15', 'Desfrute de um desempenho ágil, porém silencioso, com processadores Intel® Core™...', 2300.00),
('Mesa Gamer', 'MESA GAMER MANCER BEHOLDER, 136CM, RGB, PRETO, MCR-BHR-RGB', 1058.81);

-- CRIAÇÃO DE UMA NOVA TABELA

CREATE TABLE vendas(
  id_vendas serial PRIMARY KEY,
  fk_id_clientes int not NULL,
  fk_id_produtos int not NULL,
  CONSTRAINT fk_clientes foreign key (fk_id_clientes) REFERENCES clientes(id_clientes),
  constraint fk_produtos foreign key (fk_id_produtos) REFERENCES produtos(id_produtos)
);

-- INSERÇÃO DE DADOS EM VENDAS

insert into vendas(fk_id_clientes, fk_id_produtos)
VALUES
(3, 6),
(2, 7),
(5, 7);

-- CRIAÇÃO DE UMA NOVA TABELA

create TABLE informacoes_produto(
  id_informacoes_produto serial PRIMARY KEY,
  descricao VARCHAR(500) not NULL,
  fk_id_produtos int not NULL,
  CONSTRAINT fk_produtos foreign key (fk_id_produtos) REFERENCES produtos(id_produtos)
);

-- INSERÇÃO DE DADOS EM INFORMAÇÕES DO PRODUTO

INSERT into informacoes_produto(descricao, fk_id_produtos)
VALUES
('Processador - 12ª geração Intel® Core™ i3-1215U', 6),
('Memória 8GB DDR4', 6),
('Armazenamento SSD de 256GB PCIe NVMe M.2a', 6),
('Tela 15.6” Full HD (1920X1080)', 6),
('Sistema operacional Windows 11 Home', 6),
('Marca: Mancer', 7),
('Modelo: MCR-BHR-RGB', 7),
('Material: MDF e Melamina, Plástico, Metal, Vidro temperado', 7),
('Dimensões: 136 x 60 x 75 cm', 7);

-- CRIAÇÃO DE UMA NOVA TABELA

create TABLE imagens_produto(
  id_imagens_produto serial PRIMARY key,
  url VARCHAR(256) not NULL,
  fk_id_produtos int not NULL,
  CONSTRAINT fk_produtos foreign key (fk_id_produtos) REFERENCES produtos(id_produtos)
);

-- INSERÇÃO DE DADOS EM IMAGENS DO PRODUTO

insert into imagens_produto(url, fk_id_produtos)
VALUES
('img//produtos/dell1.jpg', 6),
('img//produtos/dell2.jpg', 6),
('img//produtos/dell3.jpg', 6),
('img//produtos/mesaGamer1.jpg', 7),
('img//produtos/mesaGamer2.jpg', 7),
('img//produtos/mesaGamer3.jpg', 7);
~~~

~~~psql

-- CONSULTAS PSQL

SELECT vendas.id_vendas, produtos.nome as produto, clientes.nome as cliente, informacoes_produto.descricao as descricao_produto
from vendas
inner join
produtos
on
vendas.fk_id_produtos = produtos.id_produtos
inner JOIN
clientes
ON
vendas.fk_id_clientes = clientes.id_clientes
INNER join
informacoes_produto
on
informacoes_produto.fk_id_produtos = produtos.id_produtos

~~~

~~~psql

-- CONSULTAS MENORES POR TABELA

SELECT * FROM clientes;
SELECT * FROM produtos;
SELECT * FROM vendas;
SELECT * FROM imagens_produto;
SELECT * FROM informacoes_produto;

~~~

_Este projeto não foi feito sozinho._

Membros colaboradores:

[![GitHub](https://img.shields.io/badge/deividson-000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/DeividsonOmedio)<br>
[![GitHub](https://img.shields.io/badge/emerson-000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/EmersonPenelli)<br>
[![GitHub](https://img.shields.io/badge/gabriel-000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Anbuyyy9)<br>
[![GitHub](https://img.shields.io/badge/devison-000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/DevisonSantana)<br>


<div align="center">

Agradecimento especial ao nosso tutor: Alvaro Neto ❤

</div>
