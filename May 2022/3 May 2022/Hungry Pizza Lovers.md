## Question
Dominos Pizza has hungry customers waiting in the queue. Each unique order is placed by a customer at time x[i], and the order takes y[i] units of time to complete.
You have information on all n orders, Find the order in which all customers will receive their pizza and return it. If two or more orders are completed at the same time then sort them by non-decreasing order number.
## Explanation
It is a pretty simple greedy question so here what we will do is create a new vector that will be of type pair<int,int> which will store the sum of ordered time+time taken to make pizza and the second will be the position of that value in original array we will follow 1-based indexing and then we will sort our new array in increasing order but we have to keep in mind when sum of two values is same so we will sort according to its order time and then we will just store the positions of the elements of our sorted array into our answer array and return it.
## Code
```
// This function will sort according to the given condition
static bool cmp(pair<int,int> &a,pair<int,int> &b){ 
    if(a.first == b.first){
        return a.second < b.second;
    }
    return a.first < b.first;
}

vector<int> permute(vector<vector<int>> &arr, int n)
{
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
}
```
