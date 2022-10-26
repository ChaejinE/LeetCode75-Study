# Intro
- Linked List를 숙지해야한다.

# Solution
- 두 연결 리스트를 받아 하나의 sorted list 를 만드는 문제다.
- head Node의 값이 작은 list의 head를 head로 갖는 새로운 list (ptr)을 만든다.
- 이후 더 작은 값을 가졌던 리스트는 다음 노드로 초기화한다. 이후, current node를 ptr로 둔다.
- while 문에서 두 list의 현재 Node의 값을 비교하며 current node의 next로 추가해준다.
- current node는 next node로 update한다. while 문은 두 리스트 중 nullptr이 나올 때 까지한다.
- 마지막으로 남아있는 list의 node를 Current Node의 next로 해주면 sorted linked list가 된다. 

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
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        if (list1 == nullptr)
            return list2;
        else if (list2 == nullptr)
            return list1;
        
        ListNode* ptr = list1;
        if (list1->val > list2->val) {
            ptr = list2;
            list2 = list2->next;
        } else {
            list1 = list1->next;
        }
        ListNode* currentPtr = ptr;
        
        while (list1 && list2) {
            if (list1->val <= list2->val) {
                currentPtr->next = list1;
                list1 = list1->next;
            } else {
                currentPtr->next = list2;
                list2 = list2->next;
            }
            
            currentPtr = currentPtr->next;
        }
        
        if (!list1)
            currentPtr->next = list2;
        else
            currentPtr->next = list1;
        
        return ptr;
    }
};
```

