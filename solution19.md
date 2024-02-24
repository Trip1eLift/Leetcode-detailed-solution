# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
Inspired by Linus Torvalds' good taste on remove node from linked list. It requires understanding from Linus Torvalds's approach in [his 2016 TED Talk](https://www.ted.com/talks/linus_torvalds_the_mind_behind_linux) which is better explained in Github repo [mkirchner/linked-list-good-taste](https://github.com/mkirchner/linked-list-good-taste?tab=readme-ov-file).

# Approach
<!-- Describe your approach to solving the problem. -->
The while loop has 2 stages. In stage 1, we simply decrease `n` while traverse the list using `curr` pointer. Once the value of `n` is zero or less, we started stage 2 where we continue to traverse linkedlist using `curr`, and we also traverse linkedlist using `p` from head. (Note here `p` is an indirect pointer to eliminate edge case of head removal later.)

This will achieve one thing where when `curr` reach the end and become `NULL`, `(*p)` points to the address of Node we want to remove.

After that, we can simply make the pointer, currently points to target Node, points to target->next Node `*p = (*p)->next` using Linus' Method.

# Complexity
- Time complexity:
The time complexity is `O(n)` where we run loop on list once while having two pointers traverse through the list simultaneously.

- Space complexity:
The space complexity is `O(1)` where we create a pointer and an indirect pointer for list traversal.

# Code
```c++
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode *curr = head, **p = &head;
        while (curr) {
            if (n-- < 1) {
                p = &(*p)->next;
            }
            curr = curr->next;
        }
        *p = (*p)->next;
        return head;
    }
};
```