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
