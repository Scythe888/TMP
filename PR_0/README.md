# Лабораторная работа №0
Простая UML-диаграмма

## Диаграмма
[UML-диаграмма](uml_diagram.puml)
```
@startuml
left to right direction

actor User as "Пользователь"

rectangle "Онлайн-магазин" {
  usecase "Просмотр товаров" as viewProducts
  usecase "Добавление товара в корзину" as addToCart
  usecase "Оформление заказа" as checkout
  usecase "Оплата заказа" as payment

  User --> viewProducts
  User --> addToCart
  User --> checkout
  User --> payment

  viewProducts --> addToCart
  addToCart --> checkout
  checkout --> payment

  usecase "Регистрация пользователя" as registerUser
  usecase "Авторизация пользователя" as authenticateUser
  usecase "Управление профилем" as manageProfile

  User --> registerUser
  User --> authenticateUser
  User --> manageProfile

  usecase "Отслеживание доставки" as trackOrder
  usecase "Управление отзывами" as manageReviews

  checkout --> trackOrder
  manageProfile --> manageReviews

  usecase "Поддержка" as support

  User --> support
}

@enduml
```
![image](https://github.com/Scythe888/TMP/assets/134215335/589162b2-bfa5-4e7f-80b5-11818fec9575)

