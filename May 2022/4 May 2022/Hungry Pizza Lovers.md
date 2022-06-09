## Problem
Dominos Pizza has hungry customers waiting in the queue. Each unique order is placed by a customer at time x[i], and the order takes y[i] units of time to complete.
You have information on all n orders, Find the order in which all customers will receive their pizza and return it. If two or more orders are completed at the same time then sort them by non-decreasing order number.

## Explanation
This is a greedy problem we have to add the x[i] and y[i] and sort it.

## Code
```
vector<pair<int,int>> a;
    int x = 1;
    for(vector<int> i : arr){
        a.push_back({i[0]+i[1],x});
        x++;
    }
    
    sort(a.begin(),a.end(),cmp);
    vector<int> ans;
    
    for(int i=0;i<n;i++){
        ans.push_back(a[i].second);
    }
    
    return ans;
    
```
