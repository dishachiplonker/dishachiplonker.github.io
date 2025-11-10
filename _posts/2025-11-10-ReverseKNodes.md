---
title: "Reverse Nodes in K-Group — Walkthrough"
date: 2025-11-10
description: "Full explanation, pointer trace, and walkthrough for Reverse Nodes in K-Group from NeetCode"
---

This is one of my favorite problems in the NeetCode 150 list because it completely stumped me the first time. Because, how can reversing a few nodes be this tricky?

Being honest, it took me 3-4 times of going back to NeetCode’s YouTube solution to start making sense of the problem.

Not because it's conceptually impossible, but because this problem demands tight pointer bookkeeping and a strong mental model.

So I wrote this blog to help anyone struggling the same way, using a full visual trace and annotated explanation.

Before we dive in, shout-out to [NeetCode](https://neetcode.io/) - phenomenal explanation and free content.  

---

## 📎 Problem Summary
> [<u>Reverse Nodes in K-Group</u>](https://leetcode.com/problems/reverse-nodes-in-k-group/description/) — LeetCode 

**Goal:**  
Given a linked list, reverse nodes in groups of `k`.  
If fewer than `k` nodes remain at the end, leave them as-is.

---

## ✅ Python Code : [<u>NeetCode Link</u>](https://neetcode.io/problems/reverse-nodes-in-k-group?list=neetcode150)

```python
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        groupPrev = dummy

        while True:
            kth = self.getKth(groupPrev, k)
            if not kth:
                break
            groupNext = kth.next

            prev, curr = kth.next, groupPrev.next
            while curr != groupNext:
                tmp = curr.next
                curr.next = prev
                prev = curr
                curr = tmp
            
            tmp = groupPrev.next
            groupPrev.next = kth
            groupPrev = tmp
        
        return dummy.next

    def getKth(self, node, k):
        while node and k > 0:
            node = node.next
            k -= 1
        return node
