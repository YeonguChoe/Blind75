# Blind75


## Implement Trie (Prefix Tree)

```cpp
class TrieNode {
public:
    TrieNode* links[26];
    bool isEnd = false;
};

class Trie {
    TrieNode* root;

public:
    Trie() { root = new TrieNode(); }

    void insert(string word) {
        TrieNode* current_node = root;
        for (char c : word) {
            if (current_node->links[c - 'a'] == nullptr) {
                current_node->links[c - 'a'] = new TrieNode();
            }
            current_node = current_node->links[c - 'a'];
        }
        current_node->isEnd = true;
    }

    bool search(string word) {
        TrieNode* current_node = root;
        for (char c : word) {
            if (current_node->links[c - 'a'] == nullptr) {
                return false;
            }
            current_node = current_node->links[c - 'a'];
        }
        if (current_node->isEnd == true) {
            return true;
        } else {
            return false;
        }
    }

    bool startsWith(string prefix) {
        TrieNode* current_node = root;

        for (char c : prefix) {
            if (current_node->links[c - 'a'] == nullptr) {
                return false;
            }
            current_node = current_node->links[c - 'a'];
        }
        return true;
    }
};
```
