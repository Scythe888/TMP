# Лабораторная работа №1
Диаграмма использования и классов

## Диаграмма вариантов использования
![image](https://github.com/Scythe888/TMP/assets/134215335/4ef5703a-51e5-46ce-8c66-763d8b88cb5e)

```
@startuml

left to right direction

actor Деканат as Deanery
actor Преподаватель as Teacher
actor Студент as Student

rectangle "Информационная система деканата" {
  Deanery --> (Прием студентов)
  Deanery --> (Отчисление студентов)
  Deanery --> (Учет успеваемости)
  Deanery --> (Перевод студентов)
  
  Teacher --> (Ввод оценок)
  
  Student --> (Просмотр успеваемости)
  Student --> (Просмотр расписания)
}

@enduml

```

## Диаграмма последовательности для прецедента "Просмотр успеваемо-сти":
![image](https://github.com/Scythe888/TMP/assets/134215335/0e9d2809-34d0-4025-9d10-d4cc8e3d17c1)

```
@startuml

actor Студент as Student
participant "Информационная система деканата" as Deanery
participant "Учет успеваемости" as Grading

Student -> Deanery: Запросить просмотр успеваемости
Deanery -> Grading: Получить оценки(Студент)
Grading --> Student: Отправить оценки

@enduml

```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab1/img/1-2.png)

## Диаграмма классов
![image](https://github.com/Scythe888/TMP/assets/134215335/58238a78-3a0a-4a06-ad78-caf8527a1279)

```
@startuml

package "Информационная система деканата" {
  
  class Студент {
    -id: int
    -имя: string
    -группа: string
    -курс: int
    +Студент(id: int, имя: string, группа: string, курс: int)
    +getId(): int
    +getИмя(): string
    +getГруппа(): string
    +getКурс(): int
    +просмотрУспеваемости(): void
    +просмотрРасписания(): void
  }
  
  class Деканат {
    -студенты: List<Студент>
    -учетУспеваемости: УчетУспеваемости
    +приемСтудентов(студент: Студент): void
    +отчислениеСтудентов(студент: Студент): void
    +переводСтудентов(студент: Студент, новаяГруппа: string, новыйКурс: int): void
    +getСтуденты(): List<Студент>
  }
  
  class УчетУспеваемости {
    -студенты: List<Студент>
    -оценки: Map<Студент, List<int>>
    +вводОценок(студент: Студент, оценки: List<int>): void
    +получитьОценки(студент: Студент): List<int>
  }
}

@enduml

```

