# Angel
pro2
AQUI PASAME LA BASE DE DATOS




/*
SQLyog Job Agent v13.1.1 (64 bit) Copyright(c) Webyog Inc. All Rights Reserved.


MySQL - 11.1.1-MariaDB : Database - hospital2
*********************************************************************
*/

/*!40101 SET NAMES utf8 */;

/*!40101 SET SQL_MODE=''*/;

/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;
CREATE DATABASE /*!32312 IF NOT EXISTS*/`hospital2` /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci */;

USE `hospital2`;

/*Table structure for table `agenda` */

DROP TABLE IF EXISTS `agenda`;

CREATE TABLE `agenda` (
  `id_agenda` smallint(6) NOT NULL,
  `fecha` date NOT NULL,
  `hora` datetime NOT NULL,
  `paciente` smallint(8) NOT NULL,
  `doctor` smallint(6) NOT NULL,
  `estado` varchar(100) NOT NULL,
  PRIMARY KEY (`id_agenda`),
  KEY `age_pacie` (`paciente`),
  KEY `age_doc` (`doctor`),
  CONSTRAINT `age_doc` FOREIGN KEY (`doctor`) REFERENCES `doctores` (`id_doctor`),
  CONSTRAINT `age_pacie` FOREIGN KEY (`paciente`) REFERENCES `pacientes` (`ci_paciente`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

/*Data for the table `agenda` */

/*Table structure for table `barrios` */

DROP TABLE IF EXISTS `barrios`;

CREATE TABLE `barrios` (
  `id_barrio` smallint(6) NOT NULL,
  `barrio` varchar(200) NOT NULL,
  `ciudad` smallint(6) NOT NULL,
  PRIMARY KEY (`id_barrio`),
  KEY `barr_ciud` (`ciudad`),
  CONSTRAINT `barr_ciud` FOREIGN KEY (`ciudad`) REFERENCES `ciudades` (`id_ciudad`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

/*Data for the table `barrios` */

insert  into `barrios` values 
(1,'Virgen de la Paz',1),
(2,'Salvador del mundo',1),
(3,'Maria Auxiliadora',2);

/*Table structure for table `ciudades` */

DROP TABLE IF EXISTS `ciudades`;

CREATE TABLE `ciudades` (
  `id_ciudad` smallint(6) NOT NULL,
  `ciudad` varchar(200) NOT NULL,
  PRIMARY KEY (`id_ciudad`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

/*Data for the table `ciudades` */

insert  into `ciudades` values 
(1,'belen'),
(2,'concepcion'),
(3,'Horqueta');

/*Table structure for table `doctores` */

DROP TABLE IF EXISTS `doctores`;

CREATE TABLE `doctores` (
  `id_doctor` smallint(6) NOT NULL,
  `nombre` varchar(100) NOT NULL,
  `apellido` varchar(100) NOT NULL,
  `especialidad` smallint(6) NOT NULL,
  `estado` varchar(100) NOT NULL,
  `sexo` varchar(100) NOT NULL,
  PRIMARY KEY (`id_doctor`),
  KEY `doc_espec` (`especialidad`),
  CONSTRAINT `doc_espec` FOREIGN KEY (`especialidad`) REFERENCES `especialidades` (`id_especialidad`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

/*Data for the table `doctores` */

insert  into `doctores` values 
(1,'Jose','Pere',1,'Inactivo','Masculino'),
(2,'juana','perez',1,'Activo','Femenino');

/*Table structure for table `enfermedades` */

DROP TABLE IF EXISTS `enfermedades`;

CREATE TABLE `enfermedades` (
  `id_enfermedad` smallint(6) NOT NULL,
  `enfermedad` varchar(200) NOT NULL,
  PRIMARY KEY (`id_enfermedad`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

/*Data for the table `enfermedades` */

insert  into `enfermedades` values 
(1,'viruela'),
(2,'dengue');

/*Table structure for table `enfermedades_base` */

DROP TABLE IF EXISTS `enfermedades_base`;

CREATE TABLE `enfermedades_base` (
  `paciente` smallint(8) NOT NULL,
  `enfermedad` smallint(6) NOT NULL,
  PRIMARY KEY (`paciente`,`enfermedad`),
  KEY `enf_enf` (`enfermedad`),
  CONSTRAINT `enf_enf` FOREIGN KEY (`enfermedad`) REFERENCES `enfermedades` (`id_enfermedad`),
  CONSTRAINT `enf_pac` FOREIGN KEY (`paciente`) REFERENCES `pacientes` (`ci_paciente`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

/*Data for the table `enfermedades_base` */

/*Table structure for table `especialidades` */

DROP TABLE IF EXISTS `especialidades`;

CREATE TABLE `especialidades` (
  `id_especialidad` smallint(6) NOT NULL,
  `especialidad` varchar(200) NOT NULL,
  PRIMARY KEY (`id_especialidad`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

/*Data for the table `especialidades` */

insert  into `especialidades` values 
(1,'PEDIATRA'),
(2,'Cardiologo');

/*Table structure for table `pacientes` */

DROP TABLE IF EXISTS `pacientes`;

CREATE TABLE `pacientes` (
  `ci_paciente` smallint(8) NOT NULL,
  `nombre` varchar(100) NOT NULL,
  `apellido` varchar(100) NOT NULL,
  `fecha_nac` date NOT NULL,
  `telefono` varchar(100) NOT NULL,
  `direccion` varchar(300) NOT NULL,
  `barrio` smallint(6) NOT NULL,
  `historia` varchar(300) DEFAULT NULL,
  `sexo` varchar(100) NOT NULL,
  PRIMARY KEY (`ci_paciente`),
  KEY `pac_barr` (`barrio`),
  CONSTRAINT `pac_barr` FOREIGN KEY (`barrio`) REFERENCES `barrios` (`id_barrio`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

/*Data for the table `pacientes` */

/*Table structure for table `turnos` */

DROP TABLE IF EXISTS `turnos`;

CREATE TABLE `turnos` (
  `id_turno` int(11) NOT NULL,
  `doctor` smallint(6) NOT NULL,
  `dia` varchar(100) NOT NULL,
  `hora_inicial` datetime NOT NULL,
  `hora_final` datetime NOT NULL,
  PRIMARY KEY (`id_turno`),
  UNIQUE KEY `turn_doc` (`doctor`,`dia`,`hora_inicial`),
  CONSTRAINT `turn_doc` FOREIGN KEY (`doctor`) REFERENCES `doctores` (`id_doctor`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

/*Data for the table `turnos` */

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

