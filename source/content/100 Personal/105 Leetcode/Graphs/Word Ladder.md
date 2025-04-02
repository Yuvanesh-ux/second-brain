#bfs #graphs
# Word Ladder

You are given two words, `beginWord` and `endWord`, and also a list of words `wordList`. All of the given words are of the same length, consisting of lowercase English letters, and are all distinct.

Your goal is to transform `beginWord` into `endWord` by following the rules:

- You may transform `beginWord` to any word within `wordList`, provided that at exactly one position the words have a different character, and the rest of the positions have the same characters.
- You may repeat the previous step with the new word that you obtain, and you may do this as many times as needed.

Return the **minimum number of words within the transformation sequence** needed to obtain the `endWord`, or `0` if no such sequence exists.

**Example 1:**

```java
Input: beginWord = "cat", endWord = "sag", wordList = ["bat","bag","sag","dag","dot"]

Output: 4
```

Copy

Explanation: The transformation sequence is `"cat" -> "bat" -> "bag" -> "sag"`.

**Example 2:**

```java
Input: beginWord = "cat", endWord = "sag", wordList = ["bat","bag","sat","dag","dot"]

Output: 0
```

Copy

Explanation: There is no possible transformation sequence from `"cat"` to `"sag"` since the word `"sag"` is not in the wordList.

**Constraints:**

- `1 <= beginWord.length <= 10`
- `1 <= wordList.length <= 100`

## Solution Intution

By creating an adjaceny list of all the words and their graph of one letter differring, we can easily get from the start word to the end word

We can create the adj list by using some symbol to stand in for a letter and match up those that have the same filters

for example `dog` can become `*og`, `d*g`, or `do*` and `dot` can become `*ot`, `d*t`, or `do*`. We can see that the do* filters match for the two words, and this is the key. We can use **BFS** to iterate through the node connections and find the shortest path from beginning word to the end word

```
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        if endWord not in wordList:
            return 0

        adjList = defaultdict(list)
        wordList.append(beginWord)

        for word in wordList:
            for j in range(len(word)):
                pattern = word[:j] + "?" + word[j + 1:]
                adjList[pattern].append(word)
        
        visit = set([beginWord])
        q = deque([beginWord])
        res = 1

        while q:
            for i in range(len(q)):
                word = q.popleft()

                if word == endWord:
                    return res
                
                for j in range(len(word)):
                    pattern = word[:j] + "?" + word[j + 1:]
                    for nei in adjList[pattern]:
                        if nei not in visit:
                            visit.add(nei)
                            q.append(nei)
            res += 1
        
        return 0
```