# Java

An FFM (Panama) wrapper over the C ABI. Construct a `Screener` from a JSON spec,
then drive it with `command(json) -> json`.

```xml
<!-- Maven Central -->
<dependency>
  <groupId>org.wickra</groupId>
  <artifactId>wickra-screener</artifactId>
  <version>0.1.0</version>
</dependency>
```

```java
import org.wickra.screener.Screener;

public final class Scan {
    public static void main(String[] args) {
        String spec = """
            {"universe":["AAA","BBB"],
             "condition":{"type":"cmp",
               "left":{"kind":"indicator","name":"Rsi","params":[14]},
               "op":"lt","right":{"kind":"const","value":30.0}}}""";

        try (Screener screener = new Screener(spec)) {
            String response = screener.command("{\"cmd\":\"scan\",\"data\":{}}");
            System.out.println("wickra-screener " + Screener.version());
            System.out.println(response);
        }
    }
}
```

The binding uses the Java Foreign Function & Memory API, so it needs JDK 22+ and
`--enable-native-access`.

## More

- [Maven Central](https://central.sonatype.com/artifact/org.wickra/wickra-screener)
- [Source & examples](https://github.com/wickra-lib/wickra-screener/tree/main/examples/java)
