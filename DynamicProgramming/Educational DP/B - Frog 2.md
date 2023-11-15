```
#include <iostream>
#include <vector>
#include <algorithm>
#define ll long long
using namespace std;
vector<ll> h(100000);
ll n,k;
int main(){
	cin.tie(0);
	ios_base::sync_with_stdio(0);
	cin>>n>>k;
	for(int i=0;i<n;++i){
		cin>>h[i];
	}
	vector<ll> dp(200000,1099890001);
	dp[0]=0;

	for(int i=0;i<n-1;++i){
		for(int j=1;j<=k;++j){
			dp[i+j]=min(dp[i+j],dp[i]+abs(h[i]-h[i+j]));
		}
	}
	cout<<dp[n-1]; //반복적 동적 계획법 해답
}
```

초기값을 987654321로 잡아서, 자꾸 틀렸었다...
조심하자......
