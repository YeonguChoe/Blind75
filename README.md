# Blind75
- Programming Language: Java, Kotlin, C#

## Implement Trie (Prefix Tree)

```java
class TrieNode {
    TrieNode[] links = new TrieNode[26];
    boolean isEnd = false;
}

class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    public void insert(String word) {
        TrieNode currentNode = root;
        for (char c : word.toCharArray()) {
            if (currentNode.links[c - 'a'] == null) {
                currentNode.links[c - 'a'] = new TrieNode();
            }
            currentNode = currentNode.links[c - 'a'];
        }
        currentNode.isEnd = true;
    }

    public boolean search(String word) {
        TrieNode currentNode = root;
        for (char c : word.toCharArray()) {
            if (currentNode.links[c - 'a'] == null) {
                return false;
            }
            currentNode = currentNode.links[c - 'a'];
        }
        return currentNode.isEnd;
    }

    public boolean startsWith(String prefix) {
        TrieNode currentNode = root;
        for (char c : prefix.toCharArray()) {
            if (currentNode.links[c - 'a'] == null) {
                return false;
            }
            currentNode = currentNode.links[c - 'a'];
        }
        return true;
    }
}
```
