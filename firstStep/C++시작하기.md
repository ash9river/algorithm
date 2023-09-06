# C++ 시작하기
---
###### 기존 C에서 C++로 바꾸면서 stdio.h나 printf같은 C형식의 헤더 혹은 입출력 배제&nbsp; 
##### standard input output-> iostream
```
#include <iostream>
int main(){
  int a;
  cin>>a;
  cout<<a;
  return 0;
}
```
---
#### 또한 자료구조를 이용할 시, 직접 구현보다는 동적 할당이 편리한 C++의 STL 사용 &nbsp; 
vector,pair,tuple,stack,queue 등이 있음&nbsp; 
그 이외의 기본적인 것들은 C와 다를 것이 없으나 빠른 입출력시&nbsp; 
```
    cin.tie(0);
    ios_base::sync_with_stdio(0);
```
cin.tie(NULL)은 cin과 cout의 묶음을 푼다. <br/>
기본적으로 cin으로 읽을 때 먼저 출력 버퍼를 비우는데, 입력과 출력을 여러 번 번갈아서 반복해야 하는 경우 필수적이다. <br/><br/>
ios_base::sync_with_stdio(false)는 C와 C++의 버퍼를 분리.<br/>
이것을 사용하면 cin/cout이 더 이상 stdin/stdout과 맞춰 줄 필요가 없으므로 속도가 빨라진다. <br/><br/>
단, 버퍼가 분리되었으므로 cin과 scanf, gets, getchar 등을 같이 혼용하면 안되고, cout과 printf, puts, putchar 등을 같이 사용하면 안된다.<br/>
그 이외의 C++헤더나 STL의 사용법은 코딩해나가면서 숙지.  
특히, 배열의 원소들을 정렬할 시, 그냥 C++의 sort() 함수 사용  
cin과 getline을 혼용시, cin은 개행 문자를 남겨두기 때문에, 입력버퍼를 비워줘야 한다.
```
  int a;
  string str;
  cin>>a;
  cin.ignore();
  getline(cin,str);
```
입력 버퍼를 비우기 위해 cin.ignore() 함수 활용한다.
<br>
EOF처리는 엄청 쉽다.
```
  string a;
  while(!cin.eof()){
    cin>>a;
  }
```
getline 함수 활용시
```
  string str;
  while(getline(cin,str)){
    cout<<str;
  }
```

---
### 그 외  
<details>
    <summary>자세히</summary>


for문 사용시 전위연산자가 후위연산자보다 성능이 아주 살짝 좋다.  
##### 후위연산자는 값을 메모리에 기억했다가 증가시키기 때문임.  
```
  for(int i=0;i<n;++i) // 전위연산자
```
```
  for(int i=0;i<n;i++) // 후위연산자
```
```
  Foo& Foo::operator++()   // called for ++i
  {
      this-> data += 1;
      return *this;
  }
  
  Foo Foo::operator++(int ignored_dummy_value)   // called for i++
  {
      Foo tmp(*this);   // variable "tmp" cannot be optimized away by the compiler
      ++(*this);
      return tmp;
  }
```
for-each 문
```
  vector<int> v(n);
  for(int i=0;i<n;++i){
      v[i]=i;
  }
  // vector를 for-each문으로 탐색할 수 있다.
  for(int k:v){
      cout<<k<<'\n;
  }
```
*그러나 보통 1000회 이상의 반복문 사용시 for문보다 while문이나 for-each문이 더 성능에 좋다.  
<!--
*for문도 하향으로 비교하면 빠르다(단 비교연산자가 compare>0 일경우) [출처](https://stackoverflow.com/questions/1340589/are-loops-really-faster-in-reverse)
!-->
> 그냥 가독성 좋은게 제일 좋다.
> >by 내 생각

</details>
<hr>

지역 변수로 선언된 배열을 함수의 매개변수 전달시, 직접 전달해서 사용하지 않고, 다른 방법 [사용](http://www.tcpschool.com/c/c_memory_structure)

* 지역변수는 스택 영역에 생성되고, 전역변수는 데이터 영역에 생성되기 때문에 데이터가 많은 경우 함수의 매개 변수로 전달시 실패할 수도 있음.(stack memory 초과)
* 알고리즘 문제 풀이할 때, 대부분의 경우 전역변수에 두는 편이 더 나음.(데이터 접근 및 변경에 용이하고, 스택영역에서 배열 생성의 메모리 제한을 감안하지 않아도 됨)
ex) [백준 16496 큰 수 만들기](https://www.acmicpc.net/problem/16496)  

### 실패코드 
<details>
    <summary>자세히</summary>

```
#include <iostream>
#include <vector>
#include <algorithm>
#define ull unsigned long long
using namespace std;
bool cmp(const string& a,const string& b){
    if(a.size()==b.size()){
        if(stoi(a)>=stoi(b)) return true;
        else return false;
    }
    else if(a.size()<b.size()){
        for(int i=0;i<a.size();i++){
            int A=a[i]-48;
            int B=b[i]-48;
            if(A>B) return true;
            else if(A<B) return false;
            else continue;
        }
        string first="";
        first=first.append(a).append(b);
        string second="";
        second=second.append(b).append(a);
        ull p=stoull(first);
        ull q=stoull(second);
        if(p>q) return true;
        else return false;
    }
    else{
        for(int i=0;i<b.size();i++){
            int A=a[i]-48;
            int B=b[i]-48;
            if(A>B) return true;
            else if(A<B) return false;
            else continue;
        }
        string first="";
        first=first.append(a).append(b);
        string second="";
        second=second.append(b).append(a);
        ull p=stoull(first);
        ull q=stoull(second);
        if(p>q) return true;
        else return false;
    }
}

int main(){
    cin.tie(0);
    ios_base::sync_with_stdio(0);
    int n;
    cin>>n;
    vector<string> v(n);
    for(int i=0;i<n;i++){
        cin>>v[i];
    }
    sort(v.begin(),v.end(),cmp);
    bool state=true;
    for(int i=0;i<v.size();i++){
        if(v[i]=="0") continue;
        else{
            state=false;
            break;
        } 
    }
    if(state) cout<<0;
    else{
        for(int i=0;i<n;i++){
            cout<<v[i];
        }
    }
}
```
</details>

### 성공 코드

<details>
    <summary>자세히</summary>

```
#include <iostream>
#include <vector>
#include <algorithm>
#define ull unsigned long long
using namespace std;
vector<string> v;
bool cmp(const string& a,const string& b){
    if(a.size()==b.size()){
        if(stoi(a)>=stoi(b)) return true;
        else return false;
    }
    else if(a.size()<b.size()){
        for(int i=0;i<a.size();i++){
            int A=a[i]-48;
            int B=b[i]-48;
            if(A>B) return true;
            else if(A<B) return false;
            else continue;
        }
        string first="";
        first=first.append(a).append(b);
        string second="";
        second=second.append(b).append(a);
        ull p=stoull(first);
        ull q=stoull(second);
        if(p>q) return true;
        else return false;
    }
    else{
        for(int i=0;i<b.size();i++){
            int A=a[i]-48;
            int B=b[i]-48;
            if(A>B) return true;
            else if(A<B) return false;
            else continue;
        }
        string first="";
        first=first.append(a).append(b);
        string second="";
        second=second.append(b).append(a);
        ull p=stoull(first);
        ull q=stoull(second);
        if(p>q) return true;
        else return false;
    }
}

int main(){
    cin.tie(0);
    ios_base::sync_with_stdio(0);
    int n;
    cin>>n;
    string str;
    for(int i=0;i<n;i++){
        cin>>str;
        v.push_back(str);
    }
    sort(v.begin(),v.end(),cmp);
    bool state=true;
    for(int i=0;i<v.size();i++){
        if(v[i]!="0"){
            state=false;
            break;
        } 
    }
    if(state) cout<<0;
    else{
        for(int i=0;i<v.size();i++){
            cout<<v[i];
        }
    }
}
```

</details>

---
배열의 매개변수 전달이 불가피한 경우, &를 사용하여 참조자로 사용  
<details>
    <summary>자세히</summary>

```
  void function(const vector& v){}
  void function2(vector& v){}
```
[참고링크](https://www.acmicpc.net/board/view/38804)
</details>

---
### 배열 초기화하기  

<details>
    <summary>배열 초기화 하는 방법</summary>

1. memset으로 초기화
```
#include <cstirng>
#include <vector>
int main(){
    int arr[10];
    bool std::vector<int> v(10);
    memset(arr,0,sizeof(arr));
    memset(v,false,sizeof(v));
}
```
1바이트 단위로 값을 세팅하기 떄문에 0이나 char 타입이 아닌 값으로 초기화할 시 오류 발생.

---
2. fill로 초기화
```
#include <algorithm>
#include <vector>
int main(){
    int arr1[10];
    std::fill(&arr1[0],&arr1[10],98);
    int arr2[10][10];
    std::fill(&arr2[0][0],&arr2[9][10],98);
    int arr3[10][10][10];
    std::fill(&arr3[0][0][0],&arr3[9][9][10],98);
    std::vector<int> v1(10);
    std::fill(v1.begin(),v1.end(),77);
    std::vector<std::vector<int>> v2(10,std::vector<int>(10));
    std::fill(v2.begin(),v2.end(),std::vector<int>(v2[0].size(),77));
}
```

</details>

---

### 절대값 함수

<details>
    <summary>절대값 함수 헤더에 따른 차이</summary>

1. std::abs()
    변수가 int형으로 프로모션할 수 없는 형태이면 오류 발생.

2. #include <algorithm>
    int 타입의 정수 절대값 함수(abs)의 오버로딩

3. #include <cmath>
    loat, double 타입의 실수 절대값 함수(abs)의 오버로딩

</details>
<br><hr>
