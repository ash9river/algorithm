##### C++ 시작하기
---
##기존 C에서 C++로 바꾸면서 stdio.h나 printf같은 C형식의 헤더 혹은 입출력 배제&nbsp; 
#standard input output-> iostream
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
##또한 자료구조를 이용할 시, 직접 구현보다는 동적 할당이 편리한 C++의 STL 사용&nbsp; 
vector,pair,tuple,stack,queue 등이 있음&nbsp; 
그 이외의 기본적인 것들은 C와 다를 것이 없으나 빠른 입출력시&nbsp; 
```
    cin.tie(0);
    ios_base::sync_with_stdio(0);
```
cin.tie(NULL)은 cin과 cout의 묶음을 푼다.&nbsp; 
기본적으로 cin으로 읽을 때 먼저 출력 버퍼를 비우는데, 입력과 출력을 여러 번 번갈아서 반복해야 하는 경우 필수적.&nbsp; 
ios_base::sync_with_stdio(false)는 C와 C++의 버퍼를 분리.&nbsp; 
이것을 사용하면 cin/cout이 더 이상 stdin/stdout과 맞춰 줄 필요가 없으므로 속도가 빨라진다.&nbsp; 
단, 버퍼가 분리되었으므로 cin과 scanf, gets, getchar 등을 같이 혼용하면 안되고, cout과 printf, puts, putchar 등을 같이 사용하면 안된다.
그 이외의 C++헤더나 STL의 사용법은 코딩해나가면서 숙지.
