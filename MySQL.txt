create database if not exists HumanFriends;
use HumanFriends;

create table type_of_animals
(
id int not null auto_increment primary key,
name varchar(45) not null
);

create table class
(
id int not null auto_increment primary key,
name varchar(45) not null,
type_of_animals_id int,
foreign key (type_of_animals_id) references type_of_animals (id)
on delete cascade on update cascade
);

create table command
(
id int not null auto_increment primary key,
name varchar(30) not null
);

create table animals
(
id int not null auto_increment primary key, 
class_id int not null,
foreign key (class_id) references class (id) 
on delete cascade on update cascade,
name varchar(45) not null,
date_of_birth date not null,
command_id int not null,
foreign key (command_id) references command (id) 
on delete cascade on update cascade

);


select *
from animals a 

insert into type_of_animals (name) 
values 
('Домашние животные'),
('Вьючные животные');

insert into class (name, type_of_animals_id)
values
('Собака', 1),
('Кошка', 1),
('Хомяк', 1),
('Лошадь', 2),
('Верблюд', 2),
('Осел', 2);

insert into command (name)
values
('Сидеть'),
('Стоять'),
('Лежать'),
('Дай лапу'),
('Голос'),
('Место'),
('Фу'),
('Гулять');

insert into animals (class_id, name, date_of_birth, command_id)
values
(1, 'Ракета', '2023-06-28', 1),
(2, 'Муся', '2018-11-05', 4),
(3, 'Степа', '2024-08-01', 6),
(1, 'Тиша', '2015-07-07', 2),
(2, 'Шурик', '2023-03-01', 8),
(4, 'Каштан', '2019-06-08', 5),
(4, 'Гонзалис', '2020-10-07', 3),
(5, 'Тимофей', '2016-09-17', 6),
(6, 'Иа', '2023-11-11', 2),
(5, 'Пако', '2022-10-13', 7);

delete from animals where class_id = 5;

create table Horse_donkey as
select * from animals where class_id = 4
union 
select * from animals where class_id = 6;

select *
from Horse_donkey;

create table young_animals as
select *,
datediff(curdate(), date_of_birth) div 31 as age
from animals
where date_add(date_of_birth, interval 1 year) < curdate() 
and date_add(date_of_birth, interval 3 year) > curdate();

select *
from young_animals;

