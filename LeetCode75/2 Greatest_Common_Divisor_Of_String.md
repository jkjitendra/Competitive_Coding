# Greatest Common Divisor Of Strings

## Problem Statement:

For two strings `s` and `t`, we say "`t` divides `s`" if and only if `s = t + ... + t` (i.e., `t` is concatenated with itself one or more times).

Given two strings `str1` and `str2`, return *the largest string *`x`* such that *`x`* divides both *`str1`* and *`str2`.

**Example 1:**

<pre><strong>Input:</strong> str1 = "ABCABC", str2 = "ABC"
<strong>Output:</strong> "ABC"
</pre>

**Example 2:**

<pre><strong>Input:</strong> str1 = "ABABAB", str2 = "ABAB"
<strong>Output:</strong> "AB"
</pre>

**Example 3:**

<pre><strong>Input:</strong> str1 = "LEET", str2 = "CODE"
<strong>Output:</strong> ""
</pre>

**Constraints:**

* `1 <= str1.length, str2.length <= 1000`
* `str1` and `str2` consist of English uppercase letters.

## Java Solution:-

#### Method 1:

```java
    class Solution {
    	public String gcdOfStrings(String str1, String str2) {
	        if (!(str1 + str2).equals(str2 + str1)) {
		     return "";
       		}
	        int res = gcd(str1.length(), str2.length());
	        return str1.substring(0, res);
    	}
        private int gcd(int str1Len, int str2Len) {
            while( str2Len != 0) {
                int tempVar = str2Len;
                str2Len = str1Len % str2Len;
                str1Len = tempVar;
            }
            return str1Len;
        }
    }
```

#### Method 2:

```java
    class Solution {
    	public String gcdOfStrings(String str1, String str2) {
            int str1Len = str1.length();
            int str2Len = str2.length();
            int minLen = Math.min(str1Len, str2Len);
            for (int i = minLen; i > 0; i--) {
                if ((str1Len % i == 0) && (str2Len % i == 0)) {
                    String divisor = str1.substring(0, i);
                    if (isFormingActualString(divisor, str1) && isFormingActualString(divisor, str2)) {
                        return divisor;
                    }
                }
       	    }
	    return "";
    	}
        private boolean isFormingActualString(String divisor, int str) {
            StringBuffer sb = new StringBuffer();
            int noOfTimesRepeated = str.length() / divisor.length();
            for (int i = 0; i < noOfTimesRepeated; i++) {
                sb.append(divisor);
            }
            return sb.toString().equals(str);
        }
    }
```
