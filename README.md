# Blind75
- Programming Language: CPP

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

Valid Parentheses
```cpp
bool isValid(string s) {
    stack<char> parentheses;

    map<char, char> pair;
    pair.insert({')', '('});
    pair.insert({'}', '{'});
    pair.insert({']', '['});

    for (char c : s) {
        if (c == '(' || c == '{' || c == '[') {
            parentheses.push(c);
        }
        if (c == ')' || c == '}' || c == ']') {
            if (parentheses.empty() or parentheses.top() != pair[c]) {
                return false;
            }
            parentheses.pop();
        }
    }
    if (!parentheses.empty()) {
        return false;
    }
    return true;
}
```

## Spiral Matrix

```cpp
vector<int> spiralOrder(vector<vector<int>>& matrix) {
    vector<int> result;
    int row = matrix.size();
    int column = matrix[0].size();

    int up_rail = 0;
    int down_rail = row - 1;
    int left_rail = 0;
    int right_rail = column - 1;

    while (result.size() < row * column) {
        // L->R
        for (int c = left_rail; c <= right_rail; c++) {
            result.push_back(matrix[up_rail][c]);
        }
        // T->B
        for (int r = up_rail + 1; r <= down_rail; r++) {
            result.push_back(matrix[r][right_rail]);
        }

        // R->L
        if (up_rail != down_rail) {
            for (int c = right_rail - 1; c >= left_rail; c--) {
                result.push_back(matrix[down_rail][c]);
            }
        }

        // B->T
        if (left_rail != right_rail) {
            for (int r = down_rail - 1; r > up_rail; r--) {
                result.push_back(matrix[r][left_rail]);
            }
        }

        left_rail += 1;
        right_rail -= 1;
        up_rail += 1;
        down_rail -= 1;
    }

    return result;
}
```
