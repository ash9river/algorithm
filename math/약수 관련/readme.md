# 오일러 피함수

- 오일러 토션트 함수라고도 불린다.
- 자연수 $n$과 $n$보다 작은 자연수 $x$에 대하여 $gcd(x,n)=1$인 $x$들의 수를 구하는 방법

$$
    \phi (n) = \phi \left( \prod_{i=1}^r p_{i}^{k_{i}} \right) = \prod_{i=1}^r \phi ( p_{i}^{k_{i}} ) = \prod_{i=1}^r { \left[ p_{i}^{k_{i}} \left( 1 - \frac{1}{p_{i}} \right) \right] }
$$

- $10^{12}$ 이하 수에 대해 시간 초과를 피하기 위해서 $\sqrt{10^{12} }$ 에 대한 수만 소수 판별을 하면 된다.
- $10^6$ 이상이면서, $10^{12}$ 이하인 수가 $10^6$ 이상의 소수를 인수를 가질 수 없기 때문이다.

```cpp
#include <iostream>
#include <vector>
#include <deque>
#include <algorithm>
#define ll long long
using namespace std;
ll NUM_MAX=1000000001LL;
vector<bool> prime(NUM_MAX);
deque<ll> table;
void makePrime(){
    prime[0]=prime[1]=false;
    for(ll i=2;i*i<NUM_MAX;++i){
        if(prime[i]){
            for(ll j=i*i;j<NUM_MAX;j+=i){
                prime[j]=false;
            }
        }
    }
}
ll phi(ll n){
    ll ans=1;
    for(ll i=2;i*i<=n;++i){
        ll tmp=0;
        while(n%i==0){
            ++tmp;
            n/=i;
        }
        if(tmp==0) continue;
        ll b=1;
        for(ll j=0;j<tmp-1;++j){
            b*=i;
        }
        b*=(i-1LL);
        if(b!=0) ans*=b;
    }
    if(n>1){
        ans*=(n-1);
    }
    return ans;
}
int main(){
    cin.tie(0);
    ios_base::sync_with_stdio(0);
    ll n;
    cin>>n;
    makePrime();
    for(ll i=1;i*i<=n;++i){
        if(n%i==0){
            table.push_back(i);
            if(i*i!=n) table.push_back(n/i);
        }
    }
    ll ans=-1;
    sort(table.begin(),table.end());
    for(int i=0;i<table.size();++i){
        ll tmp=phi(table[i]);
        if(table[i]*tmp==n){
            ans=table[i];
            break;
        }
    }
    cout<<ans;
}
```

# 약수 빠르게 구하기

```cpp
for(ll i=1;i*i<=n;++i){
        if(n%i==0){
            table.push_back(i);
            if(i*i!=n) table.push_back(n/i);
        }
    }
```
