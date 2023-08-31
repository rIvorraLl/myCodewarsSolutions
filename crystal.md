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

- Determine offspring sex based on genes XX and XY chromosomes

```crystal
def chromosome_check(sperm)
  result = sperm == "XX" ? "Congratulations! You're going to have a daughter." : "Congratulations! You're going to have a son."
end
```


