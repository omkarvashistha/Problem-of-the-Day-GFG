## Question
Given an array arr of N integers and an integer K, find the number of subsets of arr having XOR of elements as K.
## Link
https://practice.geeksforgeeks.org/problems/subsets-with-xor-value2023/1
## Explanation
One thing we understand by looking at question is that we have to make choices to weather to take any particular number or not so we understand that we have to use dynamic programming. Okay so now how to solve this question.This question looks similar to Subset Sum Problem so we use the same concept.But at first we need to find the second range that we use while creating any dp array so that second range will be the maximum value of the xor any subset will acquire so the formula for that is 
m = pow(2,log2(maxElement of array)+1)-1 . So now we got the second range so we create the dp array and intially all its values will be 0 and dp[0][0] will be 1 as when there are no elements its XOR will be 0 . We have to keep in mind the concept of Subset Sum and when iterating dp[i][j] will be dp[i-1][j]+dp[i-1][j^arr[i-1]] -> Here the part dp[i-1][j] represents that when we do not take that particular element and move forawrd and the part dp[i-1][j^arr[i-1] represents that we have taken that element.
## Code
```
  int subsetXOR(vector<int> arr, int N, int K) {
        // code here
        
        int maxEle = 0;
        for(int i=0;i<N;i++){
            maxEle = max(maxEle,arr[i]);
        }
        
        int m = (1<<(int)(log2(maxEle)+1))-1;
        
        if(K>m) return 0;
        
        int dp[N+1][m+1];
        
        for(int i=0;i<=N;i++){
            for(int j=0;j<=m;j++){
                dp[i][j] = 0;
            }
        }
        
        dp[0][0] = 1;
        
        for(int i=1;i<=N;i++){
            for(int j=0;j<=m;j++){
                dp[i][j] = dp[i-1][j] + dp[i-1][j^arr[i-1]];
            }
        }
        
        return dp[N][K];
    }
```
