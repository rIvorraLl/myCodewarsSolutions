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
