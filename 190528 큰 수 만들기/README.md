
## 큰 수 만들기
https://programmers.co.kr/learn/courses/30/lessons/42883

### 문제설명
어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.
예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.
문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

### 제한조건
 - number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
 - k는 1 이상 number의 자릿수 미만인 자연수입니다.

### 입출력 예
|number|k|return|
|------|-|------|
|"1924"|2|"94"|
|"1231234"|3|"3234"|
|"4177252841"|4|"775841"|

### 풀이
 - ver.1
 
앞에서부터 그 다음 숫자와 비교하면서 작은 숫자를 삭제하면 될것같음
입출력 예#3 에서
4,1 비교 => 4 살아남음,
1,7 비교 => 1 삭제
그뒤, 4,7 비교 필요!

 - ver.2

index와 k를 이용해서 index부터 k까지에서의 최대값을 찾고,
index부터 최대값 앞의 값을 날림.
k에서 index부터 최대값까지 길이까지 빼줌.
최대값+1값이 index값이 됨.
k가 0이 될때까지 반복해줌.
```
    var answer = '';
    var slicei,endi
    for(slicei=0,endi=k+1;k>0;){
        var arr = number.slice(slicei,endi).split('')
        var max = Math.max.apply(null,arr) +''
        var index = arr.indexOf(max)
        number = number.slice(index,number.length)
        k -= index
        endi = ++slicei + k + 1
        answer += max
        if(slicei>=number.length) return answer.slice(0,number.length - k) 
    }
    number = number.slice(slicei,number.length)
    return answer+number;
```
하나가 런타임에러남..