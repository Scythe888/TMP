# Лабораторная работа №6
Инверсия управления (Inversion of Control). Заместитель (Proxy). Компоновщик (Дерево, Composite).

## Инверсия управления
[Реализация на языке C#](ioc/)

[UML-диаграмма](ioc/ioc.puml)
```
@startuml

interface IBalanceChecker {
    + GetBalance(accountNumber: string): decimal
}

class ExternalBalanceChecker {
    + GetBalance(accountNumber: string): decimal
}

class BankClient {
    - balanceChecker: IBalanceChecker
    + BankClient(balanceChecker: IBalanceChecker)
    + CheckBalance(accountNumber: string): bool
}

IBalanceChecker <|.. ExternalBalanceChecker
BankClient --> IBalanceChecker

@enduml
```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab6/img/ioc-uml.png)

## Заместитель
[Реализация на языке C#](proxy/)

[UML-диаграмма](proxy/proxy.puml)
```
@startuml

interface IBalanceChecker {
    + GetBalance(accountNumber: string): decimal
}

class ExternalBalanceChecker {
    + GetBalance(accountNumber: string): decimal
}

class BalanceCheckerProxy {
    - balanceChecker: IBalanceChecker
    - balanceCache: Dictionary<string, decimal>
    + BalanceCheckerProxy(balanceChecker: IBalanceChecker)
    + GetBalance(accountNumber: string): decimal
}

IBalanceChecker <|.. ExternalBalanceChecker
IBalanceChecker <|.. BalanceCheckerProxy
BalanceCheckerProxy o-- IBalanceChecker

@enduml
```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab6/img/proxy-uml.png)

## Компоновщик
[Реализация на языке C#](composite/)

[UML-диаграмма](composite/composite.puml)
```
@startuml

abstract class Account {
    - accountNumber: string
    + Account(accountNumber: string)
    + GetBalance(): decimal
}

class BankAccount {
    - balance: decimal
    + BankAccount(accountNumber: string, balance: decimal)
    + GetBalance(): decimal
}

class BankAccountGroup {
    - accounts: List<Account>
    + BankAccountGroup(accountNumber: string)
    + AddAccount(account: Account): void
    + GetBalance(): decimal
}

Account <|-- BankAccount
Account <|-- BankAccountGroup
BankAccountGroup o-- Account

@enduml
```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab6/img/composite-uml.png)
