# LeetCodeSolutions
Leetcode question done

1.) Pascal's Triangle II:

```cpp
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        std::vector<std::vector<int>> pas;
        std::vector<int> stor;

        // Make an empty Pascal's triangle
        for (int i = 0; i <= rowIndex; ++i) {
            for (int j = 0; j <= i; ++j) {
                if (j == 0 || j == i) {
                    stor.push_back(1);
                } else {
                    stor.push_back(0);
                }
            }
            pas.push_back(stor);
            stor.clear();
        }

        // Complete the Pascal's triangle
        for (int i = 2; i < pas.size(); ++i) {
            for (int j = 1; j < pas[i].size() - 1; ++j) {
                pas[i][j] = pas[i - 1][j - 1] + pas[i - 1][j];
            }
        }

        return pas[rowIndex];
    }
};
```

2.) Evaluate Reverse Polish Notation:

```cpp
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        // Easy
        // Using sliding window technique
        // Whenever RPN is satisfied just shift cursor to starting point
        // Convert into integer strings to actual numbers
        if(tokens.size() == 1) { // Literally the most pointless edgecase
            return stoi(tokens[0]);
        }
        else {
        int sum = 0;
        for(int i = 0; i < tokens.size()-2; ++i) {
            if(isNumber(tokens[i]) == true && isNumber(tokens[i + 1]) == true && isOperator(tokens[i + 2]) == true) {
                if(tokens[i + 2][0] == '+') {
                    sum = (std::stoi(tokens[i])) + (std::stoi(tokens[i+1]));
                    tokens.erase(tokens.begin() + i);
                    tokens.erase(tokens.begin() + i);
                    tokens.erase(tokens.begin() + i);
                    tokens.insert(tokens.begin() + i, std::to_string(sum));
                    i = -1;
                }
                else if(tokens[i + 2][0] == '-') {
                    sum = (std::stoi(tokens[i])) - (std::stoi(tokens[i+1]));
                    tokens.erase(tokens.begin() + i);
                    tokens.erase(tokens.begin() + i);
                    tokens.erase(tokens.begin() + i);
                    tokens.insert(tokens.begin() + i, std::to_string(sum));
                    i = -1;
                }
                else if(tokens[i + 2][0] == '*') {
                    sum = (std::stoi(tokens[i])) * (std::stoi(tokens[i+1]));
                    tokens.erase(tokens.begin() + i);
                    tokens.erase(tokens.begin() + i);
                    tokens.erase(tokens.begin() + i);
                    tokens.insert(tokens.begin() + i, std::to_string(sum));
                    i = -1;
                }
                else if(tokens[i + 2][0] == '/') {
                    sum = (std::stoi(tokens[i])) / (std::stoi(tokens[i+1]));
                    cout<<sum<<endl;
                    cout<<tokens[i]<<","<<tokens[i+1]<<endl;
                    tokens.erase(tokens.begin() + i);
                    tokens.erase(tokens.begin() + i);
                    tokens.erase(tokens.begin() + i);
                    tokens.insert(tokens.begin() + i, std::to_string(sum));
                    i = -1;
                }
                if(tokens.size()==1)
                break;
            }
        }
        return stoi(tokens[0]);
        }
    }
    bool isOperator(const std::string& s) {
        return s == "+" || s == "-" || s == "*" || s == "/";
    }

    bool isNumber(const std::string& s) {
        return !isOperator(s);
    }
};
```
