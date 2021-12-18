**6 kyu**
- Create phone number

```java
public class Kata {
    public static String createPhoneNumber(int[] numbers) {
      String newString = "(" + numbers[0] + numbers[1] + numbers[2] + ")" + " "
      + numbers[3] + numbers[4] + numbers[5] + "-"
      + numbers[6] + numbers[7] + numbers[8] + numbers[9];
      return newString;
    }
```

- Bit counting
```java
public class BitCounting {

    public static int countBits(int n) {
        int j = n;
        int len = 1;
        while (j / 2 > 0) {
            j = j / 2;
            len++;
        }
        int k = 0;
        int[] binary = new int[len];
        while (n / 2 > 0) {
            binary[k] = n % 2;
            n = n / 2;
            k++;
        }
        binary[k] = n % 2;
        int counter = 0;
        for (int i = 0; i < binary.length; i++) {
            if (binary[i] == 1) {
                counter++;
            }
        }
        return counter;
    }
  }
```

**7 kyu**
- Powers of i

```java
public class Kata {

    public static String pofi(int n) {
      int power = n % 4;
      if ((power == 0) || (power == 4)) {
        return "1";
      } else if (power == 1) {
            return "i";
  
      } else if (power == 2) {
        return "-1";
      } else {
        return "-i";
      }
    }
      
  }
  ```

  - Automorphic Number (Special Numbers Series #6)
  
  ```java
  public class Solution
{
    public static String autoMorphic(int number)
    {
      int square = number * number;
      int end = 1;
      while (number*end<=square) {
        end = end * 10;
      }
      if (square % end == number) {
        return "Automorphic";
      } else {
        return "Not!!";
      }
    }
}
```

- Bumps in the Road

```java
public class BumpsTheRoad {
  public static String bumps(final String road) {
    int counter = 0;
    for (int i = 0; i < road.length(); i++) {
      if (road.charAt(i) == 'n') {
        counter +=1;
      }
    }
    if (counter > 15) {
      return "Car Dead";
    }
    return "Woohoo!";
  }
}  
```

  - Maximum Product
  
  ```java
  public class MaxProduct {
    public int adjacentElementsProduct(int[] array) {
      int i = 1;
      int prov = array[i] * array[i-1];
      for (i = 1; i < array.length; i++) {
          if (array[i] * array[i-1] > prov) {
              prov = array[i] * array[i-1];
          }
      }
      return prov;
    }
}
```

- Stanton measure

```java
public class Kata {

    public static int stantonMeasure(int[] arr) {
        int counterOnes = 0;
        int counterStanton = 0;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == 1) {
                counterOnes++;
            }
        }
        for (int j = 0; j < arr.length; j++) {
            if (arr[j] == counterOnes) {
                counterStanton++;
            }
        }
        return counterStanton;

    }

}
```

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

- Even or odd

```java
public class EvenOrOdd {
    public static String even_or_odd(int number) {
        if (number % 2 == 0) {
          return "Even";
        }
        return "Odd";
    }
}
```
