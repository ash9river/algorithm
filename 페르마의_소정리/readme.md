# 사용한 코드
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define ll long long
using namespace std;
ll f[4000001],n,k;
ll p=1000000007;
ll modInv(ll a,ll b){
	ll jisu=p-2;
	for(;jisu;jisu>>=1){
		if(jisu&(ll)1) a=a*b%p; // x*x^((n-1)/2) 이므로 x 하나 떼어냄
		b=b*b%p; // 이후 (p-2)/2 반복
	}
	return a;

}
int main(){
	cin.tie(0);
	ios_base::sync_with_stdio(0);
	cin>>n>>k;
	f[0]=1;
	for(int i=1;i<=n;++i){
		f[i]=i*f[i-1]%p;
	}
	cout<<modInv(f[n],(f[k]%p*f[n-k]%p)%p);
}
```
- 손으로 정리하다가 두번째 그림의 분할정복 기법에서 실수가 있었다.
- 홀수일 경우, $x \times (x^2)^{\frac{n-1}{2}}$ 이다.

![KakaoTalk_20240105_151025641](https://github.com/ash9river/algorithm/assets/121378532/4be22a88-cb96-49d0-819d-3d9794b80727)
![KakaoTalk_20240105_151135575](https://github.com/ash9river/algorithm/assets/121378532/6eaee84a-17b6-445a-8c82-6cd177a94abc)
