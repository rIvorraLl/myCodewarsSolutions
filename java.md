**5 kyu**
- Largest Difference in Increasing Indexes

```java
public class LargestDifference {
    public static int largestDifference(int[] data) {
    int prov = 0;
    for (int i = 0; i < data.length; i++) {
      for (int j = data.length-1; j > 0; j--) {
        if (data[i] <= data[j]) {
          if (j - i > prov) {
            prov = j - i;
            j = data.length;
          }
        }
      }
    }
      return prov;
    }
}
```

**6 kyu**
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

- Multiples of 3 or 5

```java
public class Solution {

  public int solution(int number) {
    if (number == 0) {
      return 0;
    }
    int sum = 0;
    for (int i = 3; i < number; i++) {
      if (i % 3 == 0 || i % 5 == 0) {
        sum = sum + i;
      } 
    }
    return sum;
  }
}
```

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
  
- The old switcheroo

```java
public class Kata {
    public static String vowel2Index(String s) {
        char[] vowels = { 'a', 'e', 'i', 'o', 'u' };
        String newStr = new String();
        boolean flag = false;
        for (int i = 0; i < s.length(); i++) {
            for (int j = 0; j < vowels.length; j++) {
                if (s.charAt(i) == vowels[j]) {
                    newStr += i + 1;
                    flag = true;
                    j = vowels.length;
                }
            }
            if (!flag) {
                newStr += s.charAt(i);
            } else {
                flag = false;
            }
        }
        return newStr;
    }
}
```

- Special Number (Special Numbers Series #5)

```java
public class Solution {
    public static String specialNumber(int number) {
      char[] notSpecialNums = {'6', '7', '8', '9'};
      String num = number + "";
      for (int i = 0; i < num.length(); i++) {
        for (int j = 0; j < notSpecialNums.length; j++) {
        if (num.charAt(i) == notSpecialNums[j]) {
          return "NOT!!";
          }
        }
      }
      return "Special!!";
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

- Count the digit
```java
public class CountDig {
    
    public static int nbDig(int n, int d) {
      int counter = 0;
      String keeper = new String();
      for (int i = 0; i <= n; i++) {
        int power = i * i;
        keeper += power + "";
      }
      char searched = 0;
      char[] strNums = { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9'};
      int[] nums = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
      for (int m = 0; m < nums.length; m++) {
        if (nums[m] == d) {
          searched = strNums[m];
        }
      }
      for (int j = 0; j < keeper.length(); j++) {
        if (keeper.charAt(j) == searched) {
          counter++;
        }
      }
      return counter;
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

- Printer error

```java
public class Printer {
    
    public static String printerError(String s) {
      int errors = 0;
      char[] wrongLetters = {'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'};
      for (int i = 0; i < s.length(); i++) {
        for (int j = 0; j < wrongLetters.length; j++) {
          if (s.charAt(i) == wrongLetters[j]) {
            errors++;
            j = wrongLetters.length;
          }
        }
        
      }
      return errors + "/" + s.length();
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

- Simple beads count
```java
public class BeadsCounter {
    public static int countRedBeads(final int nBlue) {
      if (nBlue < 1) {
        return 0;
      } else {
        return (nBlue -1) * 2;
      }
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
    if (b) {
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
