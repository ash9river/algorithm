> 은근히 중요한 set과 map<br/>
> 해시를 사용하고 싶으면 unordered_set, unordered_map 사용<br/>
> BBST를 사용하고 싶으면 set, multiset, map, multimap 사용<br/>

## set

`#include <set>`

그냥 집합


```cpp
    set<int> s; //선언
    s.insert(3); //삽입
    // set 순회
    for(auto it=s.begin();it!=s.end();++it){
        cout<<*it<<" ";
    }
    // set 탐색
    if(s.find(3)!=s.end()){
        cout<<"원소가 존재합니다.\n";
    }

```

---

## multiset

BST(Binary Search Tree)로 사용하는 점에서 상당히 중요하다.
set과 상당히 비슷하나, 중복된 원소를 허용한다는 점에서 다르다.

`#include <set>`

```cpp
    multiset<int> s;
    s.insert(3);
    s.insert(3);
    s.find(3); // 아무 3의 주소 반환
    cout<<s.count(3); // 원소의 개수 반환 : 시간 복잡도 O(N)
    s.erase(3); //모든 3 제거
    s.insert(1);
    s.insert(2);
    s.insert(3);
    cout<<*s.lower_bound(2); // 이분 탐색으로 2 반환
    cout<<*s.upper_bound(3); // 이분 탐색으로 2를 초과하는 값 반환
    auto it=s.lower_bound(2);
    if(it!=s.begin()){
        --it;
        cout<<*it<<"\n"; // it 탐색 후 --it하여 1 반환
    }
    // multiset 활용 예시들
    vector<multiset<pair<int,int>>> v(101,multiset<pair<int,int>>());
    v[100].insert({50,25});
    cout<<v[50].rbegin()->second<<"\n"; //  v[50] 집합의 제일 큰 원소 조회
    cout<<v[25].begin()->second<<"\n"; // v[25] 집합의 제일 작은 원소 조회
    v[100].erase({50,25}); // 원소 삭제
    // 예시 2
    multiset<pair<int,pair<int,int>>> s;
    s.insert({5,{10,25}});
    cout<<s.rbegin()->second.first<<"\n";
    cout<<s.begin()->second.first<<"\n";
```

## map

 `#include <map>`

map<key,value>
키와 값을 pair형태로 저장한다. 
key값을 오름차순으로 저장한다. << 그리디에서 사용할 때는 이 특성을 자주 이용한다.

```cpp
    map<int,int> m;
    m.insert({3,3}); //pair형태로 중괄호 사용하여 저장
    // map 탐색
    if(m.find(3)!=m.end()) cout<<"원소가 존재합니다.";
    // map 순회
    for(auto it=m.begin();it!=m.end();++it){
        cout<<"키값 : "<<it->first<<"\n";
        cout<<"밸류 : "<<it->second<<"\n";
    }
    for(auto it:m){
        cout<<it.first<<" "<<it.second;
    }
    m.erase(3);
    m.clear();
```

---

## unordered_set & unordered_map

`#include <unordered_set>`
`#include <unordered_map>`
기본적인 구성은 set & map과 같다.<br>
정렬을 하지 않고서 삽입한 일련의 순서를 유지시키고 싶다면 set이나 map이 아니라 unordered_set 또는 unordered_map 사용<br>
unordered_multiset은 중복된 원소 삽입 시 일련의 순서로 삽입되는 것이 아니라 이미 존재하는 중복 원소 뒤에 이어서 삽입된다.<br>
<br>
set이나 map과 달리 hash function을 사용하여 ***O(1)*** 로 insert, erase, find가 수행된다.

```
     unordered_set<int> s;
     unordered_multiset<int> ms;
     unordered_map<int> m;
     unordered_multimap<int> mm;
```
