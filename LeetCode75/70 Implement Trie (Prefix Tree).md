# Implement Trie (Prefix Tree)

## Problem Statement:

A [**trie**](https://en.wikipedia.org/wiki/Trie) (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

* `Trie()` Initializes the trie object.
* `void insert(String word)` Inserts the string `word` into the trie.
* `boolean search(String word)` Returns `true` if the string `word` is in the trie (i.e., was inserted before), and `false` otherwise.
* `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string `word` that has the prefix `prefix`, and `false` otherwise.

**Example 1:**

<pre><strong>Input</strong>
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
<strong>Output</strong>
[null, null, true, false, true, null, true]

<strong>Explanation</strong>
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
</pre>

**Constraints:**

* `1 <= word.length, prefix.length <= 2000`
* `word` and `prefix` consist only of lowercase English letters.
* At most `3 * 10<sup>4</sup>` calls **in total** will be made to `insert`, `search`, and `startsWith`.

## Solution:

#### Method 1:

```java
class TrieNode {
  Map<Character, TrieNode> children = new HashMap<>();
  boolean isEndOfWord = false;

  public TrieNode() {}
}

class Trie {
  private TrieNode root;
  public Trie() {
    root = new TrieNode();
  }
  
  public void insert(String word) {
    TrieNode node = root;
    for (char ch: word.toCharArray()) {
      node.children.putIfAbsent(ch, new TrieNode());
      node = node.children.get(ch);
    }
    node.isEndOfWord = true;
  }
  
  public boolean search(String word) {
    TrieNode node = root;
    for (char ch: word.toCharArray()) {
      node = node.children.get(ch);
      if (node == null) return false;
    }
    return node.isEndOfWord;
  }
  
  public boolean startsWith(String prefix) {
    TrieNode node = root;
    for (char ch: prefix.toCharArray()) {
      node = node.children.get(ch);
      if (node == null) return false;
    }
    return true;
  }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

#### Method 2:

```java
class TrieNode {
  TrieNode[] children = new TrieNode[26];
  boolean isEndOfWord = false;
  public TrieNode() {}
}

class Trie {
  private TrieNode root;
  public Trie() {
    root = new TrieNode();
  }
  
  public void insert(String word) {
    TrieNode node = root;
    for (char ch: word.toCharArray()) {
      int index = ch - 'a';
      if (node.children[index] == null) {
        node.children[index] = new TrieNode();
      }
      node = node.children[index];
    }
    node.isEndOfWord = true;
  }
  
  public boolean search(String word) {
    TrieNode node = root;
    for (char ch: word.toCharArray()) {
      int index = ch - 'a';
      if (node.children[index] == null) {
        return false;
      }
      node = node.children[index];
    }
    return node.isEndOfWord;
  }
  
  public boolean startsWith(String prefix) {
    TrieNode node = root;
    for (char ch: prefix.toCharArray()) {
      int index = ch - 'a';
      if (node.children[index] == null) {
        return false;
      }
      node = node.children[index];
    }
    return true;
  }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```
