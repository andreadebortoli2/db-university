## Description

Dopo aver creato un nuovo database nel vostro phpMyAdmin e aver importato lo schema allegato, eseguite le query del file allegato.
Dopo aver testato le vostre query con phpMyAdmin, riportatele.


- Selezionare tutti gli studenti nati nel 1990 (160)

    > SELECT * FROM `students` WHERE `date_of_birth` LIKE '1990%';


- Selezionare tutti i corsi che valgono più di 10 crediti (479)

    > SELECT * FROM `courses` WHERE `cfu` > 10;


- Selezionare tutti gli studenti che hanno più di 30 anni

    > SELECT * FROM `students` WHERE YEAR(CURRENT_DATE()) - YEAR(date_of_birth) > 30;

    <!-- correction -->
    > SELECT * FROM `students` WHERE TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE()) > 30;


- Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

    > SELECT * FROM `courses` WHERE `year` = 1 AND `period` = 'I semestre';


- Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

    > SELECT * FROM `exams` WHERE `date` = '2020-06-20' AND `hour` > '14:00:00';

    <!-- correction -->
    > SELECT * FROM `exams` WHERE `date` = '2020-06-20' AND TIME(hour) > '14:00:00';


- Selezionare tutti i corsi di laurea magistrale (38)

    > SELECT * FROM `degrees` WHERE `level` = 'magistrale';


- Da quanti dipartimenti è composta l'università? (12)

    > SELECT COUNT(*) AS number_of_departments FROM `departments`;


- Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

    > SELECT COUNT(*) AS teachers_without_phone FROM `teachers` WHERE `phone` IS NULL;