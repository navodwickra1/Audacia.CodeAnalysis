# Overview

The `Audacia.CodeAnalysis.Analyzers` library contains custom Roslyn analyzers. These analyzers are provided to enforce coding standards where no existing analyzer exists for the rule in question.

# Analyzers

## ACL1000 - Private fields should be prefixed with an underscore

The ACL1000 rule checks whether private field names are prefixed with an underscore. It also provides a code fix, which inserts an underscore.

Code with violation:
```csharp
public class MyClass
{
    private int number;
}
```

Code with fix:
```csharp
public class MyClass
{
    private int _number;
}
```

## ACL1001 - Variable declarations should not use a magic number

The ACL1001 rule checks for magic numbers being used in variable declarations. Magic numbers should generally be extracted to a well-named variable.

Code with violation:
```csharp
var totalPrice = price + 2.5m;
```

Code with fix:
```csharp
const decimal shippingCost = 2.5m;
var totalPrice = price + shippingCost;
```

## ACL1002 - Methods should not exceed a predefined number of statements

The ACL1002 rule checks the number of statements in a method (or property or constructor) against a maximum allowed value. This maximum value can be configured globally in the .editorconfig file, or locally using the [MaxMethodLength] attribute. In the absence of any configured value, a default maximum value of 10 is used.

Code with violation (assuming configured maximum of 5 statements):
```csharp
public void MyMethod()
{
    var one = 1;
	var two = 2;
	var three = 3;
	var four = 4;
	var five = 5;
	var six = 6;
}
```

Code with local override of maximum allowed statements:
```csharp
[MaxMethodLength(6)]
public void MyMethod()
{
    var one = 1;
	var two = 2;
	var three = 3;
	var four = 4;
	var five = 5;
	var six = 6;
}
```