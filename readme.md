# Ex Query

## 1. Selezionare tutti gli studenti nati nel 1990 (160)

```sql

SELECT * FROM `students` WHERE `date_of_birth` LIKE '1990-%';

```

## 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

```sql

SELECT * FROM `courses` WHERE `cfu` > 10;

```

## 3. Selezionare tutti gli studenti che hanno più di 30 anni

```sql

SELECT * FROM `students` WHERE DATEDIFF(CURRENT_DATE, `date_of_birth`) / 365 > 30;

```

## 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

```sql

SELECT * FROM `courses` WHERE `period` = 'I semestre' AND `year` = 1;

```

## 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

```sql



```

## 6. Selezionare tutti i corsi di laurea magistrale (38)

```sql

SELECT * FROM `degrees` WHERE `level`= 'magistrale';

```

# 7. Da quanti dipartimenti è composta l'università? (12)

```sql

SELECT COUNT(*) FROM `departments`;

```

# 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```sql

SELECT * FROM `teachers` WHERE `phone` IS NULL;

```

### Group By

## 1. Contare quanti iscritti ci sono stati ogni anno

```sql

SELECT COUNT(`id`) AS `number_of_students`, YEAR(`date_of_birth`) AS `school_year` FROM `students` GROUP BY YEAR(`date_of_birth`);

```

## 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql

SELECT COUNT(`id`) AS `number_of_teachers`, `office_address` FROM `teachers` GROUP BY `office_address`;

```

## 3. Calcolare la media dei voti di ogni appello d'esame

```sql

SELECT (`exam_id`), AVG(`vote`) AS `vote_average` FROM `exam_student` GROUP BY (`exam_id`);

```
## 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql

SELECT COUNT(`id`) AS `degree_courses`, (`department_id`) FROM `degrees` GROUP BY `department_id`;

```

### Joins:
## 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql

SELECT `students`.`id`, `students`.`name`, `students`.`surname`,`degrees`.`name`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

```

## 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql

SELECT `degrees`.`name` AS `degrees_name`, `departments`.`name` AS `departments_name`
FROM `degrees`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`name`
LIKE 'Corso di Laurea Magistrale%';

```

## 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql

SELECT `courses`.`name` AS `course_name`, `teachers`.`name`, `teachers`.`surname`
FROM `courses`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `teachers`.`id`=`course_teacher`.`teacher_id`
WHERE `teachers`.`id` = 44;

```

## 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql

SELECT `students`.`name`, `students`.`surname`, `degrees`.`name` AS `degree_name`, `departments`.`name` AS `department_name`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id`=`degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id`=`departments`.`id`
ORDER BY `students`.`name`, `students`.`surname`;

```

## 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql

SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, `teachers`.`name`, `teachers`.`surname` 
FROM `degrees`
JOIN `courses` ON `courses`.`degree_id`=`degrees`.`id`
JOIN `course_teacher` ON `course_teacher`.`course_id`=`courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id`= `teachers`.`id`;

```
## 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql

SELECT `departments`.`name` AS `department_name`, `teachers`.`name`, `teachers`.`surname`
FROM `departments`
JOIN `degrees` ON `degrees`.`department_id`=`departments`.`id`
JOIN `courses` ON `courses`.`degree_id`=`degrees`.`id`
JOIN `course_teacher` ON `course_teacher`.`course_id`=`courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id`=`teachers`.`id`
WHERE `departments`.`name`='Dipartimento di Matematica';

```

## 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

