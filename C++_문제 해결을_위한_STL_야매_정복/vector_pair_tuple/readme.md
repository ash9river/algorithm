## 알아야 할  것

> vector, pair, tuple, list, queue, priority_queue, map, set ,stack, deque

array는 vector가 있어서 잘 안쓰는 경향이...

----

## Vector

동적 배열 할당하는데 편하다.

### vector의  초기화

`#include <vector>`

```cpp
   vector<int> v1; //1차원 배열 생성
   vector<int> v1_init(10,987654321); //1차원 배열 [10]생성, 각 배열의 원소를 987654321로 초기화
   vector<vector<int>> v2; //2차원 배열 생성 
   vector<vector<int>> v2_init(10,vector<int>(11,987654321)); // [10][11] 생성, 987654321로 초기화
   
   v1[9]=987654321;
   v2_init[3][4]=145; //원소 접근은 배열처럼
   v1.push_back(155); //push_back()으로 원소의 개수를 하나 늘릴 수 있다.
   v1.pop_back();     //제일 마지막 원소 제거
   v2_init[3].push_back(1616); // 이런 경우에는 v2[3]만 원소의 개수가 12개가 된다
```

### vector의 resize

```cpp
    vector<int> v;
    v.resize(10);
    vector<vector<int>> v2;
    v2.resize(10,vector<int>());
    vector<vector<int>> v3;
    v3.resize(10,vector<int>(11));

```

### vector에서 쓰이는 것들

```cpp
    vector<int> v1(10,0);
    v1.begin(); //v1의 제일 첫 주소
    v1.end();   //v1의 가장 마지막 인덱스+1의 주소
    v1.back();  //v1의 가장 마지막 인덱스의 원소
    v1.pop_back();     //제일 마지막 원소 제거
    cout<<v1.size(); //v1의 크기 출력 (unsigned int이므로 -1을 할 때, 주의해야한다. 보통 .empty()로 먼저 체크하기)
    v1.clear(); //v1의 모든 원소 삭제
    v1.empty(); //비었는지 확인
    vector<int> table(10,5);
    sort(table.begin(),table.end(),greater<>()); //table 내림차순 정렬    
    sort(table.begin(),table.end()); //table 오름차순 정렬
    table.erase(unique(table.begin(),table.end()),table.end()); //table의 중복 원소 제거(정렬 필수)
```

---
## Pair

`#include <vector>`

쌍으로 값을 저장하기 편하다. 보통 x,y좌표를 저장하는 데에 사용한다.

```cpp
    pair<int,int> p;
    p=make_pair(1,2); //make_pair로 pair 만들기
    p={1,2}; //괄호로 pair 만들기
    cout<<p.first<<" "<<p.second; // first는 왼쪽, second는 오른쪽
    vector<pair<int,int>> v_p(10);//보통 단독으로 pair만 사용하진 않음.
    cout<<v_p[5].first<<v_p[6].second; // 임의접근은 이런 식으로
    pair<int,pair<int,int>> pp; //여러 개 가능
    cout<<pp.first<<pp.second.first<<pp.second.second; //상당히 쉽다.
    pair<pair<int,int>,pair<int,int>> ppp; //여러 개 여러 개 가능
    cout<<ppp.first.first; // 직관적이다.
```

---
## Tuple

`#include <tuple>`

세 개의 원소를 묶어서 저장, 보통 pair<int,pair<int,int>>로 만들기 귀찮아서 사용하는데 tuple이 더 귀찮을 때가 있다...

```cpp
    tuple<int,int,int> t;
    t=make_tuple(1,2,3); //make_tuple로 tuple 만들기
    t={1,2,3}; //괄호로 tuple만들기
    cout<<get<0>(t)<<get<1>(t)<<get<2>(t); //임의접근이 상당히 귀찮다.
    tuple<pair<int,int>,pair<int,int>,tuple<int,int,int>> tt={{1,2},{3,4},{5,6,7}}; // 뭉텅이 가능
    cout<<get<0>(tt).first; //섞이면 상당히 어렵다...
    cout<<get<0>(get<2>(tt)); //상당히 헷갈림
```
