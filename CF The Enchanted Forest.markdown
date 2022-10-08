there is an $n$ points line X，every point $i$ has $a_i$ mushrooms，Bessie can start from any point, in each miniute (start at 0 min) the following operations will happen in order：

        1. move left 1, right 1, or stay （from position $x$ to $y$，$abs(x-y)<= 1$)

        2. collect current position's mushrooms

        3. all positions' mushroom number $+1$

Bessie has $k$ minutes，solve for the maximum mushrooms she can collect

 
Solution: 

increase is a constant $\frac{k(k-1)}{2}$ (optimal），optimal is a linear interval with length $k$ (think why linear）

cases：

　　$k <= n$:

　　　　optimal is the max linear interval with length $k$ (original mushroom) + (extra mushroom gained) $\frac{k(k-1)}{2}$

　　　　using slide window achieve in $O(n)$

　　$k > n$:

　　　　all $a_i$ sum + extra mushroom 

　　　　consider complementary counting：

　　　　　　our gain = total generated - those we have not gain

　　　　　　　　total generated = $k*n$

　　　　　　assume the last point $n$，it has $1$ mushroom haven't being collected，point $n-1$ has $2$，point $n-2$ has $3$ ...... point $1$ has $n$

　　　　　　　　those we have not gain = $\frac{n(n+1)}{2}$

　　　　　　our gain = $k*n$ - $\frac{n(n+1)}{2}$

　　　　　　
,,,
#include <iostream>
#include <cstring>
#include <algorithm>
#define int long long 
using namespace std;
 
void solve(){
    int n, k; cin>>n>>k;
    int ar[n+5];
    for(int i=1;i<=n;i++) cin>>ar[i];
    if(k<=n){
        int l=1, ans=0, cur_sum=0;
        for(int r=1;r<=n;r++){
            cur_sum+=ar[r];
            while((r-l+1)>k){
                cur_sum-=ar[l];
                l++;
            }
            ans=max(ans, cur_sum);
        }
        cout<<ans+(k*(k-1))/2<<endl;
    }else{ 
        int sum=0;
        for(int i=1;i<=n;i++) sum+=ar[i];
        sum += (n*k) - n*(n+1)/2;
        cout<<sum<<endl;
    }
}
 
signed main(){
    int t; cin>>t;
    while(t--){
        solve();
    }
}
,,,
 

 

　　　　

　　　　　　

 
