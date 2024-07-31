**1. REST vs RPCs**

REST and RPC are two of the common ways to communicate over a network that can be used in distributed systems. Which of the following are true?

Pick **ONE OR MORE** options

1. In general, REST is more suitable for public access APIs than RPCS.
2. RPCs try to mimic function calls over a network architecture.
3. Custom RPC protocols, especially when using binary encoding format can achieve a better performance than REST in general.
4. RPCs are generally easier to maintain than JSONs, but JSONs are definitely better for debugging and prototyping purposes.

Answer:- 1, 2, 3

**2. Caching 2**

Caching is used to serve stored data more efficiently. It is commonly used, particularly in large scale distributed systems, to allow the most frequently accessed information to be available at a lower cost in time or resources. Since cache capacity is limited, strategies are employed to determine what is in the cache and when it should be replaced. These are referred to as eviction policies and replacement policies. Which of the following are true?

Pick **ONE OR MORE** options

1. A cache hit is a situation when the cache becomes full.
2. LRU and MRU are eviction policies that respectively discard least recently used and most recently used elements from the cache to make space for other elements. In applications like social networks with feed, LRU, in general, performs significantly better than MRU.
3. If the future is known, it is possible to design an eviction policy that is optimal.
4. The data in a cache is always consistent with the changes made to it. Any time it is requested, the most recent version is returned.

Answer:- 2, 3

**3. Good URI Design**

Which of the following are true regarding good *URI* design?

Pick **ONE OR MORE** options

1. URIs should never be changed.
2. URis must be constructed by the client.
3. URls should be short in length.
4. URIs should be case-sensitive.
5. HTTP verbs should be used instead of operation names in URIs.
6. Use spaces when designing a URI.
7. Redirection must be used if a change in URI is required.

Answer:- 3, 5, 7

**4. Architectural Constraints of REST**

Select the Architectural Constraints of REST API:

Pick **ONE OR MORE** options

1. Uniform interface
2. Stateless
3. Cacheable
4. Layered system

Answer:- 1, 2, 3, 4

**5. REST Basics**

**REST** is an architecture to provide access to data over a network through an API. Which of the following are true?

Pick **ONE OR MORE** options

1. REST is strictly a client-server interaction type meaning that the client performs requests and the server sends responses to these requests.
2. REST is a server-server interaction meaning that both sides can make requests and send responses to requests.
3. In REST architecture, a properly designed access endpoint should not specify actions as a part of the resource URI. nstead, actions should be specified using appropriate protocol methods such as GET, POST, PUT, and DELETE over НТТР.
4. REST responses are not capable of specifying any caching related information regarding the accessed resource. Caching must be resolved with other mechanisms.

Answer:- 1, 3

**6. Longest Consecutive Subsequence**

Given an array of distinct positive integers. Which of the following can be used to find the longest consecutive sub-sequence of integers? (Note that the consecutive numbers need not be sorted.)

For example, if the given array is [1, 7, 3, 2, 8], the longest consecutive subsequence is [1, 3, 2] as 1, 2,3 are consecutive integers.

Pick **ONE** option

1. Disjoint Set Union
2. Dijkstra
3. Kadane Algorithm
4. None of these

Answer:- 1

**7. What is the output of the following code?**

```
INTEGER a = 10, b = 25, c = 15
INTEGER res = 0
while (b > 0) {
    res += (a % c) + (c% a)
    b -= a % c swap (a, c)
}
PRINT res
```

Pick **ONE** option

1. 45
2. 35
3. 20
4. 30
5. Infinite Loop

Answer:- 5

**8. What is the value of 'a' after execution?**

```
INTEGER a = 315
INTEGER b = 840
while (b > 0) {
    a %= b swap (a, b)
}
```

Pick **ONE** option

1. 7
2. 35
3. 6
4. 105

Answer:- 4




