# Top Words — Formal Specification

## 1. Problem Description

A news website displays the ten most frequently occurring words beside each article.

Implement a Python 3 function that identifies the ten most frequent words in an article and returns each word with its occurrence count.

The function must support English, Russian, Kazakh, and mixed-language text.

## 2. Function Interface

- File: `top_words.py`
- Function: `top_words(text)`
- Parameter: `text`, a Python `str` containing the article.
- Return value: A Python `list` of `(word, count)` tuples.

Each `word` is a normalized string. Each `count` is a positive integer.

The function must not print results, modify external state, or modify the input.

## 3. Input Validation

Only Python strings are accepted, including the empty string.

For any non-string input, including `None`, integers, lists, and bytes, raise `TypeError`.

## 4. Unicode Processing

First, normalize the entire input using `unicodedata.normalize("NFC", text)`.

A word begins with an alphabetic Unicode character (`str.isalpha()`).

Subsequent alphabetic characters and Unicode combining marks (characters whose `unicodedata.category()` starts with `"M"`) belong to the same word.

A combining mark cannot start a word. A mark without a preceding word is treated as a separator.

All other characters, including punctuation, digits, symbols, underscores, and whitespace, separate words.

Identify all words before applying case folding.

Normalize each extracted word using:

1. Python `str.casefold()`.
2. Unicode NFC normalization again.

The resulting string is the word's counting key and output representation.

No translation, stemming, lemmatization, stop-word removal, or other text transformation is performed.

## 5. Frequency Counting

Count every occurrence of each normalized word throughout the entire article.

Words with identical normalized representations belong to the same group.

## 6. Sorting

Sort results according to:

1. Descending occurrence count.
2. Ascending Python lexicographical string order for equal counts.

The comparison uses normalized word strings and Python's default Unicode code-point ordering, not locale-specific alphabetical ordering.

## 7. Result Limit

Return only the first ten entries after sorting.

If fewer than ten unique words exist, return all of them.

If no words exist, return an empty list.

## 8. Examples and Expected Outputs

| # | Input | Expected output |
|---|---|---|
| 1 | `"cat dog cat bird dog cat"` | `[("cat", 3), ("dog", 2), ("bird", 1)]` |
| 2 | `"Hello hello HELLO World"` | `[("hello", 3), ("world", 1)]` |
| 3 | `"hello,world! hello.world"` | `[("hello", 2), ("world", 2)]` |
| 4 | `"banana apple cherry"` | `[("apple", 1), ("banana", 1), ("cherry", 1)]` |
| 5 | `"Привет мир привет МИР"` | `[("мир", 2), ("привет", 2)]` |
| 6 | `"Сәлем әлем сәлем ӘЛЕМ"` | `[("сәлем", 2), ("әлем", 2)]` |
| 7 | `"cat123dog cat-dog"` | `[("cat", 2), ("dog", 2)]` |
| 8 | `""` | `[]` |
| 9 | `"123 !!! 456"` | `[]` |
| 10 | `"a b c d e f g h i j k l"` | `[("a", 1), ("b", 1), ("c", 1), ("d", 1), ("e", 1), ("f", 1), ("g", 1), ("h", 1), ("i", 1), ("j", 1)]` |
| 11 | `"the cat and the dog"` | `[("the", 2), ("and", 1), ("cat", 1), ("dog", 1)]` |
| 12 | `"don't well-known"` | `[("don", 1), ("known", 1), ("t", 1), ("well", 1)]` |
| 13 | `"café cafe\u0301"` | `[("café", 2)]` |
| 14 | `"Straße STRASSE"` | `[("strasse", 2)]` |
| 15 | `" \n\t "` | `[]` |
| 16 | `"a\u0301 a\u0301"` | `[("á", 2)]` |

In examples 13 and 16, `\u0301` represents the Unicode combining acute accent.

## 9. Additional Edge Cases

- `top_words(None)` must raise `TypeError`.
- `top_words(123)` must raise `TypeError`.
- `top_words(["cat"])` must raise `TypeError`.
- `top_words(b"cat")` must raise `TypeError`.
- An underscore separates words, so `"cat_dog"` produces `[("cat", 1), ("dog", 1)]`.
- An isolated combining mark produces no word.
- The function must not depend on the system locale.
- Input must not be truncated before frequency counting.
- If more than ten words tie in frequency, lexicographical ordering determines which ten are returned.

## 10. Correctness Criteria

An implementation is correct if it:

1. Uses Python 3 and defines `top_words` in `top_words.py`.
2. Rejects non-string inputs with `TypeError`.
3. Applies Unicode NFC normalization.
4. Extracts words according to the specified character rules.
5. Performs case folding after word extraction.
6. Counts all occurrences accurately.
7. Applies deterministic sorting and tie-breaking.
8. Returns no more than ten `(word, count)` tuples.
9. Produces the exact expected outputs in all examples.
10. Has no printing or externally observable side effects.