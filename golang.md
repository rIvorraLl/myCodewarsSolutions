**8 kyu**

- DNA to RNA conversion

```go
package kata

func DNAtoRNA(dna string) string {
	var rna string
	for i := 0; i < len(dna); i++ {
		if dna[i] == 'T' {
			rna += "U"
		} else {
			rna += string(dna[i])
		}
	}
	return rna
}
```

- Is he gonna survive?

```go
package kata

func Hero(bullets, dragons int) bool {
  return bullets >= dragons * 2
}
```
