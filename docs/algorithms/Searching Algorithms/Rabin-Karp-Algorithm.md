---

id: Rabin-Karp Algorithm
sidebar_position: 6  
title: Rabin-Karp Algorithm
sidebar_label: Rabin-Karp Algorithm 

---

## Definition 📖

**Rabin-Karp Algorithm** is a string search algorithm that uses hashing to find any one of a set of pattern strings in a text. It is particularly useful for matching multiple patterns simultaneously.

## Characteristics ✨

- **Hashing Technique**:

   Rabin-Karp uses a hash function to convert the search pattern and substrings of the text into numerical values, allowing for efficient comparisons.

- **Multiple Patterns Search**:

   The algorithm can search for multiple patterns at once, making it more versatile than simpler string searching algorithms.

- **Sliding Window**:

   The algorithm uses a sliding window approach to examine each substring of the text of the same length as the pattern.

## Time Complexity ⏱️

- **Average Case**: `O(n + m)` 🌟  
  The average time complexity is linear, where `n` is the length of the text and `m` is the length of the pattern.

- **Worst Case**: `O(n * m)` 💥  
  The worst-case scenario occurs when there are many hash collisions, leading to excessive comparisons.

## Space Complexity 💾

- **Space Complexity**: `O(1)`  
  Rabin-Karp operates in constant space, as it only requires a few extra variables for the calculations.

## C++ Implementation 💻

Here’s a simple implementation of the Rabin-Karp Algorithm in C++:

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

const int d = 256; // Number of characters in the input alphabet

void rabinKarp(string text, string pattern, int q) {
    int M = pattern.size();
    int N = text.size();
    int i, j;
    int p = 0; // Hash value for pattern
    int t = 0; // Hash value for text
    int h = 1;

    // The value of h would be "pow(d, M-1)%q"
    for (i = 0; i < M - 1; i++)
        h = (h * d) % q;

    // Calculate the hash value of pattern and first window of text
    for (i = 0; i < M; i++) {
        p = (d * p + pattern[i]) % q;
        t = (d * t + text[i]) % q;
    }

    // Slide the pattern over text one by one
    for (i = 0; i <= N - M; i++) {
        // Check the hash values of the current window of text and pattern
        if (p == t) {
            // Check for characters one by one
            for (j = 0; j < M; j++) {
                if (text[i + j] != pattern[j])
                    break;
            }
            if (j == M)
                cout << "Pattern found at index " << i << endl;
        }

        // Calculate hash value for the next window of text: Remove leading digit and add trailing digit
        if (i < N - M) {
            t = (d * (t - text[i] * h) + text[i + M]) % q;
            // We might get negative value of t, converting it to positive
            if (t < 0)
                t = t + q;
        }
    }
}

int main() {
    string text = "GEEKS FOR GEEKS";
    string pattern = "GEEK";
    int q = 101; // A prime number

    rabinKarp(text, pattern, q);
    return 0;
}
```
## Applications of Rabin-Karp Algorithm 🌐
- **Text Search Engines:**
      Used in search engines to find relevant patterns within large bodies of text.

- **DNA Sequencing:**
      Applied in bioinformatics for finding specific patterns in DNA sequences.

- **Plagiarism Detection:**
      Helpful in comparing texts to find similar sequences and identify potential plagiarism.

## Advantages and Disadvantages
**Advantages:** ✅
- Efficient for Multiple Patterns:
    Can search for multiple patterns simultaneously, making it faster for certain applications.

- Flexible:
    Adaptable to different hash functions and can handle various types of search queries.

**Disadvantages:** ⚠️
- Hash Collisions:
    Performance can degrade in the worst case due to hash collisions, leading to increased time complexity.

- Complex Implementation:
    Requires careful implementation of hash functions and handling of collisions.

## Summary 📚
The Rabin-Karp Algorithm is an efficient string searching algorithm that utilizes hashing to find patterns within text. 
Its ability to search for multiple patterns simultaneously makes it particularly useful in various applications, including text search engines and bioinformatics. 
However, the algorithm's efficiency can be affected by hash collisions, which may lead to increased time complexity in certain scenarios.
