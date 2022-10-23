# Intro
- 해결하지 못했다.

# Solution
```cpp
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int n = s.length();
        int m = t.length();
        int j = 0;
        
        if (n > m)
            return false;
        else if (n == 0)
            return true;
        
        for (int i = 0; (i < m) && (j < n); ++i) {
            if (t[i] == s[j])
                ++j;
        }
        
        return (j == n);
    }
};
```
- s가 t의 substring인지 확인하는 문제다.
- 두 개의 Pointer를 이용해서 각 String마다 이동시켜 해결한다.
- s의 첫 char를 가리키는 j pointer로 시작해서, t의 char를 가리키는 i pointer를 증가시키며 같을 때에만 j를 증가시켜준다.
  - 이렇게하면, s의 string이 t의 string에 모두 존재했을 경우 j와 n의 값이 같게된다.
  - j는 증가시킨 최종 pointer(index)의 번호이고, n은 s string의 길이이다.
  - 두 값이 같다는 뜻은 s가 t에 모두 존재해서 순회했다는 의미이다.