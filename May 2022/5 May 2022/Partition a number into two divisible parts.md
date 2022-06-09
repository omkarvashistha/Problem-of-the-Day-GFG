## Problem
Given a number (as string) and two integers a and b, divide the string in two non-empty parts such that the first part is divisible by a and the second part is divisible by b. In case multiple answers exist, return the string such that the first non-empty part has minimum length.

## Explanation


## Code

```
  bool check(string s,int a){
        return stoi(s)%a==0? true : false;
    }
    
    string solve(string s,int a){
        int n = s.size();
        string temp = "";
        for(int i=0;i<n;i++){
            temp+=s[i];
            //cout<<temp<<endl;
            if(check(temp,a)){
                return temp;
            }
        }
        return "-1";
    }

    string stringPartition(string S, int a, int b){
        // code here 
        string s1 = "";
        string s2 = "";
        bool flg = false;
        int n = S.size();
        for(int i=0;i<n;i++){
            s1+=S[i];
            s2 = S.substr(i+1,n);
            if(check(s1,a)){
                if(s1.size()==n){
                    return "-1";
                }
                if(check(s2,b)){
                    return s1+" "+s2;
                }
                else{
                    string temp = solve(s2,b);
                    if(temp!="-1"){
                        return s1+""+temp;
                    }
                    
                }
            }
        }
        return "-1";
    }
```
