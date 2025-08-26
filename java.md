**4 kyu**

- Vigenère cipher helper

```java
import java.util.HashMap;

public class VigenereCipher {
	private String key;
	private String abc;

	public VigenereCipher(String key, String abc) {
		this.key = key;
		this.abc = abc;
	}

	public String encode(String str) {
		String result = "";
		final HashMap<String, Integer> alphabetIndexesMap = getAlphabetIndexesMap();
		final char[] strArr = str.toCharArray();
		final char[] fullKey = getFullKey(this.key, str).toCharArray();
		int i = 0;
		for (char c : strArr) {
			String cs = String.valueOf(c);
			if (alphabetIndexesMap.get(cs) == null) {
				result += cs;
				i++;
			} else {
				int strIndex = alphabetIndexesMap.get(cs);
				int keyIndex = alphabetIndexesMap.get(String.valueOf(fullKey[i]));
				int displacement = (strIndex + keyIndex) % this.abc.length();
				result += this.abc.charAt(displacement);
				i++;
			}

		}
		return result;
	}

	public String decode(String str) {
		String result = "";
		final HashMap<String, Integer> alphabetIndexesMap = getAlphabetIndexesMap();
		final char[] strArr = str.toCharArray();
		final char[] fullKey = getFullKey(this.key, str).toCharArray();
		int i = 0;
		for (char c : strArr) {
			String cs = String.valueOf(c);
			if (alphabetIndexesMap.get(cs) == null) {
				result += cs;
				i++;
			} else {
				int strIndex = alphabetIndexesMap.get(cs);
				int keyIndex = alphabetIndexesMap.get(String.valueOf(fullKey[i]));
				if (strIndex - keyIndex >= 0) {
					int displacement = (strIndex - keyIndex) % this.abc.length();
					result += this.abc.charAt(displacement);
					i++;
				} else {
					int displacement = (strIndex - keyIndex + this.abc.length()) % this.abc.length();
					result += this.abc.charAt(displacement);
					i++;
				}
			}

		}
		return result;
	}

	private final HashMap<String, Integer> getAlphabetIndexesMap() {
		HashMap<String, Integer> indexesMap = new HashMap<>();
		Integer i = 0;
		char[] alphabet = this.abc.toCharArray();
		for (char c : alphabet) {
			indexesMap.put(String.valueOf(c), i);
			i++;
		}
		return indexesMap;
	}

	private final String getFullKey(String key, String str) {
		if (str.length() <= this.key.length()) {
			return key;
		}
		String result = "";
		int repeats = str.length() / this.key.length() + 1;
		for (int i = 0; i < repeats; i++) {
			result += this.key;
		}
		return result.substring(0, str.length());
	}

	public String getKey() {
		return key;
	}

	public void setKey(String key) {
		this.key = key;
	}

	public String getAbc() {
		return abc;
	}

	public void setAbc(String abc) {
		this.abc = abc;
	}
}
```

- Snail

```java
public class Snail {

	public static int[] snail(int[][] array) {
		if (array == null || array.length == 0 || array[0].length == 0) {
			return new int[0];
		}

		int size = array.length * array[0].length;
		int[] result = new int[size];
		int resultIndex = 0;
		int consumed = 0;
		int n = array.length;
		int top = 0, bottom = n - 1, left = 0, right = n - 1;

		while (consumed < size) {
			for (int i = left; i <= right && consumed < size; i++) {
				result[resultIndex++] = array[top][i];
				consumed++;
			}
			top++;

			for (int i = top; i <= bottom && consumed < size; i++) {
				result[resultIndex++] = array[i][right];
				consumed++;
			}
			right--;

			if (top <= bottom) {
				for (int i = right; i >= left && consumed < size; i--) {
					result[resultIndex++] = array[bottom][i];
					consumed++;
				}
				bottom--;
			}

			if (left <= right) {
				for (int i = bottom; i >= top && consumed < size; i--) {
					result[resultIndex++] = array[i][left];
					consumed++;
				}
				left++;
			}
		}
		return result;
	}
}
```

- Strip Comments

```java
public class StripComments {

	public static String stripComments(String text, String[] commentSymbols) {
		String[] splStr = text.split("\n");
		String prov = "";
		String result = "";
		boolean control = false;

		for (int i = 0; i < splStr.length; i++) {
			prov = "";
			control = false;
			for (int j = 0; j < splStr[i].length(); j++) {
				if (!control) {
					for (int k = 0; k < commentSymbols.length; k++) {
						if ((splStr[i].charAt(j) + "").equals(commentSymbols[k])) {
							control = true;
							break;
						}
					}
					if (!control) {
						prov += splStr[i].charAt(j);
					}
				}
			}
			result += prov.replaceAll("\\s+$", "");
			result += "\n";
		}

		if (!text.isEmpty() && text.charAt(text.length() - 1) != '\n' && result.length() > 0) {
			result = result.substring(0, result.length() - 1);
		}

		return result;
	}
}
```

- A Simplistic TCP Finite State Machine (FSM)

```java
import java.util.HashMap;
import java.util.Map;

public class TCP {

	public static String traverseStates(String[] events) {
		Map<String, String> stateEventMap = stateEventMapBuilder();
		String state = "CLOSED";
		for (String event : events) {
			String key = state + ":" + event;
			if (stateEventMap.containsKey(key)) {
				state = stateEventMap.get(key);
			} else {
				return "ERROR";
			}
		}
		return state;
	}

	private static Map<String, String> stateEventMapBuilder() {
		Map<String, String> stateEventMap = new HashMap<String, String>();
		stateEventMap.put("CLOSED:APP_PASSIVE_OPEN", "LISTEN");
		stateEventMap.put("CLOSED:APP_ACTIVE_OPEN", "SYN_SENT");
		stateEventMap.put("LISTEN:RCV_SYN", "SYN_RCVD");
		stateEventMap.put("LISTEN:APP_SEND", "SYN_SENT");
		stateEventMap.put("LISTEN:APP_CLOSE", "CLOSED");
		stateEventMap.put("SYN_RCVD:APP_CLOSE", "FIN_WAIT_1");
		stateEventMap.put("SYN_RCVD:RCV_ACK", "ESTABLISHED");
		stateEventMap.put("SYN_SENT:RCV_SYN", "SYN_RCVD");
		stateEventMap.put("SYN_SENT:RCV_SYN_ACK", "ESTABLISHED");
		stateEventMap.put("SYN_SENT:APP_CLOSE", "CLOSED");
		stateEventMap.put("ESTABLISHED:APP_CLOSE", "FIN_WAIT_1");
		stateEventMap.put("ESTABLISHED:RCV_FIN", "CLOSE_WAIT");
		stateEventMap.put("FIN_WAIT_1:RCV_FIN", "CLOSING");
		stateEventMap.put("FIN_WAIT_1:RCV_FIN_ACK", "TIME_WAIT");
		stateEventMap.put("FIN_WAIT_1:RCV_ACK", "FIN_WAIT_2");
		stateEventMap.put("CLOSING:RCV_ACK", "TIME_WAIT");
		stateEventMap.put("FIN_WAIT_2:RCV_FIN", "TIME_WAIT");
		stateEventMap.put("TIME_WAIT:APP_TIMEOUT", "CLOSED");
		stateEventMap.put("CLOSE_WAIT:APP_CLOSE", "LAST_ACK");
		stateEventMap.put("LAST_ACK:RCV_ACK", "CLOSED");

		return stateEventMap;
	}
}
```

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

- String incrementer

```java
import java.math.BigInteger;

public class Kata {
	public static String incrementString(String str) {
		if (str == "") {
			return "1";
		}
		String number = new String();
		char lastChar = str.charAt(str.length() - 1);
		if (! Character.isDigit(lastChar)) {
			return str + "1";
		} else {
			int counter = str.length();
			while (Character.isDigit(str.charAt(counter - 1))) {
				counter--;
				if (counter == 0) {
					break;
				}
			}
			String substrEnd = str.substring(counter);
			String substrStart = str.substring(0, counter);
			String leadingZeros = new String();
			for (int i = 0; i < substrEnd.length(); i++) {
				if (substrEnd.charAt(i) == '0') {
					leadingZeros += "0";
				} else {
					i = substrEnd.length();
				}
			}
			BigInteger endNumber = new BigInteger(substrEnd);
			boolean isAllZero = true;
			for (int i = 0; i < substrEnd.length(); i++) {
				if (substrEnd.charAt(i) != '0') {
					isAllZero = false;
				}
			}
			String endNumToStr = endNumber.toString();
			BigInteger one = new BigInteger("1");
			endNumber = endNumber.add(one);
			String endPlusOne = endNumber.toString();
			if (endPlusOne.length() > endNumToStr.length()
					&& leadingZeros.length() > 0
					|| isAllZero) {
				leadingZeros = leadingZeros.substring(0, leadingZeros.length() - 1);
			}
			return substrStart + leadingZeros + endNumber;
		}
	}
}
```

- Pete the Baker
```java
import java.util.Map;
import java.util.ArrayList;
import java.util.List;
import java.util.Map.Entry;

public class PeteTheBaker {
	public static int cakes(Map<String, Integer> recipe, Map<String, Integer> available) {
		List<Integer> possibles = new ArrayList<Integer>();
		for (Entry<String, Integer> item : recipe.entrySet()) {
			if (!available.containsKey(item.getKey())) {
				return 0;
			} else {
				possibles.add(available.get(item.getKey()) / item.getValue());

			}
		}
		int result = possibles.get(0);
		for (Integer i : possibles) {
			if (i < result) {
				result = i;
			}
		}
		return result;
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

- Mean Square Error

```java
public class Solution {
	public static double solution(int[] arr1, int[] arr2) {
		int[] arr3 = new int[arr1.length];
		double total = 0;
		for (int i = 0; i < arr1.length; i++) {
			arr3[i] = (int) Math.pow(Math.abs(arr1[i] - arr2[i]), 2);
			total += arr3[i];
		}
		return total / arr1.length;
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

- Rot 13

```java
	public static String rot13(String str) {
		String result = "";
		String[] alphabet = { "a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r",
				"s", "t", "u", "v", "w", "x", "y", "z", "a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m",
				"n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z" };
		boolean isLetter = false;
		for (int i = 0; i < str.length(); i++) {
			for (int j = 0; j < alphabet.length - 26; j++) {
				String s = String.valueOf(str.charAt(i));
				if (s.equals(alphabet[j].toLowerCase())) {
					result += alphabet[j + 13];
					isLetter = true;
					break;
				} else if (s.equals(alphabet[j].toUpperCase())) {
					result += alphabet[j + 13].toUpperCase();
					isLetter = true;
					break;
				}
			}
			if (!isLetter) {
				result += str.charAt(i);
			}
			isLetter = false;
		}
		return result;
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

- Stone bridge primes

```java
import java.util.HashSet;

class Solution{
	public static int solve(int x, int y) {
		HashSet<Integer> candidatesSet = new HashSet<Integer>();
		int max_m = (int) Math.floor(Math.log(y) / Math.log(2));
		int max_n = (int) Math.floor(Math.log(y) / Math.log(3));
		for (int m = 0; m <= max_m; m++) {
			for (int n = 0; n <= max_n; n++) {
				int candidate = (int) Math.pow(2, m) * (int) Math.pow(3, n) + 1;
				if (candidate <= y && candidate >= x && isPrime(candidate)) {
					candidatesSet.add(candidate);
				}
			}
		}
		return candidatesSet.size();
	}

	static boolean isPrime(int num) {
		if (num <= 1)
			return false;
		if (num <= 3)
			return true;
		if (num % 2 == 0 || num % 3 == 0)
			return false;
		for (int i = 2; i < Math.sqrt(num) + 1; i += 1) {
			if (num % i == 0) {
				return false;
			}
		}
		return true;
	}
}
```

- Simple prime streaming

```java
public class SimplePrimeStreaming {
    public static String solve(int a, int b) {
        return primesString(a, b).substring(a, (a + b)); //..
    }
    
    private static String primesString(int index, int positions) {
    	String result = "";
    	int i = 2;
    	boolean condition = false;
    	while (!condition) {
    		if (isPrime(i)) {
    			result += i;
    		}
    		i++;
    		if (result.length() >= (index + positions)) {
    			condition = true;    			
    		}
    	}
    	return result;
    }
    
	private static boolean isPrime(int num) {
		if (num <= 3)
			return true;
		if (num % 2 == 0 || num % 3 == 0)
			return false;
		for (int i = 2; i < Math.sqrt(num) + 1; i += 1) {
			if (num % i == 0) {
				return false;
			}
		}
		return true;
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

- Follow that Spy

```java
public class Routes {
	public String findRoutes(String[][] routes) {
		String[] origins = setSubList(routes, 0);
		String[] destinations = setSubList(routes, 1);
		String[] resultArr = new String[routes.length + 1];
		int index = 1;
		String route = startingPoint(origins, destinations);
		resultArr[0] = route;
		while (index < resultArr.length) {
			for (int i = 0; i < origins.length; i++) {
				if (origins[i].equals(route)) {
					resultArr[index] = destinations[i];
					route = destinations[i];
					index++;
				}
			}
		}
		return String.join(", ", resultArr);
	}

	private String[] setSubList(String[][] routes, int index) {
		String[] result = new String[routes.length];
		for (int i = 0; i < routes.length; i++) {
			result[i] = routes[i][index];
		}
		return result;
	}

	private String startingPoint(String[] origins, String[] destinations) {
		boolean isOrigin = true;
		String result = "";
		for (int i = 0; i < origins.length; i++) {
			for (int j = 0; j < destinations.length; j++) {
				if (origins[i].equals(destinations[j])) {
					isOrigin = false;
				}
			}
			if (isOrigin) {
				result = origins[i];
				break;
			} else {
				isOrigin = true;
			}
		}
		return result;
	}
}
```

- Convert ISBN-10 to ISBN-13

```java
public class Solution {

    public static String isbnConverter(String isbn) {
        String nums = "0123456789";
        String addPrefix = "978";
        for (int i = 0; i < isbn.length() - 1; i++) {
            for (int j = 0; j < nums.length(); j++) {
                if (isbn.charAt(i) == nums.charAt(j)) {
                    addPrefix += nums.charAt(j);
                    j = nums.length();
                }
            }
        }
        int multDigit = 0;
        for (int i = 0; i < addPrefix.length(); i++) {
            if (i == 0 || i % 2 == 0) {
              char tempChar = addPrefix.charAt(i);
                int tempNum = Integer.parseInt(String.valueOf(tempChar));
                multDigit+= tempNum;
            } else {
                char tempChar = addPrefix.charAt(i);
                int tempNum2 = Integer.parseInt(String.valueOf(tempChar));
                int multiplied = tempNum2 * 3;
                multDigit+= multiplied;
                
            }
        }
        int moduloOperation = multDigit % 10;
        if (moduloOperation > 0) {
	    moduloOperation = 10 - moduloOperation;
            addPrefix += moduloOperation + " ";
        } else {
            addPrefix += "0";
        }
        return "978-" + isbn.substring(0,12) + addPrefix.charAt(12);
        
    }
}
```

- Find a Bunch of Common Elements of Two Lists in a Certain Range

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashSet;
import java.util.List;
import java.util.Set;

class Solution {
	static List<Integer> findCommonElements(int[] arrA, int[] arrB, int[] rng, String wanted) {
		Set<Integer> provisionalSet = new HashSet<Integer>();
		ArrayList<Integer> result = new ArrayList<Integer>();
		for (int i = 0; i < arrA.length; i++) {
			if (isWanted(arrA[i], wanted) && isInRange(arrA[i], rng) && isDuplicate(arrA[i], arrA)) {
				for (int j = 0; j < arrB.length; j++) {
					if (arrA[i] == arrB[j] && isDuplicate(arrB[j], arrB)) {
						provisionalSet.add(arrA[i]);
						break;
					}
				}
			}
		}
		result.addAll(provisionalSet);
		Collections.sort(result);
		return result;
	}

	private static boolean isWanted(int num, String wanted) {
		final String even = "even";
		return wanted.equals(even) ? num % 2 == 0 : num % 2 != 0;
	}

	private static boolean isInRange(int num, int[] range) {
		return num >= range[0] && num <= range[1];
	}

	private static boolean isDuplicate(int num, int[] arr) {
		int counter = 0;
		for (int i = 0; i < arr.length; i++) {
			if (arr[i] == num) {
				counter++;
				if (counter > 1) {
					break;
				}
			}
		}
		return counter > 1;
	}
}
```

- Your order, please

```java
import java.util.Arrays;

public class Order {
	public static String order(String words) {
		if (words.length() == 0) {
			return "";
		}
		String[] wordList = words.split(" ");
		int[] stringNums = new int[wordList.length];
		int index = 0;
		for (String word : wordList) {
			String number = "";
			for (int i = 0; i < word.length(); i++) {
				if (Character.isDigit(word.charAt(i))) {
					number += word.charAt(i);
				}
			}
			stringNums[index] = Integer.parseInt(number);
			index++;
			number = "";
		}
		int[] copyOfStringNums = Arrays.copyOf(stringNums, stringNums.length);
		Arrays.sort(copyOfStringNums);
		String[] sortedWords = new String[wordList.length];
		for (int i = 0; i < copyOfStringNums.length; i++) {
			for (int j = 0; j < stringNums.length; j++) {
				if (copyOfStringNums[i] == stringNums[j]) {
					sortedWords[i] = wordList[j];
					break;
				}
			}
		}
		String result = String.join(" ", sortedWords);
		return result;
	}
}
```

- Playing with digits

```java
import java.util.Arrays;

public class DigPow {

    public static long digPow(int n, int p) {
        int k = -1;
        String nStr = n + "";
        double power = p;
        int[] arr = new int[nStr.length()];
        for (int i = 0; i < nStr.length(); i++) {
            double d = Integer.parseInt(nStr.valueOf(nStr.charAt(i)));
            arr[i] = (int) Math.pow(d, power);
            power++;
        }
        int added = 0;
        for (int j = 0; j < arr.length; j++) {
            added += arr[j];
        }        
        if (added % n == 0) {
            k = added / n;
        }
        return k;
    }
}
```

- Not prime numbers

```java

import java.util.List;
import java.util.ArrayList;

public class Solution {
    public boolean isPrime(int num) {
	if (num <= 1) {
	    return false;
	}
	double nn = Math.sqrt(num);
	int n = (int) nn + 1;
	for (int i = 2; i < n; i++) {
	    if (num % i == 0) {
		return false;
	    }
	}
	return true;
    }

    public boolean checkDigits(int num) {
	while (num > 0) {
	    int digit = num % 10;
	    if (!isPrime(digit)) {
		return false;
	    }
	    num = num / 10;
	}
	return true;
    }

    public static List<Integer> notPrimes(int a, int b) {
	Solution s = new Solution();
	ArrayList<Integer> result = new ArrayList<Integer>();
	for (int i = a; i < b; i++) {
	    boolean numIsPrime = s.isPrime(i);
	    boolean digitsArePrime = s.checkDigits(i);
	    if (!numIsPrime && digitsArePrime) {
		result.add(i);
	    }
	}
	return result;
    }
}
```

- Playing with passphrases

```java
public class PlayPass {
  public static String playPass(String s, int n) {
    String result = new String();
    String lowerS = "abcdefghijklmnopqrstuvwxyz";
    String upperS = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    String numS = "0123456789";
    boolean control = false;
    for (int i = 0; i < s.length(); i++) {
      for (int k = 0; k < upperS.length(); k++) {
        char upperC = Character.toUpperCase(s.charAt(i));
        int index = (k + n) % 26;
        if (i == 0) {
          if (upperC == upperS.charAt(k)){
            result += upperS.charAt(index);
            k = upperS.length();
            control = true;
          }         
        } else if (upperC == upperS.charAt(k)) {
          if  (i % 2 == 0) {
            result += upperS.charAt(index);
            k = upperS.length();
            control = true;
          } else if (i % 2 != 0) {
            result += lowerS.charAt(index);
            k = upperS.length();
            control = true;
          }
        }
      }
      for (int j = 0; j < numS.length(); j++) {
        if (s.charAt(i) == numS.charAt(j)) {
          int resNum = (int) (Math.abs(9 - (numS.charAt(j) - '0')));
          result += resNum + "";
          j = numS.length();
          control = true;
        }
      }
      if (!control) {
        result += s.charAt(i);
      }
      control = false;
    }
    String returnInversed = new String();
    for (int j = 0; j < result.length(); j++) {
      returnInversed = result.charAt(j) + returnInversed;
    }
    return returnInversed;
  }
}
```

- Counting duplicates

```java
public class CountingDuplicates {
  public static int duplicateCount(String text) {
    String repeatedChars = new String();
    for (int i = 0; i < text.length(); i++) {
      for (int j = 1; j < text.length(); j++) {
        if ((text.charAt(i) == text.charAt(j)
            || text.toUpperCase().charAt(i) == text.charAt(j))
            && i != j) {
          repeatedChars += text.charAt(i);
          j = text.length();
        }
      }
    }

    String nonRepeated = new String();
    for (int i = 0; i < repeatedChars.length(); i++) {
      if (nonRepeated.indexOf(repeatedChars.charAt(i)) < 0) {
        nonRepeated += repeatedChars.charAt(i);
      }
    }
    int counter = nonRepeated.length();
    return counter;
  }
}
```

- Arrh, grabscrab!

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;


public class Grab {
	public static List<String> grabscrab(String s, List<String> words) {
		List<String> result = new ArrayList<String>();
		HashMap<String, Integer> mappedS = mapWord(s);
		for (String word : words) {
			HashMap<String, Integer> mappedWord = mapWord(word);
			if (mappedWord.equals(mappedS)) {
				result.add(word);
			}
		}
		return result;
	}

	private static HashMap<String, Integer> mapWord(String word) {
		HashMap<String, Integer> mappedWord = new HashMap<String, Integer>();
		for (int i = 0; i < word.length(); i++) {
			String letter = word.charAt(i) + "";
			Integer value = mappedWord.containsKey(letter) ? mappedWord.get(letter) + 1 : 1;
			mappedWord.put(letter, value);
		}
		return mappedWord;
	}
}
```

- Srot the inner ctonnet in dsnnieedcg oredr

```java
import java.util.Arrays;
import java.util.Collections;

public class SortTheInnerContent {
	public static String sortTheInnerContent(String words) {
		String[] wordsToArr = words.split(" ");
		String[] innerSortedArr = Arrays.stream(wordsToArr).map(w -> {
			if (w.length() > 3) {
				return sortInner(w);
			} else {
				return w;
			}
		}).toArray(String[]::new);

		return String.join(" ", innerSortedArr);
	}

	private static String sortInner(String word) {
		String substring = word.substring(1, word.length() - 1);
		String[] substrArr = substring.split("");
		Arrays.sort(substrArr, Collections.reverseOrder());
		String sortedSubstr = String.join("", substrArr);
		return word.charAt(0) + sortedSubstr + word.charAt(word.length() - 1);
	}
}

```

- Word a10n (abbreviation)

```java
public class Abbreviator {

	public String abbreviate(String string) {
		String result = "";
		String word = "";
		boolean isLongerThanOne = false;
		for (int i = 0; i < string.length(); i++) {
			if (Character.isLetter(string.charAt(i))) {
				word += string.charAt(i);
			} else {
				isLongerThanOne = true;
				result += transform(word) + string.charAt(i);
				word = "";
			}
		}
		if (Character.isLetter(string.charAt(string.length() - 1))) {
			result += transform(word);
		}
		return isLongerThanOne ? result : transform(word);
	}

	public String transform(String word) {
		return (word.length() >= 4)
				? "" + word.charAt(0) + word.substring(1, word.length() - 1).length() + word.charAt(word.length() - 1)
				: word;
	}

}
```

- Array.diff

```java
public class Kata {
  public static int[] arrayDiff(int[] a, int[] b) {
    int counter = 0;
    boolean control = false;
    for (int i = 0; i < a.length; i++) {
      for (int j = 0; j < b.length; j++) {
        if (a[i] == b[j]) {
          j = b.length;
          control = true;
        }
      }
      if (!control) {
        counter++;
      }
      control = false;
    }
    int[] result = new int[counter];
    control = false;
    int index = 0;
    for (int i = 0; i < a.length; i++) {
      for (int j = 0; j < b.length; j++) {
        if (a[i] == b[j]) {
          j = b.length;
          control = true;
        }
      }
      if (!control) {
        result[index] = a[i];
        index++;
      }
      control = false;
    }
    System.out.println(counter);
    return result;
  }
}
```

- Sum of Digits / Digital Root

```java
public class DRoot {
	public static int[] getNumbersArray(int n) {
		String numberToStr = Integer.toString(n);
		int[] numsArr = new int[numberToStr.length()];
		for (int i = 0; i < numberToStr.length(); i++) {
			String ch = Character.toString(numberToStr.charAt(i));
			Integer num = Integer.valueOf(ch);
			numsArr[i] = num;
		}
		return numsArr;
	}

	public static int sumArr(int[] arr) {
		int sum = 0;
		for (int i = 0; i < arr.length; i++) {
			sum += arr[i];
		}
		return sum;
	}

	public static int digital_root(int n) {
		int result = sumArr(getNumbersArray(n));
		while (result > 9) {
			result = sumArr(getNumbersArray(result));
		}
		return result;
	}
}
```

- Collatz

```java
public class Collatz {
	public static String collatz(int n) {
		String result = n + "";
		while (n != 1) {
			if (n % 2 == 0) {
				n = n / 2;
				result += "->" + n;
			} else {
				n = n * 3 + 1;
				result += "->" + n;
			}
		}
		return result;
	}
}
```

- Calculate String Rotation

```java
public class CalculateRotation {
  static int shiftedDiff(String first, String second) {
	int rotation = 0;
	while (!first.equals(second)) {
	    first = first.substring(first.length() - 1, first.length()) + first.substring(0, first.length() - 1);
	    rotation++;
	    if (rotation == first.length()) {
		    return -1;
	    }
	}
	return rotation;
  }
}
```

- Multiplication table

```java
public class Multiplication{
	public static int[][] multiplicationTable(int n) {
		int[][] result = new int[n][n];
		int[] row = new int[n];
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				row[j] = (i + 1) * (j + 1);
			}
			result[i] = row;
			row = new int[n];
		}
		return result;
	}
}
```

- Message Validator

```java
public class Kata {
	public static boolean isAValidMessage(String message) {
		if (message.length() == 0 || message.equals("0")) {
			return true;
		}
		String[] substrings = message.split("(?<=\\d)(?=\\D)|(?<=\\D)(?=\\d)");
		try {
			for (int i = 0; i < substrings.length; i++) {
				if (i == 0 || i % 2 == 0) {
					if (Integer.valueOf(substrings[i]) != substrings[i + 1].length()) {
						return false;
					}
				}
			}
		} catch (IndexOutOfBoundsException | NumberFormatException e) {
			return false;
		}
		return true;
	}
}
```

- Mexican Wave

```java
public class MexicanWave {

    public static String[] wave(String str) {
        String[] empty = new String[0];
        int spaces = 0;
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) == ' ') {
                spaces++;
            }
        }
        int len = str.length() - spaces;
        String[] result = new String[len];
        int waved = 0;
        String provisionalWord = new String();
        if ("".equals(str)) {
            return empty;
        } else {
            for (int i = 0; i < str.length() - spaces; i++) {
                for (int j = 0; j < str.length(); j++) {
                    if (j == waved) {
                        char letter = str.charAt(j);
                        provisionalWord += Character.toUpperCase(letter);
                    } else {
                        provisionalWord += str.charAt(j);
                    }
                }            
                waved++;
                if (!(provisionalWord.equals(str))) {
                    result[i] = provisionalWord;

                } else {
                    i--;
                }
                provisionalWord = "";
            }
        }
        return result;
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

- Even Fibonacci Sum

```java
class Kata {
    public static long fibonacci(long max) {
        long result = 0;
        long prov = 1;
        long first = 1;
        long second = 2;
        while (prov < max) {
        	if (prov % 2 == 0) {
        		result += prov;
        	}
        	first = second;
        	second = prov + second;
        	prov = first;
        }
        return result;
    }
}
```

- Help the bookseller!

```java
public class StockList {
	public static String stockSummary(String[] lstOfArt, String[] lstOf1stLetter) {
		if (lstOfArt.length == 0 || lstOf1stLetter.length == 0) {
			return "";
		}
		String result = "";
		for (String s1 : lstOf1stLetter) {
			int totalInCat = 0;
			for (String lA : lstOfArt) {
				if (lA.charAt(0) == s1.charAt(0)) {
					String[] splitted = lA.split(" ");
					totalInCat += Integer.valueOf(splitted[1]);
				}
			}
			result += "(" + s1 + " : " + totalInCat + ") - ";
			totalInCat = 0;
		}
		return result.substring(0, result.length() - 3);
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

- Triple trouble

```java
public class Kata
{
	public static int TripleDouble(long num1, long num2) {
		String n1toStr = Long.toString(num1);
		String n2toStr = Long.toString(num2);
		boolean n1HasTriple = false;
		boolean n2HasDouble = false;
		char numToCheck = 0;
		for (int i = 0; i < n1toStr.length() - 2; i++) {
			if (n1toStr.charAt(i) == n1toStr.charAt(i + 1) && n1toStr.charAt(i) == n1toStr.charAt(i + 2)) {
				n1HasTriple = true;
				numToCheck = n1toStr.charAt(i);
			}
		}
		if (n1HasTriple) {
			for (int i = 0; i < n2toStr.length() - 1; i++) {
				if (n2toStr.charAt(i) == numToCheck && n2toStr.charAt(i) == n2toStr.charAt(i + 1)) {
					n2HasDouble = true;
				}
			}
		}
		if (n1HasTriple && n2HasDouble) {
			return 1;
		}
		return 0;
	}
}
```

- Highest Scoring Word

```java
import java.util.HashMap;
import java.util.Map;

public class Kata {

	public static String high(String s) {
		int value = 0;
		String result = "";
		String[] wordsArray = s.split(" ");
		for (String word : wordsArray) {
			int wordValue = calculateWordValue(word);
			if (wordValue > value) {
				result = word;
				value = wordValue;
			}
		}
		return result;
	}

	private static Map<Character, Integer> wordValueMapBuilder() {
		Map<Character, Integer> wordValueMap = new HashMap<Character, Integer>();
		char[] letters = { 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r',
				's', 't', 'u', 'v', 'w', 'x', 'y', 'z' };
		int value = 1;
		for (char c : letters) {
			wordValueMap.put(c, value);
			value++;
		}
		return wordValueMap;
	}
	
	private static int calculateWordValue(String s) {
		int value = 0;
		final Map<Character, Integer> wordValueMap = wordValueMapBuilder();
		for (int i = 0; i < s.length(); i++) {
			value += wordValueMap.get(s.charAt(i));
		}
		return value;
	}
}
```

- Delete occurrences of an element if it occurs more than n times

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class EnoughIsEnough {

	public static int[] deleteNth(int[] elements, int maxOccurrences) {
		if (maxOccurrences == 0) {
			return new int[0];
		}
		List<Integer> container = new ArrayList<Integer>();
		Map<Integer, Integer> counterMap = new HashMap<Integer, Integer>();
		for (int n : elements) {
			if (!counterMap.containsKey(n)) {
				counterMap.put(n, 1);
				container.add(n);
			}
			else if (counterMap.get(n) < maxOccurrences) {
				counterMap.put(n, counterMap.get(n) + 1);
				container.add(n);
			}
		}
		int[] result = new int[container.size()];
		int index = 0;
		for (Integer i : container) {
			result[index] = i;
			index++;
		}
		
		return result;
	}
}
```

- What century is it?

```java
public class Solution{
    public static String whatCentury(int year) {
        int century = year / 100;
        if (year % 100 > 0) {
        	century += 1;
        }
        String centuryStr = Integer.toString(century);
        String strEnd = "th";
        String[] strEndArr = {"th", "st", "nd", "rd"};
        if (century % 10 < 4 && year > 2000) {
        	strEnd = strEndArr[century % 10];
        }
        return centuryStr + strEnd;
    }
}
```

- Consecutive strings
```java
class LongestConsec {
    public static String longestConsec(String[] strarr, int k) {
    	String result = "";
    	String prov = "";
    	if (strarr.length == 0 || k > strarr.length || k <= 0) {
    		return result;
    	}
    	for (int i = 0; i < strarr.length - k + 1; i++) {
    		for (int j = i; j < i + k; j++) {
    			prov += strarr[j];
    		}
    		if (prov.length() > result.length()) {
    			result = prov;
    		}
    		prov = "";
    	}
    	return result;
    }
}
```

- Vector Affinity
```java
public class Kata {
	public static double vectorAffinity(int[] xs, int[] ys) {
		if (xs.length == 0 || ys.length == 0) {
			return xs.length == 0 && ys.length == 0 ? 1.0 : 0.0;
		}
		int[] start;
		int[] end;
		double affinity = 0.0;
		if (xs.length <= ys.length) {
			start = xs;
			end = ys;
		} else {
			start = ys;
			end = xs;
		}
		for (int i = 0; i < start.length; i++) {
			if (start[i] == end[i]) {
				affinity++;
			}
		}
		return affinity / end.length;
	}
}
```

- Circularly Sorted Array

```java
public class CircleSorted {
    public boolean isCircleSorted(int[] a) {
	int min = a[0];
	int start = 0;
	for (int i = 1; i < a.length; i++) {
	    if (a[i] < min) {
		min = a[i];
		start = i;
	    }
	}
	int[] reconstructed = new int[a.length];
	int k = 0;
	for (int i = start; i < a.length; i++) {
	    reconstructed[k] = a[i];
	    k++;
	}
	if (start != 0) {
	    for (int i = 0; i < start; i++) {
		reconstructed[k] = a[i];
		k++;
	    }
	}
	Arrays.sort(a);
	return Arrays.equals(a, reconstructed);
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

- Data Reverse

```java
public class Kata {
    public static int[] DataReverse(int[] data) {
      int[] reversed = new int[data.length];
      int begin = data.length - 8;
      int end = data.length;
      int index = 0;
      for (int i = 0; i < data.length / 8; i++) {
          for (int j = begin; j < end; j++) {
        reversed[index] = data[j];
        index++;
        }
        begin = begin - 8;
        end = end - 8;
      }
      return reversed;
    }
}
```

- Which are in?

```java
import java.util.Arrays;

public class WhichAreIn {
	public static String[] inArray(String[] array1, String[] array2) {
		int arrLen = 0;
		int index = 0;
		String resultStr = new String();
		int counter = 0;
		for (int i = 0; i < array1.length; i++) {
			for (int j = 0; j < array2.length; j++) {
				if (array2[j].contains(array1[i])) {
					arrLen++;
					j = array2.length;
				}
			}
		}
		String[] resultArray = new String[arrLen];
		for (int i = 0; i < array1.length; i++) {
			for (int j = 0; j < array2.length; j++) {
				if (array2[j].contains(array1[i])) {
					resultArray[index] = array1[i];
					j = array2.length;
					index++;
				}
			}
		}
		Arrays.sort(resultArray);
		return resultArray;
	}
}
```

- Find the parity outlier

```java
public class FindOutlier{
  static int find(int[] integers){
    boolean a = integers[0] % 2 == 0;
    boolean b = integers[1] % 2 == 0;
    boolean c = integers[2] % 2 == 0;
    boolean pairs = false;
    if ((a && b) || (a && c) || (b && c)) {
      pairs = true;
    }
    int result = 0;
    if (pairs) {
      for (int i = 0; i < integers.length; i++) {
        if (integers[i] % 2 != 0) {
          result = integers[i];
          i = integers.length;
        }
      }
    } else if (!pairs) {
      for (int i = 0; i < integers.length; i++) {
        if (integers[i] % 2 == 0) {
          result = integers[i];
          i = integers.length;
        }
      }
    }
    return result;
  }
}
```

- Decode the Morse code

```java
public class MorseCodeDecoder {
    public static String decode(String morseCode) {
      morseCode = morseCode.trim();
      String result = "";
      String[] words = morseCode.split("   ");
      for (int i = 0; i < words.length; i++) {
        String[] word = words[i].split(" ");
        for (int j = 0; j < word.length; j++) {
          result += MorseCode.get(word[j]);
        }
        result += " ";
      }
      return result.trim();
    }
}
```

- Sort the odd
```
import java.util.ArrayList;
import java.util.Collections;

public class Kata {
     public static int[] sortArray(int[] array) {
        int[] result = new int[array.length];
        ArrayList<Integer> oddNums = new ArrayList<>();
        boolean cont = true;

        for (int i = 0; i < array.length; i++) {
            if (array[i] % 2 != 0) {
                oddNums.add(array[i]);
            }
        }
        System.out.println(oddNums.toString());
        int index = 0;
        Collections.sort(oddNums);
        for (int i = 0; i < array.length; i++) {
            if (array[i] % 2 != 0) {
                result[i] = oddNums.get(index);
                index++;
            } else {
                result[i] = array[i];
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

- Valid Phone Number

```java
import java.util.regex.Pattern;

public class Kata {
  public static boolean validPhoneNumber(String phoneNumber) {
    		return Pattern.matches("[(][0-9]{3}[)][ ][0-9]{3}[-][0-9]{4}", phoneNumber);

  }
}
```

- Build Tower

```java
public class Kata {

    public static String[] TowerBuilder(int nFloors) {
        String[] tower = new String[nFloors];
        String ast = "*";
        String whitespc = " ";
        int i = 1;

        for (int j = 0; j < nFloors; j++) {
            int base = (2 * nFloors - 1 - i) / 2;
            int decimal = base % 1;
            base = base - decimal;
            tower[j] = whitespc.repeat(base) + ast.repeat(i) + whitespc.repeat(base);
            i = i + 2;
        }
        return tower;
    }
}
```

- Give me a Diamond

```java
class Diamond {
  public static String print(int n) {
    String diamond = new String();
    String space = " ";
    String asterisk = "*";
    if (n <= 0 || n % 2 == 0) {
      diamond = null;
    } else {
      int i = 0;
      int j = 1;
      while (i < (n / 2) + 1) {
        diamond += (space.repeat((n / 2) - i)) + (asterisk.repeat(j)) + "\n";
        i++;
        j = j + 2;
      }
      i = 0;
      j = 1;
      int k = 2;
      while (i < (n / 2)) {
        diamond += space.repeat(j) + asterisk.repeat(n - k) + "\n";
        i++;
        j++;
        k = k + 2;
      }
    }
    return diamond;
  }
}
```

- Errors: histogram

```java

public class HistTest {

    public static String hist(String s) {
        int uErrors=0, wErrors=0, xErrors=0, zErrors = 0;
        String star = "*";
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == 'u') {
                uErrors++;
            } else if (s.charAt(i) == 'w') {
                wErrors++;
            } else if (s.charAt(i) == 'x') {
                xErrors++;
            } else if (s.charAt(i) == 'z') {
                zErrors++;
            }
        }
        int uSpaces = 5, wSpaces = 5, xSpaces = 5, zSpaces = 5;
        if (uErrors > 9) {
            uSpaces = 4;
        }
        if (wErrors > 9) {
            wSpaces = 4;
        }
        if (xErrors > 9) {
            xSpaces = 4;
        }
        if (zErrors > 9) {
            zSpaces = 4;
        }
        String space = " ";
        String u = "u  " + uErrors + space.repeat(uSpaces) + star.repeat(uErrors) + "\r";
        String w = "w  " + wErrors + space.repeat(wSpaces) + star.repeat(wErrors) + "\r";
        String x = "x  " + xErrors + space.repeat(xSpaces) + star.repeat(xErrors) + "\r";
        String z = "z  " + zErrors + space.repeat(zSpaces) + star.repeat(zErrors) + "\r";
        String result = "";
        if (uErrors > 0) {
            result += u;
        }
        if (wErrors > 0) {
            result += w;
        }
        if (xErrors > 0) {
            result += x;
        }
        if (zErrors > 0) {
            result += z;
        }
        if (result.length() > 2) {
            result = result.substring(0, result.length() - 1);
        }
        return result;
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

- Two Sum

```java
public class Solution {
  public static int[] twoSum(int[] numbers, int target) {
    int[] returnArr = new int[2];
    for (int i = 0; i < numbers.length; i++) {
      for (int j = 0; j < numbers.length; j++) {
        if (j != i) {
          if (numbers[i] + numbers[j] == target) {
            returnArr[0] = j;
            returnArr[1] = i;
            j = numbers.length;
            i = numbers.length;
          }
        }
      }
    }
    return returnArr;
  }
}
```

- Good vs Evil

```java
public class GoodVsEvil {
	public static String battle(String goodAmounts, String evilAmounts) {
		String[] goodAmountsArr = goodAmounts.split(" ");
		String[] evilAmountsArr = evilAmounts.split(" ");
		int[] goodRacesWorth = { 1, 2, 3, 3, 4, 10 };
		int[] evilRacesWorth = { 1, 2, 2, 2, 3, 5, 10 };
		int goodTotalWorth = totalWorth(goodAmountsArr, goodRacesWorth);
		int eviltTotalWorth = totalWorth(evilAmountsArr, evilRacesWorth);
		return goodTotalWorth == eviltTotalWorth ? "Battle Result: No victor on this battle field"
				: (goodTotalWorth < eviltTotalWorth ? "Battle Result: Evil eradicates all trace of Good"
						: "Battle Result: Good triumphs over Evil");
	}

	private static int totalWorth(String[] amounts, int[] racesWorth) {
		int result = 0;
		for (int i = 0; i < amounts.length; i++) {
			result += racesWorth[i] * Integer.parseInt(amounts[i]);
		}
		return result;
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

- Count characters in your string

```java
import java.util.Map;
import java.util.HashMap;


public class Kata {
    public static Map<Character, Integer> count(String str) {
	    HashMap<Character, Integer> result = new HashMap<Character, Integer>();
      if (str.length() == 0) {
        return result;
      }
      String[] split = str.split("");
      for (String s : split) {
          if (Character.isAlphabetic(s.charAt(0))) {
            if (result.get(s.charAt(0)) == null) {
                result.put(s.charAt(0), 1);

            } else {
                int value = result.get(s.charAt(0));
                result.put(s.charAt(0), value + 1);
            }
          }
      }
    return result;
    }
}
```

- Find the unique number

```java
import java.util.Arrays;   
 public class Kata {
    public static double findUniq(double arr[]) {
      Arrays.sort(arr);
      if (arr[0] != arr[1] && arr[0] != arr[2]) {
        return arr[0];
      } else {
        return arr[arr.length-1];
      }
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

- Binary addition

```java
import java.util.ArrayList;


public class Kata{
  
	public static String binaryAddition(int a, int b) {
		int sum = a + b;
		ArrayList<Integer> digits = new ArrayList<Integer>();
		while (sum / 2 > 0) {
			digits.add(sum % 2);
			sum = sum / 2;
		}
		digits.add(sum % 2);
		String binaryStr = "";
		for (int num : digits) {
			binaryStr = String.valueOf(num) + binaryStr;
		}
		return binaryStr;
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

- Anagram detection

```java
import java.util.Arrays;

public class Kata {
	public static boolean isAnagram(String test, String original) {
		String originalToLower = original.toLowerCase();
		String testToLower = test.toLowerCase();
		char originalToCharArr[] = originalToLower.toCharArray();
		char testToCharArr[] = testToLower.toCharArray();
		String newOriginal = "";
		String newTest = "";
		Arrays.sort(originalToCharArr);
		for (int i = 0; i < originalToCharArr.length; i++) {
			newOriginal += originalToCharArr[i];
		}
		Arrays.sort(testToCharArr);
		for (int i = 0; i < test.length(); i++) {
			newTest += testToCharArr[i] ;
		}
		if (newOriginal.equals(newTest)) {
			return true;
		}
		return false;
	}
}
```

- Leap Years

```java
public class LeapYears {

  public static boolean isLeapYear(int year) {
    return (year % 100 == 0 && year % 400 != 0) ? false : year % 4 == 0;
  }
}
```

- Figurate Numbers #2 - Pronic Number

```java
public class Pronic {
	public static boolean isPronic(int n) {
		int pow = (int) Math.sqrt((double) n);
		return (pow - 1) * pow == n || pow * (pow + 1) == n ? true : false;
	}
}
```

- Is valid identifier?

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class IdentifierChecker {
	public static boolean isValid(String idn) {
		Pattern pattern = Pattern.compile("^[A-Za-z\\$\\_][A-Za-z\\$\\_\\d]*$");
		Matcher matcher = pattern.matcher(idn);
		return matcher.find();
	}
}
```

- List Filtering

```java
import java.util.List;
import java.util.stream.Collectors;

public class Kata {
	  public static List<Object> filterList(final List<Object> list) {
		    return list.stream()
		    .filter(s -> !s.getClass().getSimpleName().equals("String"))
		    .collect(Collectors.toList());
		  }
}
```

- Growth of a Population

```java
class Arge {

    public static int nbYear(int p0, double percent, int aug, int p) {
	int yearsToGoal = 0;
	int currentPopulation = p0;
	double percentIndex = percent / 100;
	while (currentPopulation < p) {
	    currentPopulation = (int) (currentPopulation * percentIndex) + aug + currentPopulation;
	    yearsToGoal++;
	}
	return yearsToGoal;
    }
}
```

- Search for letters

```java
import java.util.HashMap;

public class Letters{
	public static String search(String line) {
		String result = "";
		char[] alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".toCharArray();
		HashMap<String, String> lettersMap = new HashMap<String, String>();
		for (char c : alphabet) {
			lettersMap.put(c + "", "0");
		}
		for (char c : line.toCharArray()) {
			String s = (c + "").toUpperCase();
			if (lettersMap.containsKey(s)) {
				lettersMap.put(s, "1");
			}
		}
		for (String s : lettersMap.values()) {
			result += s;
		}
		return result;
	}
}
```

- Credit card issuer checker

```java
import java.util.HashMap;

public class Kata {
	public static String getIssuer(String cardNumber) {
		final HashMap<String, String> cardMap = getCardMap();

		final String cardLen = String.valueOf(cardNumber.length());
		final String oneInitialNum = cardNumber.substring(0, 1) + cardLen;
		final String twoInitialNum = cardNumber.substring(0, 2) + cardLen;
		final String fourInitialNum = cardNumber.substring(0, 4) + cardLen;
		String[] initialNums = { oneInitialNum, twoInitialNum, fourInitialNum };
		for (String n : initialNums) {
			if (cardMap.get(n) != null) {
				return cardMap.get(n);
			}
		}

		return "Unknown";
	}

	public static final HashMap<String, String> getCardMap() {
		final HashMap<String, String> cardMap = new HashMap<>();
		cardMap.put("3415", "AMEX");
		cardMap.put("3715", "AMEX");
		cardMap.put("5116", "Mastercard");
		cardMap.put("5216", "Mastercard");
		cardMap.put("5316", "Mastercard");
		cardMap.put("5416", "Mastercard");
		cardMap.put("5516", "Mastercard");
		cardMap.put("413", "VISA");
		cardMap.put("416", "VISA");
		cardMap.put("601116", "Discover");
		return cardMap;
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

- Return substring instance count

```java
public class Solution {
	public static int substringCount(String fullText, String search) {
		if (fullText.length() <= search.length() || search.length() == 0) {
			return 0;
		}
		int counter = 0;
		for (int i = 0; i <= fullText.length() - search.length(); i++) {
			String substring = fullText.substring(i, i + search.length());
			if (substring.equals(search)) {
				counter++;
        if (search.length() > 1) {
				i += search.length();
        }
			}
		}
		return counter;
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

- Testing 1-2-3

```java
import java.util.ArrayList;
import java.util.List;

public class LineNumbering {
	public static List<String> number(List<String> lines) {
		List<String> newList = new ArrayList<String>();
		int index = 1;
		int counter = 0;
		for (String line : lines) {
			newList.add(index + ": " + lines.get(counter));
			counter++;
      			index++;
		}
		return newList;
	}
}
```

- Sum of the first nth term of Series

```java
import java.text.DecimalFormat;

public class NthSeries {
	
	public static String seriesSum(int n) {
		double dividend = 1.0;
		double divisor = 1.0;
		double sum = 0.0;

		for (int i = 0; i < n; i++) {
			sum = sum + dividend / divisor;
			divisor += 3;
		}
		DecimalFormat df = new DecimalFormat("0.00");
		String result = String.valueOf(sum);
		result = df.format(sum);
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

- Find the index of the second occurrence of a letter in a string

```java
public class SecondOcurrence {
  public static int secondSymbol(String str, char c) {
    int counter = 0;
    for (int i = 0; i < str.length(); i++) {
      if (str.charAt(i) == c) {
        counter++;
        if (counter == 2) {
          return i;
        }
      }
    }
    return -1;
  }
}
```

- Alternate capitalization

```java
class Solution{
	public static String[] capitalize(String s) {
		String[] result = new String[2];
		result[0] = (s.charAt(0) + "").toUpperCase();
		result[1] = (s.charAt(0) + "").toLowerCase();
		for (int i = 1; i < s.length(); i++) {
			String upperCased = (s.charAt(i) + "").toUpperCase();
			result[0] = i % 2 == 0 ? result[0] + upperCased : (result[0] + s.charAt(i));
			result[1] = i % 2 != 0 ? result[1] + upperCased : (result[1] + s.charAt(i));
		}
		return result;
	}
}
```

- Factorial

```java
public class Factorial {
	public int factorial(int n) {
		if (n < 0 || n > 12) {
			throw new IllegalArgumentException();
		}
		int accumulator = 1;
		for (int i = 1; i <= n; i++) {
			accumulator *= i;
		}
		return accumulator;
	}
}
```

- Exclamation marks series #8: Move all exclamation marks to the end of the sentence

```java
public class Kata {
  public static String remove(String s){
    String exclamations = new String();
    String text = new String();
    for (int i = 0; i < s.length(); i++) {
      if (s.charAt(i) == '!') {
        exclamations += s.charAt(i);
      } else {
        text += s.charAt(i);
      }
    }
    return text + exclamations;
   }
}
```

- The highest profit wins!

```java
class MinMax {

    public static int[] minMax(int[] arr) {
        int[] result = new int[2];
        int minProv = arr[0];
        int maxProv = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > maxProv) {
                maxProv = arr[i];
            } else if (arr[i] < minProv) {
                minProv = arr[i];
            }
        }
        result[0] = minProv;
        result[1] = maxProv;
        return result;
    }
}
```

- Count consonants

```java
public class Consonants {
  public static int getCount(String str) {
    int counter = 0;
    for (int i = 0; i < str.length(); i++) {
      char c = str.charAt(i);
      if (c != 'a' && c != 'e' && c != 'i' && c != 'o' && c != 'u' && Character.isLetter(c)) {
        counter++;
      }
    }
    return counter;
  }
}
```

- Sum of two lowest positive integers

```java
import java.util.Arrays;
class Kata{
  public static long sumTwoSmallestNumbers(long [] numbers) {
    Arrays.sort(numbers);
    return numbers[0] + numbers[1];
  }             
}
```

Jaden Casing
```java

public class JadenCase {

	public String toJadenCase(String phrase) {
		String result;
		if (phrase == null) || phrase == "") {
			result = null;
		} else {
			result = (phrase.charAt(0) + "").toUpperCase();
			for (int i = 1; i < phrase.length(); i++) {
				if (phrase.charAt(i) == ' ') {
					result += (" " + phrase.charAt(i + 1)).toUpperCase();
					i++;
				} else {
					result += phrase.charAt(i);
				}
			}
		}
		return result;
	}
}
```

- Mumbling

```java
	public static String accum(String s) {
		String result = "";
		int iterations = 0;
		for (int i = 0; i < s.length(); i++) {
			result += String.valueOf(s.charAt(i)).toUpperCase();
			for (int j = 0; j < iterations; j++) {
				result += String.valueOf(s.charAt(i)).toLowerCase();
			}
			iterations++;
			if (i != s.length() - 1) {
				result += "-";
			}
		}
		return result;
	}
```

- Fix string case

```java
public class Solution {
	public static String solve(final String str) {
		int lowercaseCount = countLowercaseLetters(str);
		return lowercaseCount >= str.length() / 2 + str.length() % 2 ? str.toLowerCase() : str.toUpperCase();
	}

	private static int countLowercaseLetters(String s) {
		int counter = 0;
		for (int i = 0; i < s.length(); i++) {
			if (s.charAt(i) >= 'a' && s.charAt(i) <= 'z') {
				counter++;
			}
		}
		return counter;
	}
}
```

- Shortest word

```java
public class Kata {
    public static int findShort(String s) {
    	if (s.length() == 0) {
    		return 0;
    	}
    	String[] words = s.split(" ");
    	int wordLength = words[0].length();
    	int charCounter = 0;
    	for (String word : words) {
    		char[] charArray = word.toCharArray();
    		for (char c : charArray) {
    			charCounter++;
    		}
    		if (charCounter < wordLength) {
    			wordLength = charCounter;
    		}
    		charCounter = 0;
    	}
        return wordLength;
    }
}
```

- Money, Money, Money

```java
public class Money {
	public static int calculateYears(double principal, double interest, double tax, double desired) {
		if (principal == desired) {
			return 0;
		}
		int years = 0;
		while (desired > principal) {
			double benefits = principal * interest;
			double taxes = benefits * tax;
			principal = principal + benefits - taxes;
			years++;
		}
		return years;
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

- Remove consecutive duplicate words

```java
public class Kata {
    public static String removeConsecutiveDuplicates(String s){
       String[] strArr = s.split(" ");
       String result = strArr[0];
       for (int i = 1; i < strArr.length; i++) {
           if (!(strArr[i-1].equals(strArr[i]))) {
               result += " " + strArr[i];
           }
       }
       return result;
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

- Get the Middle Character

```java
class Kata {
    public static String getMiddle(String word) {
	  String result = word.length() % 2 == 0 ? word.substring(word.length() / 2 - 1, word.length() / 2 + 1)
		  : word.substring(word.length() / 2, word.length() / 2 + 1);
	  return result;
    }
}
```

- Credit Card Mask

```java
public class Maskify {
    public static String maskify(String str) {
    	String masked = "";
    	if (str.length() <= 4) {
    		return str;
    	}
      for (int i = 0; i < str.length() - 4; i++) {
        masked += "#";
      }
      return masked + str.substring(str.length() - 4);
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

- Minimum Steps (Array Series #6)

```java
import java.util.Arrays;
public class Kata {
    public static int minimumSteps(int[] numbers, int k) {
      Arrays.sort(numbers);
      int total = numbers[0];
      int steps = 0;
      for (int i = 1; i < numbers.length; i++) {
        if (total >= k) {
          i = numbers.length;
        } else {
          total = total + numbers[i];
          steps++;
        }
      }
      return steps;
    }
}
```

- Paul's Misery

```java
public class Kata {
    public static String paul(String[] x) {
      int result = 0;
      for (int i = 0; i < x.length; i++) {
        if (x[i].equals("kata")) {
          result += 5;
        } else if (x[i].equals("Petes kata")) {
          result += 10;
        } else if (x[i].equals("eating")) {
          result += 1;
        }
      }
      String status = new String();
      if (result < 40) {
        status = "Super happy!";
      } else if (result < 70) {
        status = "Happy!";
      } else if (result < 100) {
        status = "Sad!";
      } else {
        status = "Miserable!";
      }
      return status;
    }
}
```

- Small enough? - Beginner

```java
public class Kata {
  public static boolean smallEnough(int[] a, int limit) {
    boolean result = true;
    for (int i = 0; i < a.length; i++) {
      if (a[i] > limit) {
        result = false;
        i = a.length;
      }
    }
    return result;
  }
}
```

- Highest and lowest

```java
public class Kata {
	public static String highAndLow(String numbers) {
		String[] strNumbers = numbers.split(" ");
		int max = Integer.parseInt(strNumbers[0]);
		int min = Integer.parseInt(strNumbers[0]);
		for (int i = 1; i < strNumbers.length; i++) {
			if (Integer.parseInt(strNumbers[i]) > max) {
				max = Integer.parseInt(strNumbers[i]);
			}
			if (Integer.parseInt(strNumbers[i]) < min) {
				min = Integer.parseInt(strNumbers[i]);
			}
		}
		return max + " " + min;
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

- Scoring Tests

```java

public class ScoringTests {

    public static int sol(int[] arr, int r, int o, int w) {
        int correct = 0, ommitted = 0, incorrect = 0;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == 0) {
                correct += r;
            } else if (arr[i] == 1) {
                ommitted += o;
            } else {
                incorrect += w;
            }
        }
        return correct + ommitted - incorrect;
    }
}
```

- Series of integers from 0 to n

```java
public class Kata {

    public static int[] generateIntegers(int n) {
        int[] result = new int[n + 1];
        int i = 0;
        while (i <= n) {
            result[i] = i;
            i++;
        }
        return result;
    }
}
```
- Vowel count
```java
public class Vowels {

    public static int getCount(String str) {
      int vowelsCount = 0;
      String vowels = "aeiou";
      for (int i = 0; i < str.length(); i++) {
        for (int j = 0; j < vowels.length(); j++) {
          if (str.charAt(i) == vowels.charAt(j)) {
            vowelsCount++;
            j = vowels.length();
          }
        }
      }
      return vowelsCount;
    }
```

- Count the divisors of a number

```java
public class FindDivisor {

  public long numberOfDivisors(int n) {
    int divisors = 0;
    for (int i = 1; i <= n; i++) {
      if (n % i == 0) {
        divisors++;
      }
    }
    return divisors;
  }
}
```
- makeBackronym

```java
import java.util.*;
import java.util.stream.*;

public class Backronym {
  private static Map<String, String> dictionary = Preload.dictionary;
  public static String makeBackronym(String acronym) {
    String result = new String();
    for (int i = 0; i < acronym.length(); i++) {
      String letter = acronym.charAt(i) + "";
      result += dictionary.get(letter.toUpperCase()) + " ";
    }
    result = result.trim();
    return result;
  }
}
```

- Name array capping

```java
public class Kata {
	public static String[] capMe(String[] strings) {
		for (int i = 0; i < strings.length; i++) {
			strings[i] = strings[i].length() > 1
					? Character.toUpperCase(strings[i].charAt(0)) + strings[i].substring(1).toLowerCase()
					: strings[i].toUpperCase();
		}
		return strings;
	}
}
```

- Summing a number's digits
```java
public class Kata{
	public static int sumDigits(int number) {
		int[] digits = new int[String.valueOf(number).length()];
		double numberToDouble = Math.abs((double) number);
		int result = 0;
		int i = 0;
		while (i < digits.length) {
			digits[i] = ((int) numberToDouble % 10);
			numberToDouble = numberToDouble / 10;
			result += digits[i];
			i++;
		}
		return result;
	}
}
```

- Remove anchor from URL

```java
public class Kata {
    public static String removeUrlAnchor(String url) {
      return url.split("#")[0];
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

- Hex to Decimal

```java
import java.util.HashMap;
import java.util.Map;

public class Kata {
	public static int hexToDec(final String hexString) {
		int result = 0;
		final int base = 16;
		boolean isNegative = false;
		String hex = hexString.toUpperCase();
		Map<Character, Integer> equivalencesMap = equivalencesMap();
		for (int i = hex.length() - 1; i >= 0; i--) {
			if (hex.charAt(i) == '-') {
				isNegative = true;
			} else {
				int exponent = hex.length() - 1 - i;
				result += Math.pow(base, exponent) * equivalencesMap.get(hex.charAt(i));
			}
		}
		if (isNegative) {
			result = -result;
		}
		return result;
	}

	public static Map<Character, Integer> equivalencesMap() {
		Map<Character, Integer> result = new HashMap<Character, Integer>();
		char letter = 'A';
		int num = 10;
		for (int i = 0; i < 10; i++) {
			char keyChar = (char) ('0' + i);
			result.put(keyChar, i);
		}
		for (int i = 0; i < 6; i++) {
			result.put(letter, num);
			num++;
			letter++;
		}
		return result;
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

- Collatz Conjecture (3n + 1)
```java
public class CollatzConjecture {  
  public static int hotpo(int n) {
    int counter = 0;
    while (n != 1) {
      n = n % 2 == 0 ? n = n / 2 : 3 * n + 1;
      counter++;
    }
    return counter;
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

- Enumerable Magic #25 - Take the First N Elements

```java
public class ZywOo {
	public static int[] take(int[] arr, int n) {
    if (arr.length == 0) {
      return new int[0];
    }
    if (n >= arr.length) {
      return arr;
    }
		int[] result = new int[n];
		for (int i = 0; i < n; i++) {
			result[i] = arr[i];
		}
		return result;
	}
}
```

- Beginner - Reduce but Grow

```java
public class Kata {
	public static int grow(int[] x) {
		if (x.length == 0) {
			return 0;
		}
		int result = x[0];
		for (int i = 1; i < x.length; i++) {
			result = result * x[i];
		}
		return result;

	}
}
```

- Grasshopper - Summation

```java
public class GrassHopper {

    public static int summation(int n) {
        return n * (n + 1) / 2;
    }
}
```

- Parse nice int from char problem

```java
public class CharProblem {
  public static int howOld(final String herOld) {
  char age = herOld.charAt(0);
  return age - '0';
  
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
```

- Traffic lights

```java
public class TrafficLights {

	public static String updateLight(String current) {
		switch (current) {
		  case "green":
			  return "yellow";
		  case "yellow":
			  return "red";
		  case "red":
			  return "green";
		}
		return "";
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
