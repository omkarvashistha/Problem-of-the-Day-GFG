## Question
Given two sorted linked lists consisting of N and M nodes respectively. The task is to merge both of the list (in-place) and return head of the merged list.

## Explanation

## Code
```
Node* sortedMerge(Node* head1, Node* head2)  
{  
    Node* dummy = new Node(0);
    Node* tail = dummy;
    dummy->next = tail;
    while(1){     
        if(!head1){
            tail->next = head2;
            break;
        }
        
        if(!head2 ){
            tail->next = head1;
            break;
        }
        
        if(head1->data<=head2->data){
            tail->next = head1;
            head1 = head1->next;
        }
        else if(head2->data<head1->data){
            tail->next = head2;
            head2 = head2->next;
        }
        tail = tail->next;        
    }
    return dummy->next;
}  
```
