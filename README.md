# Prova Trimestral 02: Banco de dados

**Desenvolvimento de Aplicações Web -- 2016**

**Professor: João Eduardo Montandon**

**Valor: 10 Pontos**


## Olimpíadas Rio 2016 (Valor: 06 Pontos)

Você foi convocado para ajudar na implementação do sistema que irá exibir o quadro de medalhas dos Jogos Olímpicos Rio 2016. Enquanto sua equipe faz o levantamento das funcionalidades existentes, você ficou a cargo da implementação do Banco de Dados que irá armazenar as informações do sistema.

Seu banco de dados deverá ser capaz de armazenar as seguintes informações:

* As modalidades existentes
* As competições ofertadas
* Os países participantes
* Os atletas participantes
* Os medalhistas em cada competição

Ainda, visando uma maior integridade e escalabilidade dos dados, foi repassado a você algumas restrições no que diz respeito à estrutura do banco:

* Toda competição está necessariamente atrelada a uma modalidade.
* Os atletas pertencem necessariamente a um país e a uma modalidade.
* Uma competição tem vários medalhistas, enquanto um atleta pode ser medalhista em várias competições.

Com base nas informações acima, você deverá implementar:

1. **O Diagrama Entidade Relacionamento (03 pontos)**
2. **O Diagrama Relacional (03 pontos)**


## Engenharia Reversa (04 pontos)

Um sujeito suspeito entra em contato com você pedindo ajuda na obtenção da estrutura de um sistema de informação. Para isso ele lhe enviou o arquivo com os scripts DDL de organização dos dados do sistema. **Com base no script enviado**, faça a engenharia reversa e **obtenha o Diagrama Relacional** do sistema.

```
-- -----------------------------------------------------
-- Schema serasa
-- -----------------------------------------------------
CREATE SCHEMA `serasa`;

USE `serasa` ;

-- -----------------------------------------------------
-- Table estados
-- -----------------------------------------------------
CREATE TABLE `estados` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `nome` VARCHAR(45) NOT NULL,
  
  PRIMARY KEY (`id`)
);

-- -----------------------------------------------------
-- Table cidades
-- -----------------------------------------------------
CREATE TABLE `cidades` (
  `id` INT NOT NULL AUTO_INCREMENT ,
  `nome` VARCHAR(45) NOT NULL ,
  `estados_id` INT NOT NULL ,
  
  PRIMARY KEY (`id`),
  CONSTRAINT `fk_cidades_estados1`
    FOREIGN KEY (`estados_id`)
    REFERENCES `estados` (`id`)
);


-- -----------------------------------------------------
-- Table `clientes`
-- -----------------------------------------------------
CREATE TABLE `clientes` (
  `id` INT NOT NULL AUTO_INCREMENT ,
  `cpf` VARCHAR(45) NOT NULL ,
  `nome` VARCHAR(45) NOT NULL ,
  `cidades_id` INT NOT NULL ,
  
  PRIMARY KEY (`id`),
  CONSTRAINT `fk_clientes_cidades1`
    FOREIGN KEY (`cidades_id`)
    REFERENCES `cidades` (`id`)
 );


-- -----------------------------------------------------
-- Table `estabelecimentos`
-- -----------------------------------------------------
CREATE TABLE `estabelecimentos` (
  `id` INT NOT NULL AUTO_INCREMENT ,
  `nome` VARCHAR(45) NOT NULL ,
  `cidades_id` INT NOT NULL ,
  
  PRIMARY KEY (`id`),
  CONSTRAINT `fk_estabelecimentos_cidades1`
    FOREIGN KEY (`cidades_id`)
    REFERENCES `cidades` (`id`)
 );


-- -----------------------------------------------------
-- Table `dividas`
-- -----------------------------------------------------
CREATE TABLE `dividas` (
  `clientes_id` INT NOT NULL ,
  `estabelecimentos_id` INT NOT NULL ,
  `valor` DECIMAL(10,2) NOT NULL ,
  
  PRIMARY KEY (`clientes_id`, `estabelecimentos_id`)  ,
  CONSTRAINT `fk_clientes_has_estabelecimentos_clientes`
    FOREIGN KEY (`clientes_id`)
    REFERENCES `clientes` (`id`),
  CONSTRAINT `fk_clientes_has_estabelecimentos_estabelecimentos1`
    FOREIGN KEY (`estabelecimentos_id`)
    REFERENCES `estabelecimentos` (`id`)
);
```