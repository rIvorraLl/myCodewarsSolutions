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

- Square every number

```java
public class SquareDigit {

  public static int squareDigits(int n) {
    String nStr = n + "";
    int len = nStr.length();
    int augment = 1;
    String returnStr = new String();
    int i = 0;
    while (i < len) {
      int digit = n / augment % 10;
      int power = digit * digit;
      augment = augment * 10;
      returnStr = power + returnStr;
      i++;
    }
    int returnNum = Integer.parseInt(returnStr);
    return returnNum;
    }
  }
```

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
- Maximum multiple

```java
public class MaxMultiple {
  public static int maxMultiple(int divisor, int bound) {
    int n = 0;
    while (bound > 0) {
      if (bound % divisor == 0) {
        n = bound;
        bound = 0;
      }
      bound--;
    }
    return n;
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

- Number of Decimal Digits

```java
public class DecTools {
  public static int Digits(long n) {
    String str = n + "";
    return str.length();
  }
}
```
- Will you survive the zombie onslaught?
```java
public class Kata {

  public static String zombieShootout(int zombies, int range, int ammo) {
    double dRange = range;
    int killedZombies = 0;
         if (zombies == 0) {
          return "You shot all 0 zombies.";
      } else if (ammo == 0) {
           return "You shot 0 zombies before being eaten: ran out of ammo.";
         }
    while (dRange > 0) {
        killedZombies++;
        zombies--;
        ammo--;
        dRange = dRange - 0.5;
        if (ammo == 0 && zombies > 0 && dRange == 0) {
            return "You shot " + killedZombies + " zombies before being eaten: overwhelmed.";
        } else if (ammo == 0 && zombies > 0) {
            return "You shot " + killedZombies + " zombies before being eaten: ran out of ammo.";
        } else if (zombies == 0) {
            return "You shot all " + killedZombies + " zombies.";
        } 
    }
        return "You shot " + killedZombies + " zombies before being eaten: overwhelmed.";
  }
}
```

**8 kyu**

- Convert a String to a Number!

```java
public class StringToNumber {
  public static int stringToNumber(String str) {
    int provLen = str.length();
    int len = str.length();

    char[] strNums = { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9'};
    int[] nums = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    double result = 0;
    for (int i = 0; i < provLen; i++) {
      int j = 0;
      while (j < nums.length) {
        if (str.charAt(i) == strNums[j]) {
          double augment = Math.pow(10, len-1);
          result = result +  augment * nums[j];
          len--;
          j = nums.length;
        }
        j++;
      }
    }
    int intRes = (int)result;
    if (str.charAt(0) == '-') {
      double augment = Math.pow(10, len-1);
      int augmentInt = (int) augment;
      int negative = (intRes - (2 * intRes)) / 10;
      return negative;
    } else {
    return intRes;
    }

}
}
```

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
