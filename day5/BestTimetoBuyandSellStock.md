# Intro
- Greedy 문제
- 10만 이상의 데이터일 때, max_elemnt와 같은 브루트 포스 알고리즘을 빼야할 수 있음을 알게된 문제다.
  - 문제는 풀리지만, Runtime Error가 났던 문제

# Solution
- i 번째 날에 주식의 가격을 vector Input으로 받고, 최대 이익을 계산하여 return 하는 문제다.
- 가장 싸게 사고 가장 비쌀때 매매 한다는 것이 메인 생각이다.

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        auto minElementIter = prices.begin();
        int result = 0;
        
        for (auto startIter = prices.begin(); startIter != prices.end(); ++startIter) {
            if (*startIter <= *minElementIter)
                minElementIter = startIter;
            
            if (result < (*startIter - *minElementIter))
                result = (*startIter - *minElementIter);
        }
        
        return result;
    }
};
```
- 하나의 값을 min 값(매수 값)으로 두고, 선형 순회를하면서 해당 값이 더 작은 값이면 update 해준다.
- 또한, 결과를 해당 최소 매수, 최대 매매의 값으로 update 해준다.
