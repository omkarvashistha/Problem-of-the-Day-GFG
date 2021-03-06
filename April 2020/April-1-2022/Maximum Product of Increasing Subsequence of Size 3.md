# Note
Try to first atleast give 30 minutes to the questions and think of all the possible ways you can think to reach the solution  
## Question
Given a sequence of non-negative integers, find the subsequence of length 3 having maximum product, with the elements of the subsequence  
being in increasing order.
## Explanation  
Here what we have to do is find 3 numbers of increasing order that will give the maximum product.So to do that what we can do is for every number find  
the largest number samller than current number on left and the largest number on right and then calculate its product and find those three numbers which  
gives us the largest product.  
So how to achieve this, it is pretty simple we could create either 2 extra arrays that will store the largest number smaller than current number for each index  
and the other array stores largest number on the right of current number.  
Or what we can do is we just use one extra array for finding greatest number on right and use a loop to find largest number smaller than current number  
and when we find one just find product of all three number check if it is largest product or not and store those numbers in our answer array.  
## Code  
```
vector<int> maxProductSubsequence(int *a , int n) 
    {
        vector<int> ans = {-1,-1,-1};
        long long int maxP = 1;
        vector<int> x(n,1);
        for(int i=n-2;i>=0;i--){
            x[i] = max(x[i+1],a[i+1]);
        }
        
        set<int> b;
        for(int i=0;i<n;i++){
            vector<long long int> c;
            c.push_back(a[i]);
            b.insert(a[i]);
            if((*b.begin())<a[i]){  -->(this is to check if number at starting of set is smaller than current beacause set stores in ascending order)
                auto it = b.lower_bound(a[i]); -->(we use binary search to find the first occurance of current number in set)
                it--;       -->(than we decrement it because number smaller than current will be before first occurance of current)
                c.push_back(*it);
            }
            if(x[i]>a[i]){
                c.push_back(x[i]);
            }
            if(c.size()==3 && (c[0]*c[1]*c[2])>maxP){
                ans = {c[1],c[0],c[2]};
                maxP = c[1]*c[0]*c[2];
            }
        }
        return ans;
    }
```
