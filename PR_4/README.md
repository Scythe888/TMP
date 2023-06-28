# Лабораторная работа №4
Итератор (Iterator) и Посетитель (Visitor)

## Итератор
[Реализация на языке C#](iterator/)

[UML-диаграмма](iterator/iterator.puml)
```
@startuml
interface IEnumerator<BankAccount> {
  + Current: BankAccount
  + MoveNext(): bool
  + Reset(): void
}

interface IEnumerable<BankAccount> {
  + GetEnumerator(): IEnumerator<BankAccount>
}

class BankAccounts {
  - accounts: List<BankAccount>
  + GetEnumerator(): IEnumerator<BankAccount>
  + AddAccount(account: BankAccount): void
}

class BankAccount {
  - accountNumber: string
  - balance: decimal
  + AccountNumber: string
  + Balance: decimal
}

BankAccounts -> IEnumerable
BankAccounts ..> BankAccount
BankAccount -up-|> IEnumerator
BankAccount ..> BankAccounts: contains
@enduml
```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab4/img/iter-uml.png)

## Посетитель
[Реализация на языке C#](visitor/)

[UML-диаграмма](visitor/visitor.puml)
```
@startuml
interface IBankAccountVisitor {
    + Visit(CreditAccount account)
    + Visit(SavingsAccount account)
}

abstract class BankAccount {
    + AccountNumber : string
    + Balance : decimal
    + Accept(visitor: IBankAccountVisitor) : void
}

class CreditAccount {
    + Accept(visitor: IBankAccountVisitor) : void
}

class SavingsAccount {
    + Accept(visitor: IBankAccountVisitor) : void
}

class BankReport {
    + Visit(CreditAccount account) : void
    + Visit(SavingsAccount account) : void
}

BankAccount <|-- CreditAccount 
BankAccount <|-- SavingsAccount

IBankAccountVisitor <|.. BankReport
@enduml
```

![alt text](https://github.com/st-georgy/TMP/blob/master/lab4/img/visit-uml.png)
