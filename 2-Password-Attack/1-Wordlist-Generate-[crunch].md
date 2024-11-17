# Wordlist Generator [crunch]

<img src="https://www.kali.org/tools/crunch/images/crunch-logo.svg" style="width:120px;"/>

Crunch is a wordlist generator where you can specify a standard character set or any set of characters to be used in generating the wordlists. The wordlists are created through combination and permutation of a set of characters.

---

### 1- Generate wordlist within a range
`crunch 1 4 -o wordlist.txt`

crunch will generate a wordlist that starts at `a` and ends at `zzzz`

---

### 2- Generate wordlist with set of characters
`crunch 1 4 abcd -o wordlist.txt`

crunch will generate a wordlist that starts at `a` and ends at `dddd`

note: if you want to add space to the character set, you must use the `\` escape character `crunch 1 5 abcd\` 

---

### 3- Generate wordlist with pattern 
`crunch 7 7 -t cat@,%^ -o wordlist.txt`

- @ will insert lower case characters
- , will insert upper case characters
- % will insert numbers
- ^ will insert symbols

---
