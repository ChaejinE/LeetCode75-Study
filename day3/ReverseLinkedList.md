# Intro
- Linked List의 Link를 거꾸로 바꿔줘야된다 !

# Solution
- temporary에 Linked List의 Node를 담으면서 연결을 끊고 반대로 붙이고를 nullptr를 만날 때까지 반복해야된다.


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
    ListNode* reverseList(ListNode* head) {        
        if (!head || !(head->next))
            return head;
        
        ListNode* prev = head;
        ListNode* tmp = head->next;
        prev->next = nullptr;
        
        while (tmp) {
            head = tmp;
            tmp = tmp->next;
            head->next = prev;
            prev = head;
        }
        
        return head;
    }
};
```
