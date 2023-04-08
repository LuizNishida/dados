create database clinica;
use clinica;
create table ambulatorio (
	nroa int primary key auto_increment,
    andar int not null,
    capacidade smallint
);
create table medico(
     codm int primary key auto_increment,
     nome varchar(40) not null,
     idade smallint not null,
     especialidade char(20),
     cpf varchar(11) unique,
     cidade varchar(30),
     fk_nroa int,
     foreign key(fk_nroa) references ambulatorio(nroa)
);

create table paciente (
	codp int primary key auto_increment,
    nome varchar(40) not null,
    idade smallint not null,
    cidade varchar(30),
    cpf varchar(11) unique,
    doenca varchar(40)
);
create table consulta(
	num_consulta int primary key auto_increment,
    data_consulta date,
    hora time,
    fk_codp int,
    foreign key(fk_codp) references paciente(codp),
    fk_codm int,
    foreign key(fk_codm) references medico(codm)
);
create table funcionario (
	codf int primary key auto_increment,
    nome varchar(40) not null,
    idade smallint,
    cidade varchar(30),
    salario decimal(10,2),
    cpf varchar(11) unique,
    cargo char(20)
);

describe ambulatorio;
insert into ambulatorio (nroa, andar, capacidade)
						values(1,1,30),
                        (2,1,50),
                        (3,2,40),
                        (4,2,25),
                        (5,2,55);
select * from ambulatorio;
describe medico;
insert into medico (nome, idade, especialidade, cpf, cidade, fk_nroa)
					values('Joao', 40, 'ortopedia', 10000100000, 'Florianópolis',1),
                    ('Maria', 42, 'traumatologia', 10000110000, 'Blumenau', 2),
                    ('Pedro', 51, 'pediatria', 11000100000, 'São José', 2),
                    ('Carlos', 28, 'ortopedia', 11000110000,'Joinville',4),
                    ('Marcia', 33, 'neurologia', 11000111000,'Biguacu',3);

describe paciente;
insert into paciente (nome, idade, cidade, cpf, doenca)
					values('Ana', 20, 'Florianopolis', 20000200000, 'gripe'),
                    ('Paulo', 24, 'Palhoca', 200000220000, 'fratura'),
                    ('Lucia', 30, 'Biguacu', 22000200000, 'tendinite'),
                    ('Carlos', 28, 'Joinville', 11000110000, 'sarampo');
select * from paciente;
describe funcionario;
insert into funcionario (nome, idade, cidade, salario,cpf)
					values('Rita', 32, 'Sao Jose', 1200, 20000100000),
                    ('Maria', 55, 'Palhoca', 1220, 30000110000),
                    ('Caio', 45, 'Florianopolis', 1100, 41000100000),
                    ('Carlos', 44, 'Florianopolis', 1200, 51000110000),
                    ('Paulo', 33, 'Florianopolis', 2500, 61000111000);
describe consulta;
insert into consulta (data_consulta, hora, fk_codm, fk_codp)
					values('2006/06/12', '14:00', 1 , 1),
                    ('2006/06/13', '10:00', 1, 4),
                    ('2006/06/13', '09:00', 2, 1),
                    ('2006/06/13', '11:00', 2, 2),
                    ('2006/06/14', '14:00', 2, 3),
                    ('2006/06/14', '17:00', 2, 4),
                    ('2006/06/19', '18:00', 3, 1),
                    ('2006/06/12', '10:00', 3, 3),
                    ('2006/06/19', '13:00', 3, 4),
                    ('2006/06/20', '13:00', 4, 4),
                    ('2006/06/22', '19:30', 4, 4);
select*from funcionario;
select*from paciente;
update paciente set cidade = 'Ilhota' where codp = '2';
select*from paciente;
select*from consulta;
update consulta set hora = '12:00', data_consulta = '2006/07/04' where num_consulta = '2';
select*from consulta;
update paciente set idade = 21, doenca = 'cancer' where codp = '1';
update consulta set hora_consulta = '14:30' where num_consulta = '9';
alter table funcionario add column fk_nroa int;
alter table funcionario add constraint foreign key (fk_nroa) references ambulatorio(nroa);
alter table funcionario drop column cargo;
delete from funcionario where codf =4;
delete from consulta where num_consulta = 11;
delete from paciente where doenca = 'cancer' or idade <10;
delete from medico where cidade = 'Biguacu' or cidade = 'Palhoca';



