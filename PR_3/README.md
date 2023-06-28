# Лабораторная работа №3
Стратегия (Straregy), Шаблонный метод (Template Method)

## Стратегия
[Реализация на языке C#](strategy/)

[UML-диаграмма](strategy/strategy.puml)
```
@startuml
interface IInterestRateStrategy {
    +CalculateInterest(decimal balance)
}

class LowInterestRateStrategy {
    +CalculateInterest(decimal balance)
}

class HighInterestRateStrategy {
    +CalculateInterest(decimal balance)
}

class SavingsAccount {
    -_interestRateStrategy: IInterestRateStrategy
    +SetPaymentStrategy(IInterestRateStrategy interestRateStrategy)
    +CalculateInterest(decimal balance)
}

SavingsAccount o-- IInterestRateStrategy
IInterestRateStrategy <|.. LowInterestRateStrategy
IInterestRateStrategy <|.. HighInterestRateStrategy

@enduml
```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab3/img/strat-uml.png)

## Шаблонный метод
[Реализация на языке C#](template/)

[UML-диаграмма](template/template.puml)
```
@startuml
abstract class Account {
    -payments: Payment[]
    +ProcessPayments()
    +GetPayments()
    +CalculateFee()
    +TransferMoney()
    +WriteToLog()
    {abstract} +ProcessPayment(Payment payment)
}

class SavingsAccount {
    +ProcessPayment(Payment payment)
    +CalculateFee()
    +TransferMoney()
    +WriteToLog()
}

class CreditAccount {
    +ProcessPayment(Payment payment)
    +TransferMoney()
    +WriteToLog()
}

class Payment {
    -amount: decimal
    -fromAccount: string
    -toAccount: string
    +Payment(amount: decimal, fromAccount: string, toAccount: string)
    +Amount(): decimal
    +FromAccount(): string
    +ToAccount(): string
}

Account <|-- SavingsAccount
Account <|-- CreditAccount

@enduml
```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab3/img/templ-uml.png)
