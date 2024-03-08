# Proyecto BASES DE DATOS

JEFFERSON DARIO BELTRAN LASPRILLA - Campuslands

### Creacion de Base de Datos

CREATE DATABASE bd_universidad;
 
### Creacion de tablas

CREATE TYPE sexo AS ENUM ('H','M');
CREATE TYPE tipo AS ENUM ('alumno','profesor');

CREATE TABLE persona (
	id SERIAL PRIMARY KEY,
	nif VARCHAR(9),
	nombre VARCHAR(25),
	apellido1 VARCHAR(50),
	apellido2 VARCHAR(50),
	ciudad VARCHAR(25),
	direccion VARCHAR(50),
	telefono VARCHAR(9),
	fecha_nacimiento DATE,
	sexo sexo,
	tipo tipo
	);

CREATE TABLE departamento (
	id SERIAL PRIMARY KEY,
	nombre VARCHAR(50)
	);
	
CREATE TABLE profesor (
   	id_profesor INTEGER PRIMARY KEY REFERENCES persona(id),
    	id_departamento INTEGER REFERENCES departamento(id)
	);
	
	
CREATE TABLE curso_escolar (
    	id SERIAL PRIMARY KEY,
    	anyo_inicio INTEGER CHECK (anyo_inicio >= 1900 AND anyo_inicio <= 9999),
    	anyo_fin INTEGER CHECK (anyo_fin >= 1900 AND anyo_fin <= 9999)
	);

CREATE TABLE grado (
	id SERIAL PRIMARY KEY,
	nombre VARCHAR(100)
	);


CREATE TYPE tipo_asignatura AS ENUM ('básica','obligatoria','optativa');
CREATE TABLE asignatura (
	id SERIAL PRIMARY KEY,
	nombre VARCHAR(100),
	creditos FLOAT,
	tipo tipo_asignatura,
	curso INTEGER,
	cuatrimestre INTEGER,
	id_profesor INTEGER REFERENCES profesor(id_profesor),
	id_grado INTEGER REFERENCES grado(id)
	);

CREATE TABLE alumno_se_matricula_asignatura (
	id_alumno INTEGER REFERENCES persona(id),
	id_asignatura INTEGER REFERENCES asignatura(id),
	id_curso_escolar INTEGER REFERENCES curso_escolar(id)
	);
	
