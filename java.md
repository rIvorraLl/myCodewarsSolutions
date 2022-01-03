**5 kyu**

- Gap in primes

```java
import java.util.Arrays;

class GapInPrimes {

    public static Boolean isPrime(long number) {
        long i = 2;
        boolean result = true;
        while (i < number) {
            if (number % i == 0) {
                result = false;
                i = number;
            }
            i++;
        }
        return result;
    }

    public static long[] gap(int g, long m, long n) {
        long prime1 = 0;
        long[] arr = new long[2];

        for (long i = m; i <= n; i++) {
            if (isPrime(i)) {
                if (i - prime1 == g) {
                    arr[0] = prime1;
                    arr[1] = i;
                    return arr;
                } else {
                    prime1 = i;
                }
            }
        }
        return null;
    }
}
```

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
          }
        }
      }
    }
    return prov;
    }
}
```

- Simple pig latin

```java
public class PigLatin {
    public static String pigIt(String str) {
      String[] splitStr = str.split("\\s");
      String result = new String();
      for (int i = 0; i < splitStr.length; i++) {
        int len = splitStr[i].length();
        String slice = splitStr[i];
        if (slice.equals("!") || slice.equals("?")) {
          result += slice;
        } else {
          result += slice.substring(1, len) + slice.substring(0, 1) + "ay" + " ";
        }
      }
      return result.strip();
    }
}
```

- Greed is Good

```java
    public class Greed {

        public static int greedy(int[] dice) {
            int p1 = 0;
            int p2 = 0;
            int p3 = 0;
            int p4 = 0;
            int p5 = 0;
            int p6 = 0;
            int total = 0;
            for (int i = 0; i < dice.length; i++) {
                if (dice[i] == 1) {
                    p1++;
                } else if (dice[i] == 2) {
                    p2++;
                } else if (dice[i] == 3) {
                    p3++;
                } else if (dice[i] == 4) {
                    p4++;
                } else if (dice[i] == 5) {
                    p5++;
                } else {
                    p6++;
                }
            }
            System.out.println(p1);
            if (p1 > 2) {
                total += 1000;
                p1 = p1 - 3;
            } else if (p2 > 2) {
                total += 200;
            } else if (p3 > 2) {
                total += 300;
            } else if (p4 > 2) {
                total += 400;
            } else if (p5 > 2) {
                total += 500;
                p5 = p5 - 3;
            } else if (p6 > 2) {
                total += 600;
            }
            if (p1 > 0) {
                total += 100 * p1;
            }
            if (p5 > 0) {
                total += 50 * p5;
            }
            return total;
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

- Pair of gloves

```java
class Kata {

    public static int numberOfPairs(String[] gloves) {
        String[] colors = new String[gloves.length];
        int prov = 0;
        int counter = 0;
        boolean diff = false;
        for (int i = 0; i < gloves.length; i++) {
            for (int j = 0; j < colors.length; j++) {
                if (gloves[i] == colors[j]) {
                    diff = true;
                    j = colors.length;
                }
            }
            if (!diff) {
                colors[i] = gloves[i];
            }
            diff = false;
        }
        for (int k = 0; k < colors.length; k++) {
            for (int l = 0; l < gloves.length; l++) {
                if (colors[k] != null && colors[k] == gloves[l]) {
                    prov++;
                }
            }
            counter += prov / 2;
            prov = 0;
        }
        return counter;
    }
}
```

- Sum of parts

```java
class SumParts {

  public static int[] sumParts(int[] ls) {
    int len = ls.length + 1;
    int[] result = new int[len];
    int sum = 0;
    for (int i = 0; i < ls.length; i++) {
      sum += ls[i];
    }
    result[0] = sum;
    for (int j = 0; j < ls.length; j++) {
      sum -= ls[j];
      result[j + 1] = sum;
    }
    result[result.length - 1] = 0;
    return result;
  }
}
```

- Upside down

```java
public class UpsideDown {
    public static int solve(int x, int y) {
	int counter = 0;
	String prov = new String();
	String inverted = new String();
	for (int i = x; i < y; i++) {
	    prov = i + "";
	    for (int j = 0; j < prov.length(); j++) {
		if (prov.charAt(j) == '6') {
		    inverted = "9" + inverted;
		} else if (prov.charAt(j) == '9') {
		    inverted = "6" + inverted;
		} else if (prov.charAt(j) == '0' || prov.charAt(j) == '1' || prov.charAt(j) == '8') {
		    inverted = prov.charAt(j) + "" + inverted;
		}

	    }
	    if (inverted.equals(prov)) {
		counter++;
	    }
	    prov = "";
	    inverted = "";
	}
	return counter;
    }
}
```

- Find the odd int

```java
public class FindOdd {
	public static int findIt(int[] a) {
            int[] nums = new int[a.length];
            int counter = 0;
            int result = 0;
            boolean diff = false;
            for (int i = 0; i < a.length; i++) {
                for (int j = 0; j < nums.length; j++) {
                    if (a[i] == nums[j]) {
                        diff = true;
                        j = nums.length;
                    }
                }
                if (!diff) {
                    nums[i] = a[i];
                }
                diff = false;
            }
            for (int k = 0; k < nums.length; k++) {
                for (int l = 0; l < a.length; l++) {
                    if (nums[k] == a[l]) {
                        counter++;
                    }
                }
                if (counter % 2 != 0) {
                    result = nums[k];
                    k = nums.length;
                }
            }
            return result;
  }
}
```

- Stop gninnipS My sdroW!

```java
public class SpinWords {

    public String spinWords(String sentence) {
        String[] splitted = sentence.split(" ");
        String newString = new String();
        String prov = new String();
        for (int i = 0; i < splitted.length; i++) {
            if (splitted[i].length() < 5) {
                newString += splitted[i] + " ";
            } else {
                for (int j = 0; j < splitted[i].length(); j++) {
                    String word = splitted[i];
                    prov = word.charAt(j) + prov;
                }
                newString += prov + " ";
                prov = "";
            }
        }
        return newString.trim();
    }
}
```

- Is a number prime?

```java
public class Prime {
  public static boolean isPrime(int num) {
    if (num <= 1) {
      return false;
    }
    double nn = Math.sqrt(num);
    int n = (int)nn + 1;
    for (int i = 2; i < n; i++) {
      if (num % i == 0) {
        return false;
      }
    }
    return true;
  }
}
```

- Count the smiley faces!

```java
import java.util.*;

public class SmileFaces {

    public static int countSmileys(List<String> arr) {
        int counter = 0;
        for (int i = 0; i < arr.size(); i++) {
            String fc = arr.get(i);

            if (fc.length() == 3
                    && (fc.charAt(0) == ':' || fc.charAt(0) == ';')
                    && (fc.charAt(1) == '-' || fc.charAt(1) == '~')
                    && (fc.charAt(2) == ')' || fc.charAt(2) == 'D')) {
                counter++;
            } else if (fc.length() == 2
                    && (fc.charAt(0) == ':' || fc.charAt(0) == ';')
                    && (fc.charAt(1) == ')' || fc.charAt(1) == 'D')) {
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

- Who likes it?
```java
class Solution {
    public static String whoLikesIt(String... names) {
        if (names.length == 0) {
          return "no one likes this";
        } else if (names.length == 1) {
          return names[0] + " likes this";
        } else if (names.length == 2) {
          return names[0] + " and " + names[1] + " like this";
        } else if (names.length == 3) {
          return names[0] + ", " + names[1] + " and " + names[2] + " like this";
        } else {
          int diff = names.length - 2;
          return names[0] + ", " + names[1] + " and " + diff + " others like this";
        }
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

- Isograms

```java
public class isogram {
    public static String toLower(String str) {
        String lowerStr = "abcdefghijklmnopqrstuvwxyz";
        String upperStr = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String newStr = new String();
        boolean isUpper = false;
        for (int i = 0; i < str.length(); i++) {
            for (int j = 0; j < lowerStr.length(); j++) {
                if (str.charAt(i) == upperStr.charAt(j)) {
                    newStr += lowerStr.charAt(j);
                    isUpper = true;
                    j = lowerStr.length();
                }
            }
            if (!isUpper) {
                newStr += str.charAt(i);
            }
            isUpper = false;
        }
        return newStr;

        }
    public static boolean isIsogram (String str){
        if (str == "") {
          return true;
        }
        str = toLower(str);
        String newStr = str.charAt(0) + "";
        for (int i = 1; i < str.length(); i++) {
                for (int j = 0; j < newStr.length(); j++) {
                        if (str.charAt(i) == newStr.charAt(j)) {
                                return false;
                        }
                }
                newStr += str.charAt(i);
        }
        return true;
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

- Disemvowel Trolls

```java
public class Troll {
    public static String disemvowel(String str) {
      String vowels = "aeiouAEIOU";
      String nonVowels = new String();
      boolean isVowel = false;
      for (int i = 0; i < str.length(); i++) {
        for (int j = 0; j < vowels.length(); j++) {
          if (str.charAt(i) == vowels.charAt(j)) {
            isVowel = true;
            j = vowels.length();
          }
        }
        if (!isVowel) {
          nonVowels += str.charAt(i);
        }
        isVowel = false;
      }
      return nonVowels;
    }
}
```

- Nth Smallest Element (Array Series #4)

```java
public class Kata {

  public static int nthSmallest(final int[] arr, final int n) {
      for (int i = 0; i < arr.length; i++) {
          for (int j = i + 1; j < arr.length; j++) {
              int temp = 0;
              if (arr[i] > arr[j]) {
                  temp = arr[i];
                  arr[i] = arr[j];
                  arr[j] = temp;
              }
          }
      }
      return arr[n - 1];
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

- Spoonerize me

```java
public class Spooner {
    public String spoonerize(String words) {
      String[] splitW = words.split("\\s");
      String result = new String();
      int len0 = splitW[0].length();
      int len1 = splitW[1].length();
      String slice0 = splitW[0];
      String slice1 = splitW[1];
      result += slice1.substring(0, 1) + slice0.substring(1, len0) + " "
        + slice0.substring(0, 1) + slice1.substring(1, len1);
      return result;

    }
}
```

- Incrementer

```java
public class Kata {
  
  public static int[] incrementer(int[] numbers) {
    int[] incremented = new int[numbers.length];
    for (int i = 0; i < numbers.length; i++) {
      if (numbers[i] + i + 1 > 9) {
        incremented[i] = (numbers[i] + i + 1) % 10;
      } else {
        incremented[i] = numbers[i] + i + 1;
      }
    }
    return incremented;
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

- Find the next perfect square!

```java
public class NumberFun {
  public static long findNextSquare(long sq) {
    if (Math.sqrt(sq) % 1 != 0) {
      return -1;
    }
    long i = sq;
    boolean loop = true;
    while (loop) {
      i++;
      if (Math.sqrt(i) % 1 == 0) {
        loop = false;
      }
    }
    return i;
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

- Alternate case

```java
class Kata {
    static String alternateCase(final String string) {
      String newString = new String();
      String upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
      String lower = "abcdefghijklmnopqrstuvwxyz";
      boolean insert = true;
      for (int i = 0; i < string.length(); i++) {
        for (int j = 0; j < lower.length(); j++) {
          if (string.charAt(i) == upper.charAt(j)) {
            newString += lower.charAt(j);
            j = lower.length();
            insert = false;
          } else if (string.charAt(i) == lower.charAt(j)) {
            newString += upper.charAt(j);
            j = lower.length();
            insert = false;
          }
        }
        if (insert) {
          newString += string.charAt(i);
        }
        insert = true; 
      }
      return newString;
    }
}
```

- Descending order

```java
import java.util.Arrays;

public class DescendingOrder {

    public static int sortDesc(final int num) {
        String nums = num + "";
        int[] arr = new int[nums.length()];
        String sorted = new String();
        int temp = 0;
        for (int i = 0; i < nums.length(); i++) {
            String n = nums.charAt(i) + "";
            int toInt = Integer.parseInt(n);
            arr[i] = toInt;
        }
        for (int i = 0; i < arr.length; i++) {
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[j] < arr[i]) {
                    temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }
        for (int k = 0; k < arr.length; k++) {
            sorted = arr[k] + sorted;
            System.out.println(sorted);
        }
        return Integer.parseInt(sorted);
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

- Two to One

```java
public class TwoToOne {
    
    public static String longest (String s1, String s2) {
      String alphabet = "abcdefghijklmnopqrstuvwxyz";
      String merged = s1 + s2;
      String result = new String();
      for (int i = 0; i < alphabet.length(); i++) {
        for (int j = 0; j < merged.length(); j++) {
          if (alphabet.charAt(i) == merged.charAt(j)) {
            result += alphabet.charAt(i);
            j = merged.length();
          }
        }
      }
      return result;
    }
}
```

- Halving sum

```java
public class HalvingSum {
  int halvingSum(int n) {
    int sum = n;
    int index = n;
    while (index >= 1) {
      index = index /2;
      sum = sum + index;
    }
    return sum;
  }
}
```

- Complementary DNA

```java
public class DnaStrand {
  public static String makeComplement(String dna) {
    String complement = new String();
    for (int i = 0; i < dna.length(); i++) {
      if (dna.charAt(i) == 'A') {
        complement += "T";
      } else if (dna.charAt(i) == 'T') {
        complement += "A";
      } else if (dna.charAt(i) == 'C') {
        complement += "G";
      } else {
        complement += "C";
      }
    }
    return complement;
  }
}
```

- Is this a triangle?

```java
class TriangleTester{
  public static boolean isTriangle(int a, int b, int c){
    double f = (double)(a + b + c) / 2;
    if (a < f && b < f && c < f) {
      return true;
    } else {
      return false;
    }
  }
}
```

- Count all the sheep on farm in the heights of New Zealand

```java
public class Kata {
  public static int lostSheep(int[] fridayNightCounting, int[] saturdayNightCounting, int sheepTotal) {
    int counter = 0;
    for (int i = 0; i < fridayNightCounting.length; i++) {
      counter += fridayNightCounting[i];
    }
    for (int j = 0; j < saturdayNightCounting.length; j++) {
      counter += saturdayNightCounting[j];
    }
    int lost = sheepTotal - counter;
    return lost;
  }
}
```

- Largest pair sum in array

```java
public class Solution {
    public static int largestPairSum(int[] numbers) {
        int prov1 = -1000000000;
        Integer prov2 = -1000000000;
        int noRepeat = 0;
        for (int i = 0; i < numbers.length; i++) {
            if (numbers[i] > prov1) {
                prov1 = numbers[i];
                noRepeat = i;
            }
        }
        for (int j = 0; j < (numbers.length); j++) {
            if (numbers[j] > prov2 && j != noRepeat) {
                prov2 = numbers[j];
            }
        }
        return prov1 + prov2;
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

- Abbreviate Two Words

```java
public class AbbreviateTwoWords {

    public static String abbrevName(String name) {
        String upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String lower = "abcdefghijklmnopqrstuvwxyz";
        String initials = new String();
        for (int i = 0; i < name.length(); i++) {
            for (int j = 0; j < lower.length(); j++) {
                if (i == 0) {
                    if (name.charAt(i) == upper.charAt(j)
                            || name.charAt(i) == lower.charAt(j)) {
                        initials = upper.charAt(j) + ".";
                        j = lower.length();
                    }
                } else if (name.charAt(i) == ' ') {
                    for (int k = 0; k < lower.length(); k++) {
                        if (name.charAt(i + 1) == upper.charAt(k)
                                || name.charAt(i + 1) == lower.charAt(k)) {
                            initials += upper.charAt(k);
                            k = lower.length();
                            i++;
                        }
                    }
                }
            }
        }
        return initials;
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

- Square(n) Sum

```java
public class Kata
 {
  public static int squareSum(int[] n)
  { 
    int total = 0;
    for (int i = 0; i < n.length; i++) {
      total = total + (n[i] * n[i]);
    }
    return total;
  }
 }
```

- Calculate BMI

```java
public class Calculate {
  public static String bmi(double weight, double height) {
    double bmiNum = weight / (height * height);
    if (bmiNum <= 18.5) {
      return "Underweight";
    } else if (bmiNum <= 25.0) {
      return "Normal";
    } else if (bmiNum <= 30.0) {
      return "Overweight";
    } else {
      return "Obese";
    }
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

- Grasshopper - Check for factor

```java
public class Kata {
    public static boolean checkForFactor(int base, int factor) {
        return base % factor == 0;
    }
}


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
