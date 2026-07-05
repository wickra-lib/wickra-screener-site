# C#

Idiomatic .NET over the C ABI. Construct a `Screener` from a JSON spec, then drive
it with `Command(json) -> json`.

```bash
dotnet add package WickraScreener
```

```csharp
using WickraScreener;

var spec = """
{"universe":["AAA","BBB"],
 "condition":{"type":"cmp",
   "left":{"kind":"indicator","name":"Rsi","params":[14]},
   "op":"lt","right":{"kind":"const","value":30.0}}}
""";

using var screener = new Screener(spec);
var response = screener.Command("""{"cmd":"scan","data":{ }}""");
Console.WriteLine(response);
```

Targets .NET 8.

## More

- [NuGet](https://www.nuget.org/packages/WickraScreener)
- [Source & examples](https://github.com/wickra-lib/wickra-screener/tree/main/examples/csharp)
