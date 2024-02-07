```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define ll long long
using namespace std;
int main(){
    cin.tie(0);
    ios_base::sync_with_stdio(0);
    ll n,k;
    cin>>n>>k;
    vector<pair<ll,ll>> table(n);//{wieght,val}
    vector<vector<ll>> dp(n+1,vector<ll>(k+1));
    for(ll i=0;i<n;++i){
        cin>>table[i].first>>table[i].second;
    }
    for(ll i=1;i<=n;++i){ 
    dp[i][k]=dp[i-1][k];
        for(ll j=k-1;j>=0;--j){
            if(j+table[i-1].first<=k){
                dp[i][j]=max({
                    dp[i-1][j],
                    dp[i-1][j+1],
                    dp[i-1][j+table[i-1].first]+table[i-1].second
                });
            }
            else{
                dp[i][j]=max(
                    dp[i-1][j],
                    dp[i][j+1]
                );
            }
        }
    }
    cout<<dp[n][0];
}
```
