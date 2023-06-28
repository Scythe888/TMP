# Лабораторная работа №5
Абстрактная фабрика (Abstract Factory). Строитель (Builder). Адаптер (Wrapper, Adapter). Посредник (Intermediary, Controller, Mediator).

## Абстрактная Фабрика
[Реализация на языке C#](abstract_factory/)

[UML-диаграмма](abstract_factory/abstract_factory.puml)
```
@startuml

interface IBankAccount {
    + Deposit(amount: decimal): void
    + Withdraw(amount: decimal): void
    + GetBalance(): decimal
}

interface ICreditCard {
    + MakePayment(amount: decimal): bool
    + GetBalance(): decimal
}

interface ICreditProduct {
    + GetInterestRate(): decimal
    + GetMonthlyPayment(principal: decimal, term: int): decimal
}

abstract class BankFactory {
    + CreateBankAccount(accountNumber: string, balance: decimal): IBankAccount
    + CreateCreditCard(cardNumber: string, balance: decimal): ICreditCard
    + CreateCreditProduct(principal: decimal, term: int): ICreditProduct
}

class AlphaBankAccount {
    - accountNumber: string
    - balance: decimal
    + Deposit(amount: decimal): void
    + Withdraw(amount: decimal): void
    + GetBalance(): decimal
}

class AlphaCreditCard {
    - cardNumber: string
    - balance: decimal
    + MakePayment(amount: decimal): bool
    + GetBalance(): decimal
}

class AlphaCreditProduct {
    - principal: decimal
    - term: int
    + GetInterestRate(): decimal
    + GetMonthlyPayment(principal: decimal, term: int): decimal
}

class AlphaBankFactory {
    + CreateBankAccount(accountNumber: string, balance: decimal): IBankAccount
    + CreateCreditCard(cardNumber: string, balance: decimal): ICreditCard
    + CreateCreditProduct(principal: decimal, term: int): ICreditProduct
}

class BankClient {
    - factory: BankFactory
    + OpenBankAccount(accountNumber: string, initialDeposit: decimal): IBankAccount
    + ApplyForCreditCard(cardNumber: string, creditLimit: decimal): ICreditCard
    + ApplyForCreditProduct(principal: decimal, term: int): ICreditProduct
}

BankFactory <|-- AlphaBankFactory
IBankAccount <|.. AlphaBankAccount
ICreditCard <|.. AlphaCreditCard
ICreditProduct <|.. AlphaCreditProduct
BankFactory <|-- AlphaBankFactory
BankClient --> BankFactory

@enduml
```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab5/img/absfact-uml.png)

## Строитель
[Реализация на языке C#](builder/)

[UML-диаграмма](builder/builder.puml)
```
@startuml

class BankAccount {
    + AccountNumber: string
    + Balance: decimal
    + AccountHolder: string
    + AccountType: string
}

interface IBankAccountBuilder {
    + SetAccountNumber(accountNumber: string): void
    + SetBalance(balance: decimal): void
    + SetAccountHolder(accountHolder: string): void
    + SetAccountType(accountType: string): void
    + GetBankAccount(): BankAccount
}

class BankAccountBuilder {
    - bankAccount: BankAccount
    + SetAccountNumber(accountNumber: string): void
    + SetBalance(balance: decimal): void
    + SetAccountHolder(accountHolder: string): void
    + SetAccountType(accountType: string): void
    + GetBankAccount(): BankAccount
}

class BankAccountDirector {
    - bankAccountBuilder: IBankAccountBuilder
    + CreateBankAccount(accountNumber: string, balance: decimal, accountHolder: string, accountType: string): void
    + GetBankAccount(): BankAccount
}

BankAccountBuilder ..|> IBankAccountBuilder
BankAccountDirector--> IBankAccountBuilder
BankAccountDirector --> BankAccountBuilder
BankAccountBuilder --> BankAccount

@enduml
```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab5/img/builder-uml.png)

## Адаптер
[Реализация на языке C#](adapter/)

[UML-диаграмма](adapter/adapter.puml)
```
@startuml

interface IBankAccount {
    + GetAccountNumber(): string
    + GetBalance(): decimal
}

class ThirdPartyBankAccount {
    + AccountNumber: string
    + Balance: double
}

class BankAccountAdapter {
    - thirdPartyBankAccount: ThirdPartyBankAccount
    + BankAccountAdapter(thirdPartyBankAccount: ThirdPartyBankAccount)
    + GetAccountNumber(): string
    + GetBalance(): decimal
}

IBankAccount <|.. BankAccountAdapter
BankAccountAdapter --> ThirdPartyBankAccount

@enduml
```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab5/img/adapter-uml.png)

## Посредник
[Реализация на языке C#](mediator/)

[UML-диаграмма](mediator/mediator.puml)
```
@startuml

interface IBankMediator {
    + SendTransfer(sender: BankAccount, receiver: BankAccount, amount: decimal)
    + SendWithdrawal(sender: BankAccount, amount: decimal)
}

class BankMediator {
    + SendTransfer(sender: BankAccount, receiver: BankAccount, amount: decimal)
    + SendWithdrawal(sender: BankAccount, amount: decimal)
}

class BankAccount {
    - accountNumber: string
    - balance: decimal
    - accountHolder: string
    - accountType: string
    - bankMediator: IBankMediator
    + BankAccount(accountNumber: string, balance: decimal, accountHolder: string, accountType: string, bankMediator: IBankMediator)
    + Withdraw(amount: decimal): bool
    + Transfer(receiver: BankAccount, amount: decimal): bool
    + Deposit(amount: decimal)
    + GetAccountNumber(): string
    + GetBalance(): decimal
    + GetAccountHolder(): string
    + GetAccountType(): string
}

IBankMediator <|.. BankMediator
BankMediator ..> BankAccount

@enduml
```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab5/img/mediator-uml.png)
