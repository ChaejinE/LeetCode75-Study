# Intro
- 전형적인 Binary Search

# Solution
```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int start = 0;
        int end = nums.size() - 1;
        int middle_index;
        
        while (!nums.empty() && start <= end) {
            middle_index = static_cast<int>((start + end) / 2);
            if (nums[middle_index] == target)
                return middle_index;
            else if (nums[middle_index] < target)
                start = middle_index + 1;
            else
                end = middle_index - 1;
        }
        
        return -1;
    }
};
```
- 반복문 풀이
- sorting 되었을 때 위와 같이 바로 적용 가능.
- middle_index와 같으면 해당 index를, middle_index의 값보다 target이 크면 middle_index + 1 만큼 부터 다시 탐색, 그 반대는 반대로
