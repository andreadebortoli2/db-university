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

    > SELECT COUNT(`id`) AS 'degrees_by_department', `department_id`
        FROM `degrees`
        GROUP BY `department_id`;

        return: 12 rows

        | degrees_by_department | department_id |
        | --------------------- | ------------- |
        | 10                    | 1             |
        | 4                     | 2             |
        | 4                     | 3             |
        | 9                     | 4             |
        | 4                     | 5             |
        | 6                     | 6             |
        | 7                     | 7             |
        | 8                     | 8             |
        | 5                     | 9             |
        | 8                     | 10            |
        | 3                     | 11            |
        | 7                     | 12            |


## Joins

- Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

    > SELECT `students`.`*`, `degrees`.`name` AS 'degree_name' 
        FROM `students` 
        INNER JOIN `degrees` 
        ON `students`.`degree_id` = `degrees`.`id` 
        WHERE `degrees`.`name` = 'corso di laurea in economia';

        return: 68 rows

        | id  | degree_id | name    | surname   | date_of_birth | fiscal_code      | enrolment_date | registration_number | email               | degree_name                 |
        | --- | --------- | ------- | --------- | ------------- | ---------------- | -------------- | ------------------- | ------------------- | --------------------------- |
        | 20  | 53        | Joshua  | Vitale    | 1980-08-31    | GRFBKR76L42T308O | 2021-03-27     | 620052h             | longo@benedetti.com | Corso di Laurea in Economia |
        | 57  | 53        | Doriana | Benedetti | 1978-03-22    | QSFGPL05R66U759U | 2019-05-01     | 620089o             | farina@montanari.it | Corso di Laurea in Economia |
        | ... | ...       | ...     | ...       | ...           | ...              | ...            | ...                 | ...                 | ...                         |


- Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

    > SELECT `degrees`.`id`, `degrees`.`name`, `degrees`.`level`, `departments`.`name` AS 'department_name' 
        FROM `departments` 
        INNER JOIN `degrees` 
        ON `departments`.`id` = `degrees`.`department_id` 
        WHERE `departments`.`name` = 'dipartimento di neuroscienze' 
        AND `degrees`.`level` = 'magistrale';

        return: 1 row

        | id  | name                                                  | level      | department_name              |
        | --- | ----------------------------------------------------- | ---------- | ---------------------------- |
        | 44  | Corso di Laurea Magistrale in Odontoiatria e Prote... | magistrale | Dipartimento di Neuroscienze |


- Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

    > SELECT `id` FROM `teachers` WHERE `name` = 'fulvio' AND `surname` = 'amato'; <!-- to check the teacher's id -->
        
        return: id = 44

    > SELECT `courses`.`id` AS 'course_id', `courses`.`name` AS 'course_name', `courses`.`description`, `teachers`.`id` AS 'teacher_id', `teachers`.`name`, `teachers`.`surname`
        FROM `courses` 
        INNER JOIN `course_teacher` 
        ON `courses`.`id` = `course_teacher`.`course_id` 
        INNER JOIN `teachers` 
        ON `course_teacher`.`teacher_id` = `teachers`.`id`
        WHERE `teachers`.`id` = 44;

        return: 11 rows

        | course_id	| course_name                | description                                           | teacher_id | name   | surname |
        | ---------	| -------------------------- | ----------------------------------------------------- | ---------- | ------ | ------- |
        | 23        | impedit et eaque           | Ut autem omnis repellendus officiis. Quia optio es... | 44         | Fulvio | Amato   |
        | 155       | explicabo ab voluptas      | Nam molestias iste sed error. Ullam veniam maxime ... | 44         | Fulvio | Amato   |
        | 170       | ullam ullam dignissimos    | Perferendis voluptate et ratione sunt. Laborum har... | 44         | Fulvio | Amato   |
        | 251       | aut pariatur a             | Sequi sint expedita sint tempora enim et eum. Magn... | 44         | Fulvio | Amato   |
        | 489       | alias voluptatibus sed     | Et minima molestiae eveniet. Iste est veritatis mo... | 44         | Fulvio | Amato   |
        | 601       | facilis adipisci provident | Et aut id aut officia. Doloremque quaerat sit et a... | 44         | Fulvio | Amato   |
        | 725       | doloribus nemo iure        | Ea quae porro laudantium ut. Explicabo et assumend... | 44         | Fulvio | Amato   |
        | 766       | et quasi enim              | Et ipsa enim animi dolor. Dolore et dicta sunt. Fu... | 44         | Fulvio | Amato   |
        | 1016      | facilis pariatur qui       | Dolores unde ex suscipit sint quia. A debitis dolo... | 44         | Fulvio | Amato   |
        | 1017      | dolor repellat dignissimos | Aut est id qui pariatur error. Nobis sint eum ut e... | 44         | Fulvio | Amato   |
        | 1259      | magni magni omnis          | Maxime est est vitae. Natus ut reiciendis veniam. ... | 44         | Fulvio | Amato   |


- Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

    > SELECT `students`.`name`, `students`.`surname`, `degrees`.`name` AS 'degree_name', `departments`.`name` AS 'department_name'
        FROM `students` 
        JOIN `degrees` 
        ON `students`.`degree_id` = `degrees`.`id` 
        JOIN `departments` 
        ON `degrees`.`department_id` = `departments`.`id`
        ORDER BY `students`.`surname` ASC, `students`.`name`;

        return: 5000 rows

        | name     | surname | degree_name                                           | department-name                                       |
        | -------- | ------- | ----------------------------------------------------- | ----------------------------------------------------- |
        | Brigitta | Amato   | Corso di Laurea Magistrale in Relazioni Internazio... | Dipartimento di Scienze politiche, giuridiche e st... |
        | Carlo    | Amato   | Corso di Laurea in Ingegneria per l'Ambiente e il ... | Dipartimento di Ingegneria civile, edile e ambient... |
        | ...      | ...     | ...                                                   | ...                                                   |


- Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

- Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)


## BONUS: 

- Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.