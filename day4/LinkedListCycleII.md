# Intro
- Linked List에 대한 이해가 필요하다.

# Solution
- Linked List를 입력받아 tail의 cycle idx를 가리키는 Node를 반환하면 된다.

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if (!head || !head->next)
            return nullptr;
        
        ListNode* tmp = head;
        unordered_map<ListNode*, int> table;
        int idx = 0;
        
        table[head] = idx;
        tmp = tmp->next;
        while (tmp->next && table.find(tmp->next) == table.end()) {
            ++idx;
            table[tmp] = idx;
            tmp = tmp->next;
        }
        
        return tmp->next;
    }
};
```
- 먼저, head, head->next가 nullptr인 경우는 cycle이 발생하지 않은 경우여서 nullptr을 return 했다.
- 그 이후 로직은 cycle이 발생하거나 원소가 2개 이상인 경우를 처리하고자 했다.
- 사이클이 발생한 것을 알려면 tail의 next가 어느 Node인지를 알아야한다고 생각했다.
  - 따라서 O(1)의 검색 연산을 수행할 수 있는 hash map을 활용해 해당 Node(Key)의 index(Value)를 저장했다.
- while문에서는 현재 Node의 next가 nullptr인지 즉, cycle이 발생하지 않은지와 table에 존재하는 key인지를 검사 즉, tail Node의 next가 존재하여 cycle이 발생했다는 것을 조건문으로 두었다.
- 마지막으로, cycle이 발생하지 않으면 nullptr을, cycle이 발생했으면 tmp->next를 return 한다.