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

## Design Add and Search Word Data Structure
```cpp
class LetterNode {
public:
    LetterNode* alphabet[26]; // Initialize to nullptr
    bool isEnd;
};

class WordDictionary {
public:
    LetterNode* root;

    WordDictionary() { root = new LetterNode(); }

    void addWord(string word) {
        LetterNode* current_node = root;
        for (char c : word) {
            if (current_node->alphabet[c - 'a'] == nullptr) {
                current_node->alphabet[c - 'a'] = new LetterNode();
            }
            current_node = current_node->alphabet[c - 'a'];
        }
        current_node->isEnd = true;
    }

    bool search(string word) { return dfs(word, root); }

    bool dfs(string target, LetterNode* current_root) {
        if (target.size() == 0) {
            return current_root->isEnd;
        }

        char first_letter = target[0];
        string remaining_target = target.substr(1);

        if (first_letter == '.') {
            for (int i = 0; i < 26; i++) {
                if (current_root->alphabet[i] != nullptr &&
                    dfs(remaining_target, current_root->alphabet[i])) {
                    return true;
                }
            }
        } else {
            if (current_root->alphabet[first_letter - 'a'] != nullptr) {
                return dfs(remaining_target,
                           current_root->alphabet[first_letter - 'a']);
            }
        }

        return false;
    }
};
```

## Valid Parentheses
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

## Longest Increasing Subsequence
```cpp
int lengthOfLIS(vector<int>& nums) {
    int dp[nums.size()];
    for (int i = 0; i < nums.size(); i++) {
        dp[i] = 1;
    }

    for (int i = 1; i < nums.size(); i++) {
        for (int j = 0; j < i; j++) {
            if (nums[j] < nums[i]) {
                dp[i] = max(dp[i], dp[j] + 1);
            }
        }
    }

    int max_length = 1;
    for (int length : dp) {
        max_length = max(max_length, length);
    }
    return max_length;
}
```
## Container With Most Water
```cpp
int maxArea(vector<int>& height) {
    int current_max = INT_MIN;
    int left_ptr = 0;
    int right_ptr = height.size() - 1;
    while (left_ptr < right_ptr) {
        int current_amount = (right_ptr - left_ptr) *
                             min(height[left_ptr], height[right_ptr]);
        current_max = max(current_max, current_amount);
        if (height[left_ptr] < height[right_ptr]) {
            left_ptr += 1;
        } else {
            right_ptr -= 1;
        }
    }
    return current_max;
}
```
