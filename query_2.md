### Description

Utilizzando lo stesso database della volta scorsa, eseguite le query in allegato.
Caricate un secondo file nella stessa repo di ieri db-university con le query di oggi.


## Group by

- Contare quanti iscritti ci sono stati ogni anno

    > SELECT COUNT(`id`) AS 'enrolments_by_year', YEAR(`enrolment_date`) 
        FROM `students` 
        GROUP BY YEAR(`enrolment_date`);

        retrun: 4 rows

        | enrolments_by_year | YEAR(enrolment_date) |
        | ------------------ | -------------------- |
        | 912                | 2018                 |
        | 1709               | 2019                 |
        | 1645               | 2020                 |
        | 734                | 2021                 |


- Contare gli insegnanti che hanno l'ufficio nello stesso edificio

    > SELECT COUNT(`id`) AS 'teachers_by_office', `office_address`
        FROM `teachers`
        GROUP BY `office_address`;

        return: 29 rows

        | teachers_by_office | office_address           |
        | ------------------ | ------------------------ |
        | 1                  | Borgo Demis 1            |
        | 8                  | Borgo Elga 89            |
        | 4                  | Borgo Elio 234 Piano 4   |
        | 1                  | Borgo Ippolito 5 Piano 5 |
        | ...                | ...                      |
        | ...                | ...                      |
        | 5                  | Strada Vitali 8 Piano 0  |
        | 1                  | Via Elga 7 Piano 4       |


- Calcolare la media dei voti di ogni appello d'esame

    > SELECT AVG(`vote`), `exam_id` 
        FROM `exam_student` 
        GROUP BY `exam_id`;

        return: 4078 rows

        | AVG(`vote`) | exam_id |
        | ----------- | ------- |
        | 16.8824     | 1       |
        | 16.4615     | 2       |
        | 20.3333     | 3       |
        | 27.0000     | 4       |
        | ...         | ...     |


- Contare quanti corsi di laurea ci sono per ogni dipartimento


## Joins

- Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

- Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

- Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

- Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

- Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

- Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)


## BONUS: 

- Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.