~~~psql

create table clientes(
  id_clientes serial PRIMARY KEY,
  nome VARCHAR(30) not NULL,
  sobrenome VARCHAR(100) not NULL,
  email VARCHAR(150) not NULL,
  telefone VARCHAR(20)
);

insert into clientes(nome, sobrenome, email, telefone)
VALUES
('Devison', 'Santana', 'devison@proz.com', '(71) 99412-0000'),
('Emerson', 'Penelli', 'emerson@proz.com', '(11) 97425-6345'),
('Deividson', 'Coelho', 'deividson@proz.com', '(31) 97345-1092'),
('Gabriel', 'Hacker', 'gabriel@proz.com', '(31) 97638-2634'),
('Alvaro', 'Santos do Js', 'alvinhu@proz.com', '(35) 97830-4672');

CREATE TABLE produtos(
  id_produtos serial PRIMARY KEY,
  nome VARCHAR(80) not NULL,
  descricao VARCHAR(100) not NULL,
  preco FLOAT not NULL
);

insert into produtos(nome, descricao, preco)
VALUES
('Tablet', 'EX DISPLAY : MSI Pro 16 Flex-036AU 15.6 MULTITOUCH All-In-On...', 499.00),
('Charlie', 'EX DISPLAY : MSI Pro 16 Flex-036AU 15.6 MULTITOUCH All-In-On...', 499.00),
('Bravo', 'EX DISPLAY : MSI Pro 16 Flex-036AU 15.6 MULTITOUCH All-In-On...', 499.00),
('Alpha', 'EX DISPLAY : MSI Pro 16 Flex-036AU 15.6 MULTITOUCH All-In-On...', 999.00),
('Zulu', 'EX DISPLAY : MSI Pro 16 Flex-036AU 15.6 MULTITOUCH All-In-On...', 499.00),
('inspiron 15', 'Desfrute de um desempenho ágil, porém silencioso, com processadores Intel® Core™...', 2300.00),
('Mesa Gamer', 'MESA GAMER MANCER BEHOLDER, 136CM, RGB, PRETO, MCR-BHR-RGB', 1058.81);

CREATE TABLE vendas(
  id_vendas serial PRIMARY KEY,
  fk_id_clientes int not NULL,
  fk_id_produtos int not NULL,
  CONSTRAINT fk_clientes foreign key (fk_id_clientes) REFERENCES clientes(id_clientes),
  constraint fk_produtos foreign key (fk_id_produtos) REFERENCES produtos(id_produtos)
);

insert into vendas(fk_id_clientes, fk_id_produtos)
VALUES
(3, 6),
(2, 7),
(5, 7);

create TABLE informacoes_produto(
  id_informacoes_produto serial PRIMARY KEY,
  descricao VARCHAR(500) not NULL,
  fk_id_produtos int not NULL,
  CONSTRAINT fk_produtos foreign key (fk_id_produtos) REFERENCES produtos(id_produtos)
);

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

create TABLE imagens_produto(
  id_imagens_produto serial PRIMARY key,
  url VARCHAR(256) not NULL,
  fk_id_produtos int not NULL,
  CONSTRAINT fk_produtos foreign key (fk_id_produtos) REFERENCES produtos(id_produtos)
);

insert into imagens_produto(url, fk_id_produtos)
VALUES
('img//produtos/dell1.jpg', 6),
('img//produtos/dell2.jpg', 6),
('img//produtos/dell3.jpg', 6),
('img//produtos/mesaGamer1.jpg', 7),
('img//produtos/mesaGamer2.jpg', 7),
('img//produtos/mesaGamer3.jpg', 7);

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