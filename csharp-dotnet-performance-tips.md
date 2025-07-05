# C# .NET Performance Tips

## 1) Array and List Empty
To reduce memory allocations and garbage collection overhead, leading to better performance in scenarios where empty arrays are frequently returned or initialized, try this:
```
// To initialize arrays
// Prefer
string[] cars = Array.Empty<string>();
// Or else
string[] cars = [];
```
```
// To initialize lists
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

## 6) Long Time Execution
It is good for breaking up CPU-bound work on a single-threaded context (e.g., UI thread):
```
await ProcessLargeListAsync(CreateFakeList(500));

private static async Task ProcessLargeListAsync(List<int> items)
{
  for (int i = 0; i < items.Count; i++)
  {
    DoWork(items[i]);
    if (i > 0 && i % 100 == 0)
    {
      Console.WriteLine($"[Yield] After processing item {i} yielding control...");
      await Task.Yield();
    }
  }
}

private static void DoWork(int item)
{
  Console.WriteLine("Do sometring...");
}
```

## 7) ArrayPool
Instead of creating new arrays, you reuse existing ones. Benefits like reduced Allocations, lower GC pressure, improved throughput:
```
public int UsingArrayPool()
{
  byte[] buffer = ArrayPool<byte>.Shared.Rent(minimumLength: BufferSize);
  try
  {
    for (int i = 0; i < BufferSize; i++)
      buffer[i] = 42;
    int sum = 0;
    for (int i = 0; i < BufferSize; i++)
      sum += buffer[i];
    return sum;
  }
  finally
  {
    ArrayPool<byte>.Shared.Return(buffer, clearArray: true);
  }
}
```



