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