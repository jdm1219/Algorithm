
## 문자열 다루기 기본
https://programmers.co.kr/learn/courses/30/lessons/12918

### 문제설명
문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요.
예를 들어 s가 a234이면 False를 리턴하고 1234라면 True를 리턴하면 됩니다.

### 제한조건
 - s는 길이 1 이상, 길이 8 이하인 문자열입니다.

### 입출력 예
|s|answer|
|-|------|
|"a234"|flase|
|"1234"|true|

### 풀이

문자열의 length값을 비교한 후, 문자열을 1로 나누어서 isNaN을 써서 숫자로만 구성되어있는지 확인한다.

```
    var answer = true
    if(s.length === 4 || s.legnth === 6){
        if(isNaN(s/1)) answer = !answer
    }else{
        answer = !answer
    }
    return answer;
```
하나가 실패함..
예) 소숫점 '1.23'

문자열의 각자리수마다 isNaN검사를 해줌
```
    var answer = true
    if(s.length === 4 || s.legnth === 6){
        for(var i=0,endi=s.length;i<endi;i++){
            if(isNaN(s[i])){
                answer = !answer
                break;
            }
        }
    }else{
        answer = !answer
    }
    return answer;
```
