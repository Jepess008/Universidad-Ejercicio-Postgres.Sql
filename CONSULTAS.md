##  Proyecto BASES DE DATOS

### Consultas

#Consultas sobre una tabla

1. Devuelve un listado con el primer apellido, segundo apellido y el nombre de todos los alumnos. El listado deberá estar ordenado alfabéticamente de menor a mayor por el primer apellido, segundo apellido y nombre.

SELECT apellido1,apellido2,nombre FROM persona WHERE tipo='alumno' ORDER BY apellido1,apellido2,nombre ;
	
 apellido1 | apellido2 |  nombre  
-----------+-----------+----------
 Domínguez | Guerrero  | Antonio
 Gea       | Ruiz      | Sonia
 Gutiérrez | López     | Juan
 Heller    | Pagac     | Pedro
 Herman    | Pacocha   | Daniel
 Hernández | Martínez  | Irene
 Herzog    | Tremblay  | Ramón
 Koss      | Bayer     | José
 Lakin     | Yundt     | Inma
 Saez      | Vega      | Juan
 Sánchez   | Pérez     | Salvador
 Strosin   | Turcotte  | Ismael

2. Averigua el nombre y los dos apellidos de los alumnos que no han dado de alta su número de teléfono en la base de datos.

SELECT nombre,apellido1,apellido2 FROM persona WHERE tipo='alumno' AND telefono IS NULL;

 nombre | apellido1 | apellido2 
--------+-----------+-----------
 Pedro  | Heller    | Pagac
 Ismael | Strosin   | Turcotte

3. Devuelve el listado de los alumnos que nacieron en 1999.

SELECT nombre,apellido1,apellido2,fecha_nacimiento FROM persona 
Where tipo ='alumno' AND EXTRACT (YEAR FROM fecha_nacimiento) = 1999;

 nombre  | apellido1 | apellido2 | fecha_nacimiento 
---------+-----------+-----------+------------------
 Ismael  | Strosin   | Turcotte  | 1999-05-24
 Antonio | Domínguez | Guerrero  | 1999-02-11

4. Devuelve el listado de profesores que no han dado de alta su número de teléfono en la base de datos y además su nif termina en K.

SELECT nif,nombre,apellido1,apellido2 FROM persona WHERE tipo= 'profesor' AND nif ILIKE '%K';

    nif    |  nombre   | apellido1 | apellido2 
-----------+-----------+-----------+-----------
 10485008K | Antonio   | Fahey     | Considine
 85869555K | Guillermo | Ruecker   | Upton

5. Devuelve el listado de las asignaturas que se imparten en el primer cuatrimestre, en el tercer curso del grado que tiene el identificador 7.

SELECT * FROM asignatura WHERE cuatrimestre = 1 AND curso= 3 AND id_grado =7;

 id |                  nombre                   | creditos |    tipo     | curso | cuatrimestre | id_profesor | id_grado 
----+-------------------------------------------+----------+-------------+-------+--------------+-------------+----------
 72 | Bases moleculares del desarrollo vegetal  |      4.5 | obligatoria |     3 |            1 |             |        7
 73 | Fisiología animal                         |      4.5 | obligatoria |     3 |            1 |             |        7
 74 | Metabolismo y biosíntesis de biomoléculas |        6 | obligatoria |     3 |            1 |             |        7
 75 | Operaciones de separación                 |        6 | obligatoria |     3 |            1 |             |        7
 76 | Patología molecular de plantas            |      4.5 | obligatoria |     3 |            1 |             |        7
 77 | Técnicas instrumentales básicas           |      4.5 | obligatoria |     3 |            1 |             |        7

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#Consultas multitabla (Composición interna)

1. Devuelve un listado con los datos de todas las alumnas que se han matriculado alguna vez en el Grado en Ingeniería Informática (Plan 2015).

SELECT DISTINCT persona.nombre, persona.apellido1, persona.apellido2, grado.nombre
FROM persona
JOIN alumno_se_matricula_asignatura ON persona.id = alumno_se_matricula_asignatura.id_alumno
JOIN asignatura ON alumno_se_matricula_asignatura.id_asignatura = asignatura.id
JOIN grado ON asignatura.id_grado = grado.id
WHERE grado.nombre = 'Grado en Ingeniería Informática (Plan 2015)' AND persona.tipo = 'alumno' AND persona.sexo = 'M';

 nombre | apellido1 | apellido2 |                   nombre                    
--------+-----------+-----------+---------------------------------------------
 Inma   | Lakin     | Yundt     | Grado en Ingeniería Informática (Plan 2015)
 Irene  | Hernández | Martínez  | Grado en Ingeniería Informática (Plan 2015)
 Sonia  | Gea       | Ruiz      | Grado en Ingeniería Informática (Plan 2015)
 
 2. Devuelve un listado con todas las asignaturas ofertadas en el Grado en Ingeniería Informática (Plan 2015).
 
 id |                                 nombre                                 | creditos |                   nombre                    
----+------------------------------------------------------------------------+----------+---------------------------------------------
  1 | Álgegra lineal y matemática discreta                                   |        6 | Grado en Ingeniería Informática (Plan 2015)
  2 | Cálculo                                                                |        6 | Grado en Ingeniería Informática (Plan 2015)
  3 | Física para informática                                                |        6 | Grado en Ingeniería Informática (Plan 2015)
  4 | Introducción a la programación                                         |        6 | Grado en Ingeniería Informática (Plan 2015)
  5 | Organización y gestión de empresas                                     |        6 | Grado en Ingeniería Informática (Plan 2015)
  6 | Estadística                                                            |        6 | Grado en Ingeniería Informática (Plan 2015)
  7 | Estructura y tecnología de computadores                                |        6 | Grado en Ingeniería Informática (Plan 2015)
  8 | Fundamentos de electrónica                                             |        6 | Grado en Ingeniería Informática (Plan 2015)
  9 | Lógica y algorítmica                                                   |        6 | Grado en Ingeniería Informática (Plan 2015)
 10 | Metodología de la programación                                         |        6 | Grado en Ingeniería Informática (Plan 2015)
 11 | Arquitectura de Computadores                                           |        6 | Grado en Ingeniería Informática (Plan 2015)
 12 | Estructura de Datos y Algoritmos I                                     |        6 | Grado en Ingeniería Informática (Plan 2015)
 13 | Ingeniería del Software                                                |        6 | Grado en Ingeniería Informática (Plan 2015)
 14 | Sistemas Inteligentes                                                  |        6 | Grado en Ingeniería Informática (Plan 2015)
 15 | Sistemas Operativos                                                    |        6 | Grado en Ingeniería Informática (Plan 2015)
 16 | Bases de Datos                                                         |        6 | Grado en Ingeniería Informática (Plan 2015)
 17 | Estructura de Datos y Algoritmos II                                    |        6 | Grado en Ingeniería Informática (Plan 2015)
 18 | Fundamentos de Redes de Computadores                                   |        6 | Grado en Ingeniería Informática (Plan 2015)
 19 | Planificación y Gestión de Proyectos Informáticos                      |        6 | Grado en Ingeniería Informática (Plan 2015)
 20 | Programación de Servicios Software                                     |        6 | Grado en Ingeniería Informática (Plan 2015)
 21 | Desarrollo de interfaces de usuario                                    |        6 | Grado en Ingeniería Informática (Plan 2015)
 22 | Ingeniería de Requisitos                                               |        6 | Grado en Ingeniería Informática (Plan 2015)
 23 | Integración de las Tecnologías de la Información en las Organizaciones |        6 | Grado en Ingeniería Informática (Plan 2015)
 24 | Modelado y Diseño del Software 1                                       |        6 | Grado en Ingeniería Informática (Plan 2015)
 25 | Multiprocesadores                                                      |        6 | Grado en Ingeniería Informática (Plan 2015)
 26 | Seguridad y cumplimiento normativo                                     |        6 | Grado en Ingeniería Informática (Plan 2015)
 27 | Sistema de Información para las Organizaciones                         |        6 | Grado en Ingeniería Informática (Plan 2015)
 28 | Tecnologías web                                                        |        6 | Grado en Ingeniería Informática (Plan 2015)
 29 | Teoría de códigos y criptografía                                       |        6 | Grado en Ingeniería Informática (Plan 2015)
 30 | Administración de bases de datos                                       |        6 | Grado en Ingeniería Informática (Plan 2015)
 31 | Herramientas y Métodos de Ingeniería del Software                      |        6 | Grado en Ingeniería Informática (Plan 2015)
 32 | Informática industrial y robótica                                      |        6 | Grado en Ingeniería Informática (Plan 2015)
 33 | Ingeniería de Sistemas de Información                                  |        6 | Grado en Ingeniería Informática (Plan 2015)
 34 | Modelado y Diseño del Software 2                                       |        6 | Grado en Ingeniería Informática (Plan 2015)
 35 | Negocio Electrónico                                                    |        6 | Grado en Ingeniería Informática (Plan 2015)
 36 | Periféricos e interfaces                                               |        6 | Grado en Ingeniería Informática (Plan 2015)
 37 | Sistemas de tiempo real                                                |        6 | Grado en Ingeniería Informática (Plan 2015)
 38 | Tecnologías de acceso a red                                            |        6 | Grado en Ingeniería Informática (Plan 2015)
 39 | Tratamiento digital de imágenes                                        |        6 | Grado en Ingeniería Informática (Plan 2015)
 40 | Administración de redes y sistemas operativos                          |        6 | Grado en Ingeniería Informática (Plan 2015)
 41 | Almacenes de Datos                                                     |        6 | Grado en Ingeniería Informática (Plan 2015)
 42 | Fiabilidad y Gestión de Riesgos                                        |        6 | Grado en Ingeniería Informática (Plan 2015)
 43 | Líneas de Productos Software                                           |        6 | Grado en Ingeniería Informática (Plan 2015)
 44 | Procesos de Ingeniería del Software 1                                  |        6 | Grado en Ingeniería Informática (Plan 2015)
 45 | Tecnologías multimedia                                                 |        6 | Grado en Ingeniería Informática (Plan 2015)
 46 | Análisis y planificación de las TI                                     |        6 | Grado en Ingeniería Informática (Plan 2015)
 47 | Desarrollo Rápido de Aplicaciones                                      |        6 | Grado en Ingeniería Informática (Plan 2015)
 48 | Gestión de la Calidad y de la Innovación Tecnológica                   |        6 | Grado en Ingeniería Informática (Plan 2015)
 49 | Inteligencia del Negocio                                               |        6 | Grado en Ingeniería Informática (Plan 2015)
 50 | Procesos de Ingeniería del Software 2                                  |        6 | Grado en Ingeniería Informática (Plan 2015)
 51 | Seguridad Informática                                                  |        6 | Grado en Ingeniería Informática (Plan 2015)

3. Devuelve un listado de los profesores junto con el nombre del departamento al que están vinculados. El listado debe devolver cuatro columnas, primer apellido, segundo apellido, nombre y nombre del departamento. El resultado estará ordenado alfabéticamente de menor a mayor por los apellidos y el nombre.

SELECT persona.apellido1,persona.apellido2,persona.nombre,departamento.nombre FROM persona
JOIN profesor ON persona.id = profesor.id_profesor
JOIN departamento ON departamento.id = profesor.id_departamento
WHERE persona.tipo='profesor'
ORDER BY apellido1,apellido2,persona.nombre;

 apellido1  | apellido2  |  nombre   |       nombre       
------------+------------+-----------+--------------------
 Fahey      | Considine  | Antonio   | Economía y Empresa
 Hamill     | Kozey      | Manolo    | Informática
 Kohler     | Schoen     | Alejandro | Matemáticas
 Lemke      | Rutherford | Cristina  | Economía y Empresa
 Monahan    | Murray     | Micaela   | Agronomía
 Ramirez    | Gea        | Zoe       | Informática
 Ruecker    | Upton      | Guillermo | Educación
 Schmidt    | Fisher     | David     | Matemáticas
 Schowalter | Muller     | Francesca | Química y Física
 Spencer    | Lakin      | Esther    | Educación
 Stiedemann | Morissette | Alfredo   | Química y Física
 Streich    | Hirthe     | Carmen    | Educación

4. Devuelve un listado con el nombre de las asignaturas, año de inicio y año de fin del curso escolar del alumno con nif 26902806M.

SELECT persona.nif,asignatura.nombre, curso_escolar.anyo_inicio, curso_escolar.anyo_fin FROM persona
JOIN alumno_se_matricula_asignatura ON persona.id = alumno_se_matricula_asignatura.id_alumno
JOIN asignatura ON alumno_se_matricula_asignatura.id_asignatura= asignatura.id
JOIN curso_escolar ON alumno_se_matricula_asignatura.id_curso_escolar = curso_escolar.id
WHERE persona.nif='26902806M';

    nif    |                nombre                | anyo_inicio | anyo_fin 
-----------+--------------------------------------+-------------+----------
 26902806M | Álgegra lineal y matemática discreta |        2014 |     2015
 26902806M | Cálculo                              |        2014 |     2015
 26902806M | Física para informática              |        2014 |     2015


5. Devuelve un listado con el nombre de todos los departamentos que tienen profesores que imparten alguna asignatura en el Grado en Ingeniería Informática (Plan 2015).

SELECT DISTINCT departamento.nombre from departamento
JOIN profesor ON departamento.id = profesor.id_departamento
JOIN asignatura ON profesor.id_profesor = asignatura.id_profesor
JOIN grado ON asignatura.id_grado = grado.id
WHERE grado.nombre = 'Grado en Ingeniería Informática (Plan 2015)';

   nombre    
-------------
 Informática


6. Devuelve un listado con todos los alumnos que se han matriculado en alguna asignatura durante el curso escolar 2018/2019.

SELECT DISTINCT persona.nombre,persona.apellido1,persona.apellido2,curso_escolar.anyo_inicio FROM persona
JOIN alumno_se_matricula_asignatura ON persona.id = alumno_se_matricula_asignatura.id_alumno
JOIN curso_escolar ON alumno_se_matricula_asignatura.id_curso_escolar = curso_escolar.id
WHERE curso_escolar.anyo_inicio = '2018' OR curso_escolar.anyo_inicio ='2019';

 nombre | apellido1 | apellido2 | anyo_inicio 
--------+-----------+-----------+-------------
 Inma   | Lakin     | Yundt     |        2018
 Irene  | Hernández | Martínez  |        2018
 Sonia  | Gea       | Ruiz      |        2018


# Consultas multitabla (Composición externa)

1. Devuelve un listado con los nombres de todos los profesores y los departamentos que tienen vinculados. El listado también debe mostrar aquellos profesores que no tienen ningún departamento asociado. El listado debe devolver cuatro columnas, nombre del departamento, primer apellido, segundo apellido y nombre del profesor. El resultado estará ordenado alfabéticamente de menor a mayor por el nombre del departamento, apellidos y el nombre.


SELECT departamento.nombre AS departamento, persona.apellido2, persona.apellido1, persona.nombre FROM persona
LEFT JOIN profesor ON persona.id = profesor.id_profesor
LEFT JOIN departamento ON profesor.id_departamento = departamento.id
WHERE persona.tipo ='profesor'
ORDER BY departamento ASC , persona.apellido1 ASC, persona.apellido2 ASC, persona.nombre;

    departamento    | apellido2  | apellido1  |  nombre   
--------------------+------------+------------+-----------
 Agronomía          | Murray     | Monahan    | Micaela
 Economía y Empresa | Considine  | Fahey      | Antonio
 Economía y Empresa | Rutherford | Lemke      | Cristina
 Educación          | Upton      | Ruecker    | Guillermo
 Educación          | Lakin      | Spencer    | Esther
 Educación          | Hirthe     | Streich    | Carmen
 Informática        | Kozey      | Hamill     | Manolo
 Informática        | Gea        | Ramirez    | Zoe
 Matemáticas        | Schoen     | Kohler     | Alejandro
 Matemáticas        | Fisher     | Schmidt    | David
 Química y Física   | Muller     | Schowalter | Francesca
 Química y Física   | Morissette | Stiedemann | Alfredo

2. Devuelve un listado con los profesores que no están asociados a un departamento.

SELECT persona.nombre, persona.apellido1, persona.apellido2 
FROM profesor
LEFT JOIN persona ON profesor.id_profesor = persona.id
LEFT JOIN departamento ON profesor.id_departamento = departamento.id
WHERE departamento.id IS NULL;

 nombre | apellido1 | apellido2 
--------+-----------+-----------


3. Devuelve un listado con los departamentos que no tienen profesores asociados.

SELECT departamento.nombre,profesor.id_profesor FROM departamento
LEFT JOIN profesor ON departamento.id = profesor.id_departamento
WHERE profesor.id_departamento IS NULL;

       nombre        | id_profesor 
---------------------+-------------
 Derecho             |            
 Biología y Geología |            
 Filología           |            

4. Devuelve un listado con los profesores que no imparten ninguna asignatura.

SELECT DISTINCT persona.nombre, persona.apellido1, persona.apellido2, asignatura.nombre FROM persona
LEFT JOIN profesor ON persona.id = profesor.id_profesor
LEFT JOIN asignatura ON profesor.id_profesor = asignatura.id_profesor
WHERE persona.tipo ='profesor' AND asignatura.id_profesor IS NULL;

  nombre   | apellido1  | apellido2  | nombre 
-----------+------------+------------+--------
 Alejandro | Kohler     | Schoen     | 
 Alfredo   | Stiedemann | Morissette | 
 Antonio   | Fahey      | Considine  | 
 Carmen    | Streich    | Hirthe     | 
 Cristina  | Lemke      | Rutherford | 
 David     | Schmidt    | Fisher     | 
 Esther    | Spencer    | Lakin      | 
 Francesca | Schowalter | Muller     | 
 Guillermo | Ruecker    | Upton      | 
 Micaela   | Monahan    | Murray     | 

5. Devuelve un listado con las asignaturas que no tienen un profesor asignado.

SELECT asignatura.nombre FROM profesor
RIGHT JOIN asignatura ON profesor.id_profesor = asignatura.id_profesor
WHERE profesor.id_profesor IS NULL;

                                 nombre                                 
------------------------------------------------------------------------
 Ingeniería de Requisitos
 Integración de las Tecnologías de la Información en las Organizaciones
 Modelado y Diseño del Software 1
 Multiprocesadores
 Seguridad y cumplimiento normativo
 Sistema de Información para las Organizaciones
 Tecnologías web
 Teoría de códigos y criptografía
 Administración de bases de datos
 Herramientas y Métodos de Ingeniería del Software
 Informática industrial y robótica
 Ingeniería de Sistemas de Información
 Modelado y Diseño del Software 2
 Negocio Electrónico
 Periféricos e interfaces
 Sistemas de tiempo real
 Tecnologías de acceso a red
 Tratamiento digital de imágenes
 Administración de redes y sistemas operativos
 Almacenes de Datos
 Fiabilidad y Gestión de Riesgos
 Líneas de Productos Software
 Procesos de Ingeniería del Software 1
 Tecnologías multimedia
 Análisis y planificación de las TI
 Desarrollo Rápido de Aplicaciones
 Gestión de la Calidad y de la Innovación Tecnológica
 Inteligencia del Negocio
 Procesos de Ingeniería del Software 2
 Seguridad Informática
 Biologia celular
 Física
 Matemáticas I
 Química general
 Química orgánica
 Biología vegetal y animal
 Bioquímica
 Genética
 Matemáticas II
 Microbiología
 Botánica agrícola
 Fisiología vegetal
 Genética molecular
 Ingeniería bioquímica
 Termodinámica y cinética química aplicada
 Biorreactores
 Biotecnología microbiana
 Ingeniería genética
 Inmunología
 Virología
 Bases moleculares del desarrollo vegetal
 Fisiología animal
 Metabolismo y biosíntesis de biomoléculas
 Operaciones de separación
 Patología molecular de plantas
 Técnicas instrumentales básicas
 Bioinformática
 Biotecnología de los productos hortofrutículas
 Biotecnología vegetal
 Genómica y proteómica
 Procesos biotecnológicos
 Técnicas instrumentales avanzadas

6. Devuelve un listado con todos los departamentos que tienen alguna asignatura que no se haya impartido en ningún curso escolar. El resultado debe mostrar el nombre del departamento y el nombre de la asignatura que no se haya impartido nunca.

SELECT departamento.nombre, asignatura.nombre FROM departamento
LEFT JOIN profesor ON departamento.id = profesor.id_departamento
LEFT JOIN asignatura ON profesor.id_profesor = asignatura.id_profesor
LEFT JOIN alumno_se_matricula_asignatura ON asignatura.id = alumno_se_matricula_asignatura.id_asignatura
LEFT JOIN curso_escolar ON alumno_se_matricula_asignatura.id_curso_escolar = curso_escolar.id
WHERE asignatura.id IS NULL;

   nombre    |                      nombre                       
-------------+---------------------------------------------------
 Informática | Programación de Servicios Software
 Informática | Arquitectura de Computadores
 Informática | Estructura de Datos y Algoritmos II
 Informática | Estructura de Datos y Algoritmos I
 Informática | Fundamentos de Redes de Computadores
 Informática | Sistemas Operativos
 Informática | Ingeniería del Software
 Informática | Desarrollo de interfaces de usuario
 Informática | Planificación y Gestión de Proyectos Informáticos
 Informática | Bases de Datos
 Informática | Sistemas Inteligentes
 
# Consultas resumen

1. Devuelve el número total de alumnas que hay.

SELECT COUNT(*) AS alumnas_totales FROM persona
WHERE persona.tipo = 'alumno' AND persona.sexo = 'M';

 alumnas_totales 
-----------------
               3

2. Calcula cuántos alumnos nacieron en 2005.

SELECT COUNT(*) AS alumnos_nacieron_2005 FROM persona
WHERE persona.tipo='alumno' AND EXTRACT (YEAR FROM fecha_nacimiento) = 2005;

 alumnos_nacieron_2005 
-----------------------
                     0

3. Calcula cuántos profesores hay en cada departamento. El resultado sólo debe mostrar dos columnas, una con el nombre del departamento y otra con el número de profesores que hay en ese departamento. El resultado sólo debe incluir los departamentos que tienen profesores asociados y deberá estar ordenado de mayor a menor por el número de profesores.

SELECT COUNT(*) AS profesores, departamento.nombre FROM departamento
RIGHT JOIN profesor ON departamento.id = profesor.id_departamento
GROUP BY departamento.nombre
ORDER BY profesores DESC;

 profesores |       nombre       
------------+--------------------
          3 | Educación
          2 | Química y Física
          2 | Matemáticas
          2 | Economía y Empresa
          2 | Informática
          1 | Agronomía


4. Devuelve un listado con todos los departamentos y el número de profesores que hay en cada uno de ellos. Tenga en cuenta que pueden existir departamentos que no tienen profesores asociados. Estos departamentos también tienen que aparecer en el listado.

SELECT departamento.nombre, COUNT(profesor.id_profesor) AS profesores FROM departamento
LEFT JOIN profesor ON departamento.id = profesor.id_departamento
GROUP BY departamento.nombre;

       nombre        | num_profesores 
---------------------+----------------
 Química y Física    |              2
 Educación           |              3
 Derecho             |              0
 Agronomía           |              1
 Filología           |              0
 Matemáticas         |              2
 Biología y Geología |              0
 Economía y Empresa  |              2
 Informática         |              2


5. Devuelve un listado con el nombre de todos los grados existentes en la base de datos y el número de asignaturas que tiene cada uno. Tenga en cuenta que pueden existir grados que no tienen asignaturas asociadas. Estos grados también tienen que aparecer en el listado. El resultado deberá estar ordenado de mayor a menor por el número de asignaturas.

SELECT grado.nombre, COUNT(asignatura.id) AS cantidad_asignaturas FROM grado
LEFT JOIN asignatura ON grado.id = asignatura.id_grado
GROUP BY grado.nombre
ORDER BY cantidad_asignaturas DESC;
                         nombre                         | cantidad_asignaturas 
--------------------------------------------------------+----------------------
 Grado en Ingeniería Informática (Plan 2015)            |                   51
 Grado en Biotecnología (Plan 2015)                     |                   32
 Grado en Ingeniería Electrónica Industrial (Plan 2010) |                    0
 Grado en Matemáticas (Plan 2010)                       |                    0
 Grado en Ingeniería Agrícola (Plan 2015)               |                    0
 Grado en Química (Plan 2009)                           |                    0
 Grado en Ingeniería Mecánica (Plan 2010)               |                    0
 Grado en Ciencias Ambientales (Plan 2009)              |                    0
 Grado en Ingeniería Química Industrial (Plan 2010)     |                    0
 Grado en Ingeniería Eléctrica (Plan 2014)              |                    0


6. Devuelve un listado con el nombre de todos los grados existentes en la base de datos y el número de asignaturas que tiene cada uno, de los grados que tengan más de 40 asignaturas asociadas.
 

SELECT grado.nombre, COUNT(asignatura.id) AS cantidad_asignaturas FROM grado
LEFT JOIN asignatura ON grado.id = asignatura.id_grado
GROUP BY grado.nombre
HAVING COUNT(asignatura.id)>40
ORDER BY cantidad_asignaturas DESC;

                   nombre                    | cantidad_asignaturas 
---------------------------------------------+----------------------
 Grado en Ingeniería Informática (Plan 2015) |                   51


7. Devuelve un listado que muestre el nombre de los grados y la suma del número total de créditos que hay para cada tipo de asignatura. El resultado debe tener tres columnas: nombre del grado, tipo de asignatura y la suma de los créditos de todas las asignaturas que hay de ese tipo. Ordene el resultado de mayor a menor por el número total de crédidos.

SELECT grado.nombre, asignatura.tipo, SUM(asignatura.creditos) AS creditos FROM grado 
JOIN asignatura ON grado.id = asignatura.id_grado
GROUP BY grado.nombre, asignatura.tipo
ORDER BY creditos DESC;

                   nombre                    |    tipo     | creditos 
---------------------------------------------+-------------+----------
 Grado en Ingeniería Informática (Plan 2015) | optativa    |      180
 Grado en Biotecnología (Plan 2015)          | obligatoria |      120
 Grado en Ingeniería Informática (Plan 2015) | básica      |       72
 Grado en Biotecnología (Plan 2015)          | básica      |       60
 Grado en Ingeniería Informática (Plan 2015) | obligatoria |       54


8. Devuelve un listado que muestre cuántos alumnos se han matriculado de alguna asignatura en cada uno de los cursos escolares. El resultado deberá mostrar dos columnas, una columna con el año de inicio del curso escolar y otra con el número de alumnos matriculados.

SELECT curso_escolar.anyo_inicio, COUNT(DISTINCT alumno_se_matricula_asignatura.id_alumno) FROM alumno_se_matricula_asignatura
JOIN curso_escolar ON alumno_se_matricula_asignatura.id_curso_escolar = curso_escolar.id
GROUP BY curso_escolar.anyo_inicio;

 anyo_inicio | count 
-------------+-------
        2014 |     3
        2018 |     3


9. Devuelve un listado con el número de asignaturas que imparte cada profesor. El listado debe tener en cuenta aquellos profesores que no imparten ninguna asignatura. El resultado mostrará cinco columnas: id, nombre, primer apellido, segundo apellido y número de asignaturas. El resultado estará ordenado de mayor a menor por el número de asignaturas.

SELECT persona.id, persona.nombre, persona.apellido1, persona.apellido2, COUNT(asignatura.id) AS cantidad_asignaturas FROM persona
JOIN profesor ON persona.id = profesor.id_profesor
LEFT JOIN asignatura ON profesor.id_profesor = asignatura.id_profesor
GROUP BY persona.id,persona.nombre,persona.apellido1,persona.apellido2
ORDER BY cantidad_asignaturas DESC;

 id |  nombre   | apellido1  | apellido2  | cantidad_asignaturas 
----+-----------+------------+------------+----------------------
 14 | Manolo    | Hamill     | Kozey      |                   11
  3 | Zoe       | Ramirez    | Gea        |                   10
  5 | David     | Schmidt    | Fisher     |                    0
 10 | Esther    | Spencer    | Lakin      |                    0
 13 | Alfredo   | Stiedemann | Morissette |                    0
 16 | Antonio   | Fahey      | Considine  |                    0
 12 | Carmen    | Streich    | Hirthe     |                    0
 20 | Francesca | Schowalter | Muller     |                    0
 18 | Micaela   | Monahan    | Murray     |                    0
 15 | Alejandro | Kohler     | Schoen     |                    0
  8 | Cristina  | Lemke      | Rutherford |                    0
 17 | Guillermo | Ruecker    | Upton      |                    0

# Subconsultas

1. Devuelve todos los datos del alumno más joven.

SELECT * FROM persona
WHERE fecha_nacimiento= (
    SELECT MAX(fecha_nacimiento)
    FROM persona
);

 id |    nif    | nombre | apellido1 | apellido2 | ciudad  |     direccion     | telefono | fecha_nacimiento | sexo |  tipo  
----+-----------+--------+-----------+-----------+---------+-------------------+----------+------------------+------+--------
  4 | 17105885A | Pedro  | Heller    | Pagac     | Almería | C/ Estrella fugaz |          | 2000-10-05       | H    | alumno


2. Devuelve un listado con los profesores que no están asociados a un departamento.

SELECT persona.id, persona.nombre, persona.apellido1, persona.apellido2
FROM persona
WHERE persona.tipo = 'profesor'
AND persona.id NOT IN (SELECT id_profesor FROM profesor WHERE id_departamento IS NOT NULL);

 id | nombre | apellido1 | apellido2 
----+--------+-----------+-----------
(0 rows)

3. Devuelve un listado con los departamentos que no tienen profesores asociados.

SELECT departamento.id, departamento.nombre
FROM departamento
WHERE departamento.id NOT IN (SELECT id_departamento FROM profesor);


 id |       nombre        
----+---------------------
  7 | Filología
  8 | Derecho
  9 | Biología y Geología

4. Devuelve un listado con los profesores que tienen un departamento asociado y que no imparten ninguna asignatura.

SELECT persona.id, persona.nombre, persona.apellido1, persona.apellido2
FROM persona
JOIN profesor ON persona.id = profesor.id_profesor
WHERE profesor.id_departamento IS NOT NULL
AND persona.id NOT IN (SELECT id_profesor FROM asignatura);

 id | nombre | apellido1 | apellido2 
----+--------+-----------+-----------
(0 rows)


5. Devuelve un listado con las asignaturas que no tienen un profesor asignado.

SELECT asignatura.nombre
FROM asignatura
WHERE asignatura.id_profesor IS NULL;


                                nombre                                 
------------------------------------------------------------------------
 Ingeniería de Requisitos
 Integración de las Tecnologías de la Información en las Organizaciones
 Modelado y Diseño del Software 1
 Multiprocesadores
 Seguridad y cumplimiento normativo
 Sistema de Información para las Organizaciones
 Tecnologías web
 Teoría de códigos y criptografía
 Administración de bases de datos
 Herramientas y Métodos de Ingeniería del Software
 Informática industrial y robótica
 Ingeniería de Sistemas de Información
 Modelado y Diseño del Software 2
 Negocio Electrónico
 Periféricos e interfaces
 Sistemas de tiempo real
 Tecnologías de acceso a red
 Tratamiento digital de imágenes
 Administración de redes y sistemas operativos
 Almacenes de Datos
 Fiabilidad y Gestión de Riesgos
 Líneas de Productos Software
 Procesos de Ingeniería del Software 1
 Tecnologías multimedia
 Análisis y planificación de las TI
 Desarrollo Rápido de Aplicaciones
 Gestión de la Calidad y de la Innovación Tecnológica
 Inteligencia del Negocio
 Procesos de Ingeniería del Software 2
 Seguridad Informática
 Biologia celular
 Física
 Matemáticas I
 Química general
 Química orgánica
 Biología vegetal y animal
 Bioquímica
 Genética
 Matemáticas II
 Microbiología
 Botánica agrícola
 Fisiología vegetal
 Genética molecular
 Ingeniería bioquímica
 Termodinámica y cinética química aplicada
 Biorreactores
 Biotecnología microbiana
 Ingeniería genética
 Inmunología
 Virología
 Bases moleculares del desarrollo vegetal
 Fisiología animal
 Metabolismo y biosíntesis de biomoléculas
 Operaciones de separación
 Patología molecular de plantas
 Técnicas instrumentales básicas
 Bioinformática
 Biotecnología de los productos hortofrutículas
 Biotecnología vegetal
 Genómica y proteómica
 Procesos biotecnológicos
 Técnicas instrumentales avanzadas

6. Devuelve un listado con todos los departamentos que no han impartido asignaturas en ningún curso escolar

SELECT DISTINCT departamento.nombre
FROM departamento 
LEFT JOIN profesor  ON departamento.id = profesor.id_departamento
LEFT JOIN asignatura ON asignatura.id_profesor = profesor.id_profesor
LEFT JOIN alumno_se_matricula_asignatura ON alumno_se_matricula_asignatura.id_asignatura = asignatura.id
WHERE alumno_se_matricula_asignatura.id_curso_escolar IS NULL AND asignatura.curso IS NULL;

       nombre        
---------------------
 Agronomía
 Biología y Geología
 Derecho
 Economía y Empresa
 Educación
 Filología
 Matemáticas
 Química y Física


