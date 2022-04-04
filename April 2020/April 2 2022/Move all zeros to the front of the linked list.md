## Question
Given a linked list, the task is to move all 0s to the front of the linked list.The order of all another element except 0 should be same after rearrangement.
## Explanation
So here the thought process is not much we just need to check if a nodes data is 0 then just simply put it in first and on key thing is start from second node.
So we take a node temp that refers to head and make loop till temp->next is not null and then we take a node t which will have temp->next and check if t->data is 
0 if yes then put temp->next = t->next this means we remove this node from sequence and then put t->next = head and head = t else we just move forward normally.
## Code
```
void moveZeroes(struct Node **head)
{
    Node* temp = *head;
    while(temp->next){
        Node* t = temp->next;
        if(t->data==0){
            temp->next = t->next;
            t->next = *head;
            *head = t;
        }
        else{
            temp = temp->next;
        }
    } 
}
```
