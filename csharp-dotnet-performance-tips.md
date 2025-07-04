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
