## Question
Given a non-negative number N in the form of string. The task is to apply at most one swap operation on the number N so that the result is just a previous possible number.
## Explanation
Since we have to find previous possible number then if we start from front of the string and doing swap and checking then it will take too much time and may not lead 
to correct answer, So we will start from end of the string and first find the number that is larger than all the numbers from last because that is our one target
character,now we will find the possible number that we need to swap with and the possible number that possible number will the number that is just largest number smaller 
than our target character we will again iterate from last and find that number.Proper code is below that will clear your mind on how we find that character.
## Code
```
  string previousNumber(string S){
    int n = S.size();
    int index = -1;
    for(int i=n-2;i>=0;i--){
      if(S[i] > S[i+1]){
        index = i;  --> (this is our target index that we need to swap with)
        break;
      }
    }
    if(index==-1){ -->(if index is not changed that means numbers are in increasing order and any swap will only make number larger than current)
      return "-1";
    }
    int greaterSmall = -1;
    for(int i=n-1;i>index;i--){
      if(S[i]<S[index]){
        if(greaterSmall==-1){
            greaterSmall = i;
        }
        else if(S[i]>=S[greaterSmall]){
            greaterSmall = i;
        }
      }
    }
    swap(S[index],S[greaterSmall]);
    if(S[0]=='0'){
      return "-1";
    }
    return S;
  }
```
