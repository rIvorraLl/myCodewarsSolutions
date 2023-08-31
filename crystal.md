**6 kyu**

- Multiples of 3 or 5

```crystal
def solution(number : Int32)
  i = 3
  sum = 0
  while i < number
    if i % 3 == 0 || i % 5 == 0
      sum += 1
    end
    i += 1
  end
  sum
end
```

**7 kyu**

- Cats and shelves

```crystal
  def cats(start, finish)
    diff = finish - start
    if diff % 3 == 0
        return diff // 3
    end
    if diff >= 3
        three_steps = diff // 3
        one_steps = diff - (diff // 3 * 3)
        return three_steps + one_steps
    end
    diff
  end
```

- Disemvowel trolls

```crystal
def is_vowel(char)
  char = char.downcase
  return char == 'a' || char == 'e' || char == 'i' || char == 'o' || char == 'u'
end

def disemvowel(str)
  result = ""
  str.each_char do |char|
    if !is_vowel(char)
      result += char
    end
  end
  result
end
```

  - Simple Fun #10: Range Bit Counting

```crystal
def get_binary_digits(int)
  arr = [] of Int32
  while int // 2 > 0
    n = (int % 2).to_i
    arr << n
    int = int // 2
  end
  n = (int % 2).to_i
  arr << n
  arr
end

def range_bit_count(a, b)
  counter = 0
  range_num = a .. b
  range_num.each do |value|
    to_binary = get_binary_digits(value)
    to_binary.each do |item|
        if item == 1
            counter += 1
        end
    end
  end
  counter
end
```

**8 kyu**

- Vowel count

```crystal
def get_vowel_count(str)
    counter = 0
    vowels = ['a', 'e', 'i', 'o', 'u']
    i = 0
    while i < str.size
        vowel = str[i]
        vowels.each do |item|
            if item == vowel
                counter += 1
            end
        end
        i += 1
    end
    counter
  end
```

- Determine offspring sex based on genes XX and XY chromosomes

```crystal
def chromosome_check(sperm)
  result = sperm == "XX" ? "Congratulations! You're going to have a daughter." : "Congratulations! You're going to have a son."
end
```

- Beginner Series #1 School Paperwork

```crystal
def paperwork(n, m)
  n > 0 && m > 0 ? n * m : 0
end
```

- Find the smaller integer in the array

```crystal
def find_smallest_int(arr)
  smallest = arr[0]
  arr.each do |num|
    if num < smallest
      smallest = num
    end
  end
  smallest
end
```

- Stringy strings

```crystal
def stringy(size)
    result = ""
    i = 0
    while i < size
        char = i % 2 == 0 ? "1" : "0"
        result += char
        i += 1
    end
    result
  end
```

- Remove first and last characters

```crystal
def remove_char(s : String)
  s = s[1..s.size - 2]
end
```
