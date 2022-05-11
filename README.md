# LeetcodeAddtwonumbersLinkedlist-method2
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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        if(l1==nullptr && l2==nullptr)
            return l1;
        if(l1==nullptr && l2!=nullptr)
            return l2;
        if(l1!=nullptr && l2==nullptr)
            return l1;
        
        ListNode *head = new ListNode((l1->val+l2->val)%10);
        ListNode *tmp = head;
        int carry = (l1->val+l2->val)/10;
        l1 = l1->next;
        l2 = l2->next;
        while(l1!=nullptr || l2!=nullptr){
            if(l1==nullptr){
                tmp->next = new ListNode((l2->val+carry)%10);
                carry = (l2->val+carry)/10;
                l2 = l2->next;
            }
            else if(l2==nullptr){
                tmp->next = new ListNode((l1->val+carry)%10);
                carry = (l1->val+carry)/10;
                l1 = l1->next;
            }
            else{
                tmp->next = new ListNode((l1->val+l2->val+carry)%10);
                carry = (l1->val+l2->val+carry)/10;
                l1 = l1->next;
                l2 = l2->next;
            }
            tmp = tmp->next;
        }
        if(carry==1)
            tmp->next = new ListNode(1);
        return head;
    }
};
