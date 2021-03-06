
## 최솟값 만들기
https://programmers.co.kr/learn/courses/30/lessons/12941

### 문제설명
길이가 같은 배열 A, B 두개가 있습니다. 각 배열은 자연수로 이루어져 있습니다. 
배열 A, B에서 각각 한 개의 숫자를 뽑아 두 수를 곱합니다. 이러한 과정을 배열의 길이만큼 반복하며, 두 수를 곱한 값을 누적하여 더합니다. 이때 최종적으로 누적된 값이 최소가 되도록 만드는 것이 목표입니다. (단, 각 배열에서 k번째 숫자를 뽑았다면 다음에 k번째 숫자는 다시 뽑을 수 없습니다.)

예를 들어 A = [1, 4, 2] , B = [5, 4, 4] 라면

A에서 첫번째 숫자인 1, B에서 두번째 숫자인 5를 뽑아 곱하여 더합니다. (누적된 값 : 0 + 5(1x5) = 5)
A에서 두번째 숫자인 4, B에서 세번째 숫자인 4를 뽑아 곱하여 더합니다. (누적된 값 : 5 + 16(4x4) = 21)
A에서 세번째 숫자인 2, B에서 첫번째 숫자인 4를 뽑아 곱하여 더합니다. (누적된 값 : 21 + 8(2x4) = 29)
즉, 이 경우가 최소가 되므로 29를 return 합니다.

배열 A, B가 주어질 때 최종적으로 누적된 최솟값을 return 하는 solution 함수를 완성해 주세요.

### 제한조건
 - 배열 A, B의 크기 : 1000 이하의 자연수
 - 배열 A, B의 원소의 크기 : 1000 이하의 자연수

### 입출력 예
|A|B|answer|
|-|-|------|
|[1,4,2]|[5,4,4]|29|
|[1,2]|[3,4]|10|

### 입출력 예 설명
입출력 예 #2
A에서 첫번째 숫자인 1, B에서 두번째 숫자인 4를 뽑아 곱하여 더합니다. (누적된 값 : 4) 다음, A에서 두번째 숫자인 2, B에서 첫번째 숫자인 3을 뽑아 곱하여 더합니다. (누적된 값 : 4 + 6 = 10)
이 경우가 최소이므로 10을 return 합니다.

### 풀이
A배열의 최댓값과 B배열의 최솟값을 곱해서 답에 더해주면 됨
(산술기하평균)
```
    var answer = 0;
    for(var i=0,endi=A.length;i<endi;i++){
        var maxA = Math.max.apply(null,A)
        var minB = Math.min.apply(null,B)
        answer += maxA * minB
        A.splice(A.indexOf(maxA),1)
        B.splice(B.indexOf(minB),1)
    }
    return answer;
```
테스트 1 〉	통과 (1.62ms, 36.6MB)
테스트 2 〉	통과 (1.77ms, 36.2MB)
테스트 3 〉	통과 (1.75ms, 36.6MB)
테스트 4 〉	통과 (1.73ms, 36.4MB)
테스트 5 〉	통과 (1.74ms, 36.4MB)
테스트 6 〉	통과 (1.71ms, 36.4MB)
테스트 7 〉	통과 (1.76ms, 36.5MB)
테스트 8 〉	통과 (1.71ms, 36.4MB)
테스트 9 〉	통과 (1.69ms, 36.7MB)
테스트 10 〉 통과 (1.72ms, 36.3MB)
테스트 11 〉 통과 (1.68ms, 37MB)
테스트 12 〉 통과 (1.68ms, 36.9MB)
테스트 13 〉 통과 (1.66ms, 36.3MB)
테스트 14 〉 통과 (1.78ms, 36.5MB)
테스트 15 〉 통과 (1.69ms, 36.4MB)
테스트 16 〉 통과 (1.71ms, 36.5MB)
효율성  테스트
테스트 1 〉	통과 (4.96ms, 37.1MB)
테스트 2 〉	통과 (4.86ms, 36.4MB)
테스트 3 〉	통과 (4.91ms, 36.9MB)
테스트 4 〉	통과 (5.10ms, 36.8MB)

테스트는 통과, 이렇게하면 Math.max, Math.min 은 매번 각 배열값을 비교해서(?) 효율성 낮아질것같음
처음에 한번만 정렬 후 곱하는게 더 빠를까?
```
    var answer = 0;
    A.sort(function(a,b){
        return a < b ? 1 : a > b ? -1 : 0
    })
    B.sort(function(a,b){
        return a > b ? 1 : a < b ? -1 : 0
    })
    for(var i=0,endi=A.length;i<endi;i++){
        answer += A[i] * B[i]
    }
    return answer;
```
테스트 1 〉	통과 (1.92ms, 36.9MB)
테스트 2 〉	통과 (2.16ms, 36.3MB)
테스트 3 〉	통과 (2.12ms, 36.3MB)
테스트 4 〉	통과 (2.12ms, 36.3MB)
테스트 5 〉	통과 (2.24ms, 36.3MB)
테스트 6 〉	통과 (2.11ms, 36.6MB)
테스트 7 〉	통과 (2.14ms, 36.7MB)
테스트 8 〉	통과 (2.23ms, 36.4MB)
테스트 9 〉	통과 (2.14ms, 36.7MB)
테스트 10 〉 통과 (2.14ms, 36.3MB)
테스트 11 〉 통과 (2.08ms, 36.3MB)
테스트 12 〉 통과 (2.09ms, 36.3MB)
테스트 13 〉 통과 (2.09ms, 36.8MB)
테스트 14 〉 통과 (2.10ms, 36.9MB)
테스트 15 〉 통과 (2.07ms, 37MB)
테스트 16 〉 통과 (2.10ms, 36.7MB)
효율성  테스트
테스트 1 〉	통과 (5.88ms, 37.3MB)
테스트 2 〉	통과 (5.75ms, 36.8MB)
테스트 3 〉	통과 (5.73ms, 36.7MB)
테스트 4 〉	통과 (3.18ms, 36.6MB)

아니였음...