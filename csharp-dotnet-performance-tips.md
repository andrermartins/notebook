# C# .NET Performance Tips

## 1) Array and List Empty
To initialize arrays:
```
// Prefer
string[] cars = Array.Empty<string>();
// Or else
string[] cars = [];
```
To initialize lists:
```
// Prefer
List<string> bikes = Enumerable.Empty<string>();
```

## 2) Rethrow Exceptions
The better way to rethrow exceptions:
```
try
{
  DoSomeWork();
  DoOtherWork();
}
catch (Exception ex)
{
  Console.WriteLine("An unexpected error has occurred.");
  throw;
}
```

## 3) Log Message Interpolation
Prefer to use string interpolation instead of concatenation:
```
logger.LogInformation("Number Payment: {id}", id);
```

## 4) Compile Time Regex
With source-generated Regex, eliminating any runtime parsing or IL compilation overhead and you'll get a compile-time error:
```
[GeneratedRegex(@"^\d{4}-\d{2}-\d{2}$")]
private static partial Regex DateRegex();

public bool isDateValid(string date)
{
  return DateRegex().IsMatch(date)
}
```

## 5) Sealed Class
If you don't expect or want the class to be extended through inheritance, use sealed to optimize performance:
```
public sealed class PaymentProcessor
{
  public void ProcessPayment()
  {
    Console.WriteLine("Processing payment..");
  }
}
```




