# Pairs (HackerRank)

주어지 배열에서 두가지 숫자를 고른 후 빼서 타켓 넘버가 되는 경우의 수를 리턴하는 문제다.

example
```python
k = 1 # 타켓넘버: 0 < k < 10^9
arr = [1,2,3,4] # 배열

# 1이 되는 경우의 수
(2 - 1), (3 - 2), (4 - 3)

return 3
```
___
## 첫번째 방법

```python
def sol(k, arr):
    answer = 0

    for i in range(len(arr)):
        for j in range(len(arr)):
            # 만약 k 가 0도 포함한다면 같은 인덱스라면 비교하지 않고 진행
            if i == j:
                continue
            # 타켓넘버를 찾는다면 경우의 수 증가
            if arr[i] - arr[j] == k:
                answer += 1

    return answer
```

문제의 해답을 찾을 순 있지만 **시간 복잡도 초과로 통과하지 못한다**. 첫 번째 방법의 **시간복잡도는 O(n^2)** 이다. `for` 문을 이중으로 사용하면서 요소하나에 대해 arr 전체를 순회하기 때문이다. 

## 두번째 방법

```python
def sol(k, arr):
    answer = 0
    for i in arr:
        if i + k in arr:
            answer += 1
    return answer
```

이 방법도 마찬가지로 **시간 복잡도를 통과하지 못한다.** `for` 문을 이중으로 사용하지 않았지만 `if ~ in` 을 사용하면서 다시 요소 하나에 대해 배열 전체를 순회해야하는 방법이기 때문이다. 시간 복잡도는 **O(N^2)** 이다.

## 세번째 방법

```python
def sol(k, arr):
    answer = 0
    set_arr = set(arr)
    for i in arr:
        if i + k in set_arr:
            answer += 1
    return answer
```

해답과 효율성 모두 통과하는 방법이다. 위에 방법과 다른 점은 주어진 배열을 python 의 `set` 자료형으로 변환하고 검색한 것이다. `set` 은 데이터를 배열과 다르게 저장한다. 

`set` 자료형에서 데이터를 저장하는 방식은 **해쉬 테이블**을 기반으로 구현한다.

1. 데이터를 해쉬함수를 이용해 정수형태의 해쉬코드로 변환한다.
2. 해쉬코드를 해쉬 알고리즘은 이용해 인덱스화하여 저장한다.
3. 검색할 땐 같은 데이터는 항상 같은 해쉬코드를 반환하기 때문에 해당 인덱스를 바로 검색 가능하다.

