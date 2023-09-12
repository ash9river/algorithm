[문제 링크](https://atcoder.jp/contests/dp/tasks/dp_a)

간단한 메모이제이션 방법을 반복적 동적 계획법과 재귀적 동적 계획법으로 작성

```
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
vector<int> h(100000);
vector<int> cache(100000);
int n;
int pathMin(int now){
	if(now>=n) return 987654321;
	if(now==n-1) return 0;
	int& ret=cache[now];
	if(ret!=-1) return ret;
	return ret=min(abs(h[now]-h[now+1])+pathMin(now+1),abs(h[now]-h[now+2])+pathMin(now+2));
}
int main(){
	cin.tie(0);
	ios_base::sync_with_stdio(0);
	cin>>n;
	for(int i=0;i<n;++i){
		cin>>h[i];
	}
	fill(cache.begin(),cache.end(),-1);
	cout<<pathMin(0); //재귀적 동적 계획법 해답
	vector<int> dp(100000,987654321);
	dp[0]=0;
	for(int i=0;i<n-1;++i){
		for(int j=1;j<3;++j){
			dp[i+j]=min(dp[i+j],dp[i]+abs(h[i]-h[i+j]));
		}
	}
	cout<<" & "<<dp[n-1]; //반복적 동적 계획법 해답
}
```
