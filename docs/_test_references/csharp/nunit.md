---
title: NUnit Testing Framework
language: csharp
---

# NUnit Testing Framework

## Overview

Codewars supports the [NUnit](http://www.nunit.org/) testing framework.

These notes are adapted from: [NUnit - Quickstart](http://nunit.org/index.php?p=quickStart)

## NUnit Quick Start

Let’s start with a simple example, whose full source code is available here.
Suppose we are writing a bank application and we have a basic domain class – `Account`.
`Account` supports operations to deposit, withdraw, and transfer funds.
The `Account` class may look like this:

```csharp
namespace Bank
{
  public class Account
  {
    private decimal balance;

    public void Deposit(decimal amount)
    {
      balance += amount;
    }

    public void Withdraw(decimal amount)
    {
      balance -= amount;
    }

    public void TransferFunds(Account destination, decimal amount)
    {
    }

    public decimal Balance
    {
      get { return balance; }
    }
  }
}
```

Now let’s write a test for this class – `AccountTest`. The first method we will test is `TransferFunds`.

```csharp
namespace Bank
{
  using NUnit.Framework;

  [TestFixture]
  public class AccountTest
  {
    [Test]
    public void TransferFunds()
    {
      Account source = new Account();
      source.Deposit(200m);

      Account destination = new Account();
      destination.Deposit(150m);

      source.TransferFunds(destination, 100m);

      Assert.AreEqual(250m, destination.Balance);
      Assert.AreEqual(100m, source.Balance);
    }
  }
}
```

The first thing to notice about this class is that it has a `[TestFixture]` attribute associated with it –
this is the way to indicate that the class contains test code (this attribute can be inherited).
The class has to be public and there are no restrictions on its superclass.
The class also has to have a default constructor.

The only method in the class – `TransferFunds`, has a `[Test]` attribute associated with it –
this is an indication that it is a test method.
Test methods have to return void and take no parameters.
In our test method we do the usual initialization of the required test objects,
execute the tested business method and check the state of the business objects.
The `Assert` class defines a collection of methods used to check the post-conditions and
in our example we use the `AreEqual` method to make sure that after the transfer both accounts
have the correct balances (there are several overloadings of this method,
the version that was used in this example has the following parameters:
the first parameter is an expected value and the second parameter is the actual value).

Click **RUN TESTS** and the "Results" panel displayed the following message:

```
TransferFunds : expected <250> but was <150>
```

and the stack trace shows:

```
at bank.AccountTest.TransferFunds() in C:\nunit\BankSampleTests\AccountTest.cs:line 19
```

That is expected behavior; the test has failed because we have not implemented the `TransferFunds` method yet.
Now let’s get it to work: make your TransferFunds method look like this:

```csharp
public void TransferFunds(Account destination, decimal amount)
{
  destination.Deposit(amount);
  Withdraw(amount);
}
```

Now click **RUN TESTS** again – the status bar and the test tree turn green.

Let’s add some error checking to our `Account` code.
We are adding the minimum balance requirement for the account to make sure that
banks continue to make their money by charging your minimal overdraft protection fee.
Let’s add the minimum balance property to our Account class:

```csharp
private decimal minimumBalance = 10m;

public decimal MinimumBalance
{
  get{ return minimumBalance; }
}
```

We will use an exception to indicate an overdraft:

```csharp
namespace Bank
{
  using System;

  public class InsufficientFundsException : ApplicationException
  {
  }
}
```

Add a new test method to our `AccountTest` class:

```csharp
[Test]
[ExpectedException(typeof(InsufficientFundsException))]
public void TransferWithInsufficientFunds()
{
  Account source = new Account();
  source.Deposit(200m);

  Account destination = new Account();
  destination.Deposit(150m);

  source.TransferFunds(destination, 300m);
}
```

This test method in addition to `[Test]` attribute has an `[ExpectedException]` attribute associated with it –
this is the way to indicate that the test code is expecting an exception of a certain type;
if such an exception is not thrown during the execution – the test will fail.
Click the **RUN TESTS** button – we have a red status bar again. We got the following `Failure`:

```
TransferWithInsufficentFunds : InsufficientFundsException was expected
```

Let’s fix our Account code again, modify the TransferFunds method this way:

```csharp
public void TransferFunds(Account destination, decimal amount)
{
  destination.Deposit(amount);

  if(balance-amount < minimumBalance)
    throw new InsufficientFundsException();

  Withdraw(amount);
}
```

Run the tests – green bar.
Success! But wait, looking at the code we’ve just written we can see that the bank may be
loosing money on every unsuccessful funds Transfer operation.
Let’s write a test to confirm our suspicions.
Add this test method:

```csharp
[Test]
public void TransferWithInsufficientFundsAtomicity()
{
  Account source = new Account();
  source.Deposit(200m);

  Account destination = new Account();
  destination.Deposit(150m);

  try
  {
      source.TransferFunds(destination, 300m);
  }
  catch(InsufficientFundsException expected)
  {
  }

  Assert.AreEqual(200m, source.Balance);
  Assert.AreEqual(150m, destination.Balance);
}
```

We are testing the transactional property of our business method – all operations are successful or none.
Running this gets an error again.
OK, we’ve made $300.00 out of a thin air –
the source account has the correct balance of 200.00 but the destination account shows: $450.00.
How do we fix this?
Can we just move the minimum balance check call in front of the updates:

```csharp
public void TransferFunds(Account destination, decimal amount)
{
  if (balance-amount < minimumBalance)
    throw new InsufficientFundsException();

  destination.Deposit(amount);

  Withdraw(amount);
}
```

Looking at our test code we can see that some refactoring is in order.
All test methods share a common set of test objects.
Let’s extract this initialization code into a setup method and reuse it in all of our tests.
The refactored version of our test class looks like this:

```csharp
namespace Bank
{
  using NUnit.Framework;

  [TestFixture]
  public class AccountTest
  {
    Account source;
    Account destination;

    [SetUp]
    public void Init()
    {
      source = new Account();
      source.Deposit(200m);

      destination = new Account();
      destination.Deposit(150m);
    }

    [Test]
    public void TransferFunds()
    {
      source.TransferFunds(destination, 100m);

      Assert.AreEqual(250m, destination.Balance);
      Assert.AreEqual(100m, source.Balance);
    }

    [Test]
    [ExpectedException(typeof(InsufficientFundsException))]
    public void TransferWithInsufficientFunds()
    {
      source.TransferFunds(destination, 300m);
    }

    [Test]
    [Ignore("Decide how to implement transaction management")]
    public void TransferWithInsufficientFundsAtomicity()
    {
      try
      {
        source.TransferFunds(destination, 300m);
      }
      catch(InsufficientFundsException expected)
      {
      }

      Assert.AreEqual(200m, source.Balance);
      Assert.AreEqual(150m, destination.Balance);
    }
  }
}
```

Note that `Init` method has the common initialization code,
it has void return type, no parameters, and it is marked with `[SetUp]` attribute.

## Learn More

You can learn more on the [NUnit website](http://www.nunit.org/).

{% comment %}

- <https://www.qualified.io/kb/languages/csharp/nunit>

TODO:

- Add simple references
- Move most of this to 'tutorials'

{% endcomment %}
