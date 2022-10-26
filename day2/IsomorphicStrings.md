# Intro
- 여러가지 Solution이 존재하지만, LeetCode에서 직관적이고, 최적화된 정답을 제공하고 있어 해당 내용을 숙지

# Solution
- 동일한 형태를 갖는 String인지를 구별하는 문제다.
```
s : egg
t : add
=> Isomophic True
```

```
s : foo
t : bar
=> Isomophic False
```

- s 라는 string에서 문자와 t라는 string에서 문자를 서로 hash map을 통해 key, value 형태로 매칭한다.
- 해당 hash map을 이용해 동일 구조인지 판단하는 문제다.
- **가장 먼저 3가지 케이스를 고려**한다.

|1. s의 character가 t의 character와 mapping된 적이 없는 Case | 2. s의 char가 t의 char와 mapping된 적이 있는 Case | 3. s의 char가 t의 char와 mapping된 적이 있는 데, 서로 매칭이 안되는 Case |
| :--:|:--:|:--:|
| ![image](https://user-images.githubusercontent.com/69780812/197381803-d080dcae-f900-4511-a2ec-6dce9ee09833.png)| ![image](https://user-images.githubusercontent.com/69780812/197381872-02df6f1d-7874-484f-8377-29044ec494dc.png) | |
## Case 1.
- 그대로 map[s[i]] = t[i] 형태로 maaping 한다.
## Case 2.
- isomorphic 조건에 아직 부합하고 있으므로 계속 mapping을 진행하면 된다.
## Case 3.
- map[s[i]]가 존재하는데, map[s[i]] != t[i] 인 경우이다. 이때는 isomorphic 조건이 아니므로 false를 return 한다.

---
- 위에서는 one-way-mapping 방식만을 설명한 것이다. s의 char를 t의 char와 단일 방향으로 mapping하는 것을 의미한다.
- isomorphic에서는 **추가적으로 고려할 점이 양방향으로 mapping이 성립하는지도 포함되어있어야한다.**

| 양방향 mapping 성립 Check Case |
| :--:|
| ![image](https://user-images.githubusercontent.com/69780812/197382029-27881ac7-5fdc-44bd-a874-eaa0d961bf7a.png) |

- s에서 d문자는 one-way-mapping방식으로는 t의 b문자와 mapping 되어야한다.
- 하지만 isomorphic은 1:1 매핑 관계를 성립해야하므로 t의 b문자가 2개의 key를 갖는 것은 isomorphic하지 않음을 의미하게된다.
- 따라서 hash map 2를 만들어 t를 key로, s를 value로 하는 map을 하나더 만든다. (속도 측면으로 유리)
- 이후 map2[t[i]] != s[i] 이면, false를 return 해준다.

```cpp
class Solution {
public:
    bool isIsomorphic(string s, string t) {        
        if ((s.size() == 1) && (t.size() == 1))
            return true;
        
        unordered_map<char, char> patternDict;
        unordered_map<char, char> patternDict2;
        bool result = true;
        
        for(int i = 0; i < s.size(); ++i) {
            if (patternDict.find(s[i]) != patternDict.end()) {
                if (patternDict[s[i]] != t[i]) {
                    result = false;
                    break;
                }
            } else if (patternDict2.find(t[i]) != patternDict.end()) {
                result = false;
                break;
            } else {
                patternDict[s[i]] = t[i];
                patternDict2[t[i]] = s[i];
            }
        }
        
        
        for (pair<char, char> p : patternDict) {
            cout << p.first << ", " << p.second << endl;
        }
        
        return result;
    }
};
```
