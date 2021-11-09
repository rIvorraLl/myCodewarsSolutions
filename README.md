# myCodewarsSolutions
*Not exactly brilliant solutions to some Codewars' kata. Use at your own risk.*

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

    

    
