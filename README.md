# Практическая работа 6 часть 1
## Результат работы программы
![image](https://github.com/user-attachments/assets/073a94a7-4950-469c-a3e9-e0557a6bacf5)
## Тестовые методы
```
using System;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using BankAccountNS;

namespace BankTests
{
    [TestClass]
    public class BankAccountTests
    {
        [TestMethod]
        public void Debit_WithValidAmount_UpdatesBalance()
        {
            // Arrange
            double beginningBalance = 11.99;
            double debitAmount = 4.55;
            double expected = 7.44;
            BankAccount account = new BankAccount("Mr. Roman Abramovich", beginningBalance);

            // Act
            account.Debit(debitAmount);

            // Assert
            double actual = account.Balance;
            Assert.AreEqual(expected, actual, 0.001, "Account not debited correctly");
        }

        [TestMethod]
        public void Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange()
        {
            // Arrange
            double beginningBalance = 11.99;
            double debitAmount = -100.00;
            BankAccount account = new BankAccount("Mr. Roman Abramovich", beginningBalance);

            // Act and assert
            Assert.ThrowsException<System.ArgumentOutOfRangeException>(() => account.Debit(debitAmount));
        }

        [TestMethod]
        public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()
        {
            // Arrange
            double beginningBalance = 11.99;
            double debitAmount = 20.0;
            BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

            // Act
            try
            {
                account.Debit(debitAmount);
            }
            catch (System.ArgumentOutOfRangeException e)
            {
                // Assert
                StringAssert.Contains(e.Message, BankAccount.DebitAmountExceedsBalanceMessage);
                return;
            }

            Assert.Fail("The expected exception was not thrown.");
        }

        [TestMethod]
        public void Credit_WithValidAmount_UpdatesBalance()
        {
            // Arrange
            double beginningBalance = 11.99;
            double creditAmount = 5.77;
            double expected = 17.76;
            BankAccount account = new BankAccount("Mr. Roman Abramovich", beginningBalance);

            // Act
            account.Credit(creditAmount);

            // Assert
            double actual = account.Balance;
            Assert.AreEqual(expected, actual, 0.001, "Account not credited correctly");
        }

        [TestMethod]
        public void Credit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange()
        {
            // Arrange
            double beginningBalance = 11.99;
            double creditAmount = -100.00;
            BankAccount account = new BankAccount("Mr. Roman Abramovich", beginningBalance);

            // Act and assert
            Assert.ThrowsException<System.ArgumentOutOfRangeException>(() => account.Credit(creditAmount));
        }

    }

}
```

## Обозреватель тестов
![image](https://github.com/user-attachments/assets/a23bf651-704e-453c-aa5d-9ef2157711de)

##Вывод о проведенном тестировании:
Тестирование методов `Debit` и `Credit` прошло успешно. Все тесты корректно проверяют основные сценарии: списание и добавление средств, а также обработку некорректных данных (отрицательные суммы и превышение баланса). Ошибки, обнаруженные в ходе тестирования (например, неправильное изменение баланса в `Debit`), были исправлены, что подтвердило корректность работы методов.  

##Причина успешного выполнения тестов:
1. Корректная реализация методов с проверкой входных данных.  
2. Качественное написание тестов, охватывающих все сценарии.  
3. Рефакторинг кода, улучшивший его надежность и читаемость.  
4. Своевременное исправление ошибок, выявленных тестами.  

##Причина неуспешного выполнения тестов (если бы они были):
1. Некорректная логика в методах (например, отсутствие проверок на отрицательные суммы).  
2. Неполное покрытие тестами всех возможных сценариев.  
3. Ошибки в assertions (неправильные ожидаемые значения).  
4. Отсутствие обработки исключений в тестах.





