# Intro
- Linked List의 특성을 잘 파악하고 있어야 풀 수 있다.

# Solution
- Linked List의 Middle Index Node를 찾아 return 한다.

![image](https://user-images.githubusercontent.com/69780812/198824564-582d8eb5-6688-4e35-9ee7-487ad16e4f70.png)

- 문제의 예시

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        int size = 0;
        ListNode* tmp = head;
        while (tmp) {
            tmp = tmp->next;
            ++size;
        }
        
        int middleIdx = static_cast<int>(size/2);
        for (int i = 0; i < middleIdx; ++i)
            head = head->next;
            
        return head;
    }
};
```
- 나는 Linked List의 size를 얻어 그 중간 만큼만 head를 update해서 return 했다.

![image](https://user-images.githubusercontent.com/69780812/198824602-0bf909b1-d4ab-4d68-aabc-2cca4b97b9bf.png)
- size를 계산하려고 했던 이유는 제한조건이 100개 Node면 충분히 순회할 수 있기 때문이었다.

## Other Solution - Two Pointer

```
While slow moves one step forward, fast moves two steps forward.
Finally, when fast reaches the end, slow happens to be in the middle of the linked list.
For example, head = [1, 2, 3, 4, 5], I bolded the slow and fast in the list.
```
- step 0: slow: [**1**, 2, 3, 4, 5], fast: [**1**, 2, 3, 4, 5]
- step 1: slow: [1, **2**, 3, 4, 5], fast: [1, 2, **3**, 4, 5]
- step 2: slow: [1, 2, **3**, 4, 5], fast: [1, 2, 3, 4, **5**]
```
end because fast cannot move forward anymore and return [3, 4, 5]
```

```cpp
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode *slow = head, *fast = head;
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }
};
```
- step 1 일 때, slow와 fast는 1 idx 차이,
- step 2 일 때, 3 일 때 2, 3 idx 차이가 나면서 점점 벌어진다.
- slow가 중간 idx 임을 가정하고, 움직이는 두 개의 포인터인 것이다.
  - [1, 2, 3 ... ] 인 list라고 가정해보자.
  - slow->val 2이면 1,2,3 이어야하면서, 중간 idx가 slow->val=2 이다.
  - slow->val 3이면 1,2,3,4,5 이어야하면서 중간 idx가 slow->val=3 이다.
