# myCodewarsSolutions
*My solutions to some Codewars' kata. Use at your own risk.*

**5 kyu**

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
**7 kyu**

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
