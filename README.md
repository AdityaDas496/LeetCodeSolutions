# LeetCodeSolutions
Leetcode question done

Pascal's Triangle II:

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

