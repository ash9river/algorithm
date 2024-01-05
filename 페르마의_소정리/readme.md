## 모듈러 연산 성질

$$
   (a+b)\ mod\ M =((a\ mod\ M)+(b\ mod\ M))\ mod\ M
$$

$$
   (a-b)\ mod\ M =((a\ mod\ M)-(b\ mod\ M))\ mod\ M
$$

- $a>b$,$a \ mod \ M<b\ mod M$인 경우음수로 반환할 수 있어서, 코딩할때는 M을 추가로 더해준다.

$$
   (a-b)\ mod\ M =((a\ mod\ M)-(b\ mod\ M)+M)\ mod\ M
$$

$$
   (a\times b)\ mod\ M =((a\ mod\ M)\times(b\ mod\ M))\ mod\ M
$$

- 모듈러 나눗셈은 페르마의 소정리를 사용하여 모듈러 역원을 구한다.

### 페르마의 소정리

> p가 소수이면, 모든 정수 a에 대하여 $a^p \equiv a\ (mod\ p)$이다.<br>
> a가 p의 배수가 아니면 $a^{p-1} \equiv 1\ (mod\ p)$이다.

### 모듈러 역원

- 페르마의 소정리를 이용하여 모듈러 역원을 구할 수 있다.
- 단순히 a를 두 번 나눈 것이다.

> $a^p \equiv a\ (mod\ p)$이므로 $a^{p-2} \equiv \frac{1}{a}\ (mod\ p)$

- 정수 b의 모듈러 m에 대한 역원을 $modInv(b,m)$이라 정의하자.
- $modInv(b,m) = b^{M-2}\ mod\ M$라 표현할 수 있다.
- 다음과 같이 모듈러 나눗셈을 표현할 수 있다.

$$
   (a/b)\ mod\ M=(a\times (b^{M-2})\ mod\ M)\ mod\ M=(a\times modInv(b,M))\ mod\ M
$$

## 이항계수 빠르게 구하기

- 모듈러 역원을 이용하여 이항 계수를 $O(nlogp)$만에 빠르게 구할 수 있다.
- 분할정복을 이용한 거듭제곱 방식도 사용한다.

> ${n \choose r} = _{n}\mathrm{C}_{r}$입니다.

- 충분히 큰 자연수 $n$ 과 $0<r<n$인 자연수 $r$, 소수 $p$

$$
   {n \choose r} (mod\ p) =\frac{n!}{r!\times(n-r)!} = n!\times modInv(r!(n-r)!,p)\ (mod\ p) = n! \times ((r!\times (n-r)!)^{p-2}\ mod\ p)\ (mod\ p) = ((n!\ mod\ p)\times (r!\times (n-r)!)^{p-2}\ mod\ p)\ mod\ p
$$

- 여기서 $modInv$인 $(r!\times (n-r)!\,)^{p-2}\ mod\ p\ $의 계산은 분할정복을 사용한 거듭제곱 기법을 이용한다.

$$
   x^n =
   \begin{cases}
      x\times(x^2)^{\frac{n-1}{2}}, & n=\text{홀수} \newline
      (x^2)^{\frac{n}{2}}, & n=\text{짝수}
   \end{cases}
$$

```cpp
#include <iostream>
#define ll long long
using namespace std 
ll f[4000001],n,r; //팩토리얼배열 f, 자연수 n과 r
ll p=1000000007;  // 큰 소수 p
ll nCr(ll a,ll b){
	ll jisu=p-2;  // 지수는 p-2이다. 
   ll result=a; //결과는 n!과 모듈러역원이므로, n!인 a에 곱하는 식으로 이어나갈 것이다.
   // 여기서 modInv(r!(n-r!),p)을 계산하는데, 지수의 밑인 r!(n-r)!을 x라 칭할 것이다.
	while(jisu){
      //if(jisu&1LL) 도 가능하다.
      if(jisu%2==1) result=result*b%p; // x = 홀수인 경우, x를 하나 떼어내고, n!에 곱한다.
      b=b*b%p; //x의 제곱을 한다. 홀수인 경우도 x^2을 하므로 홀수이든 짝수이든 수행한다.
      // jisu=jisu/2도 가능
      jisu=jisu>>1LL; //2의 거듭제곱을 이용한 분할제곱이므로 2로 나눈다.
   }
	return result; //결과값을 반환한다.
}
int main(){
	cin>>n>>r; 
   //팩토리얼 계산
	f[0]=1;
	for(int i=1 i<=n ++i){
		f[i]=i*f[i-1]%p; 
	}
	cout<<nCr(f[n],f[r]*f[n-r]%p);  // nCr 계산
   //nPr을 계산할려면 nCr(f[n],f[r])이다. 함수이름을 변경하면 덜헷갈림
}
```
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
