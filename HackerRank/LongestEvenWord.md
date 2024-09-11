# Longest Even Word

## Problem Statement:

Consider a string, sentence, of words separated by spaces where each word is a substring that consists of English alphabetic letters only. Find and return the first word in the sentence that has a length that is both an even number and has the greatest length of all even-length words in the sentence. If there are no even-length words in the sentence, return “00”.

**Example**
```
sentence = "Time to write great code"
```
The lengths of the words are 4, 2, 5, 5, 4 in order. The longest even-length words are “Time” and “code.” The one that occurs first is “Time,” which is the answer to return.
The even-length words in the sentence are “Time”, “to”, “code”. The longest of these is “Time”, so the function returns “Time”.

**Function Description**
Complete the function longestEvenWord in the editor below.

longestEvenWord has the following parameters:
- string sentence: a sentence string

Returns:
- string: the first occurrence of a string with maximal even number length, or the string “00” (zero-zero) if there are no even-length words.

**Constraints**
- 1 <= length of sentence <= 10^5
- The sentence string consists of spaces and letters in the range a-z, A-Z only.

Input Format for Custom Testing:
Input from stdin will be processed as follows and passed to the function:

- A single line of space-separated strings denoting the sentence.

**Sample Case 1:**

Sample Input 1:
```
It is a pleasant day today
```

Sample Output 1:
```
pleasant
```

Explanation
There are three even-length words: “it” (with length 2), “is” (2), and “pleasant” (8). The longest of these is “pleasant”, so the function returns “pleasant”.

**Sample Case 2:**

Sample Input 2:
```
You can do it the way you like
```

Sample Output 2:
```
like
```

Explanation
There are three even-length words: “do” (with length 2), “it” (2), and “like” (4). The longest of these is “like”, so the function returns “like”.

## Solution:

#### Method 1:
```java
public class Result {
    public static String findLongestEvenWord(String sentence) {
        String[] words = sentence.split(" ");
        String longestEvenWord = "00";
        int maxLength = 0;

        for (String word : words) {
            if (word.length() % 2 == 0 && word.length() > maxLength) {
                longestEvenWord = word;
                maxLength = word.length();
            }
        }
        return longestEvenWord;
    }

    public static void main(String[] args) {
        String sentence1 = "It is a pleasant day today";
        String sentence2 = "You can do it the way you like";
        
        System.out.println(findLongestEvenWord(sentence1));
        System.out.println(findLongestEvenWord(sentence2)); 
    }
}
```

