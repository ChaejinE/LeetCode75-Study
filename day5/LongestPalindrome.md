# Intro
- Greedy

# Solution
- String을 입력받아 해당 String에 있는 character로 가장 긴 Palindrome을 만들었을 때의 문자열 길이를 return 한다.
  - Palindrome은 앞으로 읽어도, 뒤로 읽어도 일치하는 것을 의미한다.
- 앞으로, 뒤로 읽어도 일치하기 위해서는 해당하는 문자가 짝수 개여야 쌍이 만들어지므로 left side, right side로 둘 수 있다.

```cpp
class Solution {
public:
    int longestPalindrome(string s) {
        if (s.length() == 1)
            return 1;
        
        set<char> tmpSet;
        for (char c : s)
            tmpSet.emplace(c);
        
        unordered_map<int, vector<char>> table;
        int tmpCount = 0;
        for (char c : tmpSet) {
            tmpCount = count(s.begin(), s.end(), c);
            table[tmpCount].emplace_back(c);
        }
        
        int result = 0;
        for (pair<int, vector<char>> p : table) {
            result += static_cast<int>(p.first / 2) * 2 * p.second.size();
            if ((result % 2 == 0) && (p.first % 2 == 1))
                ++result;
        }
        
        return result;
    }
};
```
- 임의의 character가 v번 등장한다고하면, v += v // 2 * 2로 짝수화 시켜준다. (홀수개 등장하는 문자일 수 있기 때문)
  - // 연산은 버림연산을 해준다.
- 마지막으로 임의의 character가 홀수번 등장하면, 이전의 문자들과 함께 Palindrome이 만들어져있는 것으로 계산되어 있다. 다만, 홀수개의 문자라면 unique 문자 하나가 남으므로 넣을 수 있는지 확인해야 더 긴 Palindrome을 만들 수 있다. 이렇게하려면 문자 하나를 추가하기 전에 Palindrome이 되어 있어야 한다.
  - 이는 이미 unique 문자 하나를 넣은 경우가 추가되었는지를 확인하면 된다.
  - ```((result % 2 == 0) && (p.first % 2 == 1))```
  - 계속 저장 중인 가장 긴Palindrome을 만드는 경우의 길이가 짝수이고, 해당 문자가 홀수라면 +1을 해준다. 아마 한번 정도 ? 일어날 것이다.
