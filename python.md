**5 kyu**

- RGB to Hex conversion

```python
def converter(a):
    indexes = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "A", "B", "C" ,"D", "E", "F"]
    hex1 = indexes[a // 16]
    hex2 = indexes[int((a / 16) % 1 * 16)]
    return str(hex1 + hex2)


def rgb(r, g, b):
    reListed = []
    for i in (r, g, b):
        if i < 0:
            reListed += [0]
        elif i > 255:
            reListed += [255]
        else:
            reListed += [i]
    hexed = ""
    for i in reListed:
        hexed += converter(i)
    return hexed

```
- Rotate an array matrix

```python
def rotate(matrix, direction): 
    if direction == "clockwise":
        rotateClockwise = list(zip(*matrix[::-1]))
        resultClock = []
        for i in rotateClockwise:
            resultClock.append(list(i))
        return resultClock
            
    else:
        rotateAntiClockwise = list(reversed(list(zip(*matrix))))
        resultAntiClock = []
        for j in rotateAntiClockwise:
            resultAntiClock.append(list(j))
        return resultAntiClock

```
**6 kyu**

- Are they the "same"?

```python
def comp(array1, array2):
    return False if array1 == None or array2 == None else sorted([n * n for n in array1]) == sorted(array2)

```
- Stop gninnipS My sdroW!

```python
def spin_words(sentence):
    listSentence = sentence.split()
    reversedWords = ""
    for word in listSentence:
        if len(word) > 4:
            reversedWords += word[::-1] + " "
        else:
            reversedWords += word + " "
    return reversedWords.strip()

```

- Bleatrix Trotter (The Counting Sheep)

```python
def trotter(n):
    nums = []
    counter = 0
    i = 1
    while i < 100:
        multiplied =  i * n
        for j in str(multiplied):
            if j not in nums:
                nums += [j]
                counter += 1
            if counter == 10:
                return multiplied
        i += 1
    return "INSOMNIA"

```
- Split string

```python
def solution(s):
    returnString = ""
    for i in range(0, len(s)):
        if i % 2 == 0:
            returnString += " "
        returnString += s[i]
    if len(s) % 2 != 0:
        returnString += "_"
    return returnString.split()
```
- Bit counting

```python
def count_bits(n):
    binary = ""
    while n // 2 > 0:
        binary += str(n % 2)
        n = n // 2
    binary += str(n % 2)
    counter = 0
    for i in binary:
        if i == "1":
            counter += 1
    return counter

```
- Detecting pangram

```python
def is_pangram(s):
    alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    for i in alphabet:
        if i not in s.upper():
            return False
    return True

```
- Simple nearest prime

```python
def isPrime(n):
    if n % 2 == 0 or n % 3 == 0 or n % 5 == 0:
        return False
    sqrroot = int(n ** 0.5)
    for i in range(2, sqrroot):
        if n % i == 0:
            return False
    return True
def solve(n):
    if n == 3 or n == 4:
        return 3
    low = n
    high = n
    boolean = True
    while boolean:
        if isPrime(low):
            boolean = False
        else:
            low -= 1
    while not boolean:
        if isPrime(high):
            boolean = True
        else:
            high += 1
    if n - low > high - n:
        return high
    else:
        return low

```
- Count the smiley faces!

```python
def count_smileys(arr):
    eyes = ":;"
    noses = "-~"
    mouths = ")D"
    counter = 0
    for i in arr:
        for j in range(len(i)):
            if i[j] in eyes and len(i[j:]) >= 3:
                if i[j+1] in noses and i[j+2] in mouths:
                    counter += 1
            elif i[j] in eyes and len(i[j:]) >= 2:
                if i[j+1] in mouths:
                    counter += 1
    return counter

```
**7 kyu**

- Gauß needs help! (Sums of a lot of numbers).

```python
def f(n):
    return None if type(n) != int or n <= 0 else n * (n + 1) /2

```
- String ends with?

```python
def solution(string, ending):
    return True if ending == "" else string[-len(ending):] == ending

```

- Split in parts
```python
def split_in_parts(s, part_length): 
    splitted = s[0]
    for i in range(1, len(s)):
        if i % part_length == 0:
            splitted += " " + s[i]
        else:
            splitted += s[i]
    return splitted

```
- You're a square!

```python
def is_square(n):
    if n < 0:
        return False
    return int(n ** 0.5) ** 2 == n

```
- Get decimal part of the given number

```python
def get_decimal(n): 
    boolean = False
    decimal = ""
    if "." not in str(n):
        return 0
    for i in str(n):
        if i == ".":
            boolean = True
        if boolean:
            decimal += i
    return float(decimal)

```
- Reverse a Number

```python
def reverse_number(n):
    n = str(n)
    strNum = ""
    if n[0] == "-":
        for i in n[1:]:
            strNum = i + strNum
        strNum = "-" + strNum
        return int(strNum)
    reversed = n[::-1]
    return int(reversed)

```
- 16 + 18 = 214

```python
def add(num1, num2):
    added = ""
    num1 = str(num1)
    num2 = str(num2)
    if len(num1) > len(num2):
        num2 = "0" * (len(num1) - len(num2)) + num2
    elif len(num2) > len(num1):
        num1 = "0" * (len(num2) - len(num1)) + num1
    for i in range(len(num1)):
        added += str(int(num1[i]) + int(num2[i]))
    return int(added)

```
- Bumps in the Road

```python
def bumps(road):
    counter = 0
    for i in road:
        if i == "n":
            counter += 1
    return "Woohoo!" if counter < 16 else "Car Dead"

```

- Simple fun #195: Guess Hat Color

```python
def guess_hat_color(a,b,c,d):
    winner = 0
    if (b == "white" and c == "white") or (b == "black" and c == "black"):
        winner = 1
    else:
        winner = 2
    return winner
```

- Convert an array of strings to an array of numbers

```python
def to_float_array(arr): 
    newArray = []
    for i in range(len(arr)):
        if "." in arr[i]:
            newArray += [float(arr[i])]
        else:
            newArray += [int(arr[i])]
    return newArray

```
**8 kyu**

- Difference of Volumes of Cuboids

```python
def find_difference(a, b):
    return abs(a[0] * a[1] * a[2] - b[0] * b[1] * b[2])

```
- Filter out the geese

```python
geese = ["African", "Roman Tufted", "Toulouse", "Pilgrim", "Steinbacher"]
def goose_filter(birds):
    geeseCleaned = [i for i in birds if i not in geese]
    return geeseCleaned

```
- Keep up the hoop

```python
def hoop_count(n):
    return "Great, now move on to tricks" if n>9 else "Keep at it until you get it"

```
- Can we divide it?

```python
def is_divide_by(number, a, b):
    return number % a == 0 and number % b == 0

```
- DNA to RNA conversion

```python
def dna_to_rna(dna):
    rna =""
    for i in dna:
        if i == "T":
            rna += "U"
        else:
            rna += i
    return rna

```
- I love you, a little , a lot, passionately ... not at all

```python
def how_much_i_love_you(nb_petals):
    flower = ["I love you", "a little", "a lot", "passionately", "madly", "not at all"]
    return flower[nb_petals - 1] if nb_petals <= 6 else flower[nb_petals%6-1]

```

- Will you make it?

```python
def zero_fuel(distance_to_pump, mpg, fuel_left):
    return fuel_left * mpg >= distance_to_pump

```
- Squash the bugs

```python
def find_longest(string):
    spl = string.split(" ")
    longest = 0
    i=0
    while i < len(spl):
        if len(spl[i]) > longest:
            longest = len(spl[i])
        i += 1
    return longest

```
- Calculate average

```python
def find_average(numbers):
    counter = 0
    for i in numbers:
        counter += i
    return counter / len(numbers)

```

