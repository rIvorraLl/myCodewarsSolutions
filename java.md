**8 kyu**

- String repeat
```java
public class Solution {
    public static String repeatStr(final int repeat, final String string) {
      String newStr = "";
      for (int i = 0; i < repeat; i++) {
        newStr += string;
      }
        return newStr;
    }
}

```
- Convert a boolean to string

```java
public class BooleanToString {
  public static String convert(boolean b){
    if (b == true) {
      return "true";
    } else {
      return "false";
    }
  }

}

```
- Basic variable assignment

```java
public class Kata {
    public static String a = "code";
    public static String b = "wa.rs";
    public static String name = a + b;
}

```
