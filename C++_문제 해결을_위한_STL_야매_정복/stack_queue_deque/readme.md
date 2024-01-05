## stack

`#include <stack>`

FILO
스택은 사실 스택을 활용해야하는 문제가 아니면, 다른 문제들에서 활용도가 높지 않은 것 같다.<br/>
dfs할 때, 쓰긴 하나 재귀로 하는 게 더 가독성이 좋으면서 편하고, 굳이 말한다면 SCC정도...? <br/>
게다가 C++에서는 vector, deque, list를 기반으로 내부적으로 구현하는데, 기본적으로 deque를 이용하여 구현이 되기 때문에, 생각보다 메모리를 더 잡아먹을 수 있다.

```cpp
     stack<int> s;
     s.push(3);
     cout<<s.size(); //스택의 사이즈 반환
     if(s.empty()){ // 스택이 비어있으면 true
         cout<<"이 문장은 출력이 안됩니다.";
     }
     cout<<s.top(); //스택의 제일 위 원소 반환
     s.pop(); // 스택의 원소 하나 비우기
     stack<pair<int,int>> sp; //pair 가능
```

## queue

`#include <queue>`

FIFO
큐도 무난하다.

```cpp
    queue<int> q;
    q.push(3);
    cout<<q.front();
    q.pop();
    if(q.empty()){ // 큐가 비어있으면 true
         cout<<"이 문장은 출력이 됩니다.";
     }
     cout<<q.size();
    q=queue<int>(); //큐의 초기화
```

## priority_queue

`#include <queue>`

우선순위 큐, 내부적으로 힙을 이용하여 순서를 유지한다. <br/>
기본적으로 내림차순 정렬이다. <br/>
구조체를 이용하면 정렬순서를 바꿀 수 있으나 번거로워서 굳이 추천은 안하고, 넣을 때 음수를 곱하고, 꺼낼 때 음수를 다시 곱하는 방법을 사용하는 것이 편하다.<br/>
그리디 알고리즘을 풀 때, 많이 사용한다.

```cpp
    priority_queue<int> q;
    q.push(1);
    q.push(2);
    cout<<q.top(); // 2 출력
    q=priority_queue<int>(); // 우선순위 큐 초기화
    q.push(-1);
    q.push(-2);
    cout<<-q.top(); // 1 출력
    priority_queue<tuple<int,int,int>> pq; //복잡한 순서도 가능하다.
    // 만약에 튜플의 첫 원소는 오름차순, 두번째는 내림차순, 세번째는 오름차순 정렬하고 싶으면 구조체 정렬로 복잡하게 안하고 간단히 하면 된다.
    pq.push({-원소,원소,-원소});
    // 조회할때도 마이너스
    int firstVal=-get<0>(pq.top());
    int secondVal=get<1>(pq.top());
    int thirdVal=-get<2>(pq.top());
    // 그런데 char형은 음수로 바꿀 수 없다...그럼 해결법은?
    // 추가적인 변형 or map 활용하기
```

---

## deque

`#include <deque>`

vector가 꽉 찬 상태에서 원소를 추가하면(*push_back()* 실행시) 기존의 메모리 공간에 원소들을 복사하는 것이 아니라 보통 현재 크기의 2배에 해당하는 더 큰 메모리 공간을 할당하고, 기존의 원소들을 새로운 공간으로 복사한 후 새로운 원소를 추가한다. 이 과정에서 메모리를 2배나 차지한다.

반면에 deque의 경우에는 그냥 새로운 블록을 할당한 후에 새로운 원소를 넣는다. 따라서 deque는 메모리를 효율적으로 사용하며, 맨 처음과 끝에 원소를 추가하는 작업을 많이 수행할 때 deque를 사용하는게 낫다. 

> 💡 deque는 앞뒤에서 원소를 추가하거나 제거하는 작업에 최적화되어있다.

그런데 보통 문제에서 범위가 주어지기 때문에, 고정 배열을 많이 사용한다. 그래서 deque를 웬만한 문제에선 잘 쓰지 않는다.

```cpp
    deque<int> dq;
    dq.push_back(1);
    dq.push_front(2);
    dq.pop_back();
    dq.pop_front();
    //등등 여러 가지가 있음

```

---
