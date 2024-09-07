create database empresafinal;

create table funcionarios (
id int not null auto_increment,
nome varchar(30),
cargo varchar(50) default 'Indefinido',
salario int,
admitido date,
departamento_id int,
primary key (id),
foreign key(departamento_id) references departamentos(id)
) default charset = utf8mb4;

insert into funcionarios values
(default, 'Jailson', 'Operador de maquinas', '5750', '2021-05-23', '1'),
(default, 'Cleiton', 'Vendedor', '2950', '2019-03-25', '2'),
(default, 'Jeniffer', default, '3700', '2017-09-19', null),
(default, 'Thomas', 'Caixa', '2300',  '2023-12-30', '2'),
(default, 'Matilda', default, '4500', '2022-05-21', null),
(default, 'Jonas', 'Ti', '5500', '2019-03-21', '3'),
(default, 'Hedilson', 'Marketing', '5750', '2015-12-21', '4'),
(default, 'Mendes', 'Ti', '6700', '2020-12-23', '3'),
(default, 'Thomas', 'Caixa', '2300',  '2023-12-30', '2'),
(default, 'José', default, '4500', '2022-05-21', null),
(default, 'Cleide', 'Ti', '5500', '2019-03-21', '3'),
(default, 'Marcio', 'Marketing', '5750', '2015-12-21', '4'),
(default, 'Carmen', 'Ti', '6700', '2020-12-23', '3');

drop table funcionarios;

create table departamentos (
id int not null auto_increment,
nome varchar(30),
primary key(id)
) default charset = utf8mb4;

insert into departamentos values
(default, 'Transporte'),
(default, 'Vendas'),
(default, 'Ti'),
(default, 'Marketing');

drop table departamentos;

-- 1
select f.nome
from funcionarios as f;

-- 2
select f.nome, f.cargo
from funcionarios as f
where f.departamento_id = 2;

-- 3 - Nao sei
select d.nome
from departamentos as d;

-- 4
select f.nome, f.departamento_id
from funcionarios as f;

-- 5
select f.nome, f.salario
from funcionarios as f
where f.salario > 5000;

-- 6
select f.nome, f.departamento_id
from funcionarios as f
where f.departamento_id = 3 || f.departamento_id = 4;

-- 7 nao funciono
select f.nome, f.admitido
from funcionarios as f
where admitido > 2020-01-01 && admitido < 2022-12-31;

-- 8
select f.nome
from funcionarios as f
where f.nome like 'M%';

-- 9
select f.nome, f.cargo
from funcionarios as f
where f.cargo = 'Indefinido';

-- 10 nao sei

-- 11
select max(salario) from funcionarios;

-- 13 
select avg(salario) from funcionarios;

-- 14 
update funcionarios
set cargo = 'Analista de Sistemas'
where id = '5';

-- 15

delete from funcionarios
where id = '10';
select * from funcionarios;


-- 2 - Carros

create table carrosproprietarios (
id int not null auto_increment,
marca varchar(30),
modelo varchar(50),
ano year,
proprietario_id int,
primary key (id),
foreign key (proprietario_id) references proprietarioscarros(id)
) default charset = utf8mb4; 

insert into carrosproprietarios values
(default, 'Toyota', 'Hilux', '2020', '1'),
(default, 'Mazda', 'MX-8', '2010', '2'),
(default, 'Honda', 'Civic', '1996', '3'),
(default, 'Mitsubishe', 'Eclipse', '2005', '4'),
(default, 'Mazda', 'RX-7', '1999', '5');

drop table carrosproprietarios;


create table proprietarioscarros (
id int not null auto_increment,
nome varchar(30),
idade int,
primary key(id)
) default charset = utf8mb4;

insert into proprietarioscarros values
(default, 'Carlinho', '24'),
(default, 'Roberto', '52'),
(default, 'Rodrigo', '43'),
(default, 'Joao', '28'),
(default, 'Jaison', '19');

drop table proprietarioscarros;

-- 16
select c.marca, c.modelo 
from carrosproprietarios as c;

-- 17 nao sei
select p.nome, c.modelo
from carrosproprietarios as c, proprietarioscarros as p;

-- 18
select c.modelo
from carrosproprietarios as c
where c.ano < 2010;

-- 19
select p.nome, c.marca
from  proprietarioscarros as p
join carrosproprietarios as c
on p.id = c.proprietario_id
where c.marca = 'toyota';

-- 20 nao sei
select sum(marca) from carrosproprietarios;

-- 21 Nao sei

-- 22
update carrosproprietarios
set ano = '2015'
where id = '3';

-- 23 Nao tem id 7 entao vai o 5 mesmo :p
delete from carrosproprietarios
where id = 5;

select * from carrosproprietarios;


-- Computador
create table computadoresusuarios (
id int not null auto_increment,
marca varchar(30),
modelo varchar(30),
processador varchar(30),
memoria_ram int,
usuario_id int,
primary key(id),
foreign key(usuario_id) references usuarioscomputadores(id)
) default charset = utf8mb4;

insert into computadoresusuarios values
(default, 'Dell', 'XPS 13', ' i3-1005G1', '16', '1'),
(default, 'Acer', 'Aspire 5', ' i5 10210U', '4', '2'),
(default, 'Acer', 'Predator Helios 300', 'i7-7700HQ', '32', '3'),
(default, 'Positivo', 'Stilo Q232B', 'x5 Z8350', '2', '4'),
(default, 'Dell', 'Inspiron 15', 'i9-13900HX', '16', '5');

drop table computadoresusuarios;

create table usuarioscomputadores (
id int not null auto_increment,
nome varchar(30),
email varchar(50),
primary key(id)
) default charset = utf8mb4;

insert into usuarioscomputadores values
(default, 'Jhonatan', 'jhonatan@gmail.com'),
(default, 'Luis', 'luis@gmail.com'),
(default, 'Felipe', 'felipe@gmail.com'),
(default, 'Jorge', 'jorge@gmail.com'),
(default, 'Gabriel', 'gabriel@gmail.com');

drop table usuarioscomputadores;

-- 24
select c.modelo, c.processador
from computadoresusuarios as c;

-- 25
select u.nome, c.modelo
from usuarioscomputadores as u
inner join computadoresusuarios c
on u.id = c.usuario_id;

-- 26
select c.marca, c.modelo, c.memoria_ram
from computadoresusuarios as c
where c.memoria_ram > 8;

-- 27
select u.nome, c.marca
from usuarioscomputadores as u
inner join computadoresusuarios c
on u.id = c.usuario_id
where c.marca = 'Dell';

-- 28 nao sei

-- 29 nao sei

-- 30 nao tem id 6 via o 5
delete from computadoresusuarios
where id = '5';

select * from computadoresusuarios;


-- Celular

create table celulares (
id int not null auto_increment,
marca varchar(30),
modelo varchar(30),
sistema_operacional varchar(30),
proprietario_id int,
primary key(id),
foreign key(proprietario_id) references proprietariocelular(id)
) default charset = utf8mb4;

insert into celulares values
(default, 'Apple', 'iPhone 15 Pro', 'iOS', '1'),
(default, 'Samsung', 'Galaxy S24 Ultra', 'Android', '2'),
(default, 'Google', 'Pixel 8 Pr', 'Android', '3'),
(default, 'OnePlus', '11T', 'Android', '4'),
(default, 'Xiaomi', 'Mi 13 Pro', 'Android', '5'),
(default, 'Sony', 'Xperia 1 V', 'Android', '6'),
(default, 'Motorola', 'Edge 40 Pro', 'Android', '7'),
(default, 'Oppo', 'Find X6 Pr', 'Android', '8'),
(default, 'Huawei', 'P60 Pro', 'Android', '9'),
(default, 'Realme', 'GT 3', 'Android', '10');

drop table celulares;

create table proprietariocelular (
id int not null auto_increment,
nome varchar(30),
primary key(id)
) default charset = utf8mb4;

insert into proprietariocelular values
(default, 'Ana'),
(default, 'João'),
(default, 'Maria'),
(default, 'Pedro'),
(default, 'Sofia'),
(default, 'Lucas'),
(default, 'Beatriz'),
(default, 'Rafael'),
(default, 'Clara'),
(default, 'Migue');

drop table proprietarioscelular;

-- 32
select c.marca, c.modelo
from celulares as c;

-- 33
select p.nome, c.modelo
from proprietariocelular as p
inner join celulares c
on c.proprietario_id = p.id;

-- 34
select c.modelo, c.sistema_operacional
from celulares as c
where c.sistema_operacional = 'Android';

-- 35
select p.nome, c.marca
from proprietariocelular as p
inner join celulares c
on c.proprietario_id = p.id
where c.marca = 'Samsung';

-- 36 nao sei

-- 37 nao sei

-- 38
update celulares
set sistema_operacional = 'iOS'
where id = 4;

select * from celulares;

-- 39
delete from celulares
where id = 9;



-- Redes Sociais
create table usuarios_redes (
id int not null auto_increment,
nome varchar(30),
email varchar(50),
primary key(id)
) default charset = utf8mb4;

insert into usuarios_redes values
(default, 'Laura', 'laura@gmail.com'),
(default, 'Daniel', 'daniel@gmail.com'),
(default, 'Mariana', 'mariana@gmail.com'),
(default, 'Tiago', 'tiago@gmail.com'),
(default, 'Beatriz', 'beatriz@gmail.com'),
(default, 'Bruno', 'bruno@gmail.com'),
(default, 'Carolina', 'carolina@gmail.com'),
(default, 'Andréa', 'andrea@gmail.com'),
(default, 'Henrique', 'henrique@gmail.com'),
(default, 'Vitória', 'vitoria@gmail.com');

drop table usuarios_redes;

create table post (
id int not null auto_increment,
conteudo varchar(50),
data_publicacao date,
usuario_id int,
primary key (id),
foreign key (usuario_id) references usuarios_redes(id)
) default charset = utf8mb4;

insert into post values
(default, 'Produtividade', '2024-09-10', '1'),
(default, 'Evento', '2024-09-15', '2'),
(default, 'Saúde', '2024-09-20', '3'),
(default, 'Finanças', '2024-09-25', '4'),
(default, 'Moda', '2021-09-30', '5'),
(default, 'Estresse', '2024-10-05', '6'),
(default, 'Viagem', '2022-10-10', '7'),
(default, 'Alimentação', '2024-10-15', '8'),
(default, 'Cultivo', '2024-10-20', '9'),
(default, 'Trabalho', '2020-10-25', '10');

drop table post;

create table comentarios (
id int not null auto_increment,
conteudo varchar(100),
data_publicacao date, 
post_id int,
usuario_id int,
primary key (id),
foreign key (post_id) references post(id),
foreign key (usuario_id) references usuarios_redes(id)
) default charset = utf8mb4;

insert into comentarios values
(default, 'Adorei a ideia! Muito útil e bem explicado.', '2024-09-10', '1', '1'),
(default, 'Ótimo trabalho, continue assim!', '2024-09-15', '2', '2'),
(default, 'Isso realmente fez a diferença para mim. Obrigado!', '2024-09-20', '3', '3'),
(default, 'Interessante! Nunca tinha pensado por esse ângulo.', '2024-09-25', '4', '4'),
(default, 'Concordo totalmente. Muito bom!', '2021-09-30', '5', '5'),
(default, 'Muito inspirador. Vou tentar aplicar essas dicas.', '2024-10-05', '6', '6'),
(default, 'Simples e direto ao ponto. Excelente!', '2022-10-10', '7', '7'),
(default, 'Achei muito esclarecedor. Valeu!', '2024-10-15', '8', '8'),
(default, 'Excelente conteúdo! Aprendi algo novo hoje.', '2024-10-20', '9', '9'),
(default, 'Gostei bastante! Será útil para futuros projetos.', '2020-10-25', '10', '10');

drop table comentarios;

-- 40
select u.nome, u.email
from usuarios_redes as u;

-- 41
select p.conteudo, p.data_publicacao
from post as p;

-- 42
select u.nome, p.conteudo
from usuarios_redes as u
inner join post p
on p.usuario_id = u.id;

-- 43
select p.conteudo, c.conteudo
from post as p
inner join comentarios as c
on c.usuario_id = p.id;

-- 44
select p.conteudo
from post as p
where p.data_publicacao > 2023-01-01;

-- 45
select c.conteudo
from comentarios as c
where id = '3';

-- 46 nao sei

-- 47 nao sei

-- 48

update post
set conteudo = 'Conteudo ataulizado!!!'
where id = '3';

select p.conteudo
from post as p;

-- 49
delete c.conteudo
from comentarios as c
where id = '1';
