<h3 align="center">Algorithms and data structures</h3>

  <p align="center">
    Notes on algorithms, data structures and time complexity
    <br>
    <a href="">Resources</a>
    ·
    <a href="">Main</a>
  </p>
</p>


## Table of contents

- [Pattern searching algorithms](#pattern-searching-algorithms)
    - [KMP algorithm](#kmp-algorithm)
    - [Boyer Moore Algorithm](#boyer-moore-algorithm)
    - [Rabin-Karp Algorithm](#rabin-karp-algorithm)
- [Time complexity]()


## Pattern searching algorithms
> Algorithms designed to efficiently find a particular pattern within a larger set of data (example: used when pressing CTRL + F on PDFs)

`Year 3, Semester 1` 
<br>
Notes heavy based on Geeksforgeeks resources, so credits to them:)

### KMP algorithm
**Definition**
Uses Longest Prefix Suffix array that stores, for every position in the pattern, the length of the longest proper prefix which is also a suffix of the **substring** ending at that position
- It helps the KMP algorithm determine how much to **shift** the pattern when a mismatch occurs, without rechecking matched characters
- Time complexity: **O(n + m)** 
    - O(m) for creating LPS array, O(n) for searching through the text 

| Overview |
| -------- |
| ![alt text](/resources/imgs/ALG_2.png) |

**Code for calculating LPS array:**
```python
def computeLPSArray(pattern):
    n = len(pattern)
    lps = [0] * n # placeholder for LPS array, filled with zeroes at the start

    lps_len = 0 # length of the previous longest prefix suffix
    i = 1 
    # lps[0] is always 0 because even if the pattern matches its
    # still the 'inicialization' of the pattern, not first occurence, so i doesnt count
    while i < n:
        if pattern[i] == pattern[lps_len]: # both move through pattern, 
                                           # but lps_len is starting from 0
            lps_len += 1 
            lps[i] = lps_len # store length in lps array
            i += 1
        else:
            if lps_len != 0:
                # fall back in the pattern
                lps_len = lps[lps_len - 1]
            else:
                lps[i] = 0 # when no pattern matches in this place
                i += 1

    return lps

if __name__ == "__main__":
    # from lecture, im dyslexic no way im doing all of them by hand
    examples = ["abbbbc", "abbbba", "niekoniecznie", "kajak", "abrakadabra",
                "onions", "ananas", "banan", "matematyka", "abababababb",
                "01010101011", "CCCCTCCAG", "wydrze wydrz1 wydrze wydrze wydrze wydrz1"]
    
    for i, ex in enumerate(examples):
        print(f"Example {i+1} - {computeLPSArray(ex)}")
```
out:
```python
Example 1 - [0, 0, 0, 0, 0, 0]
Example 2 - [0, 0, 0, 0, 0, 1]
Example 3 - [0, 0, 0, 0, 0, 1, 2, 3, 0, 0, 1, 2, 3]
Example 4 - [0, 0, 0, 0, 1]
# etc
```

| Example step by step |
| -------- |
| ![alt text](/resources/imgs/ALG_3.png) |

**Simple code for KMP algorithm:**
```python
def search(text, pattern):
    ps = computeLPSArray(pattern)
    i = 0
    j = 0

    while i < n:
        if text[i] == pattern[j]:
            i += 1
            j += 1
        else:
            if j != 0:
                j = ps[j - 1]
            else:
                i += 1
        if j == m:
            print(i - j)
            j = ps[j - 1]
```


### Boyer Moore Algorithm
**Definition**
<br>
Also preprocesses the pattern, but this time using **Bad Character Heuristic** (or **Good Suffix Heuristic**)
- The character of the text which doesn’t match with the current character of the pattern is called the Bad Character. Upon mismatch, we shift the pattern until: 
    - the mismatch becomes a match
    - pattern P moves past the mismatched character
- Time complexity: **O(m*n)** (worst case) **O(n/m)** (best case)
    - worst case: all characters of the text and pattern are same
    ` txt[] = "AAAAAAAAAAAAAAAAAA" pat[] = "AAAAA"`
    - best case: all the characters of the text and pattern are different

| Overview |
| -------- |
| ![alt text](/resources/imgs/ALG_4.png) |

 `Value(T) = max (1, 4–3–1) = max (1, 0) = 1 <= update the T value <= Rightmost occurrence of T`
 <br>
 "*If the same character repeats, update the table by the values from the new character (or simply consider the rightmost occurrence of the character in the pattern and calculate the value for it)*"
 - jak znak pojawia się poźniej jeszcze raz we wzorcu to wzór na tablice to L($) = max{1, m - **index_gdzie_znowu_sie_pojawia** -1}
 np. dla **T**EST to L(**T**) = max{1, 4-3-1} = **1**
 <!-- todo: smaller img with html pls -->
 ![alt text](/resources/imgs/ALG_5.jpg)
 (powinno być I = 1) 

### Rabin-Karp Algorithm
**Definition**
<br>
Speed up pattern matching using **hashing** techniques, instead of comparing characters one by one, it converts the **strings into numbers** (hashes) and compares those
- uses rolling hash to find all occurrences of a pattern in a text
- best for huuuge texts
- Time Complexity: **O(n)**
    - the substring hash is retrieved in O(1) time

| Overview |
| -------- |
| ![alt text](/resources/imgs/ALG_6.png) |
