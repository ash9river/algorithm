```
#include <iostream>
#include <vector>
#include <algorithm>
#define ll long long
using namespace std;
int main(){
	cin.tie(0);
	ios_base::sync_with_stdio(0);
	int n;
	cin>>n;
	vector<vector<int>> v(n,vector<int>(3,0));
	for(int i=0;i<n;++i){
		for(int j=0;j<3;++j){
			cin>>v[i][j];
		}
	}
	vector<vector<int>> dp(200000,vector<int>(3));
	for(int i=0;i<3;++i){
		dp[0][i]=v[0][i];
	}
	if(n>1){
		dp[1][0]=v[1][0]+max(v[0][1],v[0][2]);
		dp[1][2]=v[1][2]+max(v[0][0],v[0][1]);
		dp[1][1]=v[1][1]+max(v[0][0],v[0][2]);
	}
	for(int i=2;i<n;++i){
		dp[i][0]=v[i][0]+max(dp[i-1][1],dp[i-1][2]);
		dp[i][1]=v[i][1]+max(dp[i-1][0],dp[i-1][2]);
		dp[i][2]=v[i][2]+max(dp[i-1][0],dp[i-1][1]);
	}
	cout<<max(dp[n-1][0],max(dp[n-1][1],dp[n-1][2]));
}
```
