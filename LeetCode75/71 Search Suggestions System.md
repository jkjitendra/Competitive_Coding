# Search Suggestions System

## Problem Statement:

You are given an array of strings `products` and a string `searchWord`.

Design a system that suggests at most three product names from `products` after each character of `searchWord` is typed. Suggested products should have common prefix with `searchWord`. If there are more than three products with a common prefix return the three lexicographically minimums products.

Return *a list of lists of the suggested products after each character of *`searchWord` * is typed* .

**Example 1:**

<pre><strong>Input:</strong> products = ["mobile","mouse","moneypot","monitor","mousepad"], searchWord = "mouse"
<strong>Output:</strong> [["mobile","moneypot","monitor"],["mobile","moneypot","monitor"],["mouse","mousepad"],["mouse","mousepad"],["mouse","mousepad"]]
<strong>Explanation:</strong> products sorted lexicographically = ["mobile","moneypot","monitor","mouse","mousepad"].
After typing m and mo all products match and we show user ["mobile","moneypot","monitor"].
After typing mou, mous and mouse the system suggests ["mouse","mousepad"].
</pre>

**Example 2:**

<pre><strong>Input:</strong> products = ["havana"], searchWord = "havana"
<strong>Output:</strong> [["havana"],["havana"],["havana"],["havana"],["havana"],["havana"]]
<strong>Explanation:</strong> The only word "havana" will be always suggested while typing the search word.
</pre>

**Constraints:**

* `1 <= products.length <= 1000`
* `1 <= products[i].length <= 3000`
* `1 <= sum(products[i].length) <= 2 * 10<sup>4</sup>`
* All the strings of `products` are  **unique** .
* `products[i]` consists of lowercase English letters.
* `1 <= searchWord.length <= 1000`
* `searchWord` consists of lowercase English letters.


## Solution:

#### Method 1: {java}

```java
class TrieNode {
  Map<Character, TrieNode> children = new HashMap<>();
  List<String> suggestions = new ArrayList<>();
}

class Solution {
  private TrieNode root;

  public Solution() {
    root = new TrieNode();
  }

  private void insert(String product) {
    TrieNode node = root;
    for (char ch : product.toCharArray()) {
      node = node.children.computeIfAbsent(ch, k -> new TrieNode());
      if (node.suggestions.size() < 3) {
        node.suggestions.add(product);
      }
    }
  }

  private List<String> search(String prefix) {
    TrieNode node = root;
    for (char ch : prefix.toCharArray()) {
      if (!node.children.containsKey(ch)) {
        return Collections.emptyList();
      }
      node = node.children.get(ch);
    }
    return node.suggestions;
  }
  
  public List<List<String>> suggestedProducts(String[] products, String searchWord) {
    Arrays.sort(products);
  
    for (String product : products) {
      insert(product);
    }
  
    List<List<String>> result = new ArrayList<>();
    String prefix = "";
    for (char ch : searchWord.toCharArray()) {
      prefix += ch;
      result.add(search(prefix));
    }
    return result;
  }
}
```


#### Method 2:

```java
class TrieNode {
  TrieNode[] children = new TrieNode[26];
  List<String> suggestions = new ArrayList<>();

  public void insert(String product, int i) {
    if (i == product.length()) return;
    int index = product.charAt(i) - 'a';
    if (children[index] == null) {
      children[index] = new TrieNode();
    }
    if (children[index].suggestions.size() < 3) {
      children[index].suggestions.add(product);
    }
    children[index].insert(product, i + 1);
  }

  public TrieNode searchNode(String prefix) {
    TrieNode node = this;
    for (int i = 0; i < prefix.length(); i++) {
      int index = prefix.charAt(i) - 'a';
      if (node.children[index] == null) {
        return null;
      }
      node = node.children[index];
    }
    return node;
  }
}

class Solution {
  TrieNode root = new TrieNode();

  public List<List<String>> suggestedProducts(String[] products, String searchWord) {
    Arrays.sort(products);
    for (String product : products) {
      root.insert(product, 0);
    }

    List<List<String>> result = new ArrayList<>();
    for (int i = 0; i < searchWord.length(); i++) {
      TrieNode node = root.searchNode(searchWord.substring(0, i + 1));
      result.add(node != null ? node.suggestions : new ArrayList<>());
    }
    return result;
  }
}
```


#### Method 3:

```java
class Solution {
  public List<List<String>> suggestedProducts(String[] products, String searchWord) {
    Arrays.sort(products);
    int productsCount = products.length;
    int startIndex = 0;
    int endIndex = productsCount - 1;
    List<List<String>> suggestedProductsList = new LinkedList<>();

    for (int prefixLength = 0; prefixLength < searchWord.length(); prefixLength++) {
      char currentChar = searchWord.charAt(prefixLength);
      // Move startIndex to the first product that has the current prefix
      while (startIndex <= endIndex && (products[startIndex].length() <= prefixLength || products[startIndex].charAt(prefixLength) != currentChar)) {
        startIndex++;
      }
      // Move endIndex to the last product that has the current prefix
      while (startIndex <= endIndex && (products[endIndex].length() <= prefixLength || products[endIndex].charAt(prefixLength) != currentChar)) {
        endIndex--;
      }
      List<String> currentSuggestions = new ArrayList<>();
      // Collect up to 3 suggestions based on the current state of startIndex and endIndex
      for (int i = startIndex, limit = Math.min(startIndex + 2, endIndex); i <= limit; i++) {
        currentSuggestions.add(products[i]);
      }
      suggestedProductsList.add(currentSuggestions);
    }
    return suggestedProductsList;
  }
}
```
