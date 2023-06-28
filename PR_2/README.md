# Лабораторная работа №2
Диаграмма последовательностей и развертывания
## Диаграмма последовательностей
```
@startuml

actor Студент as Student
participant "Информационная система деканата" as Deanery
participant "Учет успеваемости" as Grading

activate Student
Student -> Deanery: Запросить просмотр успеваемости
activate Deanery
Deanery -> Grading: Получить оценки(Студент)
activate Grading
Grading --> Deanery: Отправить оценки
deactivate Grading
Deanery --> Student: Отправить оценки
deactivate Deanery
deactivate Student

@enduml
```
![image](https://github.com/Scythe888/TMP/assets/134215335/d8e76c78-5eea-433d-a90c-fb829fd34b8e)

## Диаграмма развертывания
```
@startuml

node "Студентский компьютер" as StudentComputer
node "Web-сервер" as WebServer
node "База данных" as Database

StudentComputer -> WebServer: HTTP запрос
WebServer -> Database: Запрос к базе данных
Database --> WebServer: Ответ с данными
WebServer --> StudentComputer: HTTP ответ

@enduml
```
![image](https://github.com/Scythe888/TMP/assets/134215335/f8a99b5e-b9ad-4dc6-9e0b-88f8be85738d)
